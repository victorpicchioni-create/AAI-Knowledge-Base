# Wellbine FlutterFlow Actions

**Version:** 0.1.0

**Status:** Draft

**Last Updated:** July 2026

---

# Purpose

This document defines the practical FlutterFlow action logic for Wellbine.

The goal is to translate the Wellbine app screens into concrete FlutterFlow actions, backend calls, Supabase operations, navigation rules and user interaction flows.

This document covers:

- Auth actions
- Onboarding actions
- Profile actions
- Plan selection actions
- Plan activation actions
- Home actions
- Daily actions
- Confirm / Adjust / Later actions
- Pillar actions
- Daily Stack actions
- Push-related actions
- Wearable actions
- Upload actions
- Commerce Bridge actions
- Settings actions
- Account deletion actions
- Error handling
- Loading states
- Supabase action rules
- Edge Function action rules

FlutterFlow is the interface layer.

Supabase is the source of truth.

Edge Functions should handle sensitive or multi-step workflows.

---

# Official Definition

**Wellbine FlutterFlow Actions are the frontend interaction rules that define what happens when users tap buttons, submit forms, confirm actions, adjust routines, delay tasks, open screens, upload files, use benefits or update their daily wellness state.**

---

# Core Principle

The core FlutterFlow action rule is:

```text
FlutterFlow captures user intent. Supabase stores state. Edge Functions handle critical logic.
```

FlutterFlow should not become the permanent owner of complex business logic.

FlutterFlow should:

- Capture input
- Validate basic fields
- Show loading states
- Call Supabase or Edge Functions
- Navigate users
- Show success or error states
- Update UI after backend state changes

FlutterFlow should not:

- Expose service role keys
- Bypass RLS
- Hardcode plan logic
- Hardcode commerce logic
- Run fragile multi-table workflows when Edge Functions are needed
- Make Push, Wearables or Uploads mandatory
- Show unfinished features without Feature Flags

---

# Action Categories

FlutterFlow actions should be grouped into:

```text
Auth Actions
Routing Actions
Onboarding Actions
Profile Actions
Plan Actions
Home Actions
Daily Actions
Pillar Actions
Daily Stack Actions
Push Actions
Wearable Actions
Upload Actions
Commerce Bridge Actions
Settings Actions
Account Actions
Error Handling Actions
```

---

# Global Action Rules

Every important action should follow this structure:

```text
1. Validate input
2. Set loading state
3. Execute action
4. Handle success
5. Handle failure
6. Refresh relevant data
7. Navigate or update UI
8. Clear loading state
```

Avoid silent failures.

Avoid leaving the user stuck.

Avoid duplicate submissions.

---

# Loading State Rule

For actions that write data or call backend logic, show a loading state.

Examples:

```text
Creating your profile...
Saving your preferences...
Preparing your plan...
Updating your day...
Opening your benefit...
Deleting your account...
```

Do not leave users tapping repeatedly without feedback.

---

# Error State Rule

Error messages should be clear, calm and recoverable.

Avoid:

```text
Something went wrong.
```

Better:

```text
We could not save this right now. Try again in a moment.
```

or:

```text
We could not update your plan right now. Please try again.
```

---

# Auth Actions

## Sign Up

Trigger:

```text
User taps Sign Up
```

Action sequence:

```text
Validate email
Validate password
Call Supabase Auth sign up
If success:
    Create or fetch user profile
    Create or fetch user settings
    Navigate to Onboarding
If failure:
    Show readable error
```

Data touched:

```text
auth.users
user_profiles
user_settings
```

Preferred future implementation:

```text
Call create_user_baseline Edge Function after auth success.
```

---

## Login

Trigger:

```text
User taps Login
```

Action sequence:

```text
Validate email
Validate password
Call Supabase Auth login
If success:
    Check onboarding_completed
    Check active plan
    Route user
If failure:
    Show readable error
```

Routing:

```text
If onboarding incomplete:
    Onboarding

If onboarding complete and no active plan:
    Plan Selection

If active plan exists:
    Home
```

---

