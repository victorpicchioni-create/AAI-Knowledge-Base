# Wellbine Supabase Schema

**Version:** 0.1.0

**Status:** Draft

**Last Updated:** July 2026

---

# Purpose

This document defines the practical Supabase schema direction for Wellbine.

The goal is to translate the conceptual `DATA_MODEL.md` into a more operational database structure that can be implemented in Supabase and consumed by FlutterFlow, Admin and AAI services.

This document covers:

- Core tables
- Approximate fields
- Relationships
- JSON configuration fields
- Row Level Security direction
- Storage buckets
- Edge Functions
- Admin publishing
- Event tracking
- Implementation phases

This is not the final SQL migration file.

This is the implementation blueprint.

---

# Official Definition

**Wellbine Supabase Schema is the practical database and backend structure that stores users, plans, daily actions, pillars, push events, wearable data, uploads, recommendations, commerce benefits and AAI context for the Wellbine product.**

---

# Core Principle

The core schema rule is:

```text
Supabase is the source of truth. FlutterFlow is the interface layer.
```

FlutterFlow should read and write from Supabase.

Admin should configure Supabase data.

AAI should interpret Supabase context.

The database should remain flexible enough for product evolution without requiring app redeployment for every business rule change.

---

# Supabase Role In Wellbine

Supabase should provide:

- Authentication
- User profile storage
- Plan Template storage
- User Active Plan storage
- Home state
- Daily plans
- Daily actions
- Pillar states
- Push events
- Daily Stack items
- Wearable connections
- Upload metadata
- Recommendation records
- Commerce benefit records
- Admin configuration
- Event tracking
- Audit logs
- Storage for user files
- Edge Functions for controlled backend logic

Supabase should not be used only as a passive database.

It is the operational backend of Wellbine.

---

# Architecture Direction

Recommended architecture:

```text
FlutterFlow App
↓
Supabase Auth
↓
Supabase Database
↓
Supabase Storage
↓
Supabase Edge Functions
↓
Admin Panel
↓
AAI Context Layer
```

The core relationship:

```text
Admin configures
↓
Supabase stores
↓
FlutterFlow displays
↓
User acts
↓
Supabase records
↓
AAI adapts
```

---

# Naming Convention

Database naming should use:

```text
lower_snake_case
```

Examples:

```text
user_profiles
user_settings
plan_templates
daily_actions
push_events
wearable_connections
```

Documentation files use:

```text
UPPERCASE_WITH_UNDERSCORES.md
```

Example:

```text
SUPABASE_SCHEMA.md
```

---

# Schema Flexibility Rule

Do not over-normalize too early.

The schema should use structured tables for core entities and JSON fields for flexible configuration.

Recommended JSON field names:

```text
configuration_json
metadata_json
rules_json
eligibility_rules_json
visibility_rules_json
content_json
payload_json
```

JSON should be used for flexible business rules.

Core relational fields should be used for identity, ownership, status, timestamps and important queries.

---

# Status Field Rule

For MVP, status fields may use text values.

Examples:

```text
draft
published
archived
active
inactive
completed
skipped
expired
cancelled
```

Strict database enums may be added later.

Do not block MVP implementation with excessive enum design.

---

# Core Tables Overview

Recommended core tables:

```text
user_profiles
user_settings
user_aai_context

plan_templates
plan_template_versions
user_active_plans

pillar_definitions
user_pillar_states

daily_plans
daily_actions

push_events

stack_items

wearable_connections
wearable_metric_snapshots

user_uploads

content_modules
recommendations

commerce_benefits
user_commerce_benefits
commerce_events

admin_audit_log
```

---

# Authentication

Supabase Auth should manage user identity.

The authenticated user ID should be referenced through:

```text
auth.users.id
```

Most user-owned tables should include:

```text
user_id uuid references auth.users(id)
```

User-owned data should be protected with Row Level Security.

---

# user_profiles

Stores stable user profile baseline.

Purpose:

```text
Stores the baseline personal profile required to activate Wellbine.
```

Possible fields:

```text
id uuid primary key
user_id uuid references auth.users(id)
name text
biological_sex text
age integer
height_cm numeric
weight_kg numeric
country text
language text
timezone text
relevant_comorbidities_json jsonb
onboarding_completed boolean
onboarding_completed_at timestamptz
created_at timestamptz
updated_at timestamptz
```

