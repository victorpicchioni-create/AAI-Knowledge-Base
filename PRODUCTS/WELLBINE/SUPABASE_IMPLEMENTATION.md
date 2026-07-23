# Wellbine Supabase Implementation

**Version:** 0.1.0

**Status:** Draft

**Last Updated:** July 2026

---

# Purpose

This document defines the practical Supabase implementation plan for Wellbine.

The goal is to translate `SUPABASE_SCHEMA.md` into a buildable Supabase backend structure that supports FlutterFlow, Admin, AAI, Push, Daily, Home, Pillars, Wearables, Uploads and Commerce Bridge.

This document covers:

- Supabase project setup
- Environment structure
- Authentication
- Database implementation order
- Table creation direction
- Row Level Security
- Storage buckets
- Edge Functions
- Admin access
- Seed data
- FlutterFlow connection
- Testing
- Launch readiness

This document is an implementation guide.

It is not the final SQL migration file.

---

# Official Definition

**Wellbine Supabase Implementation is the practical backend setup process that turns the Wellbine data model and schema blueprint into a working Supabase environment for the mobile app, Admin layer and AAI services.**

---

# Core Principle

The core implementation rule is:

```text
Build Supabase as the source of truth before building complex frontend behavior.
```

FlutterFlow should not become the place where Wellbine logic is permanently hardcoded.

Supabase should store:

- User identity
- User profile
- User settings
- Plan Templates
- Active plan snapshots
- Pillar states
- Daily plans
- Daily actions
- Home state
- Push events
- Stack items
- Wearable connections
- Upload metadata
- Commerce benefits
- AAI context
- Admin-managed configuration

FlutterFlow should display, capture and trigger.

Supabase should own durable state.

---

# Implementation Philosophy

Wellbine should be implemented in layers.

The backend should not try to solve every future possibility in the first version.

The correct approach is:

```text
Stable core tables
+
Flexible JSON configuration
+
RLS protection
+
Edge Functions for sensitive workflows
+
Admin-managed configuration
```

Avoid two extremes:

```text
Too rigid:
Everything hardcoded into columns and frontend logic.

Too loose:
Everything stored as unstructured JSON with no clear relationships.
```

The right MVP balance is:

```text
Relational identity and ownership
+
JSON for flexible product rules
```

---

# Recommended Environment Structure

Use separate environments where possible:

```text
Development
Staging
Production
```

---

## Development

Used for:

- Fast iteration
- Schema drafts
- FlutterFlow testing
- Broken data allowed
- Developer experiments
- Temporary tables
- Early Edge Function testing

Development should not be used for app review or real users.

---

## Staging

Used for:

- QA
- Internal testing
- TestFlight
- Google internal testing
- App review preparation
- Release candidate validation

Staging should be as close as possible to production.

---

## Production

Used for:

- Real users
- Real subscriptions
- Real Push behavior
- Real uploaded files
- Real privacy obligations
- Real commerce benefits
- Real app store release

Production changes should be controlled.

---

# Supabase Project Setup

Initial setup:

```text
Create Supabase project
Set project region
Configure authentication
Configure database
Enable RLS
Create storage buckets
Prepare environment variables
Prepare Edge Functions
Connect FlutterFlow
Create initial admin user strategy
Create seed data
Run QA
```

Important rule:

```text
Do not connect production FlutterFlow builds to an unstable development database.
```

---

# Environment Variables

Wellbine should separate environment variables by environment.

Possible variables:

```text
SUPABASE_URL
SUPABASE_ANON_KEY
SUPABASE_SERVICE_ROLE_KEY
SUPABASE_PROJECT_REF
APP_ENV
APP_BASE_URL
ADMIN_BASE_URL
EDGE_FUNCTION_BASE_URL
PUSH_PROVIDER_KEY
AI_PROVIDER_KEY
STORAGE_BUCKET_USER_UPLOADS
```

Security rule:

```text
The service role key must never be exposed in FlutterFlow frontend code.
```

Frontend uses:

```text
SUPABASE_URL
SUPABASE_ANON_KEY
```

Backend / Edge Functions may use:

```text
SUPABASE_SERVICE_ROLE_KEY
```

only when properly protected.

---

# Authentication Implementation

Supabase Auth should manage user identity.

