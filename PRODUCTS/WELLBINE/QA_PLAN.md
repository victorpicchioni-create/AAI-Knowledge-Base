# Wellbine QA Plan

**Version:** 0.1.0

**Status:** Draft

**Last Updated:** July 2026

---

# Purpose

This document defines the Quality Assurance plan for Wellbine.

The goal is to make sure the product works reliably before release, especially across:

- Onboarding
- Plan Activation
- Home
- Daily
- Push
- Pillars
- Daily Stack
- Wearables
- Uploads
- Commerce Bridge
- Admin
- Supabase
- Row Level Security
- App Release
- Privacy
- Account deletion
- Regression testing

QA is not only bug testing.

QA is the process of proving that Wellbine works as an adaptive operating system for daily wellness.

---

# Official Definition

**Wellbine QA Plan is the structured testing and validation process used to verify that Wellbine works safely, reliably and coherently across product experience, backend logic, user data, admin configuration, app release and privacy-sensitive flows.**

---

# Core Principle

The core QA rule is:

```text
Do not launch a feature because it exists. Launch it because it works as part of the system.
```

A feature is not ready when the screen is built.

A feature is ready when:

- The user can understand it
- The user can complete the flow
- The data is stored correctly
- The app handles failure gracefully
- The experience remains coherent
- Privacy rules are respected
- Admin configuration behaves correctly
- The feature does not break other parts of the system

---

# QA Scope

QA should cover:

- Product logic
- User experience
- Backend data
- App state
- Admin configuration
- Permissions
- Privacy flows
- App Store / Google Play readiness
- Edge cases
- Regression
- Error states
- Fallback states

Wellbine should be tested as a connected system, not as isolated screens.

---

# Testing Environments

Recommended environments:

```text
Development
↓
Staging
↓
Internal Testing
↓
Beta Testing
↓
Production
```

---

## Development

Used for building and early debugging.

May contain:

- Test data
- Draft plans
- Incomplete flows
- Developer accounts
- Temporary configuration

Development is not reliable enough for release decisions.

---

## Staging

Used for release validation.

Should be as close as possible to production.

Staging should include:

- Realistic plan templates
- Realistic onboarding
- Realistic Home states
- Realistic Daily plans
- Push testing
- Permission testing
- Admin publishing tests
- Supabase RLS tests
- Commerce Bridge test links
- Wearable mock or test data
- Upload testing

Staging is the main QA environment.

---

## Internal Testing

Used by the internal team before public release.

Should test:

- Full user journey
- App stability
- Device behavior
- Permission prompts
- Push behavior
- App review readiness
- Test accounts

---

## Beta Testing

Used with selected external users.

Should test:

- User comprehension
- Activation
- Retention signals
- Friction
- Bugs
- Confusion
- Push relevance
- Home usefulness
- Daily completion
- Plan clarity

Beta testing should not include risky unfinished features.

---

## Production

Used only after release criteria are met.

Production should be monitored for:

- Crashes
- Signup errors
- Onboarding drop-off
- Plan activation failures
- Push failures
- Broken links
- Account deletion requests
- Permission issues
- Subscription issues
- Commerce link issues
- Unexpected app review problems

---

# QA Personas

Wellbine should be tested with different user profiles.

Minimum QA personas:

```text
New user with no wearable
New user with wearable
User who denies Push
User who accepts Push
User who skips uploads
User who uploads a file
User with active plan
User with no active plan
User with Daily Stack items
User with Commerce Bridge visible
User with Commerce Bridge hidden
User using iOS
User using Android
User deleting account
```

---

# Critical User Journeys

The most important journeys are:

```text
Signup
↓
Onboarding
↓
Plan Selection
↓
Plan Activation
↓
Home
↓
Daily
↓
Push Response
↓
Pillar Update
↓
Next Best Action
```

And:

```text
Existing User
↓
Open App
↓
Home Loads
↓
Current Insight Is Clear
↓
Next Best Action Is Relevant
↓
User Acts
↓
State Updates
```