Notes:

- `biological_sex` supports physiological personalization.
- Sensitive fields should be optional.
- Comorbidities should not turn Wellbine into a medical record.
- User profile should remain editable.

---

# user_settings

Stores user preferences and app controls.

Purpose:

```text
Stores user-level preferences for Push, Mental Detox, units, privacy and app behavior.
```

Possible fields:

```text
id uuid primary key
user_id uuid references auth.users(id)
push_enabled boolean
mental_detox_enabled boolean
preferred_units text
preferred_language text
preferred_timezone text
notification_preferences_json jsonb
privacy_preferences_json jsonb
accessibility_preferences_json jsonb
commerce_preferences_json jsonb
metadata_json jsonb
created_at timestamptz
updated_at timestamptz
```

Notes:

- Push must be optional.
- Mental Detox should be controlled here.
- Commerce visibility preferences may be stored here later.

---

# user_aai_context

Stores the current adaptive context used by AAI.

Purpose:

```text
Stores the latest interpreted context that allows AAI to personalize guidance.
```

Possible fields:

```text
id uuid primary key
user_id uuid references auth.users(id)
current_context_json jsonb
recent_behavior_json jsonb
current_plan_context_json jsonb
pillar_context_json jsonb
wearable_context_json jsonb
daily_context_json jsonb
commerce_context_json jsonb
last_evaluated_at timestamptz
created_at timestamptz
updated_at timestamptz
```

Notes:

- This table is not the raw event store.
- It stores interpreted state.
- It should be updated by controlled logic, not randomly from the frontend.

---

# plan_templates

Stores high-level Plan Template records.

Purpose:

```text
Stores admin-managed plan models available for user activation.
```

Possible fields:

```text
id uuid primary key
name text
slug text
description text
status text
category text
audience text
is_featured boolean
sort_order integer
current_version_id uuid
metadata_json jsonb
created_by uuid
updated_by uuid
created_at timestamptz
updated_at timestamptz
```

Possible statuses:

```text
draft
published
archived
```

Notes:

- Plan Templates should be admin-managed.
- Published plans can be shown to users.
- Archived plans should not be offered to new users.
- Do not hardcode plan categories.

---

# plan_template_versions

Stores versioned Plan Template configurations.

Purpose:

```text
Stores version-specific configuration for each Plan Template.
```

Possible fields:

```text
id uuid primary key
plan_template_id uuid references plan_templates(id)
version_number integer
status text
configuration_json jsonb
pillar_defaults_json jsonb
daily_rules_json jsonb
push_rules_json jsonb
home_rules_json jsonb
wearable_rules_json jsonb
commerce_rules_json jsonb
content_rules_json jsonb
created_by uuid
published_at timestamptz
created_at timestamptz
updated_at timestamptz
```

Notes:

- User activation should reference a specific plan version.
- Changing a plan template should not unexpectedly rewrite existing active user plans.
- Versioning protects stability.

---

# user_active_plans

Stores the user’s currently activated plan snapshot.

Purpose:

```text
Stores the active plan configuration assigned to a user.
```

Possible fields:

```text
id uuid primary key
user_id uuid references auth.users(id)
plan_template_id uuid references plan_templates(id)
plan_template_version_id uuid references plan_template_versions(id)
status text
started_at timestamptz
ended_at timestamptz
active_configuration_json jsonb
activation_source text
metadata_json jsonb
created_at timestamptz
updated_at timestamptz
```

Possible statuses:

```text
active
paused
completed
cancelled
replaced
```

Notes:

- `active_configuration_json` is a snapshot.
- This avoids breaking users when templates change.
- A user may have historical plans, but only one primary active plan at a time for MVP.

---

# pillar_definitions

Stores available operational pillars.

Purpose:

```text
Stores the core Wellbine pillars available to the product.
```

Possible fields:

```text
id uuid primary key
name text
slug text
description text
status text
sort_order integer
default_configuration_json jsonb
metadata_json jsonb
created_at timestamptz
updated_at timestamptz
```

Initial pillars:

```text
mind
sun
hydration
sleep
nutrition
movement
daily_stack
```

Notes:

- Pillars should be configurable.
- Do not hardcode all pillar behavior in FlutterFlow.
- Admin may later control copy, rules and visibility.

