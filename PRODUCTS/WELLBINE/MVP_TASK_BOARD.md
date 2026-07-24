# Wellbine MVP Task Board

**Version:** 0.1.0

**Status:** Draft

**Last Updated:** July 2026

---

# Purpose

This document defines the practical MVP task board for building Wellbine.

The goal is to transform the Wellbine documentation into executable tasks.

This document should be used as the operational checklist for building the first usable version of Wellbine across:

- GitHub
- Supabase
- FlutterFlow
- Edge Functions
- Admin
- Feature Flags
- QA
- Privacy
- Terms
- App Release

This is the working construction board.

---

# Official Definition

**Wellbine MVP Task Board is the execution checklist used to build, validate and prepare the first usable version of Wellbine for internal testing, beta testing and controlled launch.**

---

# Core Principle

The core MVP task rule is:

```text
Build the operating loop first.
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

Do not prioritize secondary features until this loop works.

---

# MVP Status Legend

Use this status system:

```text
[ ] Not started
[/] In progress
[x] Done
[!] Blocked
[-] Deferred
```

---

# Phase 0 — Repository And Project Setup

## GitHub

```text
[ ] Confirm repository structure
[ ] Keep AAI-Knowledge-Base as documentation source of truth
[ ] Decide whether Wellbine code will live in same repo or separate product repo
[ ] Create product implementation folders if using same repo
[ ] Create /supabase folder
[ ] Create /supabase/migrations folder
[ ] Create /supabase/functions folder
[ ] Create /apps/mobile folder if FlutterFlow code is pushed to same repo
[ ] Create /apps/admin folder if Lovable/Admin code is pushed to same repo
[ ] Create branch strategy
[ ] Define main branch protection
[ ] Define PR review rule
[ ] Define agent workflow for Codex / Claude review
```

## Recommended repository structure

```text
AAI-Knowledge-Base/
    PRODUCTS/
        WELLBINE/
            documentation files

    supabase/
        migrations/
        functions/
        seed.sql

    apps/
        mobile/
        admin/

    .github/
        workflows/
