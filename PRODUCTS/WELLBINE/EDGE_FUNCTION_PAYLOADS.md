# Wellbine Edge Function Payloads

**Version:** 0.1.0

**Status:** Draft

**Last Updated:** July 2026

---

# Purpose

This document defines the standard request and response payloads for Wellbine Edge Functions.

The goal is to make FlutterFlow, Supabase and backend workflows communicate through predictable contracts.

This document covers payloads for:

- create_user_baseline
- activate_plan
- generate_daily_plan
- update_home_state
- process_daily_action
- process_push_response
- evaluate_aai_context
- sync_wearable_snapshot
- process_user_upload
- issue_commerce_benefit
- track_commerce_event
- admin_publish_plan
- delete_account

Edge Functions should handle sensitive, adaptive or multi-table workflows that should not live entirely inside FlutterFlow.

---

# Official Definition

**Wellbine Edge Function Payloads are the standard request and response contracts used by the Wellbine app, Admin layer and backend services to execute secure workflows consistently.**

---

# Core Principle

The core payload rule is:

```text
Every Edge Function should receive clear intent and return a predictable result.
```

FlutterFlow should not need to guess what happened.

Every function should return:

```text
success
message
data
error
```

---

# Standard Success Response

All Edge Functions should follow this structure:

```json
{
  "success": true,
  "message": "Operation completed successfully.",
  "data": {},
  "error": null
}
```

---

# Standard Error Response

All Edge Functions should return errors like this:

```json
{
  "success": false,
  "message": "Operation could not be completed.",
  "data": null,
  "error": {
    "code": "ERROR_CODE",
    "details": "Readable technical detail for debugging."
  }
}
```

---

# Common Error Codes

Recommended common error codes:

```text
UNAUTHORIZED
FORBIDDEN
VALIDATION_ERROR
NOT_FOUND
CONFLICT
FEATURE_DISABLED
RATE_LIMITED
DATABASE_ERROR
EXTERNAL_PROVIDER_ERROR
INTERNAL_ERROR
```

---

# Authentication Rule

Most Edge Functions should require an authenticated Supabase user.

The function should derive the user from the auth token.

FlutterFlow should not send `user_id` unless there is a strong reason.

Preferred pattern:

```text
User identity comes from auth token.
Request payload contains action-specific data.
```

---

# Admin Rule

Admin functions must validate admin role.

Admin validation may use:

```text
user_roles
is_admin()
custom claims
service role protected backend
```

Admin functions should not trust frontend UI visibility alone.

---

# Idempotency Rule

Critical functions should avoid duplicate damage.

Important for:

```text
activate_plan
process_daily_action
process_push_response
issue_commerce_benefit
delete_account
```

Recommended payload field:

```json
{
  "idempotency_key": "unique-client-generated-key"
}
```

For MVP, idempotency may be enforced by checking existing state before writing.

---

# 1. create_user_baseline

Purpose:

```text
Create or update the minimum user profile and settings after signup.
```

Used by:

```text
FlutterFlow Auth
Onboarding
```

Request:

```json
{
  "profile": {
    "name": "Victor",
    "biological_sex": "male",
    "age": 43,
    "height_cm": 170,
    "weight_kg": 85,
    "country": "BR",
    "language": "en",
    "timezone": "America/Sao_Paulo",
    "relevant_comorbidities_json": []
  },
  "settings": {
    "preferred_units": "metric",
    "preferred_language": "en",
    "preferred_timezone": "America/Sao_Paulo",
    "push_enabled": false,
    "mental_detox_enabled": true
  }
}
```

Success response:

```json
{
  "success": true,
  "message": "User baseline created.",
  "data": {
    "profile_created": true,
    "settings_created": true,
    "onboarding_completed": false
  },
  "error": null
}
```

Main tables:

```text
user_profiles
user_settings
```

Validation:

```text
Authenticated user required.
Age must be reasonable.
Biological sex can be female, male or prefer_not_to_say.
Optional fields should not block baseline creation.
```

---

# 2. activate_plan

Purpose:

```text
Activate a published Plan Template version and create the user's first operating state.
```

Used by:

```text
Plan Activation screen
Onboarding final step
```

Request:

```json
{
  "plan_template_id": "uuid",
  "plan_template_version_id": "uuid",
  "activation_source": "onboarding",
  "idempotency_key": "activate-plan-user-date-001"
}
```

Alternative request using slug:

```json
{
  "plan_slug": "7-day-sync-plan",
  "activation_source": "onboarding",
  "idempotency_key": "activate-plan-user-date-001"
}
```

Success response:

```json
{
  "success": true,
  "message": "Plan activated successfully.",
  "data": {
    "active_plan_id": "uuid",
    "daily_plan_id": "uuid",
    "home_state_id": "uuid",
    "created_pillar_states": 7,
    "created_daily_actions": 6,
    "next_screen": "home"
  },
  "error": null
}
```

Main tables:

```text
plan_templates
plan_template_versions
user_active_plans
pillar_definitions
user_pillar_states
daily_plans
daily_actions
user_home_state
user_profiles
```

Validation:

```text
User must be authenticated.
Plan must exist.
Plan must be published.
Plan version must be published.
Plan version must belong to Plan Template.
Avoid duplicate active plan creation.
```

Important behavior:

```text
Set user_profiles.onboarding_completed = true.
Create active plan snapshot.
Create pillar states.
Create first daily plan.
Create first daily actions.
Create Home state.
```

---

# 3. generate_daily_plan

Purpose:

```text
Generate or regenerate a Daily plan for the authenticated user.
```

Used by:

```text
Daily screen
Scheduled backend jobs
Plan activation
Recovery flow
```

Request:

```json
{
  "plan_date": "2026-07-23",
  "generation_reason": "missing_daily_plan",
  "force_regenerate": false
}
```

Success response:

```json
{
  "success": true,
  "message": "Daily plan generated.",
  "data": {
    "daily_plan_id": "uuid",
    "plan_date": "2026-07-23",
    "created_daily_actions": 6,
    "updated_existing": false
  },
  "error": null
}
```

Main tables:

```text
user_active_plans
daily_plans
daily_actions
user_pillar_states
user_home_state
```

Validation:

```text
User must be authenticated.
User must have active plan.
Plan date must be valid.
Do not overwrite completed actions unless force_regenerate is explicitly allowed.
```

---

# 4. update_home_state

Purpose:

```text
Recalculate and update the user's Home operating state.
```

Used by:

```text
Home refresh
Daily action updates
Pillar updates
Push responses
Wearable sync
Upload processing
Commerce events
```

Request:

```json
{
  "reason": "daily_action_updated",
  "source_entity_type": "daily_action",
  "source_entity_id": "uuid"
}
```

Success response:

```json
{
  "success": true,
  "message": "Home state updated.",
  "data": {
    "home_state_id": "uuid",
    "current_insight": "Your morning rhythm is active.",
    "next_best_action": "Confirm hydration check.",
    "home_status": "active",
    "updated_at": "2026-07-23T12:00:00Z"
  },
  "error": null
}
```

Main tables:

```text
user_home_state
user_active_plans
user_pillar_states
daily_plans
daily_actions
feature_flags
recommendations
user_aai_context
```

Validation:

```text
User must be authenticated.
Home state should be created if missing.
Do not return fake precision.
```

Important behavior:

```text
Home should never become blank.
Fallback state should exist.
```

---

# 5. process_daily_action

Purpose:

```text
Process Confirm, Adjust, Later or Skip for a Daily action.
```

Used by:

```text
Daily
Daily Action Detail
Pillar Detail
Push response flow
```

Request — Confirm:

```json
{
  "daily_action_id": "uuid",
  "response": "confirm",
  "adjustment_payload": {},
  "delay_minutes": null,
  "idempotency_key": "daily-action-confirm-001"
}
```

Request — Adjust:

```json
{
  "daily_action_id": "uuid",
  "response": "adjust",
  "adjustment_payload": {
    "adjustment_type": "lower_intensity",
    "value": "light_movement"
  },
  "delay_minutes": null,
  "idempotency_key": "daily-action-adjust-001"
}
```