If these flows do not work, Wellbine is not ready.

---

# Onboarding QA

Onboarding must be tested carefully because it is the first activation flow.

Test:

- Welcome screen loads
- Name input works
- Biological sex selection works
- Age input works
- Height input works
- Weight input works
- Comorbidities step is optional
- Wearable connection is optional
- Push permission is optional
- Mental Detox explanation appears before Push permission
- Goals can be selected
- Plan model can be selected
- Pillar preferences can be adjusted
- Upload step is optional
- User can skip non-required steps
- User can complete onboarding
- Onboarding completion updates Supabase
- User enters Home after completion

Failure cases:

- User exits onboarding
- User loses connection
- User skips optional steps
- User denies permissions
- User enters incomplete data
- User returns later

Success criteria:

```text
A new user can complete onboarding without wearable, without upload and without Push permission.
```

---

# Plan Activation QA

Plan Activation is critical because it connects onboarding to the operating system.

Test:

- Published plans appear
- Draft plans do not appear
- Archived plans do not appear
- User can select a plan
- Recommended plan can be shown
- Adapted plan can be shown
- Plan activation creates active plan
- Active plan references correct template version
- Active plan stores snapshot
- Pillar states are created
- Daily plan is created
- Home state is initialized
- Push schedule can be prepared if enabled
- User can enter Home after activation

Failure cases:

- No published plan available
- Plan activation fails
- Network fails during activation
- User closes app during activation
- Plan template is updated after user activation

Success criteria:

```text
A user can activate a plan and receive a stable plan snapshot without being affected by later template edits.
```

---

# Home QA

Home is the central operating surface.

Test:

- Home loads after onboarding
- Home loads for returning users
- Home loads with active plan
- Home loads without active plan
- Main Orb displays useful state
- Pillar Orbs display correct statuses
- Current Insight appears
- Next Best Action appears
- Adaptive Summary opens
- Pillar quick panel opens
- Ask Wellbine entry point works
- Settings / Personal Center is accessible
- Home reflects Daily progress
- Home reflects Push responses
- Home reflects wearable data when available
- Home works without wearable data
- Home does not become a Store
- Commerce card appears only when configured

Failure cases:

- No Daily plan
- No wearable data
- No Push permission
- Missing pillar state
- Slow Supabase response
- Empty recommendations

Success criteria:

```text
Home should never feel blank, broken or confusing after activation.
```

---

# Daily QA

Daily is the deeper execution layer.

Test:

- Daily plan loads
- Daily actions appear in correct order
- Actions show status correctly
- Upcoming actions appear
- Active actions appear
- Completed actions update
- Delayed actions update
- Expired actions do not punish user
- Adjust opens correct flow
- Confirm marks action complete
- Later delays action
- Daily adapts when user responds
- Daily syncs with Home
- Daily syncs with Push
- Daily respects active plan
- Daily respects fasting or protocol context when applicable
- Daily uses recovery-aware language

Failure cases:

- User misses a window
- User completes action late
- User skips action
- User changes plan
- Daily plan expires
- No internet connection

Success criteria:

```text
Daily should help the user continue from the current state, not feel like a failed checklist.
```

---

# Push QA

Push is an orchestration layer, not a reminder layer.

Test:

- Push permission prompt appears at correct time
- User can accept Push
- User can deny Push
- App works if Push is denied
- Push respects Mental Detox
- Push respects frequency limits
- Push deep-links correctly
- Confirm works
- Adjust opens correct screen
- Later schedules follow-up
- Push response updates daily action
- Push response updates Home
- Push event is recorded
- Push does not become promotional spam
- Commerce Push appears only when configured and relevant

Failure cases:

- Push not delivered
- Push delivered late
- User taps after action window
- User dismisses Push
- User changes notification settings
- Device blocks notifications

Success criteria:

```text
Push should improve execution without becoming noise.
```

---

# Pillars QA

Operational Pillars must reflect user state accurately.

