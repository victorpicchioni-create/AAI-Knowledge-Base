# Wellbine MVP Build Sequence

**Version:** 0.1.0

**Status:** Draft

**Last Updated:** July 2026

---

# Purpose

This document defines the practical MVP build sequence for Wellbine.

The goal is to turn the full Wellbine documentation into a clear execution order.

This document answers:

- What should be built first
- What should wait
- What belongs in the real MVP
- Which Supabase tables come first
- Which FlutterFlow screens come first
- Which Edge Functions are mandatory
- When Push enters
- When Wearables enter
- When Uploads enter
- When Commerce Bridge enters
- When Admin becomes necessary
- When the product is ready for internal testing
- When the product is ready for App Store and Google Play preparation

This document is the construction roadmap.

---

# Official Definition

**Wellbine MVP Build Sequence is the ordered execution plan that defines how to build the first usable version of Wellbine across Supabase, FlutterFlow, Admin, Edge Functions, Home, Daily, Push, Pillars, privacy and release readiness.**

---

# Core Principle

The core MVP rule is:

```text
Build the operating loop before expanding the ecosystem.
```

The operating loop is:

```text
Signup
↓
Onboarding
↓
Plan Activation
↓
Home
↓
Daily
↓
User Action
↓
State Update
↓
Home adapts
```

Nothing should distract from proving this loop first.

---

# MVP Philosophy

The MVP should prove that Wellbine can act as an adaptive daily wellness operating system.

The MVP does not need to prove every future feature.

The MVP must prove:

- A user can join
- A user can activate a plan
- A user can understand what to do now
- A user can act
- The system updates
- The experience feels adaptive
- The product works without wearable
- The product works without uploads
- The product works without Push
- Commerce can remain hidden
- Admin can control key configuration
- Supabase remains the source of truth

The MVP should be simple, but not shallow.

---

# What The MVP Must Prove

The first MVP must prove:

```text
Can Wellbine guide a user through a useful day?
```

This means:

- Onboarding cannot be confusing
- Plan activation must work
- Home cannot be blank
- Daily must be actionable
- Pillars must reflect state
- Confirm / Adjust / Later must work
- Supabase data must update correctly
- The system must feel coherent
- The user must know what to do next

If this is not proven, adding wearables, uploads, commerce or complex AI will only create noise.

---

# What The MVP Should Not Try To Prove

The MVP should not try to prove everything at once.

Do not make the first MVP dependent on:

- Full wearable integration
- Full AI automation
- Full supplement commerce
- Full checkout integration
- Full upload interpretation
- Advanced admin analytics
- Complex plan marketplace
- Complex subscription tiers
- Full Push orchestration
- Advanced recommendation engine
- Advanced A/B testing
- Complete medical document processing
- Complex long-term analytics

These are later layers.

---

# MVP Build Layers

Recommended build layers:

```text
Layer 1: Foundation
Layer 2: Core Database
Layer 3: Auth And Profile
Layer 4: Onboarding
Layer 5: Plan Activation
Layer 6: Home
Layer 7: Daily
Layer 8: Pillars
Layer 9: Settings And Privacy
Layer 10: Basic Admin
Layer 11: QA Core Loop
Layer 12: Push
Layer 13: Daily Stack
Layer 14: Wearables Placeholder
Layer 15: Uploads Placeholder
Layer 16: Commerce Bridge Placeholder
Layer 17: App Release Preparation
```

The build should move forward only when each layer is stable enough.

---

# Phase 0 — Project Setup

Purpose:

```text
Prepare the working environment.
```

Build:

- Supabase project
- FlutterFlow project
- GitHub documentation repository
- Environment naming
- Development environment
- Basic app design direction
- Basic Supabase connection
- Basic FlutterFlow navigation shell

Output:

```text
A working technical foundation.
```

Do not build complex product logic before the technical base works.

---

# Phase 1 — Supabase Core Foundation

