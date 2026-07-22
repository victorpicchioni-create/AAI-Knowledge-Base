# Wellbine Implementation Plan

**Version:** 0.1.0

**Status:** Draft

**Last Updated:** July 2026

---

# Purpose

This document defines the implementation plan for Wellbine.

The goal is to transform the Wellbine product architecture into a practical build sequence.

This implementation plan connects:

- Supabase
- FlutterFlow
- Data Model
- Authentication
- User Profile
- Onboarding
- Plan Templates
- User Active Plan Snapshots
- Home
- Daily
- Push
- Pillars
- Daily Stack
- Wearables
- Uploads
- Admin
- AAI Context
- Commerce Bridge
- App Store and Google Play release readiness
- QA and production launch

This document should guide the practical construction of Wellbine.

---

# Official Definition

**The Wellbine Implementation Plan is the staged execution roadmap for building Wellbine as an AAI-powered adaptive health alignment system using Supabase, FlutterFlow, Admin configuration and progressive product deployment.**

---

# Core Principle

The implementation should follow one rule:

```text
Build the operating system first.
Expand monetization and integrations after the core experience works.
```

The core product must come before complex extensions.

The heart of Wellbine is:

```text
AAI
↓
Plan Templates
↓
Onboarding
↓
Home
↓
Daily
↓
Push
↓
Pillars
```

Everything else should support this core.

---

# Implementation Philosophy

Wellbine should be built in layers.

Each layer should make the next layer possible.

Recommended logic:

```text
Foundation
↓
Data
↓
Interface
↓
Activation
↓
Daily operation
↓
Adaptive behavior
↓
Integrations
↓
Monetization extensions
↓
Release readiness
```

The first build should be useful, not perfect.

The system should support fast iteration without becoming chaotic.

---

# Core Architecture

Recommended product architecture:

```text
Supabase
↓
Data Model
↓
Admin Configuration
↓
FlutterFlow App
↓
User Experience
↓
AAI Context Evolution
```

Supabase is the data and configuration foundation.

FlutterFlow is the product interface layer.

Admin is the operational control layer.

AAI is the intelligence architecture.

---

# Supabase Role

Supabase should be used for:

- Authentication
- Database
- Storage
- Row Level Security
- User data
- Plan configuration
- User active plans
- Pillar states
- Daily actions
- Push events
- Upload metadata
- Admin configuration
- AAI context storage
- Audit logs

Supabase is the source of truth for structured data.

---

# FlutterFlow Role

FlutterFlow should be used to build:

- App interface
- Onboarding flow
- Home operating surface
- Daily execution flow
- Pillar panels
- Push adjustment screens
- Daily Stack screens
- Wearable connection screens
- Upload screens
- Settings screens
- Subscriber benefits screens
- Admin MVP if chosen inside FlutterFlow

FlutterFlow should consume Supabase data.

FlutterFlow should not become the source of truth.

---

# FlutterFlow Rule

```text
FlutterFlow is the product interface layer, not the source of truth.
```

Business logic that changes frequently should not be hardcoded inside FlutterFlow screens.

Examples of logic that should be database-driven when practical:

- Plan Templates
- Push copy
- Push timing
- Pillar defaults
- Daily sequences
- Home messages
- Recommendations
- Onboarding options
- Subscriber benefit rules

FlutterFlow should render and execute configuration.

Supabase and Admin should store and manage configuration.

---

# Admin Role

Admin should allow authorized operators to configure Wellbine without code changes.

Admin should control:

- Plan Templates
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
- Commerce Bridge
- Subscriber Benefits
- Publishing
- Users
- Analytics

Admin may start simple.

It does not need to be perfect in the MVP.

But the architecture should assume Admin-driven configuration from the beginning.

---

# MVP Priority Rule

The MVP should not try to build every possible feature.

The MVP should prove:

```text
A user can activate a plan and receive adaptive daily guidance.
```

The first MVP should focus on:

- Auth
- Profile
- Onboarding
- Plan Template
- User Active Plan Snapshot
- Home
- Daily
- Push logic
- Pillar states
- Basic Admin configuration
- Basic Data Model
- Basic AAI context