Initial pillars:

```text
Mind
Sun
Hydration
Sleep
Nutrition
Movement
Daily Stack
```

Test:

- Each pillar loads
- Each pillar has correct status
- Pillar Orb matches pillar state
- Pillar quick panel opens
- Pillar action can be confirmed
- Pillar state updates after action
- Pillar state updates after Daily action
- Pillar state updates after Push response
- Pillar works without wearable data
- Pillar works with wearable data when available
- Pillar copy is clear
- Pillar does not overstate medical claims

Success criteria:

```text
Pillars should be simple enough for the user and structured enough for AAI.
```

---

# Daily Stack QA

Daily Stack handles sensitive routine items.

Test:

- User can add item
- User can edit item
- User can remove item
- User can mark item taken
- User can skip item
- User can set timing
- User can set frequency
- Refill tracking can be enabled or disabled
- Stack item appears in Daily when relevant
- Stack item appears in Home when relevant
- Stack can connect to Commerce Bridge when configured
- Medication language is careful
- App does not prescribe medication

Failure cases:

- User enters unclear dosage
- User adds medication
- User skips repeatedly
- Refill date passes
- Commerce benefit unavailable

Success criteria:

```text
Daily Stack should organize routines without pretending to prescribe or treat.
```

---

# Wearables QA

Wearables are optional context enhancers.

Test:

- Wearable connection screen loads
- User can skip wearable connection
- App works without wearable
- Manual fallback works
- Connected provider status displays correctly
- Disconnected provider status displays correctly
- Revoked permission is handled
- Last sync time displays correctly
- Wearable snapshot updates context
- Wearable data improves Home when available
- Wearable data improves Daily when available
- Wearable data improves AAI context when available
- App does not claim unsupported providers

Failure cases:

- Provider unavailable
- Permission denied
- Permission revoked
- Sync fails
- Data missing
- Data stale
- Data inconsistent

Success criteria:

```text
Wearables should improve Wellbine, but Wellbine must work without them.
```

---

# Uploads QA

Uploads are optional and privacy-sensitive.

Test:

- Upload screen loads
- User can skip upload
- User can upload supported file
- Unsupported file is rejected gracefully
- File metadata is saved
- File is stored in correct bucket
- User can view upload status
- User can delete uploaded file
- Upload summary appears only when available
- Upload does not block onboarding
- Upload does not expose user files to other users

Failure cases:

- Large file
- Unsupported file type
- Upload interrupted
- Extraction fails
- User deletes file
- Storage permission error

Success criteria:

```text
Uploads should enrich context without becoming mandatory or risky.
```

---

# Commerce Bridge QA

Commerce Bridge must reduce friction without making commerce central.

Test:

- Commerce Bridge can be hidden
- Commerce Bridge can be enabled
- Benefit appears only for eligible users
- Ineligible users do not see restricted benefits
- Benefit copy is clear
- One primary action appears
- Button copies benefit code
- Button opens external commerce destination
- Automatic coupon link works if configured
- Manual coupon fallback works
- External URL opens correctly
- Benefit events are recorded
- Commerce does not appear as fixed Store tab in MVP
- Commerce does not dominate Home
- Commerce Push appears only if allowed and relevant

Failure cases:

- Coupon copy fails
- External link fails
- User is not eligible
- Benefit expired
- Commerce platform changes URL behavior
- User returns from store

Success criteria:

```text
One tap should copy the benefit and open the external destination, while preserving fallback.
```

---

# Admin QA

Admin controls configuration and publishing.

Test:

- Admin can create draft Plan Template
- Admin can edit draft Plan Template
- Admin can publish Plan Template
- Admin can archive Plan Template
- Draft plans are hidden from users
- Published plans are visible
- Archived plans are hidden from new activation
- Admin can configure Home copy
- Admin can configure Push copy
- Admin can configure Pillar defaults
- Admin can configure Commerce Benefits
- Admin can hide Commerce Bridge
- Admin changes are logged
- Admin cannot accidentally expose draft content
- Non-admin users cannot access admin actions

