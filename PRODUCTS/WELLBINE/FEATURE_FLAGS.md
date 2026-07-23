# Wellbine Feature Flags

**Version:** 0.1.0

**Status:** Draft

**Last Updated:** July 2026

---

# Purpose

This document defines the Feature Flags strategy for Wellbine.

The goal is to control which product features are visible, active, hidden, limited, experimental or disabled without requiring app redeployment for every operational change.

Feature Flags should help Wellbine manage:

- MVP rollout
- App review safety
- Beta testing
- User segmentation
- Plan-specific experiences
- Admin control
- Commerce Bridge visibility
- Wearables visibility
- Uploads visibility
- Push behavior
- Ask Wellbine visibility
- Subscription features
- Experimental features
- Rollback

Feature Flags are part of the operational control layer.

---

# Official Definition

**Wellbine Feature Flags are configuration controls that determine whether specific features, screens, flows, recommendations, benefits or system behaviors are enabled, disabled, hidden or limited for users, plans, environments or release stages.**

---

# Core Principle

The core Feature Flags rule is:

```text
Unfinished, risky or context-specific features should be controlled by configuration, not hardcoded into the app.
```

Feature Flags allow Wellbine to move faster without exposing incomplete or unsafe experiences.

They also allow the team to disable features quickly if something breaks.

---

# Why Feature Flags Matter

Feature Flags are important because Wellbine includes several sensitive or operationally complex areas:

- Health-related guidance
- Wearables
- Uploads
- AI-assisted guidance
- Push notifications
- Commerce Bridge
- Subscriptions
- Daily Stack
- Admin-managed content
- App release review
- Privacy-sensitive flows

Not every feature should be visible to every user at every stage.

Feature Flags allow controlled rollout.

---

# What Feature Flags Should Control

Feature Flags may control:

- Screen visibility
- Feature availability
- Button visibility
- User flow access
- Recommendation visibility
- Commerce benefit visibility
- Provider visibility
- Push categories
- Plan-specific modules
- Experimental features
- Beta-only functionality
- App review mode
- Country-specific behavior
- Subscription-gated behavior

---

# What Feature Flags Should Not Do

Feature Flags should not replace:

- Proper data model
- Supabase RLS
- Privacy rules
- Legal review
- QA
- App Store compliance
- Google Play compliance
- Secure backend logic
- User consent
- Medical claim review

Feature Flags control visibility and behavior.

They do not make unsafe features safe by themselves.

---

# Flag Types

Recommended flag types:

```text
global_flags
environment_flags
plan_flags
user_flags
role_flags
release_flags
commerce_flags
provider_flags
experimental_flags
```

---

## global_flags

Apply to the whole product.

Examples:

```text
wearables_enabled
uploads_enabled
commerce_bridge_enabled
ask_wellbine_enabled
subscriptions_enabled
push_enabled
daily_stack_enabled
recommendations_enabled
```

---

## environment_flags

Apply by environment.

Examples:

```text
development
staging
production
app_review
beta
```

Environment flags help prevent unfinished features from appearing in production.

---

## plan_flags

Apply by Plan Template or active plan.

Examples:

```text
plan_has_daily_stack
plan_has_commerce_benefits
plan_has_uploads
plan_has_wearable_support
plan_has_push_sequence
plan_has_recommendations
```

Plan flags allow different plans to activate different product modules.

---

## user_flags

Apply to specific users.

Examples:

```text
beta_user
internal_tester
support_test_user
commerce_enabled_for_user
ask_wellbine_enabled_for_user
wearables_enabled_for_user
```

Useful for testing before wide rollout.

---

## role_flags

Apply by role.

Examples:

```text
admin_access_enabled
support_view_enabled
editor_tools_enabled
release_review_enabled
```

Role flags must not replace real access control.

They only help control UI visibility.

---

## release_flags

Apply to release stage.

Examples:

```text
mvp_mode
beta_mode
controlled_launch_mode
public_launch_mode
app_review_mode
```

These help simplify the app during review and launch.

---

## commerce_flags

Apply to Commerce Bridge.

Examples:

```text
commerce_bridge_enabled
subscriber_benefits_enabled
commerce_home_card_enabled
commerce_daily_stack_entry_enabled
commerce_push_enabled
commerce_external_links_enabled
coupon_auto_copy_enabled
coupon_auto_apply_link_enabled
```

Commerce flags are important because commerce may affect app review and user trust.

---

## provider_flags

Apply to external providers.

Examples:

```text
apple_health_enabled
google_health_connect_enabled
garmin_enabled
oura_enabled
whoop_enabled
fitbit_enabled
manual_wearable_enabled
```