Minimum MVP auth:

```text
Email signup
Email login
Logout
Password reset
Auth session persistence
```

Possible future auth:

```text
Apple Sign In
Google Sign In
Magic link
Phone login
```

Auth should produce:

```text
auth.users.id
```

This ID should connect to user-owned records through:

```text
user_id
```

---

# User Creation Flow

After signup, create the user baseline.

Recommended flow:

```text
User signs up
↓
Supabase Auth creates auth user
↓
App checks user_profiles
↓
If missing, create user_profiles record
↓
Create user_settings record
↓
Route to onboarding
```

Possible implementation:

```text
FlutterFlow creates profile after auth
```

or:

```text
Database trigger creates profile automatically
```

or:

```text
Edge Function creates profile and settings
```

Recommended MVP:

```text
Use controlled frontend creation first if RLS is correct.
Move to Edge Function or trigger if needed.
```

---

# Database Implementation Order

Recommended table implementation order:

```text
1. user_profiles
2. user_settings
3. plan_templates
4. plan_template_versions
5. user_active_plans
6. pillar_definitions
7. user_pillar_states
8. daily_plans
9. daily_actions
10. user_home_state
11. push_events
12. stack_items
13. wearable_connections
14. wearable_metric_snapshots
15. user_uploads
16. content_modules
17. recommendations
18. commerce_benefits
19. user_commerce_benefits
20. commerce_events
21. user_aai_context
22. admin_audit_log
```

The first functional MVP does not need every table fully advanced.