Wearables, uploads, commerce and full store integration should be prepared architecturally, but not allowed to delay the core experience.

---

# Implementation Phases

The recommended implementation sequence is:

```text
Phase 0 — Documentation Baseline
Phase 1 — Supabase Foundation
Phase 2 — FlutterFlow Foundation
Phase 3 — Authentication And User Profile
Phase 4 — Data Model MVP
Phase 5 — Plan Templates MVP
Phase 6 — User Active Plan Snapshot
Phase 7 — Onboarding
Phase 8 — Home
Phase 9 — Daily
Phase 10 — Pillars
Phase 11 — Push Orchestration
Phase 12 — Daily Stack
Phase 13 — Wearables Connectivity
Phase 14 — Uploads
Phase 15 — Admin MVP
Phase 16 — AAI Context Layer
Phase 17 — Commerce Bridge / Subscriber Benefits
Phase 18 — App Store And Google Play Readiness
Phase 19 — QA And Testing
Phase 20 — Production Launch
```

---

# Phase 0 — Documentation Baseline

Purpose:

Create a clear source of truth before building.

Already defined documents:

- AAI Constitution
- AAI Glossary
- AAI Principles
- POPAE
- Wellbine Product
- BCAS
- Plan Templates
- Onboarding
- Home
- Daily
- Push
- Pillars
- Daily Stack
- Admin
- Data Model
- Architecture Decisions

Output:

```text
The team understands what is being built before implementation starts.
```

---

# Phase 1 — Supabase Foundation

Purpose:

Create the backend foundation.

Tasks:

- Create Supabase project
- Configure environments
- Configure authentication
- Create initial tables
- Configure Row Level Security
- Configure storage buckets
- Configure admin access strategy
- Define basic role model
- Prepare database naming convention
- Prepare migration strategy

Initial Supabase areas:

- Auth
- Database
- Storage
- RLS
- Edge Functions when needed
- Admin data access
- Event logs

Output:

```text
Supabase is ready to support the first version of Wellbine.
```

---

# Phase 2 — FlutterFlow Foundation

Purpose:

Create the app foundation.

Tasks:

- Create FlutterFlow project
- Connect FlutterFlow to Supabase
- Configure app theme
- Configure brand styles
- Configure navigation model
- Configure app state
- Configure authentication connection
- Configure reusable components
- Configure responsive behavior
- Configure build targets for iOS and Android

Important rule:

```text
Do not rebuild old Bottom Navigation architecture.
```

Home should become the central operating surface.

FlutterFlow should support contextual navigation.

Output:

```text
FlutterFlow is connected to Supabase and ready to build product flows.
```

---

# Phase 3 — Authentication And User Profile

Purpose:

Allow users to create accounts and store basic profile information.

Tasks:

- Implement sign up
- Implement login
- Implement logout
- Implement password reset
- Create user profile after signup
- Store display name
- Store biological sex
- Store age
- Store height
- Store weight
- Store relevant comorbidities status
- Store timezone
- Store language
- Store basic settings

Core tables:

- user_profiles
- user_settings

Output:

```text
A user can create an account and have a basic profile.
```

---

# Phase 4 — Data Model MVP

Purpose:

Create the minimum viable data model.

Initial MVP tables:

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

Rules:

- Use lower_snake_case for database tables.
- Keep fields practical.
- Use JSON fields where early flexibility is needed.
- Structure later what becomes stable.
- Avoid over-engineering before MVP.

Output:

```text
The database can support the first operational version of Wellbine.
```

---

# Phase 5 — Plan Templates MVP

Purpose:

Create database-driven Plan Templates.

Tasks:

- Create plan_templates table
- Create plan_template_versions table
- Create first test templates
- Create first published template
- Define default pillar configuration
- Define default Daily configuration
- Define default Push configuration
- Define default Home configuration
- Define basic settings defaults
- Define plan status: draft, published, archived

Initial test plans may include:

```text
LONG40
ENERGY_BASE
SLEEP_RECOVERY
METABOLIC_RESET
START_SIMPLE
```