Provider flags prevent the app from showing integrations that are not ready.

---

## experimental_flags

Apply to test features.

Examples:

```text
experimental_home_summary
experimental_aai_recommendations
experimental_sleep_recovery
experimental_daily_regeneration
experimental_commerce_recommendations
```

Experimental flags should be limited and carefully monitored.

---

# Recommended Initial Flags

Initial MVP flags:

```text
onboarding_enabled
home_enabled
daily_enabled
pillars_enabled
daily_stack_enabled
push_enabled
wearables_enabled
uploads_enabled
commerce_bridge_enabled
ask_wellbine_enabled
subscriptions_enabled
recommendations_enabled
app_review_mode
beta_mode
```

Recommended default for MVP:

```text
onboarding_enabled = true
home_enabled = true
daily_enabled = true
pillars_enabled = true
daily_stack_enabled = true
push_enabled = false or limited
wearables_enabled = false or placeholder
uploads_enabled = false or placeholder
commerce_bridge_enabled = false
ask_wellbine_enabled = false or limited
subscriptions_enabled = false until payment model is ready
recommendations_enabled = limited
app_review_mode = false except review builds
beta_mode = true for beta users
```

---

# Feature Flag Hierarchy

Feature visibility should follow a hierarchy.

Recommended order:

```text
1. Environment flag
2. Global flag
3. Release mode
4. Plan flag
5. User flag
6. Role flag
7. Eligibility rule
```

Example:

```text
Commerce Bridge appears only if:

production configuration allows it
+
global commerce_bridge_enabled is true
+
user is eligible
+
benefit is active
+
placement is enabled
```

---

# Feature Flag Decision Logic

Recommended logic:

```text
If environment disables feature:
    hide feature

Else if global flag disables feature:
    hide feature

Else if release mode disables feature:
    hide feature

Else if plan does not include feature:
    hide feature

Else if user is not eligible:
    hide feature

Else:
    show feature
```

Important rule:

```text
A feature should appear only when all required conditions are satisfied.
```

---

# Supabase Storage Direction

Feature Flags may be stored in Supabase.

Possible table:

```text
feature_flags
```

Possible fields:

```text
id uuid primary key
flag_key text
description text
status text
scope text
scope_id text
enabled boolean
rules_json jsonb
metadata_json jsonb
created_by uuid
updated_by uuid
created_at timestamptz
updated_at timestamptz
```

Possible statuses:

```text
active
inactive
archived
testing
```

Possible scopes:

```text
global
environment
plan_template
plan_version
user
role
country
release
```

---

# Alternative Remote Config Table

A broader configuration table may also be used.

Possible table:

```text
remote_config
```

Possible fields:

```text
id uuid primary key
config_key text
config_value_json jsonb
scope text
scope_id text
status text
created_by uuid
updated_by uuid
created_at timestamptz
updated_at timestamptz
```

This can support both feature flags and other app configuration.

Recommended MVP approach:

```text
Start simple with feature_flags or remote_config.
Avoid building an overly complex configuration system too early.
```

---

# Admin Control

Feature Flags should be manageable through Admin.

Admin should be able to:

- Enable feature
- Disable feature
- Set environment scope
- Set plan scope
- Set user scope
- Set release mode
- Add notes
- Preview impact
- Publish change
- Archive flag
- View change history

Important changes should be recorded in:

```text
admin_audit_log
```

---

# Feature Flag Safety

Some flags are release-sensitive.

Examples:

```text
commerce_bridge_enabled
uploads_enabled
wearables_enabled
subscriptions_enabled
ask_wellbine_enabled
push_enabled
```

Before enabling these in production, confirm:

- QA passed
- Privacy Policy covers behavior
- Terms cover behavior
- App Release Checklist passed
- Admin configuration is correct
- No unsafe claims are visible
- User fallback exists

---

# App Review Mode

Wellbine may need an `app_review_mode`.

Purpose:

```text
Ensure reviewers see a clean, testable, compliant experience.
```

App review mode may:

- Hide unfinished Commerce Bridge
- Hide unfinished Wearables
- Hide unfinished Uploads
- Hide experimental AI
- Show test-friendly plan
- Avoid requiring real wearable
- Avoid requiring real payment
- Avoid requiring real uploaded file
- Ensure account deletion is visible
- Ensure Privacy and Terms are visible

Important rule:

```text
App review mode must not deceive reviewers.
```

It should simplify the experience, not hide required compliance information.

---

# Beta Mode

Beta mode may enable features for selected users.

Possible beta features:

```text
Push
Daily Stack
Wearables placeholder
Uploads
Ask Wellbine
Commerce Bridge
Advanced recommendations
```

Beta mode should allow learning without exposing all users to instability.

---

# Commerce Bridge Flags

Commerce Bridge should be heavily flag-controlled.

Recommended flags:

```text
commerce_bridge_enabled
subscriber_benefits_enabled
commerce_home_card_enabled
commerce_personal_center_enabled
commerce_daily_stack_enabled
commerce_push_enabled
coupon_auto_copy_enabled
coupon_auto_apply_link_enabled
external_store_open_enabled
```

Rules:

```text
Commerce Bridge must be hideable.
Commerce should not become fixed primary navigation in MVP.
Commerce Push must be disabled unless clearly relevant and allowed.
```

---

# Wearables Flags

Wearables should be flag-controlled by provider.

Recommended flags:

```text
wearables_enabled
manual_wearable_enabled
apple_health_enabled
google_health_connect_enabled
garmin_enabled
oura_enabled
whoop_enabled
fitbit_enabled
wearable_sync_enabled
wearable_recovery_insights_enabled
```

Rules:

```text
Do not show providers as active before implementation.
Wearables must remain optional.
Manual fallback should exist.
```

---

# Upload Flags

Uploads should be flag-controlled.

Recommended flags:

```text
uploads_enabled
lab_uploads_enabled
nutrition_plan_uploads_enabled
wearable_export_uploads_enabled
supplement_list_uploads_enabled
upload_processing_enabled
upload_summary_enabled
upload_delete_enabled
```

Rules:

```text
Uploads must remain optional.
Uploads should not imply diagnosis.
Private storage must be ready before enabling uploads.
```

---

# Push Flags

Push should be flag-controlled.

Recommended flags:

```text
push_enabled
push_morning_enabled
push_midday_enabled
push_evening_enabled
push_night_enabled
push_commerce_enabled
push_daily_stack_enabled
push_later_followup_enabled
mental_detox_enabled
```

Rules:

```text
Push must be optional.
Push should not become spam.
Commerce Push should be disabled by default until tested.
```

---

# Ask Wellbine Flags

Ask Wellbine should be flag-controlled.

Recommended flags:

```text
ask_wellbine_enabled
ask_wellbine_home_enabled
ask_wellbine_daily_enabled
ask_wellbine_upload_summary_enabled
ask_wellbine_stack_enabled
ask_wellbine_commerce_enabled
```

Rules:

```text
Ask Wellbine should support guidance.
Ask Wellbine should not diagnose or treat.
Ask Wellbine should respect available user context and privacy.
```

---

# Subscription Flags

Subscription-related features should be controlled.

Recommended flags:

```text
subscriptions_enabled
trial_enabled
monthly_plan_enabled
quarterly_plan_enabled
annual_plan_enabled
subscriber_benefits_enabled
paywall_enabled
restore_purchase_enabled
```

Rules:

```text
Do not show subscription flows before payment model is ready.
Subscription copy must be clear before release.
```

---

# Recommendations Flags

Recommendations should be controlled.

Recommended flags:

```text
recommendations_enabled
home_recommendations_enabled
daily_recommendations_enabled
pillar_recommendations_enabled
commerce_recommendations_enabled
stack_recommendations_enabled
```

Rules:

```text
Recommendations should be contextual.
Recommendations should not become noise.
Commerce recommendations should be especially careful.
```

---

# MVP Flag Defaults

Suggested MVP defaults:

```text
onboarding_enabled: true
home_enabled: true
daily_enabled: true
pillars_enabled: true
daily_stack_enabled: true
push_enabled: false
wearables_enabled: false
uploads_enabled: false
commerce_bridge_enabled: false
ask_wellbine_enabled: false
subscriptions_enabled: false
recommendations_enabled: limited
app_review_mode: false
beta_mode: true
```

As features stabilize, flags can be enabled gradually.

---

# Controlled Launch Flag Defaults

Suggested controlled launch defaults:

```text
onboarding_enabled: true
home_enabled: true
daily_enabled: true
pillars_enabled: true
daily_stack_enabled: true
push_enabled: true
wearables_enabled: optional / limited
uploads_enabled: optional / limited
commerce_bridge_enabled: hidden or limited
ask_wellbine_enabled: limited
subscriptions_enabled: according to release model
recommendations_enabled: true
app_review_mode: false
beta_mode: false
```

---

# Emergency Disable

Feature Flags should allow fast disable.

Emergency disable may apply to:

```text
commerce_bridge_enabled
push_enabled
uploads_enabled
ask_wellbine_enabled
wearables_enabled
subscriptions_enabled
recommendations_enabled
```