Request — Later:

```json
{
  "daily_action_id": "uuid",
  "response": "later",
  "adjustment_payload": {},
  "delay_minutes": 60,
  "idempotency_key": "daily-action-later-001"
}
```

Request — Skip:

```json
{
  "daily_action_id": "uuid",
  "response": "skip",
  "adjustment_payload": {
    "reason": "not_possible_now"
  },
  "delay_minutes": null,
  "idempotency_key": "daily-action-skip-001"
}
```

Success response:

```json
{
  "success": true,
  "message": "Daily action processed.",
  "data": {
    "daily_action_id": "uuid",
    "new_status": "completed",
    "daily_plan_id": "uuid",
    "pillar_updated": true,
    "home_updated": true,
    "next_best_action": "Prepare your next alignment step."
  },
  "error": null
}
```

Main tables:

```text
daily_actions
daily_plans
user_pillar_states
user_home_state
user_active_plans
```

Validation:

```text
User must own Daily action.
Response must be confirm, adjust, later or skip.
Delay must be reasonable.
Completed actions should not be duplicated.
```

Important behavior:

```text
Update Daily action.
Update related Pillar state.
Update Home state.
Use non-punitive recovery language.
```

---

# 6. process_push_response

Purpose:

```text
Process user response to Push notification.
```

Used by:

```text
Push notification actions
Push deep links
```

Request:

```json
{
  "push_event_id": "uuid",
  "response": "confirm",
  "response_payload": {},
  "idempotency_key": "push-response-001"
}
```

Possible responses:

```text
confirm
adjust
later
open
dismiss
```

Success response:

```json
{
  "success": true,
  "message": "Push response processed.",
  "data": {
    "push_event_id": "uuid",
    "response": "confirm",
    "daily_action_updated": true,
    "home_updated": true,
    "deep_link": "wellbine://daily/action/uuid"
  },
  "error": null
}
```

Main tables:

```text
push_events
daily_actions
daily_plans
user_home_state
user_pillar_states
user_settings
```

Validation:

```text
User must own Push event.
Push must be enabled.
Push event must not be already finalized unless idempotent.
```

Important behavior:

```text
If Push is tied to Daily action, update Daily action.
If Push is Later, schedule or record delayed follow-up.
If Push is Adjust, return deep link to adjustment screen.
```

---

# 7. evaluate_aai_context

Purpose:

```text
Evaluate user context and produce structured adaptive context for future decisions.
```

Used by:

```text
Home
Daily
Push
Plan adaptation
Recommendations
```

Request:

```json
{
  "evaluation_reason": "home_refresh",
  "context_scope": "today",
  "include_wearable_data": true,
  "include_upload_context": false
}
```

Success response:

```json
{
  "success": true,
  "message": "AAI context evaluated.",
  "data": {
    "user_aai_context_id": "uuid",
    "context_scope": "today",
    "readiness_state": "moderate",
    "recovery_state": "still_recoverable",
    "recommended_focus": ["hydration", "movement", "sleep"],
    "confidence_level": "limited"
  },
  "error": null
}
```

Main tables:

```text
user_aai_context
user_profiles
user_settings
user_active_plans
user_pillar_states
daily_plans
daily_actions
wearable_metric_snapshots
user_uploads
```

Validation:

```text
User must be authenticated.
Do not claim medical diagnosis.
Do not imply unsupported precision.
Use available context only.
```

Important behavior:

```text
Return useful structured context.
Avoid black-box fake certainty.
```

---

# 8. sync_wearable_snapshot

Purpose:

```text
Store or update wearable metric snapshot from a connected provider.
```

Used by:

```text
Wearable sync backend
Manual sync
Provider integration
```

Request:

```json
{
  "provider": "apple_health",
  "snapshot_date": "2026-07-23",
  "metrics": {
    "resting_heart_rate_bpm": 62,
    "hrv_ms": 48,
    "sleep_duration_minutes": 420,
    "steps": 8500,
    "active_minutes": 45,
    "spo2_pct": 98,
    "respiratory_rate": 14,
    "wrist_temperature_delta": 0.1
  },
  "source_payload_json": {}
}
```