Success criteria:

```text
Admin should control product behavior without requiring app redeployment for every business rule change.
```

---

# Supabase QA

Supabase is the source of truth.

Test:

- Auth works
- User profile is created
- User settings are created
- Plan templates load
- User active plan is created
- Pillar states are created
- Daily plans are created
- Daily actions are created
- Push events are recorded
- Home state is updated
- Stack items are stored
- Wearable connections are stored
- Upload metadata is stored
- Commerce benefits are stored
- Commerce events are recorded
- Admin audit log records key changes

Success criteria:

```text
Supabase data should match the user experience shown in FlutterFlow.
```

---

# Row Level Security QA

RLS is critical.

Test:

- User can read own profile
- User cannot read another user’s profile
- User can read own Daily plan
- User cannot read another user’s Daily plan
- User can update own settings
- User cannot update another user’s settings
- User can access own uploads
- User cannot access another user’s uploads
- User can read published plans
- User cannot edit plan templates
- User cannot edit commerce benefits
- User cannot access admin audit logs
- Admin can manage admin tables
- Service role key is never exposed to app frontend

Success criteria:

```text
No user should be able to access or modify another user’s private data.
```

---

# Edge Function QA

Edge Functions should be tested as controlled backend logic.

Test:

- `activate_plan`
- `generate_daily_plan`
- `process_push_response`
- `update_home_state`
- `evaluate_aai_context`
- `sync_wearable_snapshot`
- `process_user_upload`
- `issue_commerce_benefit`
- `track_commerce_event`
- `admin_publish_plan`

Each function should test:

- Valid input
- Invalid input
- Unauthorized user
- Missing data
- Duplicate request
- Partial failure
- Correct database updates
- Correct error response
- No private data leakage

Success criteria:

```text
Edge Functions should protect important logic from fragile frontend-only behavior.
```

---

# App Release QA

App Release QA prepares Wellbine for App Store and Google Play review.

Test:

- App icon
- App name
- Bundle ID / package name
- App description
- Screenshots
- Privacy Policy URL
- Terms URL
- Support URL
- Account deletion path
- Test account
- App Review notes
- Health permission copy
- Push permission copy
- Wearable permission copy
- AI explanation
- External commerce explanation
- Subscription language if applicable
- No unsupported medical claims
- No broken links

Success criteria:

```text
A reviewer should understand what Wellbine does, what it does not do and how to test it.
```

---

# Privacy QA

Privacy-sensitive flows must be tested before launch.

Test:

- Privacy Policy is accessible
- Terms are accessible
- User understands health data usage
- User understands wearable data usage
- User understands upload usage
- User understands AI usage
- User understands external commerce behavior
- User can delete account
- User can delete uploads
- User can revoke Push
- User can disconnect wearable
- Private files are not publicly accessible

Success criteria:

```text
Privacy behavior in the app must match the Privacy Policy.
```

---

# Account Deletion QA

Account deletion is mandatory for release readiness.

Test:

- User can find deletion path
- User receives confirmation
- User can cancel deletion
- User can confirm deletion
- Profile deletion behavior works
- Upload deletion behavior works
- Wearable disconnection works
- Active plan handling works
- Daily data handling works
- Commerce data handling works
- Auth user handling works
- User cannot log in after deletion if fully deleted
- Privacy Policy matches actual deletion behavior

Success criteria:

```text
Account deletion should be clear, functional and consistent with policy.
```

---

# Regression QA

Regression testing prevents old features from breaking.

Run regression after changes to:

- Onboarding
- Plan Templates
- Home
- Daily
- Push
- Pillars
- Supabase Schema
- Admin
- Commerce Bridge
- Wearables
- App Release configuration

Minimum regression checklist:

```text
Signup works
Onboarding works
Plan activation works
Home loads
Daily loads
Push response works
Pillar state updates
Settings open
Account deletion path exists
RLS still protects user data
```