---

# user_pillar_states

Stores current state for each pillar per user.

Purpose:

```text
Stores the user's current status, progress and context for each pillar.
```

Possible fields:

```text
id uuid primary key
user_id uuid references auth.users(id)
pillar_id uuid references pillar_definitions(id)
active_plan_id uuid references user_active_plans(id)
status text
score numeric
state_json jsonb
last_action_at timestamptz
last_evaluated_at timestamptz
created_at timestamptz
updated_at timestamptz
```

Possible statuses:

```text
active
inactive
attention
completed_today
needs_input
```

Notes:

- Pillar state powers Home orbs.
- Pillar state also informs Daily and Push.
- The score should not be overexposed to users if it creates false precision.

---

# daily_plans

Stores the daily execution plan generated for the user.

Purpose:

```text
Stores the user's adaptive daily plan for a specific date.
```

Possible fields:

```text
id uuid primary key
user_id uuid references auth.users(id)
active_plan_id uuid references user_active_plans(id)
plan_date date
status text
daily_summary text
daily_context_json jsonb
schedule_json jsonb
created_by text
generated_at timestamptz
created_at timestamptz
updated_at timestamptz
```

Possible statuses:

```text
planned
active
completed
expired
regenerated
```

Notes:

- Daily plans should be generated from active plan, profile, pillar state, wearable data and recent user behavior.
- Daily should adapt without creating chaos.

---

# daily_actions

Stores individual actions inside a Daily plan.

Purpose:

```text
Stores specific actions suggested, confirmed, adjusted, delayed or skipped by the user.
```

Possible fields:

```text
id uuid primary key
user_id uuid references auth.users(id)
daily_plan_id uuid references daily_plans(id)
pillar_id uuid references pillar_definitions(id)
action_type text
title text
description text
status text
scheduled_window_start timestamptz
scheduled_window_end timestamptz
completed_at timestamptz
skipped_at timestamptz
delayed_until timestamptz
source text
metadata_json jsonb
created_at timestamptz
updated_at timestamptz
```

Possible statuses:

```text
upcoming
active
completed
adjusted
delayed
skipped
expired
```

Possible sources:

```text
plan_template
aai
manual
push
admin
```

Notes:

- Daily actions should support Confirm, Adjust and Later.
- Expired actions should not punish users.
- Recovery language should be used in the app.

---

# push_events

Stores push orchestration events.

Purpose:

```text
Stores push messages, user responses and push-related outcomes.
```

Possible fields:

```text
id uuid primary key
user_id uuid references auth.users(id)
daily_plan_id uuid references daily_plans(id)
daily_action_id uuid references daily_actions(id)
push_type text
title text
body text
status text
response text
sent_at timestamptz
responded_at timestamptz
scheduled_for timestamptz
deep_link text
payload_json jsonb
created_at timestamptz
updated_at timestamptz
```

Possible statuses:

```text
scheduled
sent
delivered
responded
failed
cancelled
expired
```

Possible responses:

```text
confirm
adjust
later
dismissed
none
```

Notes:

- Push is orchestration, not spam.
- Push should respect Mental Detox settings.
- Push should never become commerce-first.

---

# stack_items

Stores user Daily Stack items.

Purpose:

```text
Stores supplements, vitamins, nutraceuticals, medications or routine items that the user tracks.
```

Possible fields:

```text
id uuid primary key
user_id uuid references auth.users(id)
name text
item_type text
status text
dosage_text text
frequency_json jsonb
timing_json jsonb
instructions text
refill_tracking_enabled boolean
refill_context_json jsonb
safety_notes text
source text
metadata_json jsonb
created_at timestamptz
updated_at timestamptz
```

Possible item types:

```text
supplement
vitamin
nutraceutical
medication
habit_item
other
```

Notes:

- Daily Stack organizes routine.
- It should not prescribe medication.
- Medical language should be careful.

---

# wearable_connections

Stores wearable and health platform connections.

Purpose:

```text
Stores the user's connected wearable providers and permission status.
```

Possible fields:

```text
id uuid primary key
user_id uuid references auth.users(id)
provider text
status text
permission_scope_json jsonb
last_sync_at timestamptz
connection_metadata_json jsonb
created_at timestamptz
updated_at timestamptz
```

