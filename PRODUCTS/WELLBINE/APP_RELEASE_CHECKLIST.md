# Wellbine App Release Checklist

**Version:** 0.1.0

**Status:** Draft

**Last Updated:** July 2026

---

# Purpose

This document defines the practical release checklist for publishing Wellbine on iOS and Android.

This checklist translates the release strategy from `APP_RELEASE.md` into concrete verification items.

This document covers:

- Product readiness
- App Store readiness
- Google Play readiness
- Build readiness
- Account readiness
- Legal readiness
- Privacy readiness
- Health data readiness
- AI disclosure readiness
- Wearables readiness
- Push readiness
- Subscription readiness
- Commerce Bridge readiness
- QA readiness
- Review notes
- Test accounts
- Launch gates

This document is operational.

It should be used before each submission.

---

# Official Definition

**Wellbine App Release Checklist is the practical verification document used to confirm that Wellbine is ready for App Store review, Google Play review, internal testing, beta testing and controlled production launch.**

---

# Core Principle

The core release checklist rule is:

```text
Do not submit the app until the reviewer, the user and the system can understand the product clearly.
```

App review failure often comes from confusion.

Wellbine should be clear about:

- What the app does
- What the app does not do
- What data it collects
- Why permissions are requested
- Whether features are optional
- How AI is used
- How health guidance is limited
- How subscriptions work
- How external commerce works
- How users delete accounts
- How reviewers can test the app

---

# Release Scope Decision

Before submission, define the exact release scope.

```text
Release Name:
Release Version:
iOS Build Number:
Android Build Number:
Target Release Type:
Target Markets:
Target Languages:
```

Release type:

```text
Internal Test
TestFlight
Google Internal Testing
Closed Beta
Controlled Production
Public Production
```

---

# Feature Visibility Decision

Before submission, decide which features are visible.

```text
Onboarding: visible / hidden
Home: visible / hidden
Daily: visible / hidden
Push: visible / hidden
Pillars: visible / hidden
Daily Stack: visible / hidden
Wearables: visible / hidden
Uploads: visible / hidden
Commerce Bridge: visible / hidden
Subscriptions: visible / hidden
AI Chat / Ask Wellbine: visible / hidden
```

Important rule:

```text
Do not expose unfinished features to reviewers.
```

If a feature is not ready, hide it through Admin or configuration.

---

# Product Readiness Checklist

Confirm:

```text
Signup works
Login works
Logout works
Onboarding works
Plan selection works
Plan activation works
Home loads after activation
Home loads for returning users
Daily loads
Daily actions work
Push logic works or degrades gracefully
Pillars load
Pillar states update
Daily Stack works if visible
Wearables are optional if visible
Uploads are optional if visible
Commerce Bridge is optional if visible
Settings open
Account deletion path exists
Privacy Policy is accessible
Terms are accessible
No blank critical screens
No broken primary links
No draft admin content visible
```

---

# Product Boundary Checklist

Confirm user-facing copy does not position Wellbine as:

```text
Medical diagnosis
Medical treatment
Emergency service
Disease detection
Clinical monitoring device
Replacement for doctor
Replacement for medication guidance
Guaranteed health outcome
```

Preferred positioning:

```text
Adaptive wellness guidance
Daily routine alignment
Health behavior organization
Recovery-aware wellness support
Personalized habit execution
```

---

# Health Claim Checklist

Review all user-facing copy.

Avoid:

```text
diagnose
treat
cure
prevent disease
guarantee
medical-grade
replace doctor
replace medication
detect disease
clinical monitoring
```

Preferred language:

```text
supports
helps organize
guides
suggests
encourages
may help
wellness routine
daily alignment
recovery-aware guidance
```

Confirm:

```text
No unsupported medical claims
No disease treatment claims
No guaranteed results
No misleading supplement claims
No unsafe Daily Stack wording
No AI medical authority wording
```

---

# AI Readiness Checklist

Confirm AI usage is explained clearly.

```text
AI explanation exists
AI is described as wellness support
AI is not described as diagnosis
AI is not described as medical treatment
AI output boundary is clear
User remains responsible for decisions
AI guidance can be reviewed by user
AI does not create emergency-use expectation
```

Recommended boundary:

```text
Wellbine uses AI-assisted guidance to help organize wellness context and suggest practical next actions. It does not provide medical diagnosis, treatment or emergency care.
```

---

# AAI Readiness Checklist

Confirm AAI is framed correctly.

```text
AAI is described as internal intelligence architecture
AAI is not described as medical diagnosis
AAI supports personalization
AAI supports context alignment
AAI supports daily guidance
AAI does not replace professional care
```

Approved AAI definition:

```text
Adaptive Alignment Intelligence (AAI) is a Deep Intelligence Architecture designed to understand context, continuously learn, anticipate needs, align systems and optimize outcomes.
```