Use cases:

```text
Broken external link
Unsafe content
App review issue
Privacy issue
Provider integration failure
Push malfunction
Commerce checkout problem
AI behavior issue
```

Important rule:

```text
The team should be able to disable risky features without waiting for app store approval.
```

---

# FlutterFlow Usage

FlutterFlow should read Feature Flags from Supabase or remote config.

FlutterFlow may use flags for:

- Conditional visibility
- Navigation access
- Button visibility
- Screen access
- Feature cards
- Optional steps
- Beta features
- App review mode
- Commerce visibility
- Wearable provider visibility

Do not hardcode feature visibility permanently in FlutterFlow.

---

# Edge Function Usage

Edge Functions should also check flags when needed.

Examples:

```text
issue_commerce_benefit checks commerce_bridge_enabled
process_user_upload checks uploads_enabled
sync_wearable_snapshot checks provider enabled
process_push_response checks push_enabled
```

Important rule:

```text
Frontend hiding is not enough for sensitive features.
Backend should enforce important flags.
```

---

# Admin Usage

Admin should manage Feature Flags.

Admin should show:

```text
Flag key
Description
Enabled state
Scope
Environment
Plan
User segment
Last updated
Updated by
Internal notes
```

Admin should prevent accidental production exposure.

---

# QA Usage

QA should test features in both states:

```text
Feature enabled
Feature disabled
```

Examples:

```text
Commerce enabled → benefit appears
Commerce disabled → benefit hidden

Wearables enabled → wearable manager appears
Wearables disabled → wearable manager hidden or unavailable

Uploads enabled → upload screen appears
Uploads disabled → upload screen hidden

Push enabled → permission flow appears
Push disabled → app still works
```

---

# App Release Usage

Before app submission, confirm flags:

```text
No unfinished feature visible
Commerce Bridge hidden or working
Wearables hidden or optional
Uploads hidden or optional
Push optional
Ask Wellbine safe or hidden
Subscriptions working or hidden
Account deletion visible
Privacy and Terms visible
```

Feature Flags are part of App Release readiness.

---

# Risk Areas

High-risk flags:

```text
commerce_bridge_enabled
subscriptions_enabled
uploads_enabled
ask_wellbine_enabled
wearables_enabled
push_commerce_enabled
upload_processing_enabled
```

These should require review before production activation.

---

# What To Avoid

Avoid:

- Too many flags with no documentation
- Flags that nobody owns
- Flags that stay forever after becoming obsolete
- Backend ignoring important flags
- App showing hidden features through deep links
- App review seeing unfinished features
- Feature flags used instead of permissions
- Feature flags used instead of RLS
- Feature flags used instead of legal review

---

# Success Criteria

Feature Flags are successful when:

- Unfinished features can remain hidden
- Risky features can be disabled quickly
- Beta features can be tested safely
- App review sees only ready flows
- Commerce Bridge can be hidden or enabled
- Wearables can be provider-controlled
- Uploads can be controlled
- Push can be controlled
- FlutterFlow does not hardcode every decision
- Admin can manage visibility
- Supabase remains source of truth

---

# Current Status

Feature Flags are currently a draft strategy.

Next steps:

- Decide between `feature_flags` and `remote_config`
- Create MVP flags
- Add Admin control
- Connect FlutterFlow conditional visibility
- Add backend checks for sensitive flags
- Test enabled and disabled states
- Use flags during app review preparation

---

# Related Documents

- PRODUCTS/WELLBINE/PRODUCT.md
- PRODUCTS/WELLBINE/ADMIN.md
- PRODUCTS/WELLBINE/ADMIN_BUILD_GUIDE.md
- PRODUCTS/WELLBINE/APP_RELEASE.md
- PRODUCTS/WELLBINE/APP_RELEASE_CHECKLIST.md
- PRODUCTS/WELLBINE/COMMERCE_BRIDGE.md
- PRODUCTS/WELLBINE/EDGE_FUNCTIONS.md
- PRODUCTS/WELLBINE/FLUTTERFLOW_BUILD_GUIDE.md
- PRODUCTS/WELLBINE/MVP_BUILD_SEQUENCE.md
- PRODUCTS/WELLBINE/QA_PLAN.md
- PRODUCTS/WELLBINE/SCREEN_MAP.md
- PRODUCTS/WELLBINE/SUPABASE_IMPLEMENTATION.md
- PRODUCTS/WELLBINE/SUPABASE_SCHEMA.md
- PRODUCTS/WELLBINE/WEARABLES.md