Possible providers:

```text
apple_health
google_health_connect
garmin
oura
whoop
fitbit
manual
```

Possible statuses:

```text
connected
disconnected
revoked
error
manual_only
```

Notes:

- Wearables are optional.
- Wellbine must work without wearables.
- Do not claim active integrations before implementation.

---

# wearable_metric_snapshots

Stores normalized wearable summary data.

Purpose:

```text
Stores daily or periodic wearable metrics used by AAI and Wellbine guidance.
```

Possible fields:

```text
id uuid primary key
user_id uuid references auth.users(id)
provider text
snapshot_date date
sleep_duration_minutes integer
sleep_score numeric
hrv_ms numeric
resting_heart_rate_bpm numeric
steps integer
active_minutes integer
spo2_pct numeric
respiratory_rate numeric
wrist_temperature_delta numeric
readiness_score numeric
stress_score numeric
raw_payload_json jsonb
created_at timestamptz
updated_at timestamptz
```

Notes:

- This is a normalized snapshot table.
- Raw wearable data may be stored carefully only when necessary.
- Keep MVP focused on useful summaries, not excessive raw health storage.

---

# user_uploads

Stores metadata for user-uploaded files.

Purpose:

```text
Stores uploaded file metadata and links to Supabase Storage.
```

Possible fields:

```text
id uuid primary key
user_id uuid references auth.users(id)
file_name text
file_type text
storage_bucket text
storage_path text
status text
upload_category text
extracted_summary text
extraction_status text
metadata_json jsonb
created_at timestamptz
updated_at timestamptz
```

Possible upload categories:

```text
lab_exam
medical_report
nutrition_plan
fitness_assessment
sleep_report
wearable_export
supplement_list
medication_list
personal_note
other
```

Notes:

- Uploads are optional.
- User should be able to delete uploaded files.
- Sensitive files require strict access control.

---

# content_modules

Stores reusable content controlled by Admin.

Purpose:

```text
Stores educational, guidance or product content used across Wellbine.
```

Possible fields:

```text
id uuid primary key
title text
slug text
content_type text
status text
language text
body_markdown text
content_json jsonb
tags_json jsonb
created_by uuid
updated_by uuid
published_at timestamptz
created_at timestamptz
updated_at timestamptz
```

Possible content types:

```text
education
guidance
plan_content
pillar_content
stack_content
commerce_content
onboarding_content
faq
```

Notes:

- Content should be admin-managed.
- Avoid hardcoding important educational copy in FlutterFlow.

---

# recommendations

Stores recommendations shown to the user.

Purpose:

```text
Stores personalized or admin-managed recommendations for a user.
```

Possible fields:

```text
id uuid primary key
user_id uuid references auth.users(id)
active_plan_id uuid references user_active_plans(id)
recommendation_type text
title text
description text
status text
source text
priority integer
placement text
action_label text
action_url text
related_pillar_id uuid references pillar_definitions(id)
related_content_module_id uuid references content_modules(id)
metadata_json jsonb
shown_at timestamptz
acted_at timestamptz
dismissed_at timestamptz
created_at timestamptz
updated_at timestamptz
```

Possible recommendation types:

```text
daily_guidance
pillar_guidance
content
stack
commerce
wearable
upload
plan_adjustment
```

Notes:

- Recommendations should not become noise.
- AAI may create or prioritize recommendations.
- Admin may also configure recommendations.

---

# commerce_benefits

Stores available commerce benefits.

Purpose:

```text
Stores admin-managed subscriber benefits and external commerce offers.
```

Possible fields:

```text
id uuid primary key
name text
description text
status text
benefit_type text
platform text
code text
external_url text
button_label text
placement text
eligibility_rules_json jsonb
visibility_rules_json jsonb
starts_at timestamptz
ends_at timestamptz
metadata_json jsonb
created_by uuid
updated_by uuid
created_at timestamptz
updated_at timestamptz
```

Possible statuses:

```text
draft
active
paused
expired
archived
```

Notes:

- Do not hardcode discount percentage.
- Do not hardcode commerce platform.
- One button should copy the benefit code and open the external destination.
- Automatic coupon application may be supported when available.

---

# user_commerce_benefits

Stores user-specific benefit availability and usage.

Purpose:

```text
Stores which commerce benefits are available, shown or used by each user.
```

Possible fields:

```text
id uuid primary key
user_id uuid references auth.users(id)
commerce_benefit_id uuid references commerce_benefits(id)
status text
shown_at timestamptz
used_at timestamptz
copied_at timestamptz
opened_at timestamptz
expires_at timestamptz
metadata_json jsonb
created_at timestamptz
updated_at timestamptz
```

Possible statuses:

```text
available
shown
used
expired
disabled
```

Notes:

- This enables monthly or campaign-based benefits.
- Eligibility should remain configurable.

---

# commerce_events

Stores commerce-related events.

Purpose:

```text
Tracks Commerce Bridge events without turning the app into a store.
```

Possible fields:

```text
id uuid primary key
user_id uuid references auth.users(id)
commerce_benefit_id uuid references commerce_benefits(id)
event_type text
event_payload_json jsonb
created_at timestamptz
```

Possible event types:

```text
benefit_viewed
benefit_button_tapped
coupon_copied
external_store_opened
checkout_started
coupon_applied
purchase_completed
redemption_confirmed
expired
```

Notes:

- MVP only needs basic events.
- Purchase confirmation may require future integration or webhook.

---

# admin_audit_log

Stores admin changes.

Purpose:

```text
Records important admin actions for traceability.
```

Possible fields:

```text
id uuid primary key
admin_user_id uuid
action text
entity_type text
entity_id uuid
before_json jsonb
after_json jsonb
metadata_json jsonb
created_at timestamptz
```

Notes:

- Admin configuration changes should be traceable.
- This matters for plans, content, commerce, onboarding and push.

---

# Storage Buckets

Recommended Supabase Storage buckets:

```text
user_uploads
public_assets
admin_assets
```

---

## user_uploads

Purpose:

```text
Stores private user-uploaded files.
```

Examples:

- Lab exams
- Medical reports
- Nutrition plans
- Sleep reports
- Wearable exports
- Supplement lists
- Personal notes

Rules:

- Private bucket
- User can access only own files
- Admin access only if explicitly allowed
- Deletion path required

---

## public_assets

Purpose:

```text
Stores public app assets.
```

Examples:

- Public images
- App content visuals
- Public educational assets

Rules:

- Public read
- Admin write

---

## admin_assets

Purpose:

```text
Stores admin-managed internal assets.
```

Examples:

- Draft content assets
- Campaign images
- Plan images
- Internal documents

Rules:

- Admin-only access
- Not exposed unless published

---

# Row Level Security Direction

RLS should be enabled for user-owned tables.

User-owned tables include:

```text
user_profiles
user_settings
user_aai_context
user_active_plans
user_pillar_states
daily_plans
daily_actions
push_events
stack_items
wearable_connections
wearable_metric_snapshots
user_uploads
recommendations
user_commerce_benefits
commerce_events
```

Basic rule:

```text
Authenticated users can read and write only their own data.
```

Admin-managed tables should not be freely writable by users.

Admin-managed tables include:

```text
plan_templates
plan_template_versions
pillar_definitions
content_modules
commerce_benefits
admin_audit_log
```

Basic rule:

```text
Users can read published/active records when allowed.
Only admins can create, update or archive admin-managed records.
```

---

# RLS Pattern

Recommended user-owned read rule:

```text
user_id = auth.uid()
```

Recommended user-owned insert rule:

```text
user_id = auth.uid()
```

Recommended user-owned update rule:

```text
user_id = auth.uid()
```

Recommended admin rule:

```text
user has admin role
```

Admin role may be implemented through:

```text
user_roles table
custom claims
service role only
admin panel backend
```

Do not expose service role keys to FlutterFlow.

---

# Edge Functions

Supabase Edge Functions may be used for controlled backend logic.

Possible Edge Functions:

```text
activate_plan
generate_daily_plan
process_push_response
update_home_state
evaluate_aai_context
sync_wearable_snapshot
process_user_upload
issue_commerce_benefit
track_commerce_event
admin_publish_plan
```

---

## activate_plan

Purpose:

```text
Creates a user active plan snapshot from a published Plan Template version.
```

Actions:

- Validate user
- Validate plan version
- Create user_active_plans record
- Create initial pillar states
- Create first daily plan
- Initialize home state
- Log activation event