---

# Onboarding Checklist

Confirm:

```text
Welcome screen works
Name input works
Biological sex step works
Age input works
Height input works
Weight input works
Comorbidities are optional
Wearable connection is optional
Push permission is optional
Mental Detox is explained before Push permission
Goals can be selected
Plan model can be selected
Pillar preferences can be adjusted
Upload step is optional
Onboarding can be completed without wearable
Onboarding can be completed without upload
Onboarding can be completed without Push
Onboarding completion saves to Supabase
User enters Home after onboarding
```

---

# Home Checklist

Confirm:

```text
Home loads after onboarding
Home loads for returning users
Home does not appear blank
Main Orb displays meaningful state
Pillar Orbs display meaningful state
Current Insight appears
Next Best Action appears
Adaptive Summary opens
Pillar quick panel opens
Ask Wellbine entry point works if visible
Settings / Personal Center is accessible
Commerce card appears only if configured
Home is not a Store
```

---

# Daily Checklist

Confirm:

```text
Daily plan loads
Daily actions load
Action status works
Confirm works
Adjust works
Later works
Completed action updates
Delayed action updates
Expired action uses recovery-aware language
Daily syncs with Home
Daily syncs with Pillars
Daily syncs with Push
Daily works without wearable
Daily works without Push
```

---

# Push Checklist

Confirm:

```text
Push permission prompt appears at correct moment
Push explanation is clear
User can deny Push
App works if Push is denied
Mental Detox settings affect Push behavior
Confirm action works
Adjust deep-link works
Later action works
Push events are recorded
Push does not become promotional spam
Commerce Push appears only if allowed and relevant
```

Push should be optional.

Push should not block app usage.

---

# Pillars Checklist

Confirm all active pillars work:

```text
Mind
Sun
Hydration
Sleep
Nutrition
Movement
Daily Stack
```

For each pillar, confirm:

```text
Pillar loads
Pillar state displays
Pillar Orb matches state
Pillar quick panel opens
Pillar actions can update state
Pillar syncs with Daily
Pillar syncs with Home
Pillar works without wearable
Copy is safe
No unsupported medical claims
```

---

# Daily Stack Checklist

Confirm:

```text
User can add item
User can edit item
User can remove item
User can mark item taken
User can skip item
Timing works
Frequency works
Refill context works if visible
Daily Stack can appear in Daily
Daily Stack can appear in Home
Commerce Bridge link appears only if configured
Medication language is careful
No prescription behavior
```

Important boundary:

```text
Daily Stack organizes routines. It does not prescribe medication.
```

---

# Wearables Checklist

Confirm:

```text
Wearable connection is optional
User can skip wearable connection
Manual fallback works
Only implemented providers are shown
Permission explanation is clear
Data usage explanation is clear
Connection status displays correctly
Disconnection works
Revoked permission is handled
Sync failure is handled
Stale data is handled
Home works without wearable
Daily works without wearable
AAI context works without wearable
```

Do not claim unsupported provider integrations.

---

# Uploads Checklist

Confirm:

```text
Uploads are optional
User can skip upload
Supported file upload works
Unsupported file fails gracefully
Large file behavior is handled
Upload metadata saves
Storage path saves
Private bucket is used
User can delete upload
Upload summary appears only if available
Upload does not imply diagnosis
Upload does not block onboarding
```

---

# Commerce Bridge Checklist

Confirm:

```text
Commerce Bridge can be hidden
Commerce Bridge can be enabled
Benefit appears only for eligible users
Benefit is admin-configurable
No hardcoded discount rule
No hardcoded commerce platform
One primary action exists
Button copies benefit code
Button opens external commerce destination
Fallback works if automatic coupon application fails
External link works
Benefit events are tracked
Commerce does not become fixed Store tab
Commerce does not dominate Home
Commerce language is safe
External purchase boundary is clear
```

Preferred MVP action:

```text
Use Benefit
↓
Copy benefit code
↓
Open external commerce destination
```

---

# Subscription Checklist

If subscriptions are visible, confirm:

```text
Price is clear
Billing period is clear
Trial behavior is clear
Renewal behavior is clear
Cancellation path is clear
Included features are clear
Subscriber benefits are clear
Refund path is clear
Subscription status updates access
Expired subscription behavior works
Cancelled subscription behavior works
Past due behavior works if applicable
```

If subscriptions are not visible:

```text
No subscription copy appears
No broken subscription screen appears
No reviewer is forced into payment
```

---

# Privacy Checklist

Confirm:

```text
Privacy Policy URL is live
Privacy Policy opens from app
Privacy Policy matches actual data behavior
Data collection is accurately described
Health data usage is explained
Wearable data usage is explained
Upload usage is explained
AI usage is explained
Commerce Bridge tracking is explained if visible
Third-party providers are accurate
Account deletion is explained
Data deletion behavior is explained
```

