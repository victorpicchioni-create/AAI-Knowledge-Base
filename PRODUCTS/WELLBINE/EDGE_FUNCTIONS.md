# Wellbine Edge Functions

**Version:** 0.1.0

**Status:** Draft

**Last Updated:** July 2026

---

# Purpose

This document defines the Edge Functions layer for Wellbine.

The goal is to separate sensitive, multi-step and system-critical logic from FlutterFlow frontend actions.

Edge Functions should support:

- Plan activation
- Daily plan generation
- Home state updates
- Push response processing
- AAI context evaluation
- Upload processing
- Commerce benefit issuance
- Commerce event tracking
- Wearable snapshot sync
- Admin publishing
- Account deletion

FlutterFlow should trigger important workflows.

Edge Functions should execute controlled backend logic.

---

# Official Definition

**Wellbine Edge Functions are secure backend functions used to process sensitive, multi-step and adaptive workflows that should not live entirely inside the FlutterFlow frontend.**

---

# Core Principle

The core Edge Functions rule is:

```text
Frontend triggers. Backend decides.
```

FlutterFlow should not own critical business logic.

FlutterFlow should not directly perform complex chains of database writes when those writes must remain consistent.

Edge Functions should be used when:

- Multiple tables must update together
- Business rules must be enforced
- User eligibility must be checked
- Sensitive logic is involved
- Admin rules must be respected
- Duplicates must be prevented
- AAI context must be evaluated
- App state must remain consistent
- Private data should not be exposed to the frontend

---

# Edge Function Responsibilities

Edge Functions may handle:

- Input validation
- Auth validation
- User ownership checks
- Admin permission checks
- Plan version validation
- Plan snapshot creation
- Daily action generation
- Push response processing
- Home state calculation
- AAI context update
- Upload metadata processing
- Commerce benefit eligibility
- Event tracking
- Account deletion
- Audit logging

Edge Functions should keep the app reliable.

---

# What Should Stay In FlutterFlow

FlutterFlow can handle:

- UI rendering
- Form inputs
- Navigation
- Loading states
- Empty states
- Error states
- Basic user-owned inserts
- Basic user-owned updates
- Supabase reads through RLS
- Button interactions
- External link opening
- Clipboard copy
- File picker interface

FlutterFlow should not handle:

- Service role logic
- Admin publishing
- Multi-table plan activation
- AAI evaluation logic
- Sensitive eligibility rules
- Account deletion cascade
- Private backend validation
- Security-sensitive workflows

---

# Function List

Recommended Edge Functions:

```text
create_user_baseline
activate_plan
generate_daily_plan
update_home_state
process_daily_action
process_push_response
evaluate_aai_context
sync_wearable_snapshot
process_user_upload
issue_commerce_benefit
track_commerce_event
admin_publish_plan
delete_account
```

MVP priority:

```text
1. activate_plan
2. update_home_state
3. process_daily_action
4. process_push_response
5. delete_account
```

Second layer:

```text
6. generate_daily_plan
7. evaluate_aai_context
8. process_user_upload
9. issue_commerce_benefit
10. track_commerce_event
```

Admin and advanced layer:

```text
11. admin_publish_plan
12. sync_wearable_snapshot
13. create_user_baseline
```

---

# Shared Function Requirements

Every Edge Function should include:

```text
Auth validation
Input validation
Permission validation
Clear success response
Clear error response
No service role exposure
No unnecessary sensitive logging
Idempotency where needed
Audit logging where useful
```

---

# Standard Response Format

Recommended success response:

```json
{
  "success": true,
  "data": {},
  "message": "Operation completed."
}
```

Recommended error response:

```json
{
  "success": false,
  "error": {
    "code": "ERROR_CODE",
    "message": "Human-readable error message."
  }
}
```

Avoid exposing internal stack traces to the app.

---

# Standard Error Codes

Possible error codes:

```text
UNAUTHORIZED
FORBIDDEN
INVALID_INPUT
NOT_FOUND
ALREADY_EXISTS
DUPLICATE_REQUEST
PLAN_NOT_PUBLISHED
PLAN_VERSION_INVALID
NO_ACTIVE_PLAN
ACTION_EXPIRED
PERMISSION_DENIED
UPLOAD_FAILED
COMMERCE_NOT_ELIGIBLE
EXTERNAL_PROVIDER_ERROR
ACCOUNT_DELETION_FAILED
INTERNAL_ERROR
```

Error messages should be clear enough for the app to guide the user.

---

# Auth Validation

Every user-facing Edge Function should verify:

```text
User is authenticated
JWT is valid
auth.uid() matches requested user_id when user_id is provided
User has permission to perform the action
```

Do not trust frontend-provided `user_id` blindly.

Preferred logic:

```text
Read user identity from auth context.
Use that identity as source of truth.
```

---

# Admin Validation

Admin-only functions should verify admin status.

Possible admin validation sources:

```text
user_roles table
custom claims
secure admin backend
service role context
```

Admin functions should not be callable by regular users.

Admin function examples:

```text
admin_publish_plan
admin_archive_plan
admin_update_commerce_benefit
admin_publish_content
```

---

# Idempotency Rule

Some functions must prevent duplicate records.

Idempotency is important for:

```text
activate_plan
generate_daily_plan
process_push_response
process_daily_action
issue_commerce_benefit
delete_account
```

Example:

```text
If the user already has an active plan for the selected version, do not create duplicates.
```

or:

```text
If the same Push response was already processed, do not process it twice.
```

---

# create_user_baseline

Purpose:

```text
Creates the minimum user-owned records required after authentication.
```

May create:

- user_profiles
- user_settings

Input:

```json
{
  "name": "optional",
  "language": "optional",
  "timezone": "optional"
}
```

Actions:

```text
Validate authenticated user
Check if user_profiles exists
Create user_profiles if missing
Check if user_settings exists
Create user_settings if missing
Return baseline status
```

Output:

```json
{
  "success": true,
  "data": {
    "profile_created": true,
    "settings_created": true
  }
}
```

Notes:

- This can be handled by FlutterFlow in MVP if RLS is correct.
- Edge Function is safer when baseline creation becomes more complex.

---

# activate_plan

Purpose:

```text
Activates a published Plan Template version for the user and creates the initial operating state.
```

This is one of the most important Edge Functions.

Input:

```json
{
  "plan_template_id": "uuid",
  "plan_template_version_id": "uuid",
  "activation_source": "onboarding"
}
```

Actions:

```text
Validate authenticated user
Validate plan_template exists
Validate plan_template_version exists
Validate version is published
Check user does not already have conflicting active plan
Create user_active_plans snapshot
Create user_pillar_states
Create daily_plans record
Create daily_actions records
Create user_home_state
Update user_aai_context if needed
Log activation event
Return active plan and home state
```

Tables affected:

```text
user_active_plans
user_pillar_states
daily_plans
daily_actions
user_home_state
user_aai_context
```

Success criteria:

```text
After activation, the user can enter Home and see useful state.
```

Important rule:

```text
Plan activation should not be built as fragile frontend-only multi-table inserts.
```

---

# generate_daily_plan

Purpose:

```text
Generates or regenerates a Daily plan for the user.
```

Input:

```json
{
  "date": "YYYY-MM-DD",
  "force_regenerate": false
}
```

Actions:

```text
Validate authenticated user
Find active plan
Read active_configuration_json
Read user profile
Read user settings
Read pillar states
Read wearable snapshot if available
Read recent Daily behavior
Read Push response history
Create or update daily_plans
Create or update daily_actions
Update user_home_state
Update user_aai_context if needed
Return Daily plan
```

Tables affected:

```text
daily_plans
daily_actions
user_home_state
user_aai_context
```

Important rule:

```text
Daily should adapt without creating chaos.
```

If a Daily plan already exists:

```text
Do not overwrite completed actions unless explicitly intended.
```

---

# update_home_state

Purpose:

```text
Updates the user’s Home operating state.
```

Input:

```json
{
  "reason": "daily_action_updated"
}
```

Possible reasons:

```text
plan_activated
daily_generated
daily_action_updated
push_response_processed
pillar_updated
wearable_synced
upload_processed
commerce_benefit_changed
manual_refresh
```

Actions:

```text
Validate authenticated user
Read active plan
Read Daily plan
Read Daily actions
Read pillar states
Read wearable context if available
Read recommendations
Read commerce benefits if visible
Build current insight
Build next best action
Build pillar orb states
Build adaptive summary
Update user_home_state
Return updated home state
```

Tables affected:

```text
user_home_state
```

May read:

```text
user_profiles
user_settings
user_active_plans
daily_plans
daily_actions
user_pillar_states
wearable_metric_snapshots
recommendations
user_commerce_benefits
```

Success criteria:

```text
Home should not be blank after a meaningful user action.
```

---

# process_daily_action

Purpose:

```text
Processes user action on a Daily item.
```

Input:

```json
{
  "daily_action_id": "uuid",
  "response": "confirm",
  "adjustment_payload": {},
  "delay_minutes": 60
}
```

Supported responses:

```text
confirm
adjust
later
skip
```

Actions:

```text
Validate authenticated user
Validate daily_action belongs to user
Validate action status
Apply response
Update daily_actions
Update related user_pillar_states
Update user_home_state
Update user_aai_context if needed
Return updated action and Home state
```

Tables affected:

```text
daily_actions
user_pillar_states
user_home_state
user_aai_context
```

Rules:

```text
Confirm marks action completed.
Adjust opens or records modified context.
Later delays action.
Skip records intentional skip without punitive language.
```

Important language rule:

```text
The system should help the user continue, not punish the user for missing a window.
```

---

# process_push_response

Purpose:

```text
Processes Confirm, Adjust or Later from Push.
```

Input:

```json
{
  "push_event_id": "uuid",
  "response": "confirm",
  "response_payload": {}
}
```

Supported responses:

```text
confirm
adjust
later
dismissed
```

Actions:

```text
Validate authenticated user
Validate push_event belongs to user
Validate push_event is actionable
Update push_events
Update related daily_actions if applicable
Update related user_pillar_states if applicable
Update user_home_state
Schedule follow-up if Later
Update user_aai_context if needed
Return routing or updated state
```

Tables affected:

```text
push_events
daily_actions
user_pillar_states
user_home_state
user_aai_context
```

Important rule:

```text
Push is orchestration, not spam.
```

Push should respect:

```text
push_enabled
mental_detox_enabled
notification_preferences_json
```

---

# evaluate_aai_context

Purpose:

```text
Updates the interpreted AAI context for a user.
```

Input:

```json
{
  "reason": "home_state_updated"
}
```

Possible reasons:

```text
onboarding_completed
plan_activated
daily_action_completed
push_response_processed
wearable_synced
upload_processed
commerce_event_tracked
manual_refresh
```

Actions:

```text
Validate authenticated user or backend caller
Read relevant user context
Read active plan
Read Daily history
Read Pillar states
Read wearable summaries
Read upload summaries
Read Commerce context if relevant
Build interpreted context
Update user_aai_context
Return context summary
```

Tables affected:

```text
user_aai_context
```

Important rule:

```text
user_aai_context stores interpreted state, not every raw event.
```

---

# sync_wearable_snapshot

Purpose:

```text
Stores normalized wearable data summaries.
```

Input:

```json
{
  "provider": "apple_health",
  "snapshot_date": "YYYY-MM-DD",
  "metrics": {}
}
```

Actions:

```text
Validate authenticated user
Validate provider connection
Normalize metrics
Store wearable_metric_snapshots
Update wearable_connections.last_sync_at
Update user_home_state if needed
Update user_aai_context if needed
Return snapshot status
```

Tables affected:

```text
wearable_connections
wearable_metric_snapshots
user_home_state
user_aai_context
```

Important rules:

```text
Wearables are optional.
Store useful summaries, not excessive raw streams.
Do not claim unsupported integrations.
```

---

# process_user_upload

Purpose:

```text
Processes uploaded user files and updates metadata.
```

Input:

```json
{
  "user_upload_id": "uuid"
}
```