---

# Device QA

Test on multiple devices.

Minimum:

```text
iPhone recent model
iPhone older supported model
Android recent model
Android older supported model
Tablet if supported
```

Test:

- Screen layout
- Keyboard behavior
- Safe areas
- Push permission
- Health permission
- Deep links
- External links
- App restart
- Slow connection
- Offline behavior
- Dark mode if supported

---

# Performance QA

Wellbine should feel fast enough to trust.

Test:

- App launch time
- Home load time
- Daily load time
- Push response processing
- Plan activation time
- File upload time
- Recommendation loading
- Admin-configured content loading
- Supabase query performance

Success criteria:

```text
The user should not feel that Wellbine is slow when trying to act.
```

---

# Offline And Poor Connection QA

Wellbine should fail gracefully.

Test:

- App opens with poor connection
- Home handles loading state
- Daily handles loading state
- User action handles failure
- Push response handles delayed sync
- Upload interruption is handled
- External commerce link failure is handled
- Error messages are understandable

Success criteria:

```text
Connection problems should not make the product feel broken or unsafe.
```

---

# Error Message QA

Error messages should be useful.

Avoid:

```text
Something went wrong.
```

Better:

```text
We could not update this action right now. Try again in a moment.
```

Errors should be:

- Clear
- Human
- Non-technical
- Recoverable
- Calm
- Not blame the user

---

# Health Claim QA

Review all user-facing copy for unsafe claims.

Avoid:

- Diagnose
- Treat
- Cure
- Prevent disease
- Guarantee results
- Replace doctor
- Replace medication
- Medical-grade outcome without basis

Preferred language:

- Supports
- Helps organize
- Guides
- Suggests
- Encourages
- Wellness routine
- Daily alignment
- Recovery-aware guidance

Success criteria:

```text
Wellbine should remain a wellness guidance system, not a medical diagnosis product.
```

---

# Launch Readiness Checklist

Before controlled launch, verify:

```text
Onboarding works
Plan Activation works
Home works
Daily works
Push works or degrades gracefully
Pillars work
Daily Stack works
Wearables are optional
Uploads are optional
Commerce Bridge can be hidden or enabled
Admin publishing works
Supabase RLS works
Account deletion works
Privacy Policy is live
Terms are live
App Review notes are ready
Test account is ready
No unsupported health claims
No critical crashes
No broken primary flows
```

---

# Blocker Criteria

Do not launch if:

- Signup fails
- Onboarding cannot complete
- Plan Activation fails
- Home is blank after activation
- Daily does not load
- User data leaks across accounts
- RLS is broken
- Account deletion does not exist
- Privacy Policy is missing
- Terms are missing
- App makes unsafe health claims
- Push is required for app usage
- Wearable connection is required for app usage
- Upload is required for app usage
- Commerce flow is broken but visible
- Draft admin content is visible to users

---

# QA Metrics

Track:

- Crash rate
- Signup completion
- Onboarding completion
- Plan activation success
- Home load success
- Daily action completion
- Push permission acceptance
- Push response rate
- Wearable connection rate
- Upload usage
- Commerce benefit usage
- Account deletion requests
- Support tickets
- App review issues
- User confusion points

---

# Current Status

QA Plan is currently a draft.

The next steps are:

- Convert this plan into test cases
- Define staging environment
- Create internal test accounts
- Prepare QA checklist for each release
- Validate Supabase RLS
- Validate App Release requirements
- Validate Privacy and Terms alignment
- Run first end-to-end test from signup to Home

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
- ARCHITECTURE_DECISIONS/HOME_CENTRAL.md
- ARCHITECTURE_DECISIONS/PUSH_ORCHESTRATION.md
- ARCHITECTURE_DECISIONS/PLAN_TEMPLATES_DB.md
- ARCHITECTURE_DECISIONS/ADMIN_CONTROL_LAYER.md
- ARCHITECTURE_DECISIONS/ONBOARDING_ACTIVATION.md