## Logout

Trigger:

```text
User taps Logout
```

Action sequence:

```text
Call Supabase logout
Clear local temporary state
Navigate to Auth
```

---

## Password Reset

Trigger:

```text
User requests password reset
```

Action sequence:

```text
Validate email
Call Supabase password reset
Show confirmation message
```

---

# Routing Actions

## App Start Routing

Trigger:

```text
App opens
```

Action sequence:

```text
Check auth session
If no session:
    Navigate to Auth

If session exists:
    Query user_profiles
    Query user_active_plans

If profile missing:
    Create baseline or route to Onboarding

If onboarding incomplete:
    Navigate to Onboarding

If onboarding complete and no active plan:
    Navigate to Plan Selection

If active plan exists:
    Navigate to Home
```

Important rule:

```text
Do not send every authenticated user directly to Home.
```

---

# Onboarding Actions

## Save Profile Step

Trigger:

```text
User completes profile baseline step
```

Action sequence:

```text
Validate required fields
Update user_profiles
Update user_settings if language/timezone changed
Save onboarding progress if used
Navigate to next onboarding step
```

Fields:

```text
name
biological_sex
age
height_cm
weight_kg
country
language
timezone
relevant_comorbidities_json
```

Rules:

```text
Comorbidities optional.
Biological sex can be Prefer not to say.
Do not block user for optional fields.
```

---

## Skip Wearable Step

Trigger:

```text
User taps Continue Without Wearable
```

Action sequence:

```text
Record wearable skipped preference if needed
Navigate to next onboarding step
```

Data touched:

```text
user_settings
```

Important rule:

```text
Wearable connection must not block onboarding.
```

---

## Enable Push From Onboarding

Trigger:

```text
User taps Enable Guidance
```

Action sequence:

```text
Show device Push permission prompt
If accepted:
    Update user_settings.push_enabled = true
If denied:
    Update user_settings.push_enabled = false
Navigate to next onboarding step
```

Important rule:

```text
Push must not block onboarding.
```

---

## Skip Push From Onboarding

Trigger:

```text
User taps Not Now
```

Action sequence:

```text
Update user_settings.push_enabled = false
Navigate to next onboarding step
```

---

## Save Goals

Trigger:

```text
User selects goals
```

Action sequence:

```text
Store selected goals in user_profiles.metadata_json or user_settings.metadata_json
Navigate to Plan Selection
```

Future direction:

```text
Goals may later influence recommended Plan Template.
```

---

## Save Pillar Preferences

Trigger:

```text
User adjusts pillar preferences
```

Action sequence:

```text
Store preferences in user_settings or onboarding context
Navigate to optional upload or plan activation
```

---

## Skip Upload Step

Trigger:

```text
User taps Continue Without Upload
```

Action sequence:

```text
Record upload skipped state if needed
Navigate to Plan Activation
```

Important rule:

```text
Uploads must not block activation.
```

---

# Plan Actions

## Load Plan Templates

Trigger:

```text
Plan Selection screen opens
```

Action sequence:

```text
Query plan_templates where status = published
Query current published version if needed
Display Plan Cards
```

Do not display:

```text
draft plans
archived plans
broken plans
```

---

## Select Plan

Trigger:

```text
User taps a Plan Card
```

Action sequence:

```text
Store selected plan in local state
Show plan confirmation or continue to activation
```

---

## Activate Plan

Trigger:

```text
User taps Activate Plan
```

Preferred action:

```text
Call activate_plan Edge Function
```

Payload:

```json
{
  "plan_template_id": "selected_plan_template_id",
  "plan_template_version_id": "selected_plan_template_version_id",
  "activation_source": "onboarding"
}
```

Success:

```text
Set onboarding_completed = true
Refresh active plan
Refresh Home state
Navigate to Home
```

Failure:

```text
Show retry state
Do not create duplicate plans
Do not leave user stuck
```

Important rule:

```text
Plan activation should not be a fragile frontend-only multi-table insert.
```

---

# Home Actions

## Load Home

Trigger:

```text
Home screen opens
```

