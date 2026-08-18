# Wellbine Data Model

**Version:** 0.1.0

**Status:** Draft

**Last Updated:** July 2026

---

# Purpose

This document defines the initial data model direction for Wellbine.

The goal is to translate the product architecture into database-ready structures that can support:

- Plan Templates
- User Active Plan Snapshots
- Onboarding
- Home
- Daily
- Push
- Pillars
- Daily Stack
- Wearables
- Settings
- Uploads
- Content
- Recommendations
- Admin configuration
- AAI context evolution

This document is not the final SQL schema.

It defines the conceptual and operational data model that should guide Supabase, FlutterFlow and Admin implementation.

---

# Official Definition

**The Wellbine Data Model is the structured representation of users, plans, pillars, actions, signals, settings and adaptive context required to operate Wellbine as an AAI-powered daily health alignment system.**

---

# Core Principle

The data model should support one main rule:

```text
Wellbine should be configurable, adaptive and user-specific without requiring code changes for normal business updates.
```

The database should not only store user data.

It should also store product configuration.

This allows Wellbine to operate as a system, not a static app.

---

# Data Model Philosophy

The data model should support:

- Database-driven product behavior
- Admin-managed configuration
- User-specific personalization
- Plan versioning
- Active plan snapshots
- Progressive profiling
- Push orchestration
- Pillar state tracking
- Daily execution
- Wearable fallback
- Upload enrichment
- AAI context evolution

The model should remain flexible enough for early product iteration.

It should not become over-engineered before the first usable product is built.

---

# Naming Convention

Database tables should use:

```text
lower_snake_case
```

Examples:

```text
user_profiles
plan_templates
user_active_plans
daily_actions
push_events
user_pillar_states
```

Document filenames remain uppercase.

Database tables should remain lowercase.

---

# High-Level Architecture

Recommended data flow:

```text
Admin Configuration
↓
Plan Templates
↓
Onboarding
↓
User Active Plan Snapshot
↓
Daily + Push + Pillars + Home
↓
User Actions + Wearable Signals + Uploads
↓
AAI Context Evolution
```

---

# Core Data Groups

The Wellbine data model can be organized into the following groups:

```text
1. Users
2. Plan Templates
3. User Active Plans
4. Pillars
5. Daily
6. Push
7. Home
8. Daily Stack
9. Wearables
10. Settings
11. Uploads
12. Content
13. Recommendations
14. Admin
15. AAI Context
16. Events / Logs
```

---

# 1. Users

Users are the foundation of the system.

The user model should separate authentication from health/profile context.

Authentication may be handled by Supabase Auth.

Product-specific information should be stored in app tables.

---

## user_profiles

Stores essential profile information.

Possible fields:

```text
id
user_id
display_name
biological_sex
age
height_cm
weight_kg
relevant_comorbidities_status
relevant_comorbidities_notes
primary_goal
timezone
language
units
created_at
updated_at
```

Notes:

- `user_id` should connect to Supabase Auth.
- Biological sex should be treated as a physiological personalization field.
- Relevant comorbidities should remain optional.
- This table should not become a complete medical record.

---

## user_health_context

Stores additional evolving health context.

Possible fields:

```text
id
user_id
sleep_preference
wake_preference
nutrition_preference
movement_level
hydration_preference
stress_context
recovery_need
fasting_preference
daily_stack_interest
wearable_status
upload_status
created_at
updated_at
```

This table supports progressive profiling.

Not all fields need to be collected during Onboarding.

---

# 2. Plan Templates

Plan Templates define reusable starting configurations.

They should be database-driven and admin-managed.

---

## plan_templates

Stores the main plan entity.

Possible fields:

```text
id
name
slug
description
category
status
featured
default_duration_days
primary_goal
target_profile
admin_notes
created_at
updated_at
```

Possible statuses:

```text
draft
published
archived
```

Examples:

```text
LONG40
METABOLIC_RESET
GLP1_SUPPORT
SLEEP_RECOVERY
ENERGY_BASE
```

The system should not hardcode plan names.

---

## plan_template_versions

Stores versioned configurations for plans.

Possible fields:

```text
id
plan_template_id
version_number
status
configuration_json
created_by
published_at
created_at
updated_at
```

`configuration_json` may include:

```text
home_config
daily_config
push_config
pillar_config
wearable_config
settings_config
content_config
recommendation_config
```

This allows flexible configuration before final schema hardening.

---

## plan_events

Stores plan-level lifecycle events.

Possible fields:

```text
id
plan_template_id
event_type
event_payload
created_by
created_at
```

Examples of event types:

```text
created
edited
published
archived
duplicated
featured
unfeatured
```

---

# 3. User Active Plans

When a user activates a plan, the system should create a user-specific snapshot.