Purpose:

```text
Create the first database foundation.
```

Create these tables first:

```text
user_profiles
user_settings
plan_templates
plan_template_versions
pillar_definitions
user_active_plans
user_pillar_states
daily_plans
daily_actions
user_home_state
```

Also prepare:

```text
RLS enabled
Basic policies
Initial seed data
Initial pillar definitions
One published test plan
One published plan version
```

Do not start with every future table.

Start with the tables required for the operating loop.

---

# Phase 2 — Authentication

Purpose:

```text
Allow users to enter the system.
```

Build in FlutterFlow:

- Signup
- Login
- Logout
- Auth state check
- Password reset if needed
- Initial routing

Routing logic:

```text
If not authenticated:
    show Auth

If authenticated and onboarding incomplete:
    show Onboarding

If authenticated and onboarding complete but no active plan:
    show Plan Selection

If authenticated and active plan exists:
    show Home
```

Output:

```text
User can create account and return to correct state.
```

---

# Phase 3 — User Profile Baseline

Purpose:

```text
Capture minimum user context required for personalization.
```

Build:

- Name
- Biological sex
- Age
- Height
- Weight
- Country / region if needed
- Language
- Timezone
- Relevant comorbidities optional

Save to:

```text
user_profiles
user_settings
```

Rules:

```text
Comorbidities are optional.
Biological sex should include Prefer not to say.
Do not make onboarding feel like a medical exam.
Do not overcollect.
```

Output:

```text
User baseline exists in Supabase.
```

---

# Phase 4 — Onboarding Flow

Purpose:

```text
Turn registration into activation.
```

Build sequence:

```text
Welcome
↓
Profile Baseline
↓
Wearable Optional Step
↓
Mental Detox / Push Explanation
↓
Goals
↓
Plan Selection
↓
Pillar Preferences
↓
Upload Optional Step
↓
Activate Plan
```

Important MVP rule:

```text
Wearable, Push and Upload must be optional.
```

The user must be able to complete onboarding without:

- Connecting wearable
- Accepting Push
- Uploading files
- Entering sensitive medical data

Output:

```text
User reaches Plan Activation without friction.
```

---

# Phase 5 — Plan Templates MVP

Purpose:

```text
Give the user a starting configuration.
```

Create at least one test Plan Template.

Minimum Plan Template needs:

```text
name
slug
description
status
category
audience
current_version_id
```

Minimum Plan Version needs:

```text
configuration_json
pillar_defaults_json
daily_rules_json
push_rules_json
home_rules_json
```

For MVP, start with one general plan.

Example internal direction:

```text
7-Day Sync Plan
```

Do not overbuild plan categories yet.

Output:

```text
A published plan is available for activation.
```

---

# Phase 6 — Plan Activation

Purpose:

```text
Create the user's operating state.
```

Preferred implementation:

```text
activate_plan Edge Function
```

Minimum activation should create:

```text
user_active_plans
user_pillar_states
daily_plans
daily_actions
user_home_state
```

Plan activation must:

- Validate published plan
- Store active plan snapshot
- Create pillar states
- Create first daily plan
- Create initial daily actions
- Create Home state
- Route user to Home

Output:

```text
User enters Home with a useful initial state.
```

This is a critical milestone.

---

# Phase 7 — Home MVP

Purpose:

```text
Create the central operating surface.
```

Home must show:

- Main Orb
- Current Insight
- Next Best Action
- Pillar Orbs
- Daily access
- Personal Center access

Home reads from:

```text
user_home_state
user_active_plans
user_pillar_states
daily_plans
daily_actions
```

Home must not be:

- Blank
- Dashboard-heavy
- Store-focused
- Dependent on wearables
- Dependent on Push

Output:

```text
User opens the app and immediately understands what matters now.
```

---

# Phase 8 — Daily MVP

Purpose:

```text
Give the user a simple execution layer.
```

Daily must show:

- Current action
- Upcoming actions
- Completed actions
- Delayed actions
- Recovery-aware state

Daily action controls:

```text
Confirm
Adjust
Later
```

For MVP:

```text
Confirm = mark complete
Later = delay action
Adjust = open simple adjustment state or screen
```

Daily updates:

```text
daily_actions
user_pillar_states
user_home_state
```

Output:

```text
User can act and see the system update.
```

---

# Phase 9 — Pillars MVP

Purpose:

```text
Represent user wellness areas as operational modules.
```

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

Each pillar needs:

- Name
- Status
- Simple detail view
- Connection to Daily
- Connection to Home Orb
- Basic action update

Do not build deep pillar analytics yet.

Output:

```text
Pillars reflect the user's day without becoming complex dashboards.
```

---

# Phase 10 — State Update Loop

Purpose:

```text
Prove that user actions update the system.
```

Build the loop:

```text
User taps Confirm
↓
daily_actions updates
↓
user_pillar_states updates
↓
user_home_state updates
↓
Home shows updated state
```

Minimum required Edge Function:

```text
process_daily_action
```

or MVP direct write if still simple.

Preferred:

```text
Use Edge Function once multiple tables update together.
```

Output:

```text
Wellbine feels alive and coherent.
```

This is the most important MVP proof.

---

# Phase 11 — Settings / Personal Center

Purpose:

```text
Give the user control.
```

Build:

- Profile
- Settings
- Push preferences placeholder
- Mental Detox setting
- Wearables placeholder
- Uploads placeholder
- Daily Stack access
- Privacy Policy link
- Terms link
- Account
- Delete Account
- Logout

Output:

```text
User can manage basic account and product controls.
```

---

# Phase 12 — Account Deletion

Purpose:

```text
Prepare release-critical privacy control.
```

Build path:

```text
Settings
↓
Account
↓
Delete Account
↓
Confirmation
```

Preferred implementation:

```text
delete_account Edge Function
```

MVP deletion may begin with:

- Mark account deleted
- Disable access
- Delete or anonymize user data according to defined policy
- Delete uploads if implemented
- Match Privacy Policy language

Output:

```text
Account deletion path exists and works.
```

This is release-critical.

---

# Phase 13 — Basic Admin MVP

Purpose:

```text
Allow product configuration without app redeployment.
```

Minimum Admin controls:

```text
Plan Templates
Plan Template Versions
Pillar Definitions
Content Modules
Feature Flags
Commerce Benefits hidden/visible
Publishing status
```

Admin platform may be:

```text
Softr
Retool
Supabase Studio
Custom Admin
```

MVP Admin does not need advanced analytics.

Output:

```text
Internal team can control what users see.
```

---

# Phase 14 — QA Core Loop

Purpose:

```text
Validate the real MVP.
```

Test:

```text
Signup
Onboarding
Plan Activation
Home
Daily
Confirm / Adjust / Later
Pillar update
Settings
Privacy link
Terms link
Account deletion
RLS
```

Minimum success:

```text
A new user can go from signup to useful Home state and complete a Daily action.
```

No further feature should be prioritized until this passes.

---

# Phase 15 — Push MVP

Purpose:

```text
Add outside-app orchestration after the core loop works.
```

Push should not be built before Home and Daily are stable.

MVP Push:

- Permission explanation
- User can accept or deny
- Push optional
- Simple scheduled check-in
- Confirm / Adjust / Later
- Deep link to Daily or relevant panel
- Push event recorded

Tables:

```text
push_events
user_settings
daily_actions
user_home_state
```

Function:

```text
process_push_response
```

Output:

```text
Push improves execution without being required.
```

---

# Phase 16 — Daily Stack MVP

Purpose:

```text
Support routine organization.
```

Build:

- Add item
- Edit item
- Delete item
- Mark taken
- Skip item
- Timing
- Frequency

Table:

```text
stack_items
```

Daily Stack may connect to:

```text
Daily
Home
Pillars
Commerce Bridge later
```

Output:

```text
User can organize routine items safely.
```

---

# Phase 17 — Wearables MVP Placeholder

Purpose:

```text
Prepare wearable architecture without blocking MVP.
```

Build:

- Wearable Manager screen
- Optional connection copy
- Manual fallback
- Provider status
- Coming soon state if not integrated
- Last sync placeholder if needed

Tables:

```text
wearable_connections
wearable_metric_snapshots
```

Important rule:

```text
Do not claim integration before it exists.
```

Output:

```text
Wearables are positioned correctly but do not block launch.
```

---

# Phase 18 — Uploads MVP Placeholder

Purpose:

```text
Prepare optional file enrichment.
```

Build:

- Upload Manager
- Upload optional explanation
- File picker if ready
- Upload metadata
- Delete upload
- Private storage bucket

Tables:

```text
user_uploads
```

Storage:

```text
user_uploads bucket
```

Output:

```text
Uploads enrich context without becoming mandatory.
```

---

# Phase 19 — Commerce Bridge MVP

Purpose:

```text
Add subscriber benefit layer without making commerce central.
```

Build only after core experience is stable.

MVP Commerce Bridge:

- Benefit visibility by configuration
- Eligibility check
- One primary button
- Copy benefit code
- Open external destination
- Track event
- Hide if not ready

Tables:

```text
commerce_benefits
user_commerce_benefits
commerce_events
```

Button behavior:

```text
Use Benefit
↓
Copy benefit code
↓
Open external commerce destination
```

Important rules:

```text
Do not hardcode discount amounts.
Do not hardcode commerce platform.
Do not make Store a fixed primary tab.
Commerce must be hideable.
```

Output:

```text
Monetization support exists without weakening product trust.
```

---

# Phase 20 — App Release Preparation

Purpose:

```text
Prepare iOS and Android submission.
```

Required before submission:

- Privacy Policy URL
- Terms URL
- Account deletion
- App description
- Screenshots
- Test account
- Review notes
- No unsupported medical claims
- Push optional
- Wearables optional
- Uploads optional
- Commerce hidden or working
- RLS validated
- No critical crashes

Output:

```text
App is ready for internal testing and review preparation.
```

---

# MVP Critical Path

The true MVP critical path is:

```text
Supabase Core
↓
Auth
↓
Profile
↓
Onboarding
↓
Plan Template
↓
Plan Activation
↓
Home
↓
Daily
↓
Action Update
↓
Pillar State
↓
Settings
↓
Account Deletion
↓
QA
```

Everything else is secondary until this works.

---

# Mandatory MVP Tables

Mandatory:

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

Strongly recommended:

```text
push_events
stack_items
content_modules
admin_audit_log
```

Optional for first internal MVP:

```text
wearable_connections
wearable_metric_snapshots
user_uploads
recommendations
commerce_benefits
user_commerce_benefits
commerce_events
user_aai_context
```

---

# Mandatory MVP Screens

Mandatory:

```text
Auth
Welcome
Profile Baseline
Onboarding
Plan Selection
Plan Activation Loading
Home
Daily
Pillar Detail
Settings / Personal Center
Privacy / Terms
Account
Delete Account
Error / Loading states
```

Strongly recommended:

```text
Daily Stack
Mental Detox / Push Explanation
Push Preferences
```

Optional first internal MVP:

```text
Wearable Manager
Upload Manager
Commerce Benefit Detail
Ask Wellbine
```

---

# Mandatory MVP Edge Functions

Mandatory:

```text
activate_plan
update_home_state
process_daily_action
delete_account
```

Strongly recommended:

```text
generate_daily_plan
process_push_response
evaluate_aai_context
```

Optional first MVP:

```text
process_user_upload
issue_commerce_benefit
track_commerce_event
sync_wearable_snapshot
admin_publish_plan
```