Actions:

```text
Validate authenticated user
Validate upload belongs to user
Validate file exists in storage
Update extraction_status to processing
Extract summary if supported
Update user_uploads
Update user_aai_context if useful
Return processing result
```

Tables affected:

```text
user_uploads
user_aai_context
```

Storage affected:

```text
user_uploads bucket
```

Important rules:

```text
Uploads are optional.
Uploads should be deletable.
Uploads should not create diagnosis.
Uploads should not block onboarding.
```

---

# issue_commerce_benefit

Purpose:

```text
Determines whether a user is eligible for a Commerce Bridge benefit.
```

Input:

```json
{
  "commerce_benefit_id": "uuid"
}
```

Actions:

```text
Validate authenticated user
Read commerce_benefit
Validate benefit is active
Validate eligibility rules
Validate subscription status if needed
Create or update user_commerce_benefits
Return benefit availability
```

Tables affected:

```text
commerce_benefits
user_commerce_benefits
commerce_events
```

Important rules:

```text
Do not hardcode discount amounts.
Do not hardcode commerce platform.
Commerce Bridge must be hideable.
```

---

# track_commerce_event

Purpose:

```text
Tracks Commerce Bridge events.
```

Input:

```json
{
  "commerce_benefit_id": "uuid",
  "event_type": "benefit_button_tapped",
  "event_payload": {}
}
```

MVP event types:

```text
benefit_viewed
benefit_button_tapped
coupon_copied
external_store_opened
```

Future event types:

```text
checkout_started
coupon_applied
purchase_completed
redemption_confirmed
expired
```

Actions:

```text
Validate authenticated user
Validate benefit visibility if needed
Insert commerce_events record
Update user_commerce_benefits timestamps if needed
Return success
```

Tables affected:

```text
commerce_events
user_commerce_benefits
```

Important rule:

```text
Tracking should support product learning without becoming invasive.
```

---

# admin_publish_plan

Purpose:

```text
Publishes a Plan Template version for user activation.
```

Input:

```json
{
  "plan_template_id": "uuid",
  "plan_template_version_id": "uuid"
}
```

Actions:

```text
Validate admin user
Validate draft version
Validate required configuration fields
Set version status to published
Update plan_templates.current_version_id
Update published_at
Write admin_audit_log
Return published version
```

Tables affected:

```text
plan_templates
plan_template_versions
admin_audit_log
```

Important rules:

```text
Only admins can publish plans.
Draft plans should not appear to regular users.
Published changes should not unexpectedly mutate existing user active plan snapshots.
```

---

# delete_account

Purpose:

```text
Deletes or deactivates a user account according to implemented privacy rules.
```

Input:

```json
{
  "confirmation": true
}
```

Actions may include:

```text
Validate authenticated user
Confirm deletion request
Delete or anonymize user_profiles
Delete or anonymize user_settings
Delete or anonymize user_aai_context
Handle user_active_plans
Handle daily_plans
Handle daily_actions
Handle user_pillar_states
Handle push_events
Handle stack_items
Handle wearable_connections
Handle wearable_metric_snapshots
Handle user_uploads
Delete files from storage where required
Handle recommendations
Handle user_commerce_benefits
Handle commerce_events
Handle subscription implications
Delete or disable auth user
Return deletion status
```

Important rules:

```text
Account deletion must match Privacy Policy.
Do not promise deletion behavior that is not implemented.
Some records may need retention for legal, accounting, security or compliance reasons.
```

This is a release-critical function.

---

# Function Security Rules

Every Edge Function should follow:

```text
Validate auth
Validate input
Validate ownership
Use RLS where possible
Use service role only when required
Do not expose service role key
Avoid logging sensitive data
Return safe errors
Prevent duplicate processing
```

---

# Function Logging

Log enough to debug.

Do not log unnecessary sensitive data.

Useful logs:

```text
function_name
request_id
user_id
event_type
success/failure
error_code
timestamp
```

Avoid logging:

```text
full health data
full uploaded document text
full medical notes
raw tokens
service keys
payment details
private user files
```

---

# Function Testing