```

## Output

```text
[ ] GitHub repository is ready to support real implementation
```

---

# Phase 1 — Supabase Project Setup

```text
[ ] Create Supabase development project
[ ] Choose project region
[ ] Save Supabase project URL
[ ] Save anon key
[ ] Store service role key securely
[ ] Confirm service role key is never exposed in FlutterFlow
[ ] Enable Supabase Auth
[ ] Configure email auth
[ ] Configure password reset if needed
[ ] Confirm database access
[ ] Confirm SQL editor access
[ ] Confirm Edge Functions access
[ ] Confirm Storage access
```

## Environment variables

```text
[ ] SUPABASE_URL
[ ] SUPABASE_ANON_KEY
[ ] SUPABASE_SERVICE_ROLE_KEY
[ ] SUPABASE_PROJECT_REF
[ ] APP_ENV
```

## Output

```text
[ ] Supabase development project is ready
```

---

# Phase 2 — Run Supabase SQL MVP

Reference:

```text
PRODUCTS/WELLBINE/SUPABASE_SQL_MVP.md
```

## SQL Execution

```text
[ ] Review SUPABASE_SQL_MVP.md
[ ] Copy SQL into Supabase SQL editor
[ ] Run extension setup
[ ] Run updated_at trigger function
[ ] Create user_roles
[ ] Create is_admin helper
[ ] Create user_profiles
[ ] Create user_settings
[ ] Create plan_templates
[ ] Create plan_template_versions
[ ] Create user_active_plans
[ ] Create pillar_definitions
[ ] Create user_pillar_states
[ ] Create daily_plans
[ ] Create daily_actions
[ ] Create user_home_state
[ ] Create feature_flags
[ ] Create content_modules
[ ] Create admin_audit_log
[ ] Create optional push_events
[ ] Create optional stack_items
[ ] Enable RLS
[ ] Create RLS policies
[ ] Seed pillar_definitions
[ ] Seed feature_flags
[ ] Seed starter Plan Template
[ ] Seed starter Plan Version
```

## SQL Validation

```text
[ ] Confirm all tables exist
[ ] Confirm all triggers exist
[ ] Confirm RLS is enabled
[ ] Confirm seed pillars exist
[ ] Confirm starter plan exists
[ ] Confirm starter plan version exists
[ ] Confirm feature flags exist
[ ] Confirm plan_templates.current_version_id is populated
```

## Output

```text
[ ] Supabase MVP database exists
```

---

# Phase 3 — Initial Admin Access

```text
[ ] Create first authenticated user
[ ] Insert owner role manually in user_roles
[ ] Confirm owner role status is active
[ ] Test public.is_admin()
[ ] Confirm normal user is not admin
[ ] Confirm admin can read admin-managed tables
[ ] Confirm normal user cannot update admin-managed tables
```

## Initial owner role example

```text
Insert authenticated user ID into user_roles with role = owner.
```

## Output

```text
[ ] Initial admin access works
```

---

# Phase 4 — RLS Security Tests

Reference:

```text
PRODUCTS/WELLBINE/SUPABASE_SQL_MVP.md
PRODUCTS/WELLBINE/QA_PLAN.md
```

## User-owned data

```text
[ ] User can read own profile
[ ] User can update own profile
[ ] User cannot read another user's profile
[ ] User can read own settings
[ ] User can update own settings
[ ] User cannot read another user's settings
[ ] User can read own active plans
[ ] User can read own daily plans
[ ] User can read own daily actions
[ ] User can read own pillar states
[ ] User can read own home state
```

## Admin-managed data

```text
[ ] User can read published plans
[ ] User cannot read draft plans
[ ] User cannot update plan templates
[ ] User cannot update plan versions
[ ] User can read active pillar definitions
[ ] User cannot update pillar definitions
[ ] Admin can create plan template
[ ] Admin can update plan template
[ ] Admin can read audit log
```

## Output

```text
[ ] RLS protects MVP data correctly
```

---

# Phase 5 — FlutterFlow Project Setup

Reference:

```text
PRODUCTS/WELLBINE/FLUTTERFLOW_BUILD_GUIDE.md
PRODUCTS/WELLBINE/SCREEN_MAP.md
PRODUCTS/WELLBINE/FLUTTERFLOW_ACTIONS.md
```

## Project setup

```text
[ ] Create FlutterFlow project
[ ] Define app name
[ ] Define package name / bundle ID draft
[ ] Connect FlutterFlow to Supabase
[ ] Add Supabase URL
[ ] Add Supabase anon key
[ ] Refresh Supabase schema
[ ] Confirm tables appear in FlutterFlow
[ ] Configure authentication
[ ] Create app theme
[ ] Create typography system
[ ] Create button styles
[ ] Create card styles
[ ] Create loading component
[ ] Create empty state component
[ ] Create error state component
```

## GitHub connection

```text
[ ] Connect FlutterFlow to GitHub
[ ] Configure FlutterFlow GitHub app
[ ] Push FlutterFlow code to GitHub
[ ] Confirm FlutterFlow branch is created
[ ] Do not manually edit FlutterFlow branch directly
[ ] Create separate branch for custom code if needed
```

## Output

```text
[ ] FlutterFlow project is connected to Supabase and GitHub
```

---

# Phase 6 — FlutterFlow App Routing

Reference:

```text
PRODUCTS/WELLBINE/SCREEN_MAP.md
```

## Routing logic

```text
[ ] Create Splash / Loading screen
[ ] Check auth session on app start
[ ] If unauthenticated, route to Auth
[ ] If authenticated and onboarding incomplete, route to Onboarding
[ ] If authenticated and onboarding complete but no active plan, route to Plan Selection
[ ] If authenticated and active plan exists, route to Home
[ ] Add fallback error state
```

## Screens

```text
[ ] Splash / Loading
[ ] Auth
[ ] Welcome
[ ] Profile Baseline
[ ] Onboarding
[ ] Plan Selection
[ ] Plan Activation Loading
[ ] Home
[ ] Daily
[ ] Pillar Detail
[ ] Settings / Personal Center
[ ] Privacy Policy
[ ] Terms of Use
[ ] Account
[ ] Delete Account
[ ] Error State
```

## Output

```text
[ ] App routes user to correct state
```

---

# Phase 7 — Auth MVP

Reference:

```text
PRODUCTS/WELLBINE/FLUTTERFLOW_ACTIONS.md
```

## Auth screens

```text
[ ] Build Sign Up form
[ ] Build Login form
[ ] Build Password Reset form
[ ] Add Privacy Policy link
[ ] Add Terms of Use link
[ ] Add loading states
[ ] Add readable error states
```

## Auth actions

```text
[ ] Sign Up action
[ ] Login action
[ ] Logout action
[ ] Password Reset action
[ ] Duplicate tap protection
[ ] Auth failure handling
```

## Output

```text
[ ] User can sign up, log in, log out and reset password
```

---

# Phase 8 — Profile Baseline

Reference:

```text
PRODUCTS/WELLBINE/ONBOARDING.md
PRODUCTS/WELLBINE/FLUTTERFLOW_ACTIONS.md
```

## Profile fields

```text
[ ] Name
[ ] Biological sex
[ ] Age
[ ] Height
[ ] Weight
[ ] Country / region if needed
[ ] Language
[ ] Timezone
[ ] Relevant comorbidities optional
```

## Rules

```text
[ ] Biological sex includes Prefer not to say
[ ] Comorbidities are optional
[ ] Optional fields do not block onboarding
[ ] Profile saves to user_profiles
[ ] Settings save to user_settings
```

## Output

```text
[ ] User profile baseline is saved
```

---

# Phase 9 — Onboarding MVP

Reference:

```text
PRODUCTS/WELLBINE/ONBOARDING.md
PRODUCTS/WELLBINE/SCREEN_MAP.md
```

## Onboarding screens

```text
[ ] Welcome
[ ] Profile Baseline
[ ] Wearable Optional Step
[ ] Mental Detox / Push Explanation
[ ] Goals
[ ] Plan Selection
[ ] Pillar Preferences
[ ] Upload Optional Step
[ ] Activate Plan
```

## Onboarding rules

```text
[ ] Wearable is optional
[ ] Push is optional
[ ] Upload is optional
[ ] User can continue without wearable
[ ] User can continue without Push
[ ] User can continue without upload
[ ] Onboarding does not feel like a medical exam
```

## Output

```text
[ ] User can complete onboarding without optional features
```

---

# Phase 10 — Plan Templates MVP

Reference:

```text
PRODUCTS/WELLBINE/PLAN_TEMPLATES.md
PRODUCTS/WELLBINE/SUPABASE_SQL_MVP.md
```

## Supabase

```text
[ ] Confirm starter plan exists
[ ] Confirm starter plan status is published
[ ] Confirm starter plan version exists
[ ] Confirm version status is published
[ ] Confirm current_version_id is set
```

## FlutterFlow

```text
[ ] Build Plan Selection screen
[ ] Query published plan_templates
[ ] Display Plan Cards
[ ] Hide draft plans
[ ] Hide archived plans
[ ] Select plan action
[ ] Store selected plan in local state
```

## Output

```text
[ ] User can select a published plan
```

---

# Phase 11 — Edge Function: activate_plan

Reference:

```text
PRODUCTS/WELLBINE/EDGE_FUNCTIONS.md
PRODUCTS/WELLBINE/EDGE_FUNCTION_PAYLOADS.md
```

## Function build

```text
[ ] Create supabase/functions/activate_plan
[ ] Validate authenticated user
[ ] Validate plan_template_id or plan_slug
[ ] Validate plan is published
[ ] Validate plan version is published
[ ] Prevent duplicate active plan if needed
[ ] Create user_active_plans
[ ] Create user_pillar_states
[ ] Create daily_plans
[ ] Create daily_actions
[ ] Create user_home_state
[ ] Set user_profiles.onboarding_completed = true
[ ] Return active_plan_id
[ ] Return daily_plan_id
[ ] Return home_state_id
[ ] Return next_screen = home
[ ] Handle errors cleanly
[ ] Add idempotency protection or duplicate-state check
```

## FlutterFlow connection

```text
[ ] Call activate_plan from Plan Activation Loading screen
[ ] Send selected plan data
[ ] Show loading state
[ ] On success, navigate to Home
[ ] On failure, show retry state
```

## Output

```text
[ ] User can activate plan and enter Home
```

---

# Phase 12 — Home MVP

Reference:

```text
PRODUCTS/WELLBINE/HOME.md
PRODUCTS/WELLBINE/SCREEN_MAP.md
```

## Home UI

```text
[ ] Build Home screen
[ ] Add Main Orb
[ ] Add Current Insight
[ ] Add Next Best Action
[ ] Add Pillar Orbs
[ ] Add Daily access
[ ] Add Personal Center access
[ ] Add loading state
[ ] Add empty state
[ ] Add error state
```

## Home data

```text
[ ] Query user_home_state
[ ] Query user_active_plans
[ ] Query user_pillar_states
[ ] Query current daily_plan
[ ] Query daily_actions
[ ] Query feature_flags
```

## Home rules

```text
[ ] Home is not blank
[ ] Home is not Store-first
[ ] Home does not depend on wearable
[ ] Home does not depend on Push
[ ] Home shows what matters now
```

## Output

```text
[ ] User opens Home and understands next action
```

---

# Phase 13 — Daily MVP

Reference:

```text
PRODUCTS/WELLBINE/DAILY.md
PRODUCTS/WELLBINE/FLUTTERFLOW_ACTIONS.md
```

## Daily UI

```text
[ ] Build Daily screen
[ ] Show current action
[ ] Show upcoming actions
[ ] Show completed actions
[ ] Show delayed actions
[ ] Show recoverable actions
[ ] Add Daily Action Detail
[ ] Add Confirm button
[ ] Add Adjust button
[ ] Add Later button
```

## Daily data

```text
[ ] Query today's daily_plan
[ ] Query daily_actions for daily_plan_id
[ ] Group actions by status
[ ] Open selected action detail
```

## Output

```text
[ ] User can see and interact with Daily actions
```

---

# Phase 14 — Edge Function: process_daily_action

Reference:

```text
PRODUCTS/WELLBINE/EDGE_FUNCTIONS.md
PRODUCTS/WELLBINE/EDGE_FUNCTION_PAYLOADS.md
```

## Function build

```text
[ ] Create supabase/functions/process_daily_action
[ ] Validate authenticated user
[ ] Validate user owns daily_action_id
[ ] Validate response = confirm / adjust / later / skip
[ ] For confirm, mark action completed
[ ] For adjust, store adjustment payload
[ ] For later, set delayed_until
[ ] For skip, mark action skipped
[ ] Update related user_pillar_states
[ ] Update or trigger update_home_state
[ ] Return new action status
[ ] Return home_updated
[ ] Return next_best_action
[ ] Handle duplicate taps
[ ] Handle already completed actions
```

## FlutterFlow connection

```text
[ ] Connect Confirm button
[ ] Connect Adjust save action
[ ] Connect Later button
[ ] Refresh Daily after success
[ ] Refresh Home after success
[ ] Show clear success state
[ ] Show clear error state
```

## Output

```text
[ ] Daily action updates Daily, Pillars and Home
```

---

# Phase 15 — Edge Function: update_home_state

Reference:

```text
PRODUCTS/WELLBINE/HOME.md
PRODUCTS/WELLBINE/EDGE_FUNCTION_PAYLOADS.md
```

## Function build

```text
[ ] Create supabase/functions/update_home_state
[ ] Validate authenticated user
[ ] Read active plan
[ ] Read pillar states
[ ] Read today's daily plan
[ ] Read daily actions
[ ] Generate current_insight
[ ] Generate next_best_action
[ ] Generate adaptive_summary_json
[ ] Generate pillar_orbs_json
[ ] Save user_home_state
[ ] Return updated home state
[ ] Ensure fallback state exists
```

## FlutterFlow connection

```text
[ ] Call update_home_state on Home refresh if needed
[ ] Call after Daily action update if needed
[ ] Re-query user_home_state
[ ] Update Home UI
```

## Output

```text
[ ] Home adapts after user action
```

---

# Phase 16 — Pillars MVP

Reference:

```text
PRODUCTS/WELLBINE/PILLARS.md
PRODUCTS/WELLBINE/SCREEN_MAP.md
```

## Pillar UI

```text
[ ] Build Pillar Quick Panel
[ ] Build Pillar Detail screen
[ ] Show pillar status
[ ] Show related Daily action
[ ] Show simple guidance
[ ] Show adjust option
```

## Initial pillars

```text
[ ] Mind
[ ] Sun
[ ] Hydration
[ ] Sleep
[ ] Nutrition
[ ] Movement
[ ] Daily Stack
```

## Pillar rules

```text
[ ] Pillars reflect state
[ ] Pillars do not become complex dashboards
[ ] Pillar updates reflect in Home
[ ] Nutrition respects fasting context later
[ ] Movement respects recovery context later
```

## Output

```text
[ ] Pillars operate as simple state modules
```

---

# Phase 17 — Settings / Personal Center MVP

Reference:

```text
PRODUCTS/WELLBINE/SCREEN_MAP.md
PRODUCTS/WELLBINE/APP_RELEASE_CHECKLIST.md
```

## Settings UI

```text
[ ] Build Personal Center
[ ] Build Profile Settings
[ ] Build Push Preferences placeholder
[ ] Build Mental Detox Settings
[ ] Build Plan Settings
[ ] Build Privacy Policy screen/link
[ ] Build Terms of Use screen/link
[ ] Build Account screen
[ ] Build Delete Account screen
[ ] Build Logout action
```

## Rules

```text
[ ] Settings are accessible from Home
[ ] Privacy is accessible
[ ] Terms are accessible
[ ] Account deletion is accessible
[ ] Push is optional
[ ] Wearables are optional
[ ] Uploads are optional
```

## Output

```text
[ ] User has account and privacy control
```

---

# Phase 18 — Edge Function: delete_account

Reference:

```text
PRODUCTS/WELLBINE/EDGE_FUNCTIONS.md
PRODUCTS/WELLBINE/EDGE_FUNCTION_PAYLOADS.md
PRODUCTS/WELLBINE/PRIVACY_POLICY_DRAFT.md
```

## Function build

```text
[ ] Create supabase/functions/delete_account
[ ] Validate authenticated user
[ ] Require confirmation
[ ] Define deletion strategy
[ ] Delete or anonymize user profile
[ ] Delete or anonymize user settings
[ ] Handle active plans
[ ] Handle daily plans
[ ] Handle daily actions
[ ] Handle pillar states
[ ] Handle home state
[ ] Handle stack items if implemented
[ ] Handle uploads if implemented
[ ] Handle commerce records if implemented
[ ] Match Privacy Policy language
[ ] Return logout_required = true
```

## FlutterFlow connection

```text
[ ] Build delete account confirmation
[ ] Call delete_account
[ ] Show result
[ ] Log user out
[ ] Navigate to Auth or Goodbye screen
```

## Output

```text
[ ] Account deletion flow works
```

---

# Phase 19 — Basic Admin MVP

Reference:

```text
PRODUCTS/WELLBINE/ADMIN.md
PRODUCTS/WELLBINE/ADMIN_BUILD_GUIDE.md
```

## Admin platform decision

```text
[ ] Decide first Admin platform
[ ] Supabase Studio for earliest MVP
[ ] Lovable for internal Admin web
[ ] Retool or Softr if preferred
```

## Minimum Admin controls

```text
[ ] Plan Templates
[ ] Plan Template Versions
[ ] Pillar Definitions
[ ] Content Modules
[ ] Feature Flags
[ ] Commerce Benefits hidden/visible
[ ] Publishing status
[ ] Admin Audit Log
```

## Lovable Admin direction

```text
[ ] Create Lovable Admin project if using Lovable
[ ] Connect Lovable Admin to Supabase
[ ] Build Plan Templates screen
[ ] Build Plan Versions screen
[ ] Build Feature Flags screen
[ ] Build Content Modules screen
[ ] Build Commerce Benefits screen
[ ] Build Release Review screen
[ ] Push Lovable code to GitHub if used
```

## Output

```text
[ ] Internal team can control core configuration
```

---

# Phase 20 — Feature Flags MVP

Reference:

```text
PRODUCTS/WELLBINE/FEATURE_FLAGS.md
```

## Flags

```text
[ ] onboarding_enabled
[ ] home_enabled
[ ] daily_enabled
[ ] pillars_enabled
[ ] daily_stack_enabled
[ ] push_enabled
[ ] wearables_enabled
[ ] uploads_enabled
[ ] commerce_bridge_enabled
[ ] ask_wellbine_enabled
[ ] subscriptions_enabled
[ ] recommendations_enabled
[ ] app_review_mode
[ ] beta_mode
```

## FlutterFlow usage

```text
[ ] Load feature_flags on app start or Home
[ ] Use flags for conditional visibility
[ ] Hide Wearables if disabled
[ ] Hide Uploads if disabled
[ ] Hide Commerce Bridge if disabled
[ ] Hide Ask Wellbine if disabled
[ ] Hide unfinished features before app review
```

## Backend usage

```text
[ ] Edge Functions check sensitive flags where needed
[ ] Commerce function checks commerce_bridge_enabled
[ ] Upload function checks uploads_enabled
[ ] Push function checks push_enabled
```

## Output

```text
[ ] Feature visibility can be controlled without app redeployment
```

---

# Phase 21 — Daily Stack MVP

Reference:

```text
PRODUCTS/WELLBINE/STACK.md
PRODUCTS/WELLBINE/FLUTTERFLOW_ACTIONS.md
```

## Stack UI

```text
[ ] Build Daily Stack screen
[ ] Build Add Stack Item
[ ] Build Edit Stack Item
[ ] Build Stack Item Detail
[ ] Build Mark Taken action
[ ] Build Skip action
[ ] Build Delete action
```

## Stack data

```text
[ ] Use stack_items table
[ ] Add item
[ ] Edit item
[ ] Delete or deactivate item
[ ] Refresh stack list
```

## Boundary

```text
[ ] Add safety language
[ ] Daily Stack organizes routines
[ ] Daily Stack does not prescribe medication
```

## Output

```text
[ ] User can manage routine items safely
```

---

# Phase 22 — Push MVP

Reference:

```text
PRODUCTS/WELLBINE/PUSH.md
PRODUCTS/WELLBINE/EDGE_FUNCTION_PAYLOADS.md
```

## Push setup

```text
[ ] Choose Push provider / implementation path
[ ] Configure Push permission request
[ ] Explain Push before asking permission
[ ] Build Push Preferences
[ ] Store push_enabled in user_settings
[ ] Store push events in push_events
```

## process_push_response

```text
[ ] Create supabase/functions/process_push_response
[ ] Validate user owns Push event
[ ] Validate Push is enabled
[ ] Process confirm
[ ] Process adjust
[ ] Process later
[ ] Update Daily if linked
[ ] Update Home if needed
[ ] Return deep link
```

## FlutterFlow

```text
[ ] Enable Push permission flow
[ ] Handle Push deep links
[ ] Route Push to Daily Action Detail
[ ] Route Push to Pillar Detail if needed
[ ] Avoid generic Home-only Push
```

## Output

```text
[ ] Push improves execution without being required
```

---

# Phase 23 — Wearables Placeholder

Reference:

```text
PRODUCTS/WELLBINE/WEARABLES.md
PRODUCTS/WELLBINE/FEATURE_FLAGS.md
```

## Placeholder MVP

```text
[ ] Build Wearable Manager screen
[ ] Show optional connection copy
[ ] Show manual fallback
[ ] Show coming soon providers only if appropriate
[ ] Hide providers not implemented
[ ] Respect wearables_enabled flag
```

## Future integration

```text
[ ] wearable_connections table
[ ] wearable_metric_snapshots table
[ ] sync_wearable_snapshot function
```

## Output

```text
[ ] Wearables are positioned correctly but do not block MVP
```

---

# Phase 24 — Uploads Placeholder

Reference:

```text
PRODUCTS/WELLBINE/FEATURE_FLAGS.md
PRODUCTS/WELLBINE/EDGE_FUNCTION_PAYLOADS.md
```

## Placeholder MVP

```text
[ ] Build Upload Manager screen if enabled
[ ] Explain uploads are optional
[ ] Hide upload feature if disabled
[ ] Create private user_uploads bucket before enabling
[ ] Define allowed file types before enabling
[ ] Add Delete Upload flow before enabling
```

## Future integration

```text
[ ] user_uploads table
[ ] process_user_upload function
[ ] Upload summary display
```

## Output

```text
[ ] Uploads enrich context later without blocking MVP
```

---

# Phase 25 — Commerce Bridge MVP

Reference:

```text
PRODUCTS/WELLBINE/COMMERCE_BRIDGE.md
PRODUCTS/WELLBINE/FEATURE_FLAGS.md
```

## Commerce setup

```text
[ ] Keep Commerce Bridge hidden by default
[ ] Create commerce_benefits table later if not yet created
[ ] Create user_commerce_benefits table later
[ ] Create commerce_events table later
[ ] Build Commerce Benefit Detail only when enabled
[ ] Use one primary button
[ ] Copy benefit code
[ ] Open external destination
[ ] Track event
```

## Rules

```text
[ ] Do not hardcode discount amount
[ ] Do not hardcode commerce platform
[ ] Do not create fixed Store tab
[ ] Commerce must be hideable
[ ] Commerce should not weaken trust
```

## Output

```text
[ ] Commerce Bridge is ready as controlled subscriber benefit layer
```

---

# Phase 26 — Ask Wellbine MVP

Reference:

```text
PRODUCTS/WELLBINE/EDGE_FUNCTION_PAYLOADS.md
PRODUCTS/WELLBINE/FEATURE_FLAGS.md
```

## Ask Wellbine scope

```text
[ ] Keep Ask Wellbine hidden or limited in first MVP
[ ] Define safe use cases
[ ] Explain Daily actions
[ ] Explain Plan
[ ] Explain Pillars
[ ] Help user adjust routine
[ ] Avoid diagnosis
[ ] Avoid treatment claims
[ ] Avoid emergency guidance
```

## Backend direction

```text
[ ] Prefer Supabase Edge Function for core AAI behavior
[ ] Do not place AAI core only inside FlutterFlow AI Agent
[ ] Use feature flag ask_wellbine_enabled
```

## Output

```text
[ ] Ask Wellbine has safe limited scope
```

---

# Phase 27 — Privacy, Terms And Legal Readiness

Reference:

```text
PRODUCTS/WELLBINE/PRIVACY_POLICY_DRAFT.md
PRODUCTS/WELLBINE/TERMS_DRAFT.md
PRODUCTS/WELLBINE/APP_RELEASE_CHECKLIST.md
```

## Privacy

```text
[ ] Finalize Privacy Policy draft
[ ] Confirm data collected
[ ] Confirm wearable language
[ ] Confirm upload language
[ ] Confirm Push language
[ ] Confirm AI guidance language
[ ] Confirm Commerce Bridge language
[ ] Confirm account deletion language
[ ] Publish Privacy Policy URL
[ ] Add link in Auth
[ ] Add link in Settings
```

## Terms

```text
[ ] Finalize Terms draft
[ ] Confirm product boundary
[ ] Confirm no medical advice language
[ ] Confirm AI guidance limitation
[ ] Confirm subscription language if used
[ ] Confirm Commerce Bridge external purchase language
[ ] Publish Terms URL
[ ] Add link in Auth
[ ] Add link in Settings
```

## Output

```text
[ ] Privacy and Terms are visible and consistent with product behavior
```

---

# Phase 28 — App Release Preparation

Reference:

```text
PRODUCTS/WELLBINE/APP_RELEASE.md
PRODUCTS/WELLBINE/APP_RELEASE_CHECKLIST.md
```

## iOS / Android basics

```text
[ ] Define app name
[ ] Define app icon
[ ] Define bundle ID
[ ] Define package name
[ ] Prepare screenshots
[ ] Prepare app description
[ ] Prepare keywords
[ ] Prepare support URL
[ ] Prepare marketing URL if needed
[ ] Prepare Privacy Policy URL
[ ] Prepare Terms URL
[ ] Prepare test account
[ ] Prepare review notes
```

## Release-sensitive items

```text
[ ] Account deletion works
[ ] Privacy link works
[ ] Terms link works
[ ] Push optional
[ ] Wearables optional
[ ] Uploads optional
[ ] Commerce hidden or working
[ ] No unsafe health claims
[ ] No unsupported provider claims
[ ] No broken screens visible
[ ] Feature Flags hide unfinished features
```

## Output

```text
[ ] App is ready for internal review preparation
```

---

# Phase 29 — QA Core Loop

Reference:

```text
PRODUCTS/WELLBINE/QA_PLAN.md
```

## Core user flow

```text
[ ] User can sign up
[ ] User can log in
[ ] User can complete profile baseline
[ ] User can complete onboarding
[ ] User can select plan
[ ] User can activate plan
[ ] User reaches Home
[ ] Home shows current insight
[ ] Home shows next best action
[ ] User opens Daily
[ ] User confirms action
[ ] Daily updates
[ ] Pillar updates
[ ] Home updates
[ ] User opens Settings
[ ] User opens Privacy
[ ] User opens Terms
[ ] User deletes account
```

## Failure tests

```text
[ ] Failed login shows error
[ ] Failed plan activation shows retry
[ ] Missing Home state creates fallback
[ ] Failed Daily action update shows retry
[ ] Offline state does not trap user
[ ] Duplicate taps do not duplicate records
[ ] Feature disabled means screen hidden
[ ] Normal user cannot access admin data
```

## Output

```text
[ ] Core MVP passes QA
```

---

# Phase 30 — Internal MVP Acceptance

Internal MVP is acceptable when:

```text
[ ] Supabase database exists
[ ] RLS passes basic tests
[ ] FlutterFlow app connects to Supabase
[ ] User can sign up
[ ] User can complete onboarding
[ ] User can activate plan
[ ] User can reach Home
[ ] User can open Daily
[ ] User can confirm Daily action
[ ] Home updates after action
[ ] Pillars reflect state
[ ] Settings works
[ ] Privacy and Terms are accessible
[ ] Account deletion works
[ ] No critical blank screen
[ ] No optional feature blocks the user
[ ] No unsafe health claim is visible
```

---

# Phase 31 — Beta MVP Acceptance

Beta MVP is acceptable when:

```text
[ ] Internal MVP passes
[ ] Push is optional and stable if enabled
[ ] Daily Stack works if visible
[ ] Basic Admin can control published plans
[ ] Feature Flags hide unfinished features
[ ] App has no unsafe medical claims
[ ] Privacy Policy is live
[ ] Terms are live
[ ] Test accounts work
[ ] Core analytics are available or manually traceable
[ ] App Release Checklist mostly passes
```

---

# Phase 32 — Controlled Launch Acceptance

Controlled launch is acceptable when:

```text
[ ] Beta MVP passes
[ ] App Store requirements are ready
[ ] Google Play requirements are ready
[ ] Account deletion works
[ ] RLS is validated
[ ] Core flows are stable
[ ] No critical crashes
[ ] Commerce Bridge is hidden or working
[ ] Wearables are optional
[ ] Uploads are optional
[ ] Push is optional
[ ] Support process exists
[ ] Admin can disable risky features
```

---

# Critical Path Summary

The real MVP critical path is:

```text
[ ] Supabase project
[ ] SQL MVP
[ ] RLS tests
[ ] FlutterFlow project
[ ] Supabase connection
[ ] Auth
[ ] Profile Baseline
[ ] Onboarding
[ ] Plan Selection
[ ] activate_plan
[ ] Home
[ ] Daily
[ ] process_daily_action
[ ] update_home_state
[ ] Pillars
[ ] Settings
[ ] delete_account
[ ] QA Core Loop
```

Nothing is more important than this path.

---

# Deferred Until Core Loop Works

Do not prioritize these before core loop works:

```text
[-] Advanced AI automation
[-] Full wearable integrations
[-] Full upload interpretation
[-] Full commerce system
[-] Advanced analytics dashboard
[-] Complex subscription logic
[-] Plan marketplace
[-] Community features
[-] Gamification system
[-] Advanced recommendation engine
[-] A/B testing
[-] Partner dashboard
```

---

# Current Status

MVP Task Board is currently a draft.

Next steps:

```text
[ ] Confirm implementation repository structure
[ ] Create Supabase development project
[ ] Run Supabase SQL MVP
[ ] Create first admin user role
[ ] Test RLS
[ ] Create FlutterFlow project
[ ] Connect FlutterFlow to Supabase
[ ] Build Auth
[ ] Build Profile Baseline
[ ] Build Onboarding
[ ] Build Plan Selection
[ ] Build activate_plan
[ ] Build Home
[ ] Build Daily
[ ] Build process_daily_action
[ ] Build update_home_state
[ ] Build delete_account
[ ] Run QA Core Loop
```

---

# Related Documents

- FOUNDATION/AAI_CONSTITUTION.md
- FOUNDATION/AAI_GLOSSARY.md
- FOUNDATION/AAI_PRINCIPLES.md
- FRAMEWORKS/POPAE.md
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
- PRODUCTS/WELLBINE/SUPABASE_SQL_MVP.md
- PRODUCTS/WELLBINE/EDGE_FUNCTIONS.md
- PRODUCTS/WELLBINE/EDGE_FUNCTION_PAYLOADS.md
- PRODUCTS/WELLBINE/FLUTTERFLOW_BUILD_GUIDE.md
- PRODUCTS/WELLBINE/FLUTTERFLOW_ACTIONS.md
- PRODUCTS/WELLBINE/SCREEN_MAP.md
- PRODUCTS/WELLBINE/FEATURE_FLAGS.md
- PRODUCTS/WELLBINE/ADMIN_BUILD_GUIDE.md
- PRODUCTS/WELLBINE/MVP_BUILD_SEQUENCE.md
- PRODUCTS/WELLBINE/QA_PLAN.md
- PRODUCTS/WELLBINE/PRIVACY_POLICY_DRAFT.md
- PRODUCTS/WELLBINE/TERMS_DRAFT.md
- PRODUCTS/WELLBINE/APP_RELEASE_CHECKLIST.md