---

# Feature Timing

Recommended timing:

```text
Push:
After Home and Daily work.

Daily Stack:
After Daily works.

Wearables:
After manual flow works.

Uploads:
After profile and plan activation work.

Commerce Bridge:
After core product value is clear.

Advanced AI:
After structured context exists.

Admin Analytics:
After users generate real events.
```

---

# MVP Feature Priority

Priority 1:

```text
Auth
Onboarding
Plan Activation
Home
Daily
Pillars
State Updates
Settings
Account Deletion
RLS
```

Priority 2:

```text
Push
Daily Stack
Basic Admin
Content Modules
QA
App Release
```

Priority 3:

```text
Wearables
Uploads
Commerce Bridge
Recommendations
AAI Context
```

Priority 4:

```text
Advanced analytics
Advanced AI
Full commerce integration
Full wearable integrations
Partner dashboards
A/B testing
```

---

# What To Avoid During MVP

Avoid:

- Building too many plans
- Building complex AI before data exists
- Building commerce before trust exists
- Building wearables before manual flow works
- Building upload interpretation before privacy is clear
- Building analytics dashboards before core events exist
- Building a Store tab
- Hardcoding plan behavior into FlutterFlow
- Skipping RLS
- Skipping account deletion
- Making Push required
- Making wearable required
- Making uploads required

---

# Internal MVP Acceptance Criteria

Internal MVP is acceptable when:

```text
User can sign up
User can complete onboarding
User can activate a plan
User can reach Home
Home shows useful state
User can open Daily
User can complete at least one action
Action updates Daily
Action updates Pillars
Action updates Home
User can open Settings
User can access Privacy and Terms
User can delete account
RLS protects user data
No critical screen is blank
```

---

# Beta MVP Acceptance Criteria

Beta MVP is acceptable when:

```text
Internal MVP passes
Push is optional and stable
Daily Stack works if visible
Basic Admin can control published plans
Feature flags can hide unfinished features
App has no unsafe medical claims
Privacy Policy is live
Terms are live
App Release Checklist mostly passes
Test accounts work
Basic analytics exist
```

---

# Controlled Launch Criteria

Controlled launch is acceptable when:

```text
Beta MVP passes
App Store / Google Play requirements are ready
Account deletion works
RLS is validated
Core flows are stable
No critical crashes
Commerce Bridge is hidden or working
Wearables are optional
Uploads are optional
Push is optional
Support process exists
Admin can disable risky features
```

---

# Build Sequence Summary

Recommended order:

```text
1. Supabase foundation
2. Auth
3. Profile baseline
4. Onboarding
5. Plan Templates
6. Plan Activation
7. Home
8. Daily
9. Pillars
10. State update loop
11. Settings
12. Account deletion
13. Basic Admin
14. QA core loop
15. Push
16. Daily Stack
17. Wearables placeholder
18. Uploads placeholder
19. Commerce Bridge MVP
20. App Release preparation
```

---

# Current Status

MVP Build Sequence is currently a draft.

Next steps:

- Confirm MVP scope
- Build Supabase core tables
- Build FlutterFlow Auth
- Build Onboarding
- Build Plan Activation
- Build Home
- Build Daily
- Build State Update Loop
- Run core QA
- Add secondary layers only after core loop works

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
- PRODUCTS/WELLBINE/EDGE_FUNCTIONS.md
- PRODUCTS/WELLBINE/QA_PLAN.md
- PRODUCTS/WELLBINE/PRIVACY_POLICY_DRAFT.md
- PRODUCTS/WELLBINE/TERMS_DRAFT.md
- PRODUCTS/WELLBINE/APP_RELEASE_CHECKLIST.md
- PRODUCTS/WELLBINE/FLUTTERFLOW_BUILD_GUIDE.md
- PRODUCTS/WELLBINE/ADMIN_BUILD_GUIDE.md