Each function should be tested for:

```text
Valid request
Missing auth
Invalid input
Wrong user
Missing record
Duplicate request
Expired state
Unauthorized admin access
Database failure
Partial failure
Successful response
Safe error response
```

Important launch blocker:

```text
No user should be able to affect another user’s private data.
```

---

# Function Deployment

Recommended deployment approach:

```text
Write function
Test locally if possible
Deploy to development
Test with Supabase
Test with FlutterFlow
Deploy to staging
Run QA
Deploy to production only after validation
```

Do not deploy untested function changes directly to production.

---

# Relationship With Supabase RLS

Edge Functions do not replace RLS.

RLS should still protect user data.

Edge Functions add controlled workflows for complex operations.

Correct model:

```text
RLS protects direct data access.
Edge Functions protect complex workflows.
```

---

# Relationship With FlutterFlow

FlutterFlow should call Edge Functions for:

```text
activate_plan
process_daily_action
process_push_response
update_home_state
delete_account
```

FlutterFlow may perform simple direct Supabase operations when safe.

Examples:

```text
edit user profile
update settings
add stack item
mark simple user-owned preference
```

But critical system transitions should use Edge Functions.

---

# Relationship With Admin

Admin should use Edge Functions when publishing or changing important records.

Examples:

```text
admin_publish_plan
admin_archive_plan
admin_publish_content
admin_update_commerce_benefit
```

Admin changes should be traceable.

Use:

```text
admin_audit_log
```

where practical.

---

# Relationship With AAI

AAI logic should be backend-controlled.

AAI may be triggered by:

```text
plan activation
daily generation
daily action response
push response
wearable sync
upload processing
commerce event
manual refresh
```

AAI should use structured context from Supabase.

It should not depend only on frontend state.

---

# MVP Function Set

Minimum useful MVP function set:

```text
activate_plan
process_daily_action
update_home_state
delete_account
```

Strong MVP function set:

```text
activate_plan
generate_daily_plan
process_daily_action
process_push_response
update_home_state
evaluate_aai_context
delete_account
```

Commerce-enabled MVP adds:

```text
issue_commerce_benefit
track_commerce_event
```

Uploads-enabled MVP adds:

```text
process_user_upload
```

Wearables-enabled MVP adds:

```text
sync_wearable_snapshot
```

---

# What Edge Functions Should Not Do

Edge Functions should not:

- Replace a clean data model
- Store everything as unstructured blobs
- Ignore RLS
- Expose service role keys
- Trust frontend user_id blindly
- Log sensitive raw health data unnecessarily
- Create duplicate active plans
- Overwrite completed Daily actions carelessly
- Make commerce mandatory
- Require wearables
- Require uploads
- Make medical claims
- Hide errors from the app
- Break active user snapshots when templates change

---

# Success Criteria

The Edge Functions layer is successful when:

- Plan activation is reliable
- Daily action processing is consistent
- Push responses update the system correctly
- Home state remains coherent
- User data ownership is protected
- Admin publishing is controlled
- Account deletion works
- Commerce Bridge can run without fragile frontend logic
- Upload processing is controlled
- Wearable snapshots can update context
- FlutterFlow stays clean and simple
- Supabase remains the source of truth

---

# Current Status

Edge Functions are currently in planning.

Next steps:

- Define first MVP function set
- Implement `activate_plan`
- Implement `update_home_state`
- Implement `process_daily_action`
- Implement `delete_account`
- Test functions in development
- Connect FlutterFlow actions
- Validate RLS
- Expand to Push, AAI, Uploads, Wearables and Commerce Bridge

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
- PRODUCTS/WELLBINE/SUPABASE_IMPLEMENTATION.md
- PRODUCTS/WELLBINE/QA_PLAN.md
- PRODUCTS/WELLBINE/PRIVACY_POLICY_DRAFT.md
- PRODUCTS/WELLBINE/TERMS_DRAFT.md
- PRODUCTS/WELLBINE/APP_RELEASE_CHECKLIST.md
- PRODUCTS/WELLBINE/FLUTTERFLOW_BUILD_GUIDE.md
