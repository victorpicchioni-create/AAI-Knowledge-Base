# Wellbine FlutterFlow Build Guide

**Version:** 0.1.0

**Status:** Draft

**Last Updated:** July 2026

---

# Purpose

This document defines the practical FlutterFlow build guide for Wellbine.

The goal is to translate the Wellbine product architecture into screens, components, actions, backend connections and user flows that can be built in FlutterFlow.

This document connects:

- Product architecture
- Onboarding
- Home
- Daily
- Push
- Pillars
- Daily Stack
- Wearables
- Uploads
- Commerce Bridge
- Supabase
- Edge Functions
- App Release
- QA

FlutterFlow is the app interface and execution layer.

Supabase remains the source of truth.

---

# Official Definition

**Wellbine FlutterFlow Build Guide is the practical implementation guide for building the Wellbine mobile app interface, user flows, screen logic, Supabase connections and adaptive user experience in FlutterFlow.**

---

# Core Principle

The core FlutterFlow rule is:

```text
FlutterFlow is the product interface layer, not the source of truth.
```

FlutterFlow should:

- Display data from Supabase
- Capture user input
- Trigger user actions
- Call Edge Functions when logic is sensitive
- Navigate users through the experience
- Handle loading, empty and error states
- Support app release builds

FlutterFlow should not:

- Hardcode business rules unnecessarily
- Become the main database
- Store sensitive logic in frontend-only actions
- Define permanent plan logic inside screens
- Replace Supabase
- Replace Admin
- Replace AAI logic
- Expose service role keys
- Handle private backend logic insecurely

---

# Product Build Philosophy

Wellbine should be built as an adaptive operating system, not as a collection of disconnected app screens.

The app should feel like:

```text
Open app
↓
Understand current state
↓
See what matters now
↓
Act quickly
↓
System adapts
```

Not like:

```text
Open app
↓
Search menus
↓
Interpret dashboards
↓
Manually manage everything
↓
Feel behind
```

The build should prioritize:

- Fast activation
- Simple decisions
- One central Home
- Push-assisted execution
- Contextual actions
- Recovery-aware language
- Minimal friction
- Clear fallbacks
- Privacy trust

---

# FlutterFlow Role In The System

FlutterFlow should handle:

- Mobile app screens
- User interface
- Navigation
- Forms
- Buttons
- Conditional visibility
- Supabase queries
- Supabase inserts and updates
- Edge Function calls
- Push permission interface
- File upload interface
- External link opening
- Clipboard copy
- Local UI state
- App build generation
- iOS and Android deployment preparation

Supabase should handle:

- Auth
- Database
- Storage
- RLS
- User-owned data
- Admin-managed configuration
- Active plan snapshots
- Daily actions
- Push events
- Commerce benefits
- Upload metadata
- Wearable connection records

Edge Functions should handle:

- Plan activation
- Daily generation
- Push response processing
- AAI context evaluation
- Home state updates
- Upload processing
- Commerce benefit issuance
- Sensitive backend logic

Admin should handle:

- Plan Templates
- Content
- Push copy
- Pillar defaults
- Commerce benefits
- Feature visibility
- Publishing status
- Operational configuration

---

# High-Level Architecture

Recommended architecture:

```text
FlutterFlow App
↓
Supabase Auth
↓
Supabase Database
↓
Supabase Storage
↓
Supabase Edge Functions
↓
AAI Context Layer
↓
Admin Configuration
```

User flow:

```text
User opens app
↓
FlutterFlow loads Supabase data
↓
FlutterFlow displays current operating state
↓
User acts
↓
FlutterFlow writes action or calls Edge Function
↓
Supabase updates
↓
AAI context may update
↓
Home / Daily / Push adapt
```

---

# Build Order

Recommended FlutterFlow build order:

```text
1. App shell
2. Design system
3. Supabase Auth
4. Profile baseline
5. Onboarding flow
6. Plan selection
7. Plan activation call
8. Home
9. Daily
10. Pillars
11. Daily Stack
12. Settings / Personal Center
13. Push permission flow
14. Push deep-link handling
15. Wearables placeholder / optional connection
16. Uploads
17. Commerce Bridge
18. Error / empty / loading states
19. QA build
20. App release build
```

Do not start with complex AI features before the core app loop works.

The core loop is:

```text
Onboarding
↓
Plan Activation
↓
Home
↓
Daily
↓
Action
↓
State Update
```

---

# MVP Screens Overview

Recommended MVP screens:

```text
Splash / Loading
Auth
Welcome
Profile Baseline
Wearable Optional Step
Mental Detox / Push Explanation
Goals
Plan Selection
Pillar Preferences
Upload Optional Step
Plan Activation Loading
Home
Adaptive Summary
Daily
Pillar Detail
Daily Stack
Settings / Personal Center
Privacy / Terms
Account
Delete Account
Commerce Benefit Detail
Upload Manager
Wearable Manager
Ask Wellbine
Error / Offline
```

Not all screens need to be complex in MVP.

Some screens can be simple but functional.

---

# Navigation Principle

Wellbine should not depend on a fixed Bottom Navigation as the core experience.

The primary app structure should be:

```text
Home
↓
Contextual panels
↓
Daily
↓
Pillar details
↓
Settings / Personal Center
```

Home is the central operating surface.

Daily is the deeper execution layer.

Pillars are accessible through Home.

Settings are accessible through profile/avatar.

Commerce is contextual.

Store is not a fixed primary tab in the MVP.

---

# App Shell

The app shell should include:

- Splash or loading screen
- Auth state check
- Onboarding completion check
- Active plan check
- Home routing
- Safe fallback routing

Routing logic:

```text
If user is not authenticated:
    show Auth

If user is authenticated but onboarding is incomplete:
    show Onboarding

If user is authenticated and onboarding is complete but no active plan:
    show Plan Selection / First Activation

If user is authenticated and active plan exists:
    show Home
```

---

# Design System

FlutterFlow should use a consistent design system.

Core design elements:

- Dark mode-ready interface
- Clean typography
- High contrast
- Rounded cards
- Central Orb
- Pillar Orbs
- Simple action buttons
- Calm health language
- Minimal clutter
- Strong hierarchy
- Clear loading states
- Clear empty states
- Clear error states

Important rule:

```text
The user should know what to do next within seconds.
```

---

# Core Components

Create reusable components where practical:

```text
MainOrbComponent
PillarOrbComponent
CurrentInsightCard
NextBestActionCard
DailyActionCard
ConfirmAdjustLaterControls
PillarQuickPanel
AdaptiveSummaryCard
PlanCard
OnboardingStepWrapper
SettingsRow
CommerceBenefitCard
StackItemCard
WearableStatusCard
UploadCard
LoadingState
EmptyState
ErrorState
```

Reusable components reduce inconsistency.

---

# State Management Direction

FlutterFlow should use app state carefully.

Use local or app state for:

- Temporary UI selections
- Current onboarding step
- Temporary form inputs
- Current tab/panel state
- Loading flags
- Short-lived UI state
- Recently selected options before save

Use Supabase for:

- User profile
- User settings
- Active plan
- Daily plan
- Daily actions
- Pillar states
- Push events
- Stack items
- Wearable connection status
- Upload metadata
- Commerce benefits
- Home state

Important rule:

```text
If the data must survive app restart, store it in Supabase.
```

---

# Supabase Connection

FlutterFlow should connect to Supabase for:

- Authentication
- User queries
- User inserts
- User updates
- Plan reads
- Daily reads
- Pillar reads
- Settings reads
- Storage uploads
- Edge Function calls

Important security rule:

```text
FlutterFlow must never expose Supabase service role keys.
```

The frontend should use authenticated user access with RLS.

Sensitive logic should go through Edge Functions.

---

# Auth Build

Auth should support:

- Sign up
- Login
- Logout
- Auth state persistence
- Password reset if applicable
- Auth error handling

After successful auth:

```text
Check onboarding_completed
Check active plan
Route user accordingly
```

Do not send every user directly to Home without checking state.

---

# Onboarding Build

Onboarding should be built as a guided activation flow.

Recommended flow:

```text
Welcome
↓
Name
↓
Biological Sex
↓
Age
↓
Height
↓
Weight
↓
Relevant Comorbidities
↓
Wearable Optional Step
↓
Mental Detox / Push Explanation
↓
Push Permission Optional
↓
Goals
↓
Plan Model
↓
Pillar Preferences
↓
Upload Optional Step
↓
Activate 7-Day Sync Plan
↓
Home
```

Onboarding should save progressively where practical.

Do not lose everything if the user exits.

---

# Profile Baseline Build

Profile baseline fields may include:

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

- Comorbidities optional
- Biological sex should include Prefer not to say
- Do not make onboarding feel like a medical exam
- Do not ask unnecessary questions early
- Keep the user moving toward activation

---

# Wearable Optional Step

Wearable connection should be optional.

Screen purpose:

```text
Connect a wearable if available, or continue without one.
```

User options:

```text
Connect Wearable
Continue Without Wearable
```

Important copy:

```text
Wellbine works without a wearable. Connecting one can improve personalization.
```

Do not block onboarding because of wearable setup.

---

# Mental Detox / Push Explanation

Before requesting Push permission, explain why Push matters.

Screen purpose:

```text
Explain that Wellbine uses notifications for adaptive guidance, not noise.
```

Possible user-facing direction:

```text
Wellbine can guide your day with simple check-ins. You can reduce or pause notifications anytime.
```

User options:

```text
Enable Guidance
Not Now
```

Push should be optional.

---

# Goals Build

Goals should be simple.

Possible goal categories:

```text
Energy
Sleep
Weight
Focus
Stress
Longevity
Routine
Metabolic Health
Performance
Recovery
```

Do not lock the product into fixed goal categories forever.

Goals should be admin-configurable later.

---

# Plan Selection Build

Plan Selection should display published Plan Templates.

Plan cards may show:

```text
Plan name
Short description
Audience
Duration
Main focus
Recommended badge if applicable
```

Plan Selection should not show:

```text
draft plans
archived plans
broken plans
internal test plans
```

When the user selects a plan, FlutterFlow should call:

```text
activate_plan
```

Prefer Edge Function for activation rather than frontend-only inserts.

---

# Plan Activation Build

Plan activation should show a loading state.

Possible loading copy:

```text
Preparing your first Wellbine plan.
```

Activation should:

- Create user active plan
- Create pillar states
- Create daily plan
- Initialize Home state
- Route user to Home

If activation fails:

```text
Show clear retry state
Do not leave user stuck
Do not create duplicate active plans
```

---

# Home Build

Home is the central operating surface.

Home should load:

```text
user_home_state
user_active_plans
user_pillar_states
daily_plans
daily_actions
recommendations
commerce_benefits if visible and relevant
wearable context if available
```

Home should show:

- Main Orb
- Current Insight
- Next Best Action
- Pillar Orbs
- Adaptive Summary access
- Daily access
- Ask Wellbine access
- Personal Center access
- Contextual cards

Home should never feel blank.

---

# Main Orb Build

The Main Orb should represent the current adaptive state.

It may open:

```text
Adaptive Summary
```

Adaptive Summary may include:

```text
Body
Mind
Recovery
Today Sync
7-Day Sync
```

Do not overexpose fake precision.

Avoid showing overly exact scores if the system does not justify them.

---

# Pillar Orbs Build

Pillar Orbs should be static and predictable.

Initial Pillar Orbs:

```text
Mind
Sun
Hydration
Sleep
Nutrition
Movement
Daily Stack
```

Each Pillar Orb should show:

```text
status
simple visual state
quick action access
pillar detail access
```

Possible statuses:

```text
Done
Now
Upcoming
Needs Input
Recoverable
Inactive
```

Avoid language like:

```text
Failed
Lost
Bad
Punished
```

---

# Next Best Action Build

Next Best Action is one of the most important UI elements.

It should answer:

```text
What should I do now?
```

The action may come from:

- Daily plan
- Pillar state
- AAI context
- Push response
- Wearable context
- User settings
- Active plan rules

The button should be simple.

Examples of action types:

```text
Confirm
Start
Adjust
Open Daily
Open Pillar
Add Input
Review Stack
Prepare Sleep
```

---

# Daily Build

Daily is the deeper execution layer.

Daily should load:

```text
daily_plans
daily_actions
pillar states
active plan context
```

Daily should show:

- Current action
- Upcoming actions
- Completed actions
- Delayed actions
- Recoverable actions
- Daily summary

Daily action controls:

```text
Confirm
Adjust
Later
```

Daily should sync with Home.

---

# Confirm / Adjust / Later Build

The Confirm / Adjust / Later pattern is central.

Confirm:

```text
Marks action as completed or confirmed.
Updates daily_actions.
Updates pillar state.
Updates Home.
```

Adjust:

```text
Opens relevant adjustment screen or panel.
Allows the user to modify action context.
```

Later:

```text
Delays action.
Updates daily_actions.
May schedule follow-up.
```

This pattern should be reused across Daily and Push.

---

# Pillar Detail Build

Each pillar should have a detail screen or panel.

Pillar detail may include:

```text
Current status
Today’s action
Recent activity
Simple guidance
Adjust options
Related Daily actions
Related Stack items
Related recommendations
```

Pillar screens should not become overly complex in MVP.

Home should remain primary.