Rules:

- Plan names should not be hardcoded.
- Plans should be editable through data.
- A user activation should create a snapshot.
- A template should remain unchanged when the user personalizes the plan.

Output:

```text
Wellbine has database-driven plans that can activate the user experience.
```

---

# Phase 6 — User Active Plan Snapshot

Purpose:

Create the user's personal active version of a plan.

Tasks:

- Create user_active_plans logic
- Copy relevant template configuration into active snapshot
- Store source of activation
- Store duration
- Store current day
- Store status
- Store active_configuration_json
- Allow user-specific modifications
- Preserve original Plan Template

Activation sources:

```text
recommended_plan
adapted_plan
user_selected
manual_admin
```

Output:

```text
A user can activate a plan without changing the original template.
```

---

# Phase 7 — Onboarding

Purpose:

Move user from blank state to active plan state.

Tasks:

- Build Welcome screen
- Build Name screen
- Build Biological Sex screen
- Build Age screen
- Build Height screen
- Build Weight screen
- Build Relevant Comorbidities screen
- Build Wearable optional screen
- Build Push and Mental Detox explanation
- Build Push permission screen
- Build Primary Goals screen
- Build Recommended Plan / Adapted Plan screen
- Build Pillar Preference Dashboard
- Build Optional Upload screen
- Build Activate 7-Day Sync Plan screen
- Route user to Home

Output:

```text
A new user completes onboarding and reaches Home with an active plan.
```

---

# Phase 8 — Home

Purpose:

Create the central operating surface.

Tasks:

- Build Home screen
- Build First Activation Mode
- Build Active Plan display
- Build Central Main Orb
- Build Adaptive Summary
- Build Current Insight
- Build Next Best Action
- Build Pillar Orbs
- Build Pillar Orb Quick Panel
- Build Ask Wellbine entry
- Build Quick Actions
- Build Contextual Access Points
- Build Profile / Personal Center access

Rules:

- Home is not just a dashboard.
- Home is not a tab.
- Home is the central operating surface.
- Home should not depend on fixed Bottom Navigation.
- Home should update after Push, Daily and Pillar events.

Output:

```text
The user can understand current state and next action from Home.
```

---

# Phase 9 — Daily

Purpose:

Create the deeper execution layer of the day.

Tasks:

- Generate daily plan from active plan snapshot
- Build Daily screen
- Build Morning Activation section
- Build Midday Alignment section
- Build Evening Alignment section
- Build Night Reset section
- Create daily actions
- Track action status
- Support Done, Adjust, Later
- Update pillar states
- Update Home state
- Store daily check-ins

Daily statuses:

```text
planned
active
completed
partially_completed
adjusted
```

Output:

```text
The user can follow a daily adaptive sequence.
```

---

# Phase 10 — Pillars

Purpose:

Make the operational pillars functional.

Current pillars:

- Mind
- Sun
- Hydration
- Sleep
- Meal / Nutrition
- Movement
- Daily Stack

Tasks:

- Create pillar_definitions
- Create user_pillar_states
- Build pillar panels
- Build basic actions per pillar
- Connect pillars to Home
- Connect pillars to Daily
- Connect pillars to Push
- Support priority levels
- Support disabled for now
- Support state updates

Pillar priority options:

```text
high
normal
low
disabled
```

Output:

```text
Pillars become operational behavior modules.
```

---

# Phase 11 — Push Orchestration

Purpose:

Build Push as an outside-app orchestration layer.

Tasks:

- Configure push infrastructure
- Request Push permission after explanation
- Create push_events table
- Create push sequence logic
- Implement Confirm
- Implement Adjust
- Implement Later
- Implement deep links
- Connect Push responses to Daily
- Connect Push responses to Home
- Connect Push responses to Pillars
- Support Mental Detox mode
- Support frequency preferences

Default Push cycles:

```text
Morning Activation
Midday Alignment
Evening Alignment
Night Reset
```

Core action logic:

```text
Confirm
↓
Update state without opening app

Adjust
↓
Open relevant adjustment panel

Later
↓
Schedule contextual follow-up
```

Output:

```text
Push works as orchestration, not generic reminders.
```

---

# Phase 12 — Daily Stack

Purpose:

Support medications, vitamins, supplements and nutraceutical routines.

Tasks:

- Build Stack item creation
- Build Stack item list
- Build intake confirmation
- Build schedule logic
- Build stock tracking
- Build refill warning
- Connect Stack to Daily
- Connect Stack to Push
- Connect Stack to Home
- Connect Stack to Plan Templates

Stack item types:

```text
medication
vitamin
supplement
nutraceutical
other
```

Important rule:

```text
Daily Stack should support routine and adherence, not medical diagnosis.
```

Output:

```text
Users can track and confirm their Daily Stack.
```

---

# Phase 13 — Wearables Connectivity

Purpose:

Prepare wearable integration without making it required.

Wearables should improve automation.

Wearables should not be required for value.

Initial wearable direction:

- Apple Health / HealthKit
- Google Health Connect
- Garmin
- Oura
- WHOOP
- Fitbit
- Manual fallback

MVP approach:

```text
Start with optional wearable connection.
Support manual fallback.
Avoid blocking onboarding.
Use only available and permissioned data.
```

Possible wearable signals:

- Sleep duration
- Sleep quality
- Steps
- Active minutes
- Heart rate
- Resting heart rate
- HRV
- Respiratory rate
- Oxygen saturation
- Temperature trends
- Stress signals
- Readiness
- Cycle-related insights when supported
- Premenstrual period estimation when supported

Tasks:

- Build wearable connection screen
- Store wearable provider status
- Store permission status
- Store last sync timestamp
- Store wearable daily summaries
- Define fallback behavior
- Update Home with wearable data
- Update Daily with wearable data
- Update Push with wearable data
- Update AAI context with wearable signals

Rule:

```text
Wearables improve automation, but Wellbine must work without wearables.
```

Output:

```text
Wellbine can use wearable data when available and fallback when unavailable.
```

Future document:

```text
PRODUCTS/WELLBINE/WEARABLES.md
```

---

# Phase 14 — Uploads

Purpose:

Allow users to upload exams, documents and relevant health files.

Uploads should be optional.

Upload should not block activation.

Supported upload types may include:

- Lab exams
- Blood tests
- Medical reports
- Nutrition plans
- Fitness assessments
- Sleep reports
- Wearable exports
- PDF files
- Images
- Historical health documents
- Supplement lists
- Medication lists
- Personal notes

Tasks:

- Build upload screen
- Create Supabase Storage bucket
- Store upload metadata
- Store processing status
- Allow user notes
- Connect upload status to Home
- Connect extracted information to AAI context when available
- Allow skip for now

Output:

```text
Users can enrich Wellbine with optional documents without delaying activation.
```

---

# Phase 15 — Admin MVP

Purpose:

Create minimum operational control.

The first Admin does not need every feature.

It must support the core product.

Admin MVP should manage:

- Plan Templates
- Plan versions
- Onboarding copy
- Goal options
- Push copy
- Pillar defaults
- Home messages
- Content modules
- Recommendations
- User support view
- Publishing status

Possible Admin build paths:

```text
Supabase direct management
Softr
Retool
FlutterFlow Admin
Custom Admin later
```

Initial recommendation:

```text
Use the fastest safe Admin path first.
Avoid overbuilding Admin before MVP.
```

Admin actions:

- Create
- Edit
- Duplicate
- Preview
- Publish
- Archive
- Reorder
- Save Draft

Output:

```text
The team can update core Wellbine configuration without code changes.
```

---

# Phase 16 — AAI Context Layer

Purpose:

Create the first operational AAI context layer.

AAI should use signals from:

- Onboarding
- Active plan
- Daily actions
- Push responses
- Pillar states
- Wearables
- Uploads
- Settings
- Ask Wellbine
- User behavior

Initial AAI functions:

- Summarize current context
- Generate Current Insight
- Generate Next Best Action
- Adjust Daily sequence
- Interpret Push response
- Update pillar relevance
- Identify friction
- Support progressive profiling

Important rule:

```text
AAI should start useful and evolve over time.
```

Output:

```text
Wellbine begins adapting guidance based on user context and behavior.
```

---

# Phase 17 — Commerce Bridge / Subscriber Benefits

Purpose:

Support external nutraceutical commerce without making Store the center of the app.

Commerce Bridge is a planned subscriber benefit layer.

It should not become the core navigation area for the MVP.

Core logic:

```text
Active Wellbine subscriber
↓
Receives monthly benefit
↓
Gets coupon inside app
↓
Uses coupon in external e-commerce checkout
↓
Receives discount on nutraceutical purchase
```

Initial MVP approach:

- Show monthly coupon inside app
- Allow user to copy coupon
- Link to external e-commerce
- Track coupon shown
- Track coupon copied
- Track coupon used later if integration exists

Possible locations inside app:

- Personal Center
- Subscriber Benefits
- Daily Stack
- Recommendations
- Plan Benefits
- Home contextual card

Do not make Store a fixed primary navigation item.

Commerce should be contextual.

Possible future integrations:

- Shopify
- CartPanda
- WooCommerce
- Atomicat
- Custom checkout
- Coupon API
- Subscription platform
- Fulfillment partner

Admin should eventually manage:

- Coupon campaigns
- Coupon value
- Coupon validity
- Monthly availability
- Subscriber eligibility
- Product categories
- External checkout links
- Recommendation placement
- Campaign status
- Redemption tracking

Rules:

```text
Commerce Bridge is a subscriber benefit layer.
```

```text
Commerce should not dominate the Wellbine experience.
```

```text
The core product should guide first; commerce should appear when relevant.
```

Output:

```text
Wellbine can support nutraceutical monetization without turning the app into a store.
```

Future document:

```text
PRODUCTS/WELLBINE/COMMERCE_BRIDGE.md
```

---

# Phase 18 — App Store And Google Play Readiness

Purpose:

Prepare Wellbine for iOS and Android release.

This phase should be considered early, even if submission happens later.

App release readiness affects:

- Health permissions
- Push notifications
- Wearable access
- Privacy policy
- Terms of use
- Account deletion
- AI explanation
- Subscription language
- External commerce links
- Nutraceutical claims
- Health disclaimers
- App screenshots
- Review notes
- TestFlight
- Google internal testing

Tasks:

- Create Apple Developer account readiness checklist
- Create Google Play Console readiness checklist
- Define Bundle ID
- Define Android Package Name
- Prepare app icon
- Prepare screenshots
- Prepare app description
- Prepare privacy policy
- Prepare terms of use
- Prepare account deletion flow
- Prepare health data permission copy
- Prepare Push permission copy
- Prepare AI usage explanation
- Prepare wearable permission explanation
- Prepare subscription and benefits language
- Prepare external commerce explanation
- Prepare review notes
- Run TestFlight
- Run Google internal testing
- Fix review blockers
- Prepare production release

Important rule:

```text
App Store and Google Play approval should be considered during product design, not only before launch.
```

Output:

```text
Wellbine is prepared for iOS and Android review and release.
```

Future document:

```text
PRODUCTS/WELLBINE/APP_RELEASE.md
```

---

# Phase 19 — QA And Testing

Purpose:

Validate that the product works before launch.

Testing areas:

- Signup
- Login
- Onboarding
- Recommended Plan
- Adapted Plan
- Active Plan Snapshot
- Home state
- Daily actions
- Pillar states
- Push responses
- Adjust flows
- Later flows
- Mental Detox
- Daily Stack
- Wearable fallback
- Uploads
- Admin edits
- Plan publishing
- Commerce coupon display
- External checkout link
- Account deletion
- Privacy flows
- iOS build
- Android build

QA should test:

- New user
- Returning user
- User without wearable
- User with wearable
- User without Push
- User with Push
- User with no active plan
- User with active plan
- User with delayed actions
- User with changed preferences

Output:

```text
The product is stable enough for controlled launch.
```

---

# Phase 20 — Production Launch

Purpose:

Launch the first public or controlled production version.

Launch options:

```text
Internal beta
Closed beta
Soft launch
Public MVP
Paid launch
```

Recommended first launch:

```text
Controlled beta with real users before full paid scale.
```

Launch should track:

- Onboarding completion
- Plan activation
- Day 1 completion
- Push response rate
- Home engagement
- Daily engagement
- Pillar engagement
- Retention
- Subscriber conversion
- Coupon usage
- User feedback
- Bugs
- App review issues

Output:

```text
Wellbine is live with real users and measurable behavior.
```

---

# MVP Build Sequence

The practical MVP sequence should be:

```text
1. Supabase project
2. FlutterFlow project
3. Auth
4. User Profile
5. User Settings
6. Plan Templates MVP
7. User Active Plan Snapshot
8. Onboarding
9. Home
10. Daily
11. Pillars
12. Push Orchestration
13. Daily Stack basic
14. Admin MVP
15. AAI Context basic
16. Wearable optional placeholder / manual fallback
17. Upload optional placeholder
18. Subscriber Benefit coupon placeholder
19. App release readiness
20. QA
21. Controlled launch
```

---

# What Should Be Built Later

These should not delay the MVP:

- Full wearable ecosystem
- Full upload interpretation
- Full AI medical document analysis
- Full e-commerce integration
- Full coupon API integration
- Full App Store subscription complexity
- Advanced Admin roles
- Advanced analytics
- A/B testing
- FHIR mapping
- Clinical integrations
- Complex medical workflows
- Full recommendation engine
- Marketplace / store inside app

They should be planned, but not allowed to block the core product.

---

# Critical Dependencies

The most important dependencies are:

```text
Data Model
↓
Plan Templates
↓
User Active Plan Snapshot
↓
Onboarding
↓
Home
↓
Daily
↓
Push
```

If this chain works, Wellbine has a product.

If this chain does not work, extra features will not save the product.

---

# Key Product Risks

Main risks:

- Building too many features before core activation works
- Turning Wellbine into a generic habit tracker
- Overbuilding Admin too early
- Making FlutterFlow logic too hardcoded
- Making wearables required
- Making commerce too central
- Treating Push as generic reminders
- Launching without privacy and app review readiness
- Collecting sensitive health data without clear structure
- Creating a dashboard instead of an operating surface

---

# Implementation Rules

Wellbine implementation should follow these rules:

```text
Build core activation first.
```

```text
Keep plans database-driven.
```

```text
Use FlutterFlow as interface, not source of truth.
```

```text
Use Supabase as data and configuration foundation.
```

```text
Create user active plan snapshots.
```

```text
Make Home the central operating surface.
```

```text
Make Push orchestration, not reminders.
```

```text
Make wearables optional.
```

```text
Make commerce contextual, not dominant.
```

```text
Consider app store readiness early.
```

---

# Current Status

Wellbine is currently in architecture and documentation phase.

The next practical steps are:

- Create implementation-ready Supabase schema
- Define MVP tables
- Build FlutterFlow foundation
- Connect FlutterFlow to Supabase
- Build Auth and Profile
- Build Plan Templates MVP
- Build User Active Plan Snapshot logic
- Build Onboarding
- Build Home
- Build Daily
- Build Pillars
- Build Push logic
- Build Admin MVP
- Prepare release readiness checklist

---

# Future Documents

Recommended future documents:

```text
PRODUCTS/WELLBINE/WEARABLES.md
PRODUCTS/WELLBINE/APP_RELEASE.md
PRODUCTS/WELLBINE/COMMERCE_BRIDGE.md
PRODUCTS/WELLBINE/SUPABASE_SCHEMA.md
PRODUCTS/WELLBINE/QA_PLAN.md
```

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
- ARCHITECTURE_DECISIONS/HOME_CENTRAL.md
- ARCHITECTURE_DECISIONS/PUSH_ORCHESTRATION.md
- ARCHITECTURE_DECISIONS/PLAN_TEMPLATES_DB.md
- ARCHITECTURE_DECISIONS/ADMIN_CONTROL_LAYER.md
- ARCHITECTURE_DECISIONS/ONBOARDING_ACTIVATION.md