Action sequence:

```text
Query user_home_state
Query user_active_plans
Query user_pillar_states
Query current daily_plan
Query daily_actions
Query feature_flags
Query visible recommendations if implemented
Query commerce benefits if enabled
Display Home
```

Fallback:

```text
If user_home_state missing:
    Call update_home_state or show safe setup state
```

Home should never be blank.

---

## Tap Main Orb

Trigger:

```text
User taps Main Orb
```

Action sequence:

```text
Open Adaptive Summary
```

Adaptive Summary should read from:

```text
user_home_state.adaptive_summary_json
```

---

## Tap Pillar Orb

Trigger:

```text
User taps Pillar Orb
```

Action sequence:

```text
Open Pillar Quick Panel
Pass pillar_id or pillar_slug
Load user_pillar_state
```

---

## Tap Next Best Action

Trigger:

```text
User taps Next Best Action
```

Action depends on action type:

```text
If action_type = daily_action:
    Open Daily Action Detail

If action_type = pillar:
    Open Pillar Detail

If action_type = stack:
    Open Daily Stack

If action_type = input_required:
    Open relevant input panel

If action_type = commerce:
    Open Commerce Benefit Detail only if enabled and eligible
```

---

## Refresh Home

Trigger:

```text
User pulls to refresh or returns from action
```

Action sequence:

```text
Call update_home_state if needed
Re-query user_home_state
Update UI
```

---

# Daily Actions

## Load Daily

Trigger:

```text
Daily screen opens
```

Action sequence:

```text
Query today's daily_plan
Query daily_actions for daily_plan_id
Display current, upcoming, completed and delayed actions
```

Fallback:

```text
If no daily_plan:
    Call generate_daily_plan or show retry state
```

---

## Open Daily Action Detail

Trigger:

```text
User taps Daily Action Card
```

Action sequence:

```text
Load selected daily_action
Load related pillar if available
Show title, description, timing and controls
```

Controls:

```text
Confirm
Adjust
Later
```

---

## Confirm Daily Action

Trigger:

```text
User taps Confirm
```

Preferred action:

```text
Call process_daily_action Edge Function
```

Payload:

```json
{
  "daily_action_id": "selected_daily_action_id",
  "response": "confirm",
  "adjustment_payload": {},
  "delay_minutes": null
}
```

Success:

```text
Refresh daily_actions
Refresh user_pillar_states
Refresh user_home_state
Show confirmation
Return to Daily or Home depending context
```

Failure:

```text
Show clear retry message
```

---

## Adjust Daily Action

Trigger:

```text
User taps Adjust
```

Action sequence:

```text
Open Daily Adjustment screen or panel
Pass daily_action_id
Allow user to modify relevant context
```

After adjustment:

```text
Call process_daily_action Edge Function
```

Payload:

```json
{
  "daily_action_id": "selected_daily_action_id",
  "response": "adjust",
  "adjustment_payload": {
    "adjustment_type": "user_selected_option",
    "value": "selected_value"
  },
  "delay_minutes": null
}
```

Success:

```text
Refresh Daily
Refresh Home
Show adjusted state
```

---

## Later Daily Action

Trigger:

```text
User taps Later
```

Action sequence:

```text
Use default delay or allow user to select delay
Call process_daily_action Edge Function
```

Payload:

```json
{
  "daily_action_id": "selected_daily_action_id",
  "response": "later",
  "adjustment_payload": {},
  "delay_minutes": 60
}
```

Success:

```text
Update action status to delayed
Refresh Daily
Refresh Home
Show delayed state
```

Important rule:

```text
Later should feel like adaptation, not failure.
```

---

## Skip Daily Action

Trigger:

```text
User taps Skip if available
```

Action sequence:

```text
Call process_daily_action with response skip
Refresh Daily
Refresh Home
```

Important language rule:

```text
Skipping should not use punitive language.
```

---

# Pillar Actions

## Load Pillar Detail

Trigger:

```text
Pillar Detail opens
```

Action sequence:

```text
Query pillar_definitions
Query user_pillar_states
Query related daily_actions
Query related recommendations if enabled
Display pillar state
```

---

## Update Pillar Input

Trigger:

```text
User submits pillar input
```

Examples:

```text
Hydration cups
Sleep quality
Movement completion
Mind check-in
Nutrition feedback
Sun exposure
```

Preferred action:

```text
Call process_daily_action if linked to Daily action
or update user_pillar_states if simple and user-owned
then call update_home_state
```

Important rule:

```text
Pillar updates should reflect in Home.
```

---

# Daily Stack Actions

## Load Daily Stack

Trigger:

```text
Daily Stack screen opens
```

Action sequence:

```text
Query stack_items where user_id = auth.uid()
Display active items
```

---

## Add Stack Item

Trigger:

```text
User taps Add Item
```

Action sequence:

```text
Validate item name
Insert into stack_items
Refresh stack list
Show success
```

Fields:

```text
name
item_type
dosage_text
frequency_json
timing_json
instructions
refill_tracking_enabled
```

Boundary:

```text
Daily Stack organizes routines. It does not prescribe medication.
```

---

## Edit Stack Item

Trigger:

```text
User saves item edit
```

Action sequence:

```text
Update stack_items where user owns item
Refresh item
Show success
```

---

## Mark Stack Item Taken

Trigger:

```text
User taps Taken
```

MVP action:

```text
Update stack item metadata or create related daily action response
Refresh Daily Stack
Refresh Home if relevant
```

Future direction:

```text
Create stack_item_events table if detailed adherence history is needed.
```

---

## Delete Stack Item

Trigger:

```text
User deletes item
```

Action sequence:

```text
Confirm deletion
Delete stack_items row or set status inactive
Refresh list
```

---

# Push Actions

## Open Push Preferences

Trigger:

```text
User opens Push Preferences
```

Action sequence:

```text
Query user_settings
Display push_enabled
Display mental_detox_enabled
Display notification_preferences_json
```

---

## Enable Push

Trigger:

```text
User enables Push
```

Action sequence:

```text
Show permission explanation if needed
Request device notification permission
If accepted:
    Update user_settings.push_enabled = true
If denied:
    Update user_settings.push_enabled = false
Show result
```

---

## Disable Push

Trigger:

```text
User disables Push
```

Action sequence:

```text
Update user_settings.push_enabled = false
Show confirmation
```

---

## Process Push Deep Link

Trigger:

```text
User taps Push notification
```

Action sequence:

```text
Read push payload
Determine deep link type
Navigate to relevant screen
```

Deep link examples:

```text
Daily action detail
Pillar detail
Daily screen
Commerce benefit detail
Settings
```

Avoid sending every push to generic Home unless Home can resolve the context.

---

## Push Confirm / Adjust / Later

Trigger:

```text
User responds to Push action
```

Preferred action:

```text
Call process_push_response Edge Function
```

Payload:

```json
{
  "push_event_id": "selected_push_event_id",
  "response": "confirm",
  "response_payload": {}
}
```

Success:

```text
Update Daily
Update Home
Open relevant screen if needed
```

---

# Wearable Actions

## Open Wearable Manager

Trigger:

```text
User opens Wearable Manager
```

Action sequence:

```text
Check feature flag wearables_enabled
Query wearable_connections
Display provider status
Display manual fallback
```

---

## Connect Wearable Provider

Trigger:

```text
User taps provider
```

Action sequence:

```text
Check provider flag
Show permission explanation
Open provider connection flow if implemented
Save wearable_connections status
```

Important:

```text
Do not show provider as active if integration is not implemented.
```

---

## Skip Wearable

Trigger:

```text
User skips wearable
```

Action sequence:

```text
Set manual fallback or skipped status if needed
Continue flow
```

---

## Disconnect Wearable

Trigger:

```text
User disconnects wearable
```

Action sequence:

```text
Confirm disconnect
Update wearable_connections status
Refresh wearable state
```

---

# Upload Actions

## Open Upload Manager

Trigger:

```text
User opens Upload Manager
```