---

## generate_daily_plan

Purpose:

```text
Creates or updates the user’s daily plan.
```

Inputs:

- User profile
- Active plan
- Pillar states
- Wearable snapshot
- Recent daily actions
- Push response history
- AAI context

Output:

- daily_plans record
- daily_actions records
- updated home state

---

## process_push_response

Purpose:

```text
Processes Confirm, Adjust or Later from Push.
```

Actions:

- Update push_events
- Update daily_actions
- Update pillar state
- Update home state
- Schedule follow-up if needed

---

## update_home_state

Purpose:

```text
Updates the current Home operating state.
```

Home state may include:

- Current Insight
- Next Best Action
- Pillar orb states
- Daily progress
- Recovery status
- Adaptive summary

---

## evaluate_aai_context

Purpose:

```text
Updates interpreted AAI context for the user.
```

Inputs:

- Profile
- Settings
- Active plan
- Daily behavior
- Pillar states
- Wearables
- Upload summaries
- Commerce context

Output:

- updated user_aai_context

---

## process_user_upload

Purpose:

```text
Processes uploaded files when allowed.
```

Actions:

- Validate file
- Store metadata
- Extract summary if supported
- Update user context
- Respect privacy and deletion rules

---

## issue_commerce_benefit

Purpose:

```text
Determines whether a user is eligible for a commerce benefit.
```

Actions:

- Validate subscription status
- Validate rules
- Create user_commerce_benefits record
- Track benefit availability

---

# Realtime Direction

Realtime may be used carefully.

Possible realtime use cases:

- Home state updates
- Daily action updates
- Admin preview
- Push response reflection
- Recommendation updates

Avoid excessive realtime complexity in MVP.

The app can refresh data on screen load and important actions.

---

# Admin Publishing Flow

Admin-managed records should support publishing.

Example flow:

```text
Admin creates draft
↓
Admin previews
↓
Admin publishes
↓
Published version becomes visible
↓
App reads published content
```

Applies to:

- Plan Templates
- Plan Template Versions
- Content Modules
- Commerce Benefits
- Onboarding configuration
- Push copy
- Pillar configuration

Draft content should not appear to regular users.

---

# Event Tracking Direction

Wellbine should track core behavioral events.

Possible event table may be added later:

```text
user_events
```

Possible fields:

```text
id uuid primary key
user_id uuid references auth.users(id)
event_type text
event_payload_json jsonb
created_at timestamptz
```

Possible event types:

```text
signup_completed
onboarding_started
onboarding_completed
plan_activated
home_viewed
daily_action_confirmed
daily_action_adjusted
daily_action_delayed
push_permission_granted
push_permission_denied
wearable_connected
wearable_skipped
upload_added
commerce_benefit_used
account_deleted
```

For MVP, event tracking may be distributed across specific tables.

Later, a centralized `user_events` table can improve analytics.

---

# Home State Direction

A dedicated table may be added:

```text
user_home_state
```

Possible fields:

```text
id uuid primary key
user_id uuid references auth.users(id)
active_plan_id uuid references user_active_plans(id)
current_insight text
next_best_action text
adaptive_summary_json jsonb
pillar_orbs_json jsonb
home_status text
last_updated_at timestamptz
created_at timestamptz
updated_at timestamptz
```

This table may be useful because Home is the central operating surface.

If Home becomes complex, creating `user_home_state` is recommended.

---

# Account Deletion Direction

Account deletion must consider:

- user_profiles
- user_settings
- user_aai_context
- user_active_plans
- user_pillar_states
- daily_plans
- daily_actions
- push_events
- stack_items
- wearable_connections
- wearable_metric_snapshots
- user_uploads
- recommendations
- user_commerce_benefits
- commerce_events
- uploaded files in Storage

Deletion should be implemented carefully.

Some records may be deleted.

Some records may be anonymized.

Some records may be retained if legally required.

Privacy Policy must match actual behavior.

---

# Privacy Direction

Sensitive data should be minimized.

Wellbine should avoid storing unnecessary raw health data.

Preferred approach:

```text
Store useful context, not excessive raw data.
```

Examples:

- Daily wearable snapshot instead of endless raw streams
- Upload summary instead of unnecessary duplicated file content
- User-controlled settings
- Clear deletion path
- Private storage buckets