Success response:

```json
{
  "success": true,
  "message": "Wearable snapshot synced.",
  "data": {
    "wearable_metric_snapshot_id": "uuid",
    "provider": "apple_health",
    "snapshot_date": "2026-07-23",
    "home_update_recommended": true
  },
  "error": null
}
```

Main tables:

```text
wearable_connections
wearable_metric_snapshots
user_home_state
user_aai_context
feature_flags
```

Validation:

```text
Wearables feature must be enabled.
Provider must be enabled.
User must have permission.
Metrics must be within reasonable format.
```

Important behavior:

```text
Do not show unsupported provider as active.
Wearables remain optional.
```

---

# 9. process_user_upload

Purpose:

```text
Process an optional user-uploaded file and store usable context.
```

Used by:

```text
Upload Manager
Onboarding optional upload
```

Request:

```json
{
  "upload_id": "uuid",
  "processing_reason": "user_uploaded_file",
  "extract_summary": true
}
```

Success response:

```json
{
  "success": true,
  "message": "Upload processed.",
  "data": {
    "upload_id": "uuid",
    "processing_status": "processed",
    "summary_available": true,
    "home_update_recommended": true
  },
  "error": null
}
```

Main tables:

```text
user_uploads
user_aai_context
user_home_state
feature_flags
```

Validation:

```text
Uploads feature must be enabled.
User must own upload.
File must exist in private storage.
File type must be allowed.
Processing must not imply diagnosis.
```

Important behavior:

```text
Uploads enrich context.
Uploads do not become diagnosis.
Uploads must remain optional.
```

---

# 10. issue_commerce_benefit

Purpose:

```text
Issue or retrieve an eligible Commerce Bridge benefit for the user.
```

Used by:

```text
Subscriber Benefits
Daily Stack
Home contextual card
Commerce Benefit Detail
```

Request:

```json
{
  "commerce_benefit_id": "uuid",
  "placement": "personal_center",
  "idempotency_key": "commerce-benefit-001"
}
```

Success response:

```json
{
  "success": true,
  "message": "Commerce benefit available.",
  "data": {
    "user_commerce_benefit_id": "uuid",
    "benefit_title": "Subscriber Benefit",
    "benefit_code": "WELLBINE10",
    "external_url": "https://example-store.com",
    "button_label": "Use Benefit",
    "expires_at": "2026-08-23T00:00:00Z"
  },
  "error": null
}
```

Main tables:

```text
commerce_benefits
user_commerce_benefits
commerce_events
feature_flags
user_settings
```

Validation:

```text
Commerce Bridge must be enabled.
Benefit must be active.
User must be eligible.
External URL must exist if benefit is visible.
Do not hardcode discount amount.
```

Important behavior:

```text
Return benefit code if applicable.
Return external URL.
Do not process checkout inside Wellbine unless future policy allows it.
```

---

# 11. track_commerce_event

Purpose:

```text
Track Commerce Bridge events.
```

Used by:

```text
Use Benefit button
Commerce external link
Coupon copy
```

Request:

```json
{
  "commerce_benefit_id": "uuid",
  "user_commerce_benefit_id": "uuid",
  "event_type": "coupon_copied",
  "placement": "personal_center",
  "metadata_json": {
    "button_label": "Use Benefit"
  }
}
```

Possible event types:

```text
benefit_viewed
coupon_copied
external_store_opened
benefit_used
benefit_failed
```

Success response:

```json
{
  "success": true,
  "message": "Commerce event tracked.",
  "data": {
    "commerce_event_id": "uuid",
    "event_type": "coupon_copied"
  },
  "error": null
}
```

Main tables:

```text
commerce_events
commerce_benefits
user_commerce_benefits
feature_flags
```

Validation:

```text
User must be authenticated.
Commerce event must be valid.
Do not track unnecessary sensitive health information.
```

---

# 12. admin_publish_plan

Purpose:

```text
Publish a Plan Template version safely.
```

Used by:

```text
Admin
Publishing workflow
```

Request:

```json
{
  "plan_template_id": "uuid",
  "plan_template_version_id": "uuid",
  "publish_notes": "Initial MVP plan version.",
  "make_current_version": true
}
```

Success response:

```json
{
  "success": true,
  "message": "Plan version published.",
  "data": {
    "plan_template_id": "uuid",
    "plan_template_version_id": "uuid",
    "status": "published",
    "current_version_updated": true
  },
  "error": null
}
```

Main tables:

```text
plan_templates
plan_template_versions
admin_audit_log
user_roles
```

Validation:

```text
Admin user required.
Plan Template must exist.
Plan Version must exist.
Plan Version must belong to Plan Template.
Configuration must pass validation.
Audit log must be written.
```

Important behavior:

```text
Publishing new version should not mutate existing user active plan snapshots.
```

---

# 13. delete_account

Purpose:

```text
Delete, disable or anonymize a user's account according to the defined privacy policy.
```

Used by:

```text
Account screen
Delete Account flow
```

Request:

```json
{
  "confirmation": true,
  "reason": "user_requested",
  "idempotency_key": "delete-account-001"
}
```

Success response:

```json
{
  "success": true,
  "message": "Account deletion request completed.",
  "data": {
    "account_deleted": true,
    "logout_required": true
  },
  "error": null
}
```

Main tables:

```text
user_profiles
user_settings
user_active_plans
user_pillar_states
daily_plans
daily_actions
user_home_state
push_events
stack_items
user_uploads
commerce_events
user_commerce_benefits
user_aai_context
```

Validation:

```text
User must be authenticated.
Confirmation must be true.
Deletion behavior must match Privacy Policy.
```

Important behavior:

```text
This is release-critical.
Do not leave user data in inconsistent state.
Do not silently fail.
```

---

# FlutterFlow Call Pattern

Recommended FlutterFlow behavior for every Edge Function:

```text
Set loading state
Call function
Check success
If success:
    use data
    refresh Supabase queries
    navigate if needed
If error:
    show readable message
Clear loading state
```

---

# Payload Versioning

Future payloads may include:

```json
{
  "payload_version": "0.1.0"
}
```

This can help prevent frontend/backend mismatch.

For MVP, payload versioning is optional.

---

# Security Notes

Do not send:

```text
service_role_key
admin secrets
raw provider secrets
private file paths unless required
unnecessary health data
unnecessary payment data
```

Do not trust:

```text
frontend role flags
frontend-only eligibility
frontend-only feature visibility
```

Backend must validate sensitive operations.

---

# Success Criteria

Edge Function Payloads are successful when:

- FlutterFlow knows what to send
- Edge Functions return predictable responses
- Errors are readable
- Core workflows are not fragile
- Multi-table updates are controlled
- Sensitive workflows are not frontend-only
- Admin publishing is protected
- Account deletion is reliable
- Commerce Bridge is controlled
- Push responses update the correct state
- Home can refresh after meaningful events

---

# Current Status

Edge Function Payloads are currently a draft.

Next steps:

- Create Edge Functions in Supabase
- Implement activate_plan first
- Implement process_daily_action
- Implement update_home_state
- Implement delete_account
- Connect FlutterFlow actions
- Test request and response contracts
- Add error logging
- Add idempotency protection for critical workflows

---

# Related Documents

- PRODUCTS/WELLBINE/EDGE_FUNCTIONS.md
- PRODUCTS/WELLBINE/FLUTTERFLOW_ACTIONS.md
- PRODUCTS/WELLBINE/SUPABASE_SQL_MVP.md
- PRODUCTS/WELLBINE/SUPABASE_IMPLEMENTATION.md
- PRODUCTS/WELLBINE/MVP_BUILD_SEQUENCE.md
- PRODUCTS/WELLBINE/FEATURE_FLAGS.md
- PRODUCTS/WELLBINE/SCREEN_MAP.md
- PRODUCTS/WELLBINE/QA_PLAN.md