Action sequence:

```text
Check uploads_enabled flag
Query user_uploads
Display uploads
```

---

## Upload File

Trigger:

```text
User selects file
```

Action sequence:

```text
Validate file type
Validate file size
Upload to Supabase Storage
Insert user_uploads metadata
Call process_user_upload if processing enabled
Show upload status
```

Important rules:

```text
Uploads are optional.
Private bucket required.
Upload does not imply diagnosis.
```

---

## Delete Upload

Trigger:

```text
User taps Delete Upload
```

Action sequence:

```text
Confirm deletion
Delete storage object or mark deleted
Update user_uploads status
Refresh upload list
```

Deletion behavior must match Privacy Policy.

---

# Commerce Bridge Actions

## Load Commerce Benefit

Trigger:

```text
Commerce Benefit area opens
```

Action sequence:

```text
Check commerce_bridge_enabled flag
Check user eligibility
Query user_commerce_benefits
Query commerce_benefits
Display available benefit
```

If disabled:

```text
Hide Commerce Bridge
```

---

## Use Benefit

Trigger:

```text
User taps Use Benefit
```

Primary action sequence:

```text
Copy benefit code to clipboard
Track coupon_copied event
Open external commerce destination
Track external_store_opened event
Show fallback if needed
```

Preferred button:

```text
Use Benefit
```

Important rules:

```text
One primary button.
Do not hardcode discount amount.
Do not hardcode platform.
Do not make Store a fixed tab.
```

---

## Commerce Benefit Fallback

If copy fails:

```text
Show code visibly
Allow manual copy
Allow opening external link
```

If external link fails:

```text
Show retry
Keep code visible
```

---

# Settings Actions

## Open Personal Center

Trigger:

```text
User taps profile/avatar/settings
```

Action sequence:

```text
Open Personal Center
Load user profile
Load user settings
Show available controls based on Feature Flags
```

---

## Update Settings

Trigger:

```text
User changes setting
```

Action sequence:

```text
Update user_settings
Show success
Refresh settings
```

Examples:

```text
preferred_language
preferred_units
push_enabled
mental_detox_enabled
privacy_preferences_json
```

---

## Open Privacy Policy

Trigger:

```text
User taps Privacy Policy
```

Action sequence:

```text
Open internal screen or external URL
```

Must work before app review.

---

## Open Terms

Trigger:

```text
User taps Terms of Use
```

Action sequence:

```text
Open internal screen or external URL
```

Must work before app review.

---

# Account Actions

## Open Account

Trigger:

```text
User opens Account screen
```

Action sequence:

```text
Load account status
Load subscription status if visible
Show Delete Account
Show Logout
```

---

## Delete Account

Trigger:

```text
User confirms Delete Account
```

Preferred action:

```text
Call delete_account Edge Function
```

Payload:

```json
{
  "confirmation": true
}
```

Success:

```text
Show deletion confirmation
Log user out
Navigate to Auth or Goodbye screen
```

Failure:

```text
Show clear support/retry state
```

Important rule:

```text
Account deletion is release-critical.
```

---

# Feature Flag Actions

## Load Feature Flags

Trigger:

```text
App starts or Home loads
```

Action sequence:

```text
Query feature_flags
Store relevant flags in app state
Use flags for conditional visibility
```

Important:

```text
Frontend visibility is not enough for sensitive features.
Backend should also enforce important flags.
```

---

# Edge Function Call Pattern

Recommended pattern:

```text
Set loading true
Call Edge Function
If success:
    Refresh required Supabase queries
    Update UI
    Navigate if needed
If failure:
    Show readable error
Set loading false
```

Do not ignore Edge Function responses.

---

# Supabase Direct Write Pattern

Use direct writes only for simple user-owned records.

Acceptable examples:

```text
Update user profile
Update user settings
Add stack item
Edit stack item
Delete stack item
Save simple preference
```

Avoid direct frontend writes for:

```text
Plan activation
Multi-table Daily updates
Account deletion
Admin publishing
Commerce eligibility
Sensitive AAI updates
```