The snapshot protects the original Plan Template.

---

## user_active_plans

Stores the user’s active personalized plan.

Possible fields:

```text
id
user_id
plan_template_id
plan_template_version_id
status
started_at
ended_at
current_day
duration_days
active_configuration_json
source
created_at
updated_at
```

Possible statuses:

```text
active
paused
completed
cancelled
replaced
```

Possible sources:

```text
recommended_plan
adapted_plan
manual_admin
user_selected
```

---

## user_plan_history

Stores past plans.

Possible fields:

```text
id
user_id
user_active_plan_id
plan_template_id
status
started_at
ended_at
completion_summary
created_at
```

This supports plan history and future analytics.

---

# Template Versus Snapshot

Plan Template:

```text
Reusable starting configuration.
```

User Active Plan Snapshot:

```text
User-specific active version.
```

Example:

```text
LONG40 Template
↓
User activates plan
↓
Victor's LONG40 Snapshot
↓
User adjustments modify snapshot
↓
Original LONG40 Template remains unchanged
```

---

# 4. Pillars

Pillars are operational behavior modules.

Current pillars:

- Mind
- Sun
- Hydration
- Sleep
- Meal / Nutrition
- Movement
- Daily Stack

---

## pillar_definitions

Stores available pillar types.

Possible fields:

```text
id
key
name
description
status
default_icon
default_order
created_at
updated_at
```

Examples:

```text
mind
sun
hydration
sleep
meal_nutrition
movement
daily_stack
```

---

## plan_pillar_configs

Stores pillar configuration for each Plan Template or Plan Version.

Possible fields:

```text
id
plan_template_id
plan_template_version_id
pillar_key
enabled
priority
target_config_json
daily_behavior_json
push_behavior_json
home_behavior_json
created_at
updated_at
```

Possible priority values:

```text
high
normal
low
disabled
```

---

## user_pillar_states

Stores current pillar state for the user.

Possible fields:

```text
id
user_id
user_active_plan_id
pillar_key
status
score
priority
last_updated_at
current_context
state_json
created_at
updated_at
```

Possible statuses:

```text
active
done_today
needs_attention
recoverable
window_closed
disabled
```

---

## user_pillar_events

Stores pillar-level events.

Possible fields:

```text
id
user_id
user_active_plan_id
pillar_key
event_type
event_payload
source
created_at
```

Possible sources:

```text
push
daily
home
manual
wearable
admin
aai
```

---

# 5. Daily

Daily is the deeper execution layer of the day.

It should be generated from the user active plan snapshot and current context.

---

## daily_plans

Stores each user’s daily plan.

Possible fields:

```text
id
user_id
user_active_plan_id
date
status
daily_context_json
created_at
updated_at
```

Possible statuses:

```text
planned
active
completed
partially_completed
missed
adjusted
```

---

## daily_actions

Stores individual actions inside the daily plan.

Possible fields:

```text
id
daily_plan_id
user_id
pillar_key
title
description
status
window_start
window_end
priority
action_type
source
metadata_json
created_at
updated_at
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

Possible action types:

```text
hydration
movement
meal
sleep
mind
sun
stack
check_in
recovery
```

---

## daily_checkins

Stores user responses to daily questions.

Possible fields:

```text
id
user_id
daily_plan_id
pillar_key
question
answer
answer_value
source
created_at
```

Possible sources:

```text
push
daily_screen
home
ask_wellbine
```

---

# 6. Push

Push is an orchestration layer, not a reminder system.

Push should collect context and update system state.

---

## push_sequences

Stores reusable push sequence templates.

Possible fields:

```text
id
name
key
status
cycle
plan_template_id
pillar_key
sequence_config_json
created_at
updated_at
```

Possible cycles:

```text
morning_activation
midday_alignment
evening_alignment
night_reset
```

---

## user_push_state

Stores the current push state for a user.

Possible fields:

```text
id
user_id
enabled
mental_detox_enabled
frequency_preference
last_push_at
next_push_at
push_context_json
created_at
updated_at
```

---

## push_events

Stores push delivery and response events.

Possible fields:

```text
id
user_id
user_active_plan_id
daily_plan_id
pillar_key
push_sequence_id
event_type
message
response
response_action
deep_link_target
metadata_json
created_at
```

Possible event types:

```text
sent
delivered
opened
responded
confirmed
adjusted
delayed
dismissed
failed
```

Possible response actions:

```text
confirm
adjust
later
```

---

# 7. Home

Home is the central operating surface.

Home should reflect the current user state.

---

## user_home_state

Stores the current Home state for the user.

Possible fields:

```text
id
user_id
user_active_plan_id
current_insight
next_best_action
adaptive_summary_json
pillar_summary_json
quick_actions_json
contextual_access_points_json
updated_at
created_at
```

This table may be generated or cached.

Home should update after:

- Push response
- Daily action
- Pillar event
- Wearable sync
- Upload interpretation
- Plan adjustment
- AAI update

---

# 8. Daily Stack

Daily Stack handles medications, vitamins, supplements and nutraceutical routines.

---

## stack_items

Stores user stack items.

Possible fields:

```text
id
user_id
name
item_type
instructions
timing_preference
with_food
active
created_at
updated_at
```

Possible item types:

```text
medication
vitamin
supplement
nutraceutical
other
```

---

## stack_schedules

Stores schedule rules for stack items.

Possible fields:

```text
id
stack_item_id
user_id
schedule_type
time_window
frequency
days_of_week
metadata_json
created_at
updated_at
```

---

## stack_events

Stores intake confirmations and related events.

Possible fields:

```text
id
user_id
stack_item_id
daily_plan_id
status
source
confirmed_at
metadata_json
created_at
```

Possible statuses:

```text
taken
skipped
delayed
missed
adjusted
```

---

## stack_inventory

Stores stock/refill information.

Possible fields:

```text
id
user_id
stack_item_id
quantity_remaining
unit
low_stock_threshold
refill_needed
last_updated_at
created_at
```

---

# 9. Wearables

Wearables improve automation but are optional.

---

## wearable_connections

Stores wearable provider connections.

Possible fields:

```text
id
user_id
provider
status
connected_at
last_sync_at
permissions_json
created_at
updated_at
```

Possible providers:

```text
apple_health
google_fit
garmin
oura
whoop
fitbit
other
```

---

## wearable_daily_summaries

Stores daily wearable summaries.

Possible fields:

```text
id
user_id
date
sleep_duration_minutes
sleep_quality_score
resting_heart_rate
hrv_ms
steps
active_minutes
calories
spo2
respiratory_rate
temperature_delta
stress_score
readiness_score
raw_summary_json
created_at
updated_at
```

---

## wearable_events

Stores wearable sync events.

Possible fields:

```text
id
user_id
provider
event_type
event_payload
created_at
```

Possible event types:

```text
connected
disconnected
sync_started
sync_completed
sync_failed
permissions_changed
```

---

# 10. Settings

Settings define user preferences and defaults.

---

## user_settings

Stores user-level settings.

Possible fields:

```text
id
user_id
language
timezone
units
push_frequency
mental_detox_enabled
wake_time_preference
sleep_time_preference
dietary_preference
training_level
privacy_preference
upload_preference
created_at
updated_at
```

Settings should remain editable.

Plan defaults may initialize settings, but user changes should override them.

---

# 11. Uploads

Uploads allow the user to add documents, exams and personal health data.

---

## user_uploads

Stores upload metadata.

Possible fields:

```text
id
user_id
file_name
file_type
file_url
upload_type
status
processing_status
extracted_data_json
user_notes
created_at
updated_at
```

Possible upload types:

```text
lab_exam
blood_test
medical_report
nutrition_plan
fitness_assessment
sleep_report
wearable_export
pdf
image
supplement_list
medication_list
personal_note
other
```

Possible processing statuses:

```text
not_processed
processing
processed
failed
needs_review
```

---

## upload_events

Stores upload-related events.

Possible fields:

```text
id
user_id
upload_id
event_type
event_payload
created_at
```

---

# 12. Content

Content modules should be reusable and admin-managed.

---

## content_modules

Stores reusable content.

Possible fields:

```text
id
title
slug
content_type
status
language
body
metadata_json
created_at
updated_at
```

Possible content types:

```text
education_card
meditation
breathing
movement
nutrition
sleep
hydration
recovery
stack_instruction
onboarding_explanation
plan_content
```

---

## plan_content_links

Links content to Plan Templates.

Possible fields:

```text
id
plan_template_id
plan_template_version_id
content_module_id
placement
priority
created_at
```

---

# 13. Recommendations

Recommendations should be contextual and admin-managed.

---

## recommendations

Stores reusable recommendations.

Possible fields:

```text
id
title
description
recommendation_type
status
target_url
metadata_json
created_at
updated_at
```

Possible recommendation types:

```text
content
daily_action
pillar_action
store_item
refill
partner_offer
external_link
plan_upgrade
```

---

## user_recommendation_events

Stores recommendation impressions and actions.

Possible fields:

```text
id
user_id
recommendation_id
event_type
source
created_at
```

Possible event types:

```text
shown
clicked
dismissed
accepted
converted
```

---

# 14. Admin

Admin controls product configuration.

---

## admin_users

Stores admin users and roles.

Possible fields:

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

## admin_audit_log

Stores admin changes.

Possible fields:

```text
id
admin_user_id
entity_type
entity_id
action
previous_value_json
new_value_json
created_at
```

Possible actions:

```text
created
updated
published
archived
deleted
duplicated
reordered
```

---

# 15. AAI Context

AAI context stores evolving user context and system interpretation.

This should be handled carefully.

It should not become an uncontrolled dump of sensitive data.

---

## user_aai_context

Stores the current adaptive context for the user.

Possible fields:

```text
id
user_id
context_summary_json
current_state_json
risk_flags_json
preference_patterns_json
behavior_patterns_json
last_updated_at
created_at
updated_at
```

AAI context should be updated by:

- Push responses
- Daily actions
- Pillar events
- Wearable data
- Uploads
- User settings
- Ask Wellbine interactions
- Plan adjustments

---

## aai_events

Stores AAI-related system events.

Possible fields:

```text
id
user_id
event_type
input_context_json
output_context_json
source
created_at
```

Possible sources:

```text
push
daily
home
pillar
wearable
upload
ask_wellbine
admin
system
```

---

# 16. Events / Logs

Event tables help track what happened.

Events are important for:

- Analytics
- Debugging
- User history
- AAI learning
- Admin audit
- Product improvement

---

## user_events

Generic user event log.

Possible fields:

```text
id
user_id
event_type
source
entity_type
entity_id
event_payload
created_at
```

This table may be useful before all specialized event tables are mature.

---

# Minimum MVP Data Model

The first MVP does not need every table.

A practical first version may start with:

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
stack_items
wearable_connections
user_uploads
content_modules
recommendations
admin_audit_log
```