---

# Daily Stack Build

Daily Stack should allow users to manage routine items.

MVP features:

```text
Add item
Edit item
Delete item
Mark taken
Skip
Set timing
Set frequency
Optional refill tracking
```

Stack item types:

```text
supplement
vitamin
nutraceutical
medication
habit_item
other
```

Important boundary:

```text
Daily Stack organizes routines. It does not prescribe medication.
```

---

# Wearables Build

Wearables should be optional.

MVP may include:

```text
Wearable Manager screen
Provider list
Connection status
Manual fallback
Last sync indicator
Disconnect option
```

If real integrations are not ready, use clear status:

```text
Coming later
Manual tracking available
```

Do not pretend integrations are active before they exist.

---

# Uploads Build

Uploads should be optional.

Upload Manager may include:

```text
Upload file
View upload list
View upload status
Delete upload
View extracted summary if available
```

Uploads should use Supabase Storage.

Upload metadata should be stored in:

```text
user_uploads
```

Private user files must not be publicly accessible.

---

# Commerce Bridge Build

Commerce Bridge should be contextual.

MVP behavior:

```text
Show eligible benefit
↓
User taps one primary button
↓
Copy benefit code
↓
Open external commerce destination
↓
Track event
```

Button examples:

```text
Use Benefit
Use My Benefit
Open Benefit
```

Do not hardcode discount amounts.

Do not hardcode platform assumptions.

Do not create a fixed Store tab in MVP.

Commerce should appear in:

```text
Personal Center
Subscriber Benefits
Daily Stack
Plan Benefits
Home contextual card
Recommendations
```

only when configured.

---

# Clipboard And External Link Behavior

Commerce Bridge button should perform:

```text
Copy benefit code to clipboard
Open external URL
Track event
```

If coupon auto-apply is supported:

```text
Copy code as fallback
Open URL with benefit applied
```

If copy fails:

```text
Show code visibly
Allow manual copy
Still allow opening store
```

If link fails:

```text
Show error
Allow retry
Keep code visible
```

---

# Settings / Personal Center Build

Settings should include:

```text
Profile
Plan
Push preferences
Mental Detox
Wearables
Uploads
Daily Stack
Privacy
Terms
Subscription if visible
Subscriber Benefits if visible
Account
Delete Account
Logout
```

Settings should not become the core operating surface.

It is a support area.

---

# Account Deletion Build

Account deletion path should exist before release.

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

Before deletion, show clear warning.

Account deletion should call controlled backend logic where needed.

Deletion behavior must match Privacy Policy.

---

# Privacy And Terms Build

The app should provide visible links to:

```text
Privacy Policy
Terms of Use
```

Recommended placements:

- Signup
- Settings
- Account
- App release metadata
- Subscription screen if applicable
- Commerce Bridge if applicable

Links must work before app submission.

---

# Ask Wellbine Build

Ask Wellbine may be included as an assistant entry point.

MVP role:

```text
Help users understand their plan, daily actions, pillars and routine.
```

Ask Wellbine should not:

- Diagnose
- Treat
- Replace medical advice
- Create unsupported claims
- Override safety boundaries
- Access data without proper permission

Ask Wellbine should be grounded in Wellbine context.

---

# Loading States

Every important screen needs a loading state.

Especially:

```text
Auth check
Onboarding save
Plan activation
Home load
Daily load
Pillar load
Upload
Commerce benefit load
Wearable status
Settings
```

Loading should be calm and clear.

Avoid leaving users staring at blank screens.

---

# Empty States

Every important screen needs an empty state.

Examples:

```text
No active plan
No Daily actions yet
No Stack items yet
No uploads yet
No wearable connected
No current benefit
No recommendations
```

Empty states should give the user a next action.

---

# Error States

Every important flow needs an error state.

Examples:

```text
Could not save profile
Could not activate plan
Could not load Home
Could not update action
Could not upload file
Could not open external store
Could not copy benefit code
Could not connect wearable
```

Error copy should be human and recoverable.

Avoid:

```text
Something went wrong.
```

Better:

```text
We could not update this right now. Try again in a moment.
```

---

# Offline / Poor Connection Build

Wellbine should handle poor connection gracefully.

Minimum behavior:

```text
Show loading
Show retry
Avoid data loss
Do not duplicate actions
Do not trap user
```

For MVP, offline mode can be limited.

But poor connection states must not break the core flow.

---

# Push Deep Links

Push actions should deep-link to the correct context.

Examples:

```text
Adjust hydration → Hydration panel
Adjust sleep → Sleep panel
Adjust Daily Stack → Stack item
Open Daily → Daily screen
Open benefit → Commerce Benefit screen
```

Avoid deep-linking every push to generic Home unless Home can resolve the context clearly.

---

# Permissions Build

Permissions should be requested only when needed and after explanation.

Possible permissions:

```text
Push notifications
Health data
File upload / file picker
Camera if used
Photos if used
```

Important rule:

```text
Explain before requesting permission.
```

The app should work if permission is denied.

---

# Feature Flags / Visibility

Feature visibility should be controlled by configuration where practical.

Possible configurable features:

```text
wearables_enabled
uploads_enabled
commerce_bridge_enabled
ask_wellbine_enabled
subscriptions_enabled
daily_stack_enabled
push_enabled
```

Feature flags may come from:

```text
user_settings
admin configuration
plan template configuration
remote config table
```

Do not expose unfinished features.

---

# Admin-Managed Content

FlutterFlow should read admin-managed content from Supabase where practical.

Admin-managed content may include:

```text
Plan copy
Onboarding copy
Push copy
Pillar descriptions
Recommendation copy
Commerce benefit copy
Education modules
App messages
```

Avoid hardcoding content that may change often.

---

# Supabase Tables Used By FlutterFlow

FlutterFlow may read/write:

```text
user_profiles
user_settings
user_active_plans
pillar_definitions
user_pillar_states
daily_plans
daily_actions
push_events
stack_items
wearable_connections
wearable_metric_snapshots
user_uploads
content_modules
recommendations
commerce_benefits
user_commerce_benefits
commerce_events
user_home_state
```

Some tables should be read-only for regular users.

Admin-managed tables should not be directly writable by normal users.

---

# Edge Function Calls From FlutterFlow

FlutterFlow should call Edge Functions for important logic.

Possible calls:

```text
activate_plan
generate_daily_plan
process_push_response
update_home_state
evaluate_aai_context
process_user_upload
issue_commerce_benefit
track_commerce_event
```

Use Edge Functions when:

- Multiple tables must update together
- User eligibility must be checked
- Sensitive logic is required
- Duplicates must be prevented
- AAI context must be evaluated
- Admin rules must be enforced

---

# Security Rules

FlutterFlow build must respect:

```text
No service role key in frontend
RLS enabled
User can only access own data
Admin actions protected
Private uploads protected
Sensitive logic handled by backend
External links controlled by configuration
```

Security is not optional.

---

# App Release Considerations

FlutterFlow build should prepare for:

```text
iOS build
Android build
App icons
Splash screen
Bundle ID
Package name
Deep links
Push configuration
Permission descriptions
Privacy Policy link
Terms link
Account deletion
Test account
Review notes
Screenshots
```

Do not wait until the end to solve release requirements.

---

# QA Requirements

Every FlutterFlow build milestone should be tested against:

```text
QA_PLAN.md
APP_RELEASE_CHECKLIST.md
```

Minimum QA before internal test:

```text
Signup works
Onboarding works
Plan activation works
Home loads
Daily loads
Action update works
Settings open
Privacy and Terms links work
Account deletion path exists
No user data leakage
```

---

# MVP Completion Criteria

The FlutterFlow MVP is complete when:

```text
User can sign up
User can complete onboarding
User can activate a plan
User can reach Home
Home shows useful state
Daily shows useful actions
User can Confirm / Adjust / Later
Pillars update
Settings are accessible
Privacy and Terms are accessible
Account deletion path exists
App works without wearable
App works without uploads
App works without Push
Commerce Bridge can be hidden or shown by configuration
```

---

# What FlutterFlow Build Should Not Do

FlutterFlow build should not:

- Hardcode all business rules
- Depend on fixed Bottom Navigation
- Make Store a primary tab in MVP
- Require wearable connection
- Require uploads
- Require Push permission
- Expose service role keys
- Bypass Supabase RLS
- Store sensitive logic only in frontend
- Show draft admin content
- Leave Home blank after activation
- Use medical claim language
- Launch without account deletion path

---

# Current Status

FlutterFlow Build Guide is currently a draft.

Next steps:

- Create FlutterFlow project
- Configure Supabase connection
- Build Auth
- Build onboarding flow
- Build Plan Selection
- Connect Plan Activation
- Build Home
- Build Daily
- Build Pillars
- Build Settings
- Add Push preparation
- Add optional Wearables
- Add optional Uploads
- Add Commerce Bridge when ready
- Run QA against release checklist

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