---

# MVP Implementation Order

Recommended Supabase implementation order:

```text
1. Auth
2. user_profiles
3. user_settings
4. plan_templates
5. plan_template_versions
6. user_active_plans
7. pillar_definitions
8. user_pillar_states
9. daily_plans
10. daily_actions
11. push_events
12. user_home_state
13. stack_items
14. wearable_connections
15. wearable_metric_snapshots
16. user_uploads
17. content_modules
18. recommendations
19. commerce_benefits
20. user_commerce_benefits
21. commerce_events
22. admin_audit_log
```

Commerce can be implemented after the core operating experience is stable.

Wearables can be optional.

Uploads can be optional.

Push can degrade gracefully.

---

# MVP Tables Required For First Functional Product

Minimum useful MVP:

```text
user_profiles
user_settings
plan_templates
plan_template_versions
user_active_plans
pillar_definitions
user_pillar_states
daily_plans
daily_actions
push_events
user_home_state
```

Strong next layer:

```text
stack_items
wearable_connections
wearable_metric_snapshots
user_uploads
content_modules
recommendations
```

Monetization layer:

```text
commerce_benefits
user_commerce_benefits
commerce_events
```

Operational layer:

```text
admin_audit_log
user_aai_context
```

---

# What The Schema Should Not Do

The schema should not:

- Force every future business rule into rigid columns
- Hardcode plan names
- Hardcode discount amounts
- Hardcode commerce platforms
- Hardcode wearable providers as permanent limits
- Require wearables for app usage
- Require uploads for onboarding
- Store excessive raw health data without need
- Expose admin tables to regular users
- Expose service role keys to FlutterFlow
- Make FlutterFlow the source of truth
- Break existing active plans when templates are updated

---

# Success Criteria

The Supabase schema is successful when:

- Users can onboard
- Users can activate a plan
- Home can load meaningful state
- Daily can show actions
- Push can record responses
- Pillars can update
- Admin can publish plans
- Wearables can be optional
- Uploads can be optional
- Commerce Bridge can be hidden or enabled
- AAI can read structured context
- RLS protects user data
- FlutterFlow can build the product without fragile hardcoding

---

# Current Status

Supabase Schema is currently a draft implementation blueprint.

Next steps:

- Convert this blueprint into actual Supabase SQL migrations
- Define initial RLS policies
- Define storage buckets
- Define first Edge Functions
- Build first FlutterFlow screens against real tables
- Build Admin MVP around Plan Templates and user visibility
- Test onboarding to Home activation flow

---

# Related Documents

- FOUNDATION/AAI_CONSTITUTION.md
- FOUNDATION/AAI_GLOSSARY.md
- FOUNDATION/AAI_PRINCIPLES.md
- FRAMEWORKS/POPAE.md
- PRODUCTS/WELLBINE/README.md
- PRODUCTS/WELLBINE/PRODUCT.md
- PRODUCTS/WELLBINE/BCAS.md
- PRODUCTS/WELLBINE/PLAN_TEMPLATES.md
- PRODUCTS/WELLBINE/ONBOARDING.md
- PRODUCTS/WELLBINE/HOME.md
- PRODUCTS/WELLBINE/DAILY.md
- PRODUCTS/WELLBINE/PUSH.md
- PRODUCTS/WELLBINE/PILLARS.md
- PRODUCTS/WELLBINE/STACK.md
- PRODUCTS/WELLBINE/ADMIN.md
- PRODUCTS/WELLBINE/DATA_MODEL.md
- PRODUCTS/WELLBINE/IMPLEMENTATION_PLAN.md
- PRODUCTS/WELLBINE/WEARABLES.md
- PRODUCTS/WELLBINE/APP_RELEASE.md
- PRODUCTS/WELLBINE/COMMERCE_BRIDGE.md
- ARCHITECTURE_DECISIONS/HOME_CENTRAL.md
- ARCHITECTURE_DECISIONS/PUSH_ORCHESTRATION.md
- ARCHITECTURE_DECISIONS/PLAN_TEMPLATES_DB.md
- ARCHITECTURE_DECISIONS/ADMIN_CONTROL_LAYER.md
- ARCHITECTURE_DECISIONS/ONBOARDING_ACTIVATION.md