This is enough to support the first operational version.

---

# Supabase Direction

Supabase should be used for:

- Auth
- Database
- Row Level Security
- Storage
- Edge Functions when needed
- Realtime updates when useful
- Admin data management

The model should respect Supabase Row Level Security.

Users should only access their own data.

Admin roles should have controlled access.

---

# FlutterFlow Direction

FlutterFlow should read from these tables through Supabase integration.

FlutterFlow screens may include:

- Onboarding
- Home
- Daily
- Pillar panels
- Push adjustment panels
- Daily Stack
- Settings
- Uploads
- Admin Panel if built in FlutterFlow

The data model should remain simple enough for FlutterFlow implementation.

Avoid excessive normalization too early if it makes the first version slow to build.

---

# JSON Configuration Strategy

Some fields may use JSON during early development.

Examples:

```text
configuration_json
active_configuration_json
daily_behavior_json
push_behavior_json
home_behavior_json
metadata_json
state_json
```

This allows speed and flexibility.

Over time, frequently used fields may become structured columns.

Recommended approach:

```text
Start flexible.
Structure what becomes stable.
```

---

# Privacy And Safety Direction

The data model may include sensitive health-related information.

The system should follow these principles:

- Collect only what is useful
- Keep sensitive data scoped
- Respect user permission
- Use Row Level Security
- Separate admin roles
- Avoid exposing unnecessary user details
- Avoid treating Wellbine as a diagnostic medical record
- Preserve user control over uploads and settings

---

# What This Data Model Should Not Do

The data model should not:

- Become too complex before MVP
- Hardcode business logic
- Force every plan into code
- Modify templates when users personalize plans
- Require wearables for the product to work
- Require uploads for activation
- Treat every user action as medical data
- Expose sensitive user context broadly to admin roles
- Make FlutterFlow implementation impossible
- Block fast iteration

---

# Current Status

The Wellbine Data Model is currently a conceptual model.

The next implementation steps are:

- Define MVP tables
- Decide required fields
- Create Supabase schema
- Define Row Level Security
- Connect FlutterFlow screens
- Connect Admin operations
- Define user active plan snapshot creation
- Define Push event handling
- Define Daily action updates
- Define Home state generation
- Define wearable fallback logic
- Define upload storage and metadata flow

---

# Future Evolution

Future versions may include:

- Full SQL schema
- Supabase migration files
- RLS policies
- Edge Function definitions
- Admin role permissions
- Event-driven architecture
- Analytics tables
- AAI memory architecture
- FHIR-compatible health data mapping
- Consent management
- Audit trail expansion
- Multi-language content tables
- Region-specific configuration
- Cohort analytics
- A/B testing tables

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
- ARCHITECTURE_DECISIONS/HOME_CENTRAL.md
- ARCHITECTURE_DECISIONS/PUSH_ORCHESTRATION.md
- ARCHITECTURE_DECISIONS/PLAN_TEMPLATES_DB.md
- ARCHITECTURE_DECISIONS/ADMIN_CONTROL_LAYER.md
- ARCHITECTURE_DECISIONS/ONBOARDING_ACTIVATION.md