The critical path is:

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
user_home_state
```

---

# Table Creation Direction

Every major table should include:

```text
id
created_at
updated_at
```

User-owned tables should include:

```text
user_id
```

Admin-managed tables should include when useful:

```text
created_by
updated_by
status
published_at
metadata_json
```

Flexible tables should include:

```text
configuration_json
metadata_json
rules_json
```

---

# Timestamp Standard

Recommended timestamp fields:

```text
created_at timestamptz default now()
updated_at timestamptz default now()
```

For important lifecycle events:

```text
started_at
ended_at
published_at
completed_at
deleted_at
expires_at
last_sync_at
last_evaluated_at
```

Do not rely only on `updated_at` to understand product events.

---

# Status Fields

Use text-based statuses in MVP.

Examples:

```text
draft
published
archived
active
inactive
completed
skipped
delayed
expired
cancelled
error
```

Avoid heavy enum design at the start unless needed.

Enums can be added later after the product behavior stabilizes.

---

# JSON Field Usage

Use JSONB for flexible configuration.

Recommended JSONB fields:

```text
configuration_json
metadata_json
rules_json
eligibility_rules_json
visibility_rules_json
content_json
payload_json
state_json
```

Use JSONB for:

- Plan configuration
- Pillar defaults
- Daily rules
- Push rules
- Commerce rules
- Visibility rules
- User preferences
- Provider metadata
- Upload metadata
- AAI context

Do not use JSONB for everything.

Important query fields should remain normal columns.

---

# Row Level Security Implementation

RLS should be enabled early.

Do not postpone RLS until the end.

User-owned tables should follow this rule:

```text
Users can read and write only rows where user_id = auth.uid()
```

Admin-managed tables should follow this rule:

```text
Users can read published or active records when allowed.
Only admins can create, update or archive admin-managed records.
```

---

# User-Owned Tables

Enable RLS for:

```text
user_profiles
user_settings
user_aai_context
user_active_plans
user_pillar_states
daily_plans
daily_actions
user_home_state
push_events
stack_items
wearable_connections
wearable_metric_snapshots
user_uploads
recommendations
user_commerce_benefits
commerce_events
```

Basic user policy concept:

```text
user_id = auth.uid()
```

---

# Admin-Managed Tables

Admin-managed tables include:

```text
plan_templates
plan_template_versions
pillar_definitions
content_modules
commerce_benefits
admin_audit_log
```

Regular users may read:

```text
published plans
active pillars
published content
active commerce benefits when eligible
```

Regular users should not be able to:

```text
create plan templates
edit plan templates
publish plans
edit pillar definitions
edit content modules
edit commerce campaigns
read admin audit logs
```

---

# Admin Role Direction

Admin access may be implemented through:

```text
user_roles table
custom claims
backend-only service role
admin panel authentication
```

Recommended MVP direction:

```text
Use a user_roles table or admin-only backend access.
Do not expose admin writes directly to normal app users.
```

Possible `user_roles` fields:

```text
id
user_id
role
status
created_at
updated_at
```

Possible roles:

```text
owner
admin
editor
support
viewer
```

---

# Service Role Safety

The Supabase service role key bypasses RLS.

Never expose it in:

```text
FlutterFlow
mobile app code
public frontend
client-side environment variables
public GitHub repository
```

Use service role only inside:

```text
Edge Functions
secure backend
server-side admin workflows
protected automation
```

---

# Storage Implementation

Recommended storage buckets:

```text
user_uploads
public_assets
admin_assets
```

---

## user_uploads

Use for private user files.

Rules:

```text
private bucket
authenticated access only
user can access own files only
file path should include user_id or protected ownership reference
deletion must be supported
```

Possible path structure:

```text
user_uploads/{user_id}/{upload_id}/{file_name}
```

---

## public_assets

Use for public assets.

Examples:

```text
public images
content images
public educational assets
```

Rules:

```text
public read
admin write
```

---

## admin_assets

Use for internal or admin-managed assets.

Rules:

```text
admin read/write
publish only when approved
```

---

# Upload Implementation

Upload flow:

```text
User selects file
↓
FlutterFlow uploads file to Supabase Storage
↓
Create user_uploads metadata record
↓
Optional Edge Function processes file
↓
Summary or extraction status updates user_uploads
↓
AAI context may update
```

Important rules:

```text
Uploads are optional.
Uploads must not block onboarding.
Uploads should be deletable.
Private files must not be publicly accessible.
```

---

# Plan Template Implementation

Plan Templates should be admin-managed.

Implementation tables:

```text
plan_templates
plan_template_versions
```

Flow:

```text
Admin creates draft template
↓
Admin creates version configuration
↓
Admin publishes version
↓
Published version becomes available to users
↓
User activation creates snapshot
```

Critical rule:

```text
User active plans should reference a specific published version.
```

Do not let plan edits unexpectedly change active user plans unless intentionally designed.

---

# Plan Activation Implementation

Plan activation should preferably use an Edge Function.

Function:

```text
activate_plan
```

Input:

```text
user_id
plan_template_id
plan_template_version_id
activation_source
```

Actions:

```text
Validate user
Validate published plan version
Create user_active_plans snapshot
Create user_pillar_states
Create daily_plans
Create daily_actions
Create user_home_state
Log activation
Return success and home route
```

Avoid frontend-only activation if it requires multiple dependent inserts.

---

# Pillar Implementation

Create initial `pillar_definitions`.

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

Each pillar should include:

```text
name
slug
description
status
sort_order
default_configuration_json
metadata_json
```

User-specific pillar state should live in:

```text
user_pillar_states
```

Home should read from user pillar states.

---

# Daily Implementation

Daily is driven by:

```text
daily_plans
daily_actions
```

Daily plan represents the day.

Daily actions represent specific actions.

Action statuses:

```text
upcoming
active
completed
adjusted
delayed
skipped
expired
```

Daily actions should support:

```text
Confirm
Adjust
Later
```

Daily should sync with:

```text
Home
Pillars
Push
AAI context
```

---

# Home State Implementation

Home is central enough to justify a dedicated table:

```text
user_home_state
```

Home state may include:

```text
current_insight
next_best_action
adaptive_summary_json
pillar_orbs_json
home_status
last_updated_at
```

Home should not calculate everything on the frontend.

Frontend can display Home state.

Backend logic should prepare Home state when needed.

---

# Push Implementation

Push data should be stored in:

```text
push_events
```

Push must support:

```text
scheduled
sent
delivered
responded
failed
cancelled
expired
```

Push responses:

```text
confirm
adjust
later
dismissed
none
```

Push response should call:

```text
process_push_response
```

This function should update:

```text
push_events
daily_actions
user_pillar_states
user_home_state
user_aai_context if needed
```

Push should respect:

```text
user_settings.push_enabled
user_settings.mental_detox_enabled
notification_preferences_json
```

---

# Daily Stack Implementation

Daily Stack uses:

```text
stack_items
```

MVP stack actions:

```text
add
edit
delete
mark taken
skip
set timing
set frequency
```

Important product boundary:

```text
Daily Stack organizes routines. It does not prescribe medication.
```

If Stack connects to Commerce Bridge, this should be contextual and configurable.

---

# Wearables Implementation

Wearables use:

```text
wearable_connections
wearable_metric_snapshots
```

MVP may begin with:

```text
manual provider
connection status placeholder
last sync placeholder
future provider support
```

Important rules:

```text
Wearables are optional.
Wellbine must work without wearables.
Do not claim unsupported integrations.
Store useful summaries, not excessive raw streams.
```

---

# Uploads Implementation

Uploads use:

```text
user_uploads
Supabase Storage
process_user_upload function if needed
```

Upload status values:

```text
uploaded
processing
processed
failed
deleted
```

Extraction status values:

```text
not_started
processing
completed
failed
```

Uploads should be optional and deletable.

---

# Content Module Implementation

Content should live in:

```text
content_modules
```

Use content modules for:

```text
educational content
onboarding copy
pillar explanations
plan content
stack content
commerce content
FAQ
```

Avoid hardcoding content that may change frequently.

Admin should control content where practical.

---

# Recommendations Implementation

Recommendations use:

```text
recommendations
```

Recommendation sources:

```text
aai
admin
plan_template
daily
pillar
commerce
wearable
upload
```

Recommendation placements:

```text
home
daily
pillar
stack
personal_center
commerce
```

Recommendations should be contextual.

They should not become noise.

---

# Commerce Bridge Implementation

Commerce Bridge uses:

```text
commerce_benefits
user_commerce_benefits
commerce_events
```

MVP flow:

```text
User is eligible
↓
Benefit appears
↓
User taps one primary action
↓
Benefit code is copied
↓
External commerce destination opens
↓
Event is tracked
```

Important rules:

```text
Do not hardcode discount amounts.
Do not hardcode commerce platform.
Do not create Store as fixed primary navigation in MVP.
Commerce Bridge must be hideable by configuration.
```

---

# Commerce Event Implementation

MVP events:

```text
benefit_viewed
benefit_button_tapped
coupon_copied
external_store_opened
```

Future events:

```text
checkout_started
coupon_applied
purchase_completed
redemption_confirmed
```

Purchase confirmation may require:

```text
webhook
API integration
manual import
commerce platform integration
```

Do not block MVP on purchase confirmation.

---

# AAI Context Implementation

AAI context may use:

```text
user_aai_context
```

This table stores interpreted state, not raw event history.

It may include:

```text
current_context_json
recent_behavior_json
current_plan_context_json
pillar_context_json
wearable_context_json
daily_context_json
commerce_context_json
```

AAI context should be updated through controlled backend logic.

Possible function:

```text
evaluate_aai_context
```

---

# Edge Functions Implementation Order

Recommended Edge Function order:

```text
1. activate_plan
2. generate_daily_plan
3. update_home_state
4. process_push_response
5. evaluate_aai_context
6. process_user_upload
7. issue_commerce_benefit
8. track_commerce_event
9. admin_publish_plan
10. sync_wearable_snapshot
```

Do not build all functions before the core MVP is usable.

Start with:

```text
activate_plan
update_home_state
process_push_response
```

---

# Edge Function Error Handling

Every Edge Function should handle:

```text
missing auth
invalid input
unauthorized access
missing record
duplicate action
partial failure
database error
unexpected error
```

Return clear error responses.

Avoid exposing sensitive backend details to the frontend.

---

# Seed Data

Initial seed data should include:

```text
pillar_definitions
test plan_templates
test plan_template_versions
basic content_modules
optional test commerce_benefits
test admin user role
```

Seed data should be different from production content.

Draft test data should not appear to users in production.

---

# FlutterFlow Connection

FlutterFlow should connect to Supabase using:

```text
Supabase URL
Supabase anon key
```

FlutterFlow should:

```text
Authenticate users
Read user-owned data through RLS
Write user-owned actions through RLS
Read published admin-managed records
Call Edge Functions for sensitive workflows
Upload files to protected storage
```

FlutterFlow should not:

```text
use service role key
write admin-managed tables directly as a normal user
hardcode all plan logic
hardcode all commerce rules
bypass backend validation
```

---

# Admin Implementation Direction

Admin may be built using:

```text
Softr
Retool
Supabase Studio
Custom admin panel
```

Admin should manage:

```text
Plan Templates
Plan Versions
Pillars
Content Modules
Recommendations
Commerce Benefits
Feature visibility
Publishing status
```

Admin actions should be logged in:

```text
admin_audit_log
```

Where practical.

---

# Feature Visibility Implementation

Feature visibility should be configurable.

Possible configuration sources:

```text
user_settings
plan_template_versions.configuration_json
remote_config table
admin-managed feature flags
```

Possible feature flags:

```text
wearables_enabled
uploads_enabled
commerce_bridge_enabled
ask_wellbine_enabled
daily_stack_enabled
subscriptions_enabled
push_enabled
```

Important rule:

```text
Unfinished features should be hidden by configuration.
```

---

# Account Deletion Implementation

Account deletion must be implemented before release.

Possible flow:

```text
User requests deletion
↓
Confirm intent
↓
Call delete_account Edge Function
↓
Delete or anonymize user-owned records
↓
Delete uploads or mark for deletion
↓
Disconnect wearable connections
↓
Handle subscription implications
↓
Delete auth user or mark account deleted
```

Actual behavior must match Privacy Policy.

Do not promise deletion behavior that is not implemented.

---

# Privacy Implementation

Privacy must be implemented in the backend, not only written in policy.

Required controls:

```text
RLS
private storage buckets
restricted admin access
delete upload
disconnect wearable
disable push
delete account
accurate data collection
minimal sensitive data
```

---

# Logging And Audit

Operational logs may include:

```text
admin_audit_log
commerce_events
push_events
user_events future table
edge function logs
```

Do not log sensitive personal data unnecessarily.

Logs should support debugging without creating privacy risk.

---

# Testing Before FlutterFlow Build

Before connecting FlutterFlow, confirm:

```text
Auth works
Core tables exist
RLS policies exist
Seed pillars exist
At least one published plan exists
Plan activation function works or plan activation writes are ready
Storage bucket exists if uploads are visible
Basic user can read own data
Basic user cannot read other users' data
```

---

# Testing With FlutterFlow

After connecting FlutterFlow, test:

```text
Signup
Profile creation
Settings creation
Onboarding save
Plan read
Plan activation
Home read
Daily read
Daily action update
Pillar state update
Push response simulation
Stack item creation
Upload if enabled
Commerce benefit if enabled
Account deletion path
```

---

# Launch Readiness

Supabase implementation is launch-ready when:

```text
Production project exists
RLS is enabled and tested
User-owned data is protected
Service role key is not exposed
Core tables are stable
Plan activation works
Home state works
Daily actions work
Push events work
Account deletion works
Privacy behavior matches policy
FlutterFlow app connects correctly
Admin content can be controlled
Critical features can be hidden
QA passes
```

---

# What Supabase Implementation Should Not Do

Supabase implementation should not:

- Skip RLS
- Expose service role key
- Depend on FlutterFlow for sensitive logic
- Hardcode future business rules
- Store excessive raw health data
- Require wearable connection
- Require uploads
- Make commerce mandatory
- Expose draft admin content
- Break active user plans when templates change
- Launch before account deletion exists
- Claim data deletion that is not implemented

---

# Current Status

Supabase Implementation is currently a draft.

Next steps:

- Create Supabase project
- Define environments
- Create initial tables
- Enable RLS
- Create storage buckets
- Add seed pillar definitions
- Add first Plan Template
- Create Plan Template version
- Implement plan activation
- Connect FlutterFlow
- Test signup to Home flow
- Add Daily and Pillar updates
- Add Push response handling
- Add optional Uploads, Wearables and Commerce Bridge

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
- PRODUCTS/WELLBINE/SUPABASE_SCHEMA.md
- PRODUCTS/WELLBINE/QA_PLAN.md
- PRODUCTS/WELLBINE/PRIVACY_POLICY_DRAFT.md
- PRODUCTS/WELLBINE/TERMS_DRAFT.md
- PRODUCTS/WELLBINE/APP_RELEASE_CHECKLIST.md
- PRODUCTS/WELLBINE/FLUTTERFLOW_BUILD_GUIDE.md