Privacy Policy must not claim behavior that is not implemented.

---

# Terms Checklist

Confirm:

```text
Terms URL is live
Terms open from app
Product boundary is clear
No medical advice statement exists
No emergency use statement exists
AI-assisted guidance is explained
Daily Stack boundary is clear
Wearables are optional
Uploads are optional
Push is optional
Subscriptions are explained if visible
Commerce Bridge is explained if visible
External purchases are explained if visible
Account deletion is explained
```

---

# Account Deletion Checklist

Confirm:

```text
Account deletion path exists
User can find deletion path
User receives confirmation
User can cancel before confirming
User can confirm deletion
Deletion behavior is implemented
Uploads are deleted or handled according to policy
Wearable connections are revoked or disconnected
Subscription implications are clear
Auth behavior is handled
Privacy Policy matches deletion behavior
```

Minimum path:

```text
Settings
↓
Account
↓
Delete Account
↓
Confirmation
```

---

# Supabase Checklist

Confirm:

```text
Auth works
user_profiles works
user_settings works
plan_templates works
plan_template_versions works
user_active_plans works
pillar_definitions works
user_pillar_states works
daily_plans works
daily_actions works
push_events works
user_home_state works if implemented
stack_items works if visible
wearable_connections works if visible
wearable_metric_snapshots works if visible
user_uploads works if visible
commerce_benefits works if visible
user_commerce_benefits works if visible
commerce_events works if visible
admin_audit_log works if implemented
```

---

# RLS Checklist

Confirm:

```text
RLS is enabled on user-owned tables
User can read own data
User cannot read another user's data
User can update own settings
User cannot update another user's settings
User can access own uploads
User cannot access another user's uploads
Published plans are readable
Draft plans are hidden
Admin tables are protected
Service role key is not exposed to frontend
```

This is a launch blocker.

---

# Storage Checklist

Confirm:

```text
user_uploads bucket exists if uploads are visible
user_uploads bucket is private
public_assets bucket exists if needed
admin_assets bucket exists if needed
File upload works
File deletion works
Private files are not publicly accessible
Storage paths are stored correctly
```

---

# Edge Function Checklist

If Edge Functions are used, confirm:

```text
activate_plan works
generate_daily_plan works
process_push_response works
update_home_state works
evaluate_aai_context works
sync_wearable_snapshot works if wearables visible
process_user_upload works if uploads visible
issue_commerce_benefit works if Commerce Bridge visible
track_commerce_event works if Commerce Bridge visible
admin_publish_plan works if Admin publishing visible
```

Each function should handle:

```text
Valid input
Invalid input
Unauthorized user
Missing data
Duplicate request
Partial failure
Readable error response
```

---

# Admin Checklist

Confirm:

```text
Admin can create draft plan
Admin can edit draft plan
Admin can publish plan
Admin can archive plan
Draft content is hidden from regular users
Published content appears correctly
Admin can manage onboarding copy if implemented
Admin can manage Home content if implemented
Admin can manage Push copy if implemented
Admin can manage Commerce Benefits if implemented
Admin changes are logged if audit log exists
Non-admin users cannot access admin actions
```

---

# iOS Build Checklist

Confirm:

```text
Apple Developer account ready
Bundle ID created
App signing works
iOS build generated
App icon added
Display name correct
Version number correct
Build number correct
Launch screen works
Permissions configured
Deep links configured if used
External links work
TestFlight build uploads successfully
No critical crash on launch
```

---

# Android Build Checklist

Confirm:

```text
Google Play Console account ready
Android package name created
App signing configured
Android build generated
App icon added
Display name correct
Version number correct
Build number correct
Launch screen works
Permissions configured
Deep links configured if used
External links work
Internal testing build uploads successfully
No critical crash on launch
```

---

# App Store Metadata Checklist

Prepare:

```text
App name
Subtitle
Description
Keywords
Category
Support URL
Privacy Policy URL
Marketing URL if needed
Screenshots
App preview if needed
Copyright
Age rating
Contact information
Review notes
Test account credentials
```

Review copy for:

```text
No unsupported medical claims
No unclear AI claims
No misleading subscription claims
No confusing external commerce claims
```

---

# Google Play Metadata Checklist

Prepare:

```text
App name
Short description
Full description
Feature graphic
Screenshots
App category
Privacy Policy URL
Support email
Data Safety information
Content rating
Target audience
Contact information
Testing instructions
Review notes if needed
Test account credentials
```

Review copy for:

```text
No unsupported medical claims
No unclear AI claims
No misleading subscription claims
No confusing external commerce claims
```

---

# Screenshots Checklist

Recommended screenshot themes:

```text
Onboarding activation
Home operating surface
Current Insight
Next Best Action
Daily plan
Pillar overview
Daily Stack organization
Wearable optional connection
Mental Detox / Push control
Subscriber Benefits if Commerce Bridge is visible
Settings / privacy control
```

Avoid screenshots that imply:

```text
Diagnosis
Treatment
Guaranteed outcome
Disease prevention
Medical-grade monitoring
```

---

# Review Notes Checklist

Prepare clear review notes.

Include:

```text
What Wellbine is
What Wellbine is not
How to access app
Test account credentials
Whether subscription is required for testing
Whether wearable connection is optional
Whether uploads are optional
Whether Push is optional
Whether Commerce Bridge is visible
Where account deletion is located
Any feature flags
Any test data explanation
```

Suggested wording:

```text
Wellbine is a wellness guidance app. It does not provide medical diagnosis, treatment or emergency care. Wearable connection, uploads and Push notifications are optional. The reviewer can complete onboarding without connecting a wearable or uploading files.
```

---

# Test Account Checklist

Prepare at least one test account.

Test account should allow reviewer to access:

```text
Completed onboarding
Active plan
Home
Daily
Pillars
Settings
Account deletion path
Daily Stack if visible
Wearables screen if visible
Uploads screen if visible
Commerce Bridge if visible
Subscription state if visible
```

Avoid requiring:

```text
Real payment
Real wearable device
Real medical file
Real sensitive data
```

---

# Internal Testing Checklist

Before external review:

```text
Install app on iOS
Install app on Android
Create new account
Complete onboarding
Activate plan
Use Home
Use Daily
Respond to Push
Update Pillar
Use Daily Stack if visible
Skip wearable
Skip upload
Open external commerce if visible
Delete account
Check Supabase data
Check RLS
Check app crash logs
```

---

# Beta Testing Checklist

Before public release, beta should validate:

```text
Do users understand onboarding?
Do users understand Home?
Do users understand Next Best Action?
Do users respond to Push?
Do users find Daily useful?
Do users understand Pillars?
Do users feel commerce is helpful or intrusive?
Do users understand optional wearables?
Do users understand optional uploads?
Do users trust the product?
Where do users drop off?
Where do users get confused?
```

---

# Launch Gate Checklist

Do not launch unless:

```text
Signup works
Onboarding works
Plan activation works
Home works
Daily works
Pillars work
Settings work
Account deletion works
Privacy Policy is live
Terms are live
RLS is validated
No critical crashes
No unsupported health claims
App metadata is ready
Screenshots are ready
Review notes are ready
Test account is ready
```

---

# Blocker Checklist

Block release if:

```text
User data leaks across accounts
RLS is broken
Account deletion does not exist
Privacy Policy is missing
Terms are missing
Signup fails
Onboarding fails
Plan activation fails
Home is blank
Daily is broken
Draft admin content is visible
Push is required
Wearable is required
Upload is required
Commerce Bridge is broken but visible
Medical claims are unsafe
AI is positioned as medical diagnosis
```

---

# Post-Launch Monitoring Checklist

After release, monitor:

```text
Crash rate
Signup completion
Onboarding completion
Plan activation success
Home load success
Daily action completion
Push permission acceptance
Push response rate
Wearable connection rate
Upload usage
Commerce benefit usage
Subscription conversion if visible
Account deletion requests
Support tickets
App review issues
User complaints
Broken links
Performance issues
```

---

# Rollback / Disable Checklist

Admin or configuration should allow quick disabling of:

```text
Commerce Bridge
Specific benefits
Specific Plan Templates
Specific Push campaigns
Specific recommendations
Specific content modules
Specific onboarding options
Specific wearable providers
Upload visibility
```

The product should support controlled rollback without full app redeployment where possible.

---

# Final Pre-Submission Checklist

Before pressing submit:

```text
Correct build uploaded
Correct version selected
Correct screenshots uploaded
Correct Privacy Policy URL
Correct Terms URL
Correct support contact
Correct test account
Correct review notes
No draft content visible
No broken external links
No unsupported claims
Feature visibility confirmed
RLS validated
Account deletion validated
Internal test passed
```

---

# Current Status

App Release Checklist is currently a draft.

Next steps:

- Convert checklist into release spreadsheet or issue tracker
- Assign owners
- Define pass / fail status
- Define blocker status
- Validate against real iOS build
- Validate against real Android build
- Validate before each submission

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
- ARCHITECTURE_DECISIONS/HOME_CENTRAL.md
- ARCHITECTURE_DECISIONS/PUSH_ORCHESTRATION.md
- ARCHITECTURE_DECISIONS/PLAN_TEMPLATES_DB.md
- ARCHITECTURE_DECISIONS/ADMIN_CONTROL_LAYER.md
- ARCHITECTURE_DECISIONS/ONBOARDING_ACTIVATION.md