---

# Navigation Action Rules

Navigation should be contextual.

Examples:

```text
Confirm action from Daily:
    Stay in Daily or return Home depending context

Confirm action from Push:
    Update state and open relevant screen if needed

Tap Pillar Orb:
    Open Pillar Quick Panel

Tap Main Orb:
    Open Adaptive Summary

Tap Use Benefit:
    Copy code and open external commerce

Delete Account:
    Confirmation before backend call
```

---

# Duplicate Tap Protection

Important buttons should prevent duplicate taps.

Apply to:

```text
Activate Plan
Confirm Action
Later
Adjust Save
Upload
Use Benefit
Delete Account
Signup
Login
```

Use:

```text
loading state
disabled button state
idempotent Edge Function
```

---

# Refresh Rules

After these actions, refresh Home:

```text
Plan activated
Daily action confirmed
Daily action adjusted
Daily action delayed
Pillar input updated
Push response processed
Wearable synced
Upload processed
Commerce benefit used
```

After these actions, refresh Daily:

```text
Daily action confirmed
Daily action adjusted
Daily action delayed
Push response processed
Daily regenerated
```

After these actions, refresh Settings:

```text
Profile updated
Push settings changed
Mental Detox changed
Wearable disconnected
Upload deleted
```

---

# Minimal MVP Action Set

The first MVP needs these actions:

```text
Sign Up
Login
Logout
Save Profile
Save Onboarding Step
Load Plan Templates
Select Plan
Activate Plan
Load Home
Open Daily
Confirm Daily Action
Adjust Daily Action
Later Daily Action
Open Pillar Detail
Update Pillar Input
Open Settings
Open Privacy Policy
Open Terms
Delete Account
```

Strong MVP adds:

```text
Add Stack Item
Edit Stack Item
Mark Stack Item Taken
Enable Push
Disable Push
Process Push Deep Link
```

Optional MVP adds:

```text
Upload File
Delete Upload
Connect Wearable
Use Commerce Benefit
Ask Wellbine
```

---

# QA Checklist For Actions

Test each action for:

```text
Success
Failure
Loading state
Empty state
Invalid input
No internet
Duplicate tap
Permission denied
Feature flag disabled
Wrong user access
Navigation result
Data refresh
```

---

# What FlutterFlow Actions Should Not Do

FlutterFlow actions should not:

- Expose service role key
- Bypass RLS
- Create duplicate active plans
- Depend on hardcoded plan logic forever
- Hardcode commerce discount rules
- Require Push permission
- Require wearable connection
- Require uploads
- Leave users stuck on loading
- Hide errors silently
- Show unfinished features
- Make Home blank
- Use punitive language
- Make unsupported health claims

---

# Success Criteria

FlutterFlow Actions are successful when:

- User can move through the core operating loop
- Actions update Supabase correctly
- Home refreshes after meaningful actions
- Daily reflects user responses
- Pillars reflect user state
- Settings give control
- Optional features do not block the user
- Sensitive workflows use Edge Functions
- Errors are understandable
- The app feels coherent

---

# Current Status

FlutterFlow Actions are currently a draft.

Next steps:

- Build FlutterFlow action flows screen by screen
- Connect Supabase queries
- Connect Edge Functions
- Add loading states
- Add error states
- Add duplicate tap protection
- Test core MVP actions
- Validate against QA Plan

---

# Related Documents

- PRODUCTS/WELLBINE/FLUTTERFLOW_BUILD_GUIDE.md
- PRODUCTS/WELLBINE/SCREEN_MAP.md
- PRODUCTS/WELLBINE/MVP_BUILD_SEQUENCE.md
- PRODUCTS/WELLBINE/SUPABASE_SQL_MVP.md
- PRODUCTS/WELLBINE/SUPABASE_IMPLEMENTATION.md
- PRODUCTS/WELLBINE/EDGE_FUNCTIONS.md
- PRODUCTS/WELLBINE/FEATURE_FLAGS.md
- PRODUCTS/WELLBINE/QA_PLAN.md
