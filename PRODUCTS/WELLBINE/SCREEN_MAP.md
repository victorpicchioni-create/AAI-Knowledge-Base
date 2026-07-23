# Wellbine Screen Map

**Version:** 0.1.0

**Status:** Draft

**Last Updated:** July 2026

---

# Purpose

This document defines the screen map for the Wellbine mobile app.

The goal is to translate the Wellbine product architecture into a clear app structure that can be built in FlutterFlow.

This document covers:

- App entry logic
- Screen groups
- Core screens
- Optional screens
- Navigation rules
- Home-centered structure
- Daily execution flow
- Pillar access
- Settings and privacy paths
- Commerce Bridge placement
- Wearables placement
- Uploads placement
- App release-sensitive screens

This document is not a visual design file.

It is the structural map of the app.

---

# Official Definition

**Wellbine Screen Map is the structural blueprint that defines which screens exist in the Wellbine mobile app, how users move between them and how each screen connects to the operating system experience.**

---

# Core Principle

The core screen rule is:

```text
Every screen should help the user understand, act or control the system.
```

Wellbine should avoid screens that exist only because other apps have them.

The app should not become a menu maze.

The user should always understand:

```text
Where am I?
What matters now?
What can I do next?
How do I adjust?
How do I control my data?
```

---

# Navigation Philosophy

Wellbine should be Home-centered.

Recommended structure:

```text
Home
↓
Daily
↓
Pillar Detail
↓
Settings / Personal Center
↓
Contextual Screens
```

Wellbine should not depend on fixed Bottom Navigation as the core structure.

Navigation should be contextual.

Home is the operating surface.

Daily is the execution layer.

Pillars are operational modules.

Settings / Personal Center is the control layer.

Commerce Bridge is contextual.

Wearables are optional.

Uploads are optional.

---

# App Entry Logic

The app should route users based on state.

```text
Open App
↓
Check Auth
↓
Check Onboarding
↓
Check Active Plan
↓
Route to correct screen
```

Routing logic:

```text
If user is not authenticated:
    Auth Screen

If user is authenticated and onboarding is incomplete:
    Onboarding Flow

If user is authenticated and onboarding is complete but no active plan:
    Plan Selection / First Activation

If user is authenticated and active plan exists:
    Home
```

---

# Screen Groups

Recommended screen groups:

```text
Entry Screens
Auth Screens
Onboarding Screens
Plan Activation Screens
Core Operating Screens
Daily Screens
Pillar Screens
Daily Stack Screens
Wearable Screens
Upload Screens
Commerce Bridge Screens
Ask Wellbine Screens
Settings / Personal Center Screens
Privacy / Legal Screens
Account Screens
Error / Fallback Screens
```

---

# MVP Screen List

Mandatory MVP screens:

```text
Splash / Loading
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
Privacy Policy
Terms of Use
Account
Delete Account
Error State
Empty State
Loading State
```

Strong MVP screens:

```text
Daily Stack
Mental Detox / Push Explanation
Push Preferences
Adaptive Summary
Pillar Quick Panel
```

Optional first release screens:

```text
Wearable Manager
Upload Manager
Commerce Benefit Detail
Ask Wellbine
Subscriber Benefits
```

---

# Entry Screens

## Splash / Loading

Purpose:

```text
Initial app loading and routing.
```

Checks:

```text
Auth state
Onboarding status
Active plan status
App version if needed
Feature flags if needed
```

Routes to:

```text
Auth
Onboarding
Plan Selection
Home
Error State
```

Should not feel slow or empty.

---

## App Error State

Purpose:

```text
Handle startup failure.
```

Use when:

```text
Auth check fails
Supabase unavailable
Critical app configuration unavailable
```

Action:

```text
Retry
Contact support if needed
```

---

# Auth Screens

## Auth Screen

Purpose:

```text
Allow users to sign up or log in.
```

Includes:

```text
Sign up
Login
Password reset
Privacy Policy link
Terms of Use link
```

Routes to:

```text
Onboarding
Plan Selection
Home
```

depending on user state.

---

## Password Reset

Purpose:

```text
Allow user to recover account access.
```

Should include:

```text
Email input
Clear confirmation
Return to login
```

---

# Onboarding Screens

## Welcome

Purpose:

```text
Introduce Wellbine and begin activation.
```

Should explain:

```text
Wellbine helps organize daily wellness guidance.
```

Should not overload the user.

---

## Profile Baseline

Purpose:

```text
Collect minimum personalization data.
```

Fields:

```text
Name
Biological sex
Age
Height
Weight
Country / region if needed
Language
Timezone
Relevant comorbidities optional
```

Rules:

```text
Comorbidities are optional.
Biological sex includes Prefer not to say.
Do not make onboarding feel like a medical exam.
```

---

## Wearable Optional Step

Purpose:

```text
Offer wearable connection without blocking onboarding.
```

Options:

```text
Connect Wearable
Continue Without Wearable
```

Key copy:

```text
Wellbine works without a wearable. Connecting one can improve personalization.
```

Routes to:

```text
Wearable Manager
Next onboarding step
```

---

## Mental Detox / Push Explanation

Purpose:

```text
Explain Push before asking for notification permission.
```

Should explain:

```text
Push is used for adaptive guidance, not noise.
```

Options:

```text
Enable Guidance
Not Now
```

Push must be optional.

---

## Goals

Purpose:

```text
Capture user's main wellness direction.
```

Possible categories:

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

Should be admin-configurable later.

---

## Plan Model Selection

Purpose:

```text
Help user select the first Plan Template.
```

May show:

```text
Recommended Plan
Adapted Plan
Manual selection
```

Routes to:

```text
Plan Activation Loading
```

---

## Pillar Preferences

Purpose:

```text
Let user adjust priorities before activation.
```

May include:

```text
Sleep priority
Movement preference
Nutrition preference
Hydration preference
Mind preference
Daily Stack preference
```

Should not become too long.

---

## Upload Optional Step

Purpose:

```text
Offer optional file enrichment.
```

Options:

```text
Upload File
Continue Without Upload
```

Rules:

```text
Upload is optional.
Upload should not imply diagnosis.
Upload should not block activation.
```

---

# Plan Activation Screens

## Plan Selection

Purpose:

```text
Show published Plan Templates available to the user.
```

Reads:

```text
plan_templates
plan_template_versions
```

Shows:

```text
Plan name
Description
Audience
Focus
Recommended badge if applicable
```

Should not show:

```text
Draft plans
Archived plans
Broken plans
```

---

## Plan Activation Loading

Purpose:

```text
Create the user's operating state.
```

Calls:

```text
activate_plan
```

Creates:

```text
user_active_plans
user_pillar_states
daily_plans
daily_actions
user_home_state
```

Routes to:

```text
Home
```

Failure state:

```text
Retry activation
Return to Plan Selection
```

---

# Core Operating Screens

## Home

Purpose:

```text
Central operating surface of Wellbine.
```

Home should show:

```text
Main Orb
Current Insight
Next Best Action
Pillar Orbs
Daily access
Adaptive Summary access
Ask Wellbine access if visible
Personal Center access
Contextual cards
```

Home reads:

```text
user_home_state
user_active_plans
user_pillar_states
daily_plans
daily_actions
recommendations
user_commerce_benefits if visible
wearable_metric_snapshots if available
```

Home should not be:

```text
Blank
Store-first
Dashboard maze
Dependent on wearable
Dependent on Push
```

---

## Adaptive Summary

Purpose:

```text
Show a deeper summary of current user state.
```

Possible sections:

```text
Body
Mind
Recovery
Today Sync
7-Day Sync
```

Opened from:

```text
Main Orb
Home summary card
```

Should avoid fake precision.

---

## Current Insight

Purpose:

```text
Explain the current state in plain language.
```

May be shown as a Home card rather than full screen.

Should answer:

```text
What is happening now?
```

---

## Next Best Action

Purpose:

```text
Give the user one clear action.
```

May be shown as Home card.

Action types:

```text
Confirm
Start
Adjust
Open Daily
Open Pillar
Review Stack
Prepare Sleep
Add Input
```

Should answer:

```text
What should I do now?
```

---

# Daily Screens

## Daily

Purpose:

```text
The deeper execution layer for the day.
```

Shows:

```text
Current action
Upcoming actions
Completed actions
Delayed actions
Recoverable actions
Daily summary
```

Controls:

```text
Confirm
Adjust
Later
```

Reads:

```text
daily_plans
daily_actions
user_pillar_states
user_active_plans
```

Updates:

```text
daily_actions
user_pillar_states
user_home_state
```

---

## Daily Action Detail

Purpose:

```text
Explain one action and allow interaction.
```

Shows:

```text
Action title
Description
Timing
Related pillar
Why it matters
Confirm / Adjust / Later
```

Should be simple.

---

## Daily Adjustment

Purpose:

```text
Allow user to adapt an action.
```

Examples:

```text
Change timing
Change intensity
Change meal context
Change movement option
Change hydration input
Change sleep preparation
```

Adjust should not feel like failure.

---

# Pillar Screens

## Pillar Quick Panel

Purpose:

```text
Give fast pillar access from Home.
```

Opened from:

```text
Pillar Orb
```

Shows:

```text
Current status
Quick action
Open detail
Related Daily action
```

---

## Pillar Detail

Purpose:

```text
Show one pillar's operational state.
```

Pillars:

```text
Mind
Sun
Hydration
Sleep
Nutrition
Movement
Daily Stack
```

Shows:

```text
Status
Today action
Recent activity
Simple guidance
Adjust options
Related recommendations
```

Should not become a complex analytics dashboard in MVP.

---

## Sleep Pillar

Purpose:

```text
Support sleep and recovery behavior.
```

May show:

```text
Sleep preparation
Recovery state
Bedtime guidance
Wake context
Manual sleep input
Wearable sleep summary if available
```

---

## Hydration Pillar

Purpose:

```text
Support hydration behavior.
```

May show:

```text
Cup check-in
Hydration status
Electrolyte context if configured
Daily target context
```

Use simple user-facing units.

---

## Movement Pillar

Purpose:

```text
Support movement behavior.
```

May show:

```text
Movement action
Intensity option
Recovery-aware adjustment
Walk suggestion
Training suggestion
```

Movement should adapt to readiness.

---

## Nutrition Pillar

Purpose:

```text
Support meal and nutrition behavior.
```

May show:

```text
Meal context
Fasting context
Post-meal feedback
Protocol-aware guidance
```

Should not force meal suggestions during fasting.

---

## Mind Pillar

Purpose:

```text
Support mental state, breathing, focus and meditation.
```

May show:

```text
Breathing
Meditation
Stress check-in
Focus reset
Sleep preparation support
```

---

## Sun Pillar

Purpose:

```text
Support sunlight and circadian alignment behavior.
```

May show:

```text
Morning light
Outdoor exposure
Timing guidance
Weather-aware note if implemented later
```

---

# Daily Stack Screens

## Daily Stack

Purpose:

```text
Organize supplements, vitamins, nutraceuticals, medications or routine items.
```

Shows:

```text
Today stack
Timing
Taken / skipped status
Add item
Edit item
Refill context if enabled
```

Boundary:

```text
Daily Stack organizes routines. It does not prescribe medication.
```

---

## Stack Item Detail

Purpose:

```text
Manage one Daily Stack item.
```

Fields:

```text
Name
Item type
Dosage text
Frequency
Timing
Instructions
Refill tracking
Notes
```

Item types:

```text
supplement
vitamin
nutraceutical
medication
habit_item
other
```

---

# Wearable Screens

## Wearable Manager

Purpose:

```text
Manage optional wearable and health platform connection.
```

Shows:

```text
Connected provider
Available providers
Manual fallback
Last sync
Disconnect option
Permission explanation
```

Rules:

```text
Wearables are optional.
Do not show providers as active before implementation.
App works without wearable.
```

---

## Wearable Provider Detail

Purpose:

```text
Explain one provider connection.
```

Shows:

```text
Provider name
Data requested
Why it helps
Permission status
Connect / Disconnect
```

---

# Upload Screens

## Upload Manager

Purpose:

```text
Manage optional user files.
```

Shows:

```text
Upload file
Upload list
Upload status
Delete upload
Summary if available
```

Rules:

```text
Uploads are optional.
Private files must not be publicly accessible.
Uploads do not create diagnosis.
```

---

## Upload Detail

Purpose:

```text
Show one uploaded file status.
```

Shows:

```text
File name
Category
Upload date
Processing status
Summary if available
Delete option
```

---

# Commerce Bridge Screens

## Subscriber Benefits

Purpose:

```text
Show eligible subscriber benefits.
```

May appear inside:

```text
Personal Center
Daily Stack
Plan Benefits
Home contextual card
Recommendations
```

Should not be a fixed Store tab in MVP.

---

## Commerce Benefit Detail

Purpose:

```text
Allow user to use one eligible benefit.
```

Shows:

```text
Benefit title
Short description
Benefit code if applicable
Primary action
Expiration if applicable
External purchase note
```

Primary action:

```text
Use Benefit
```

Behavior:

```text
Copy benefit code
Open external commerce destination
Track event
```

Rules:

```text
Do not hardcode discount amounts.
Do not hardcode commerce platform.
External purchase boundary must be clear.
```

---

# Ask Wellbine Screens

## Ask Wellbine

Purpose:

```text
Allow user to ask questions about their plan, day, pillars and routine.
```

MVP role:

```text
Guidance support
Plan explanation
Daily explanation
Pillar explanation
Routine clarification
```

Should not:

```text
Diagnose
Treat
Replace medical advice
Override safety boundaries
```

---

# Settings / Personal Center Screens

## Personal Center

Purpose:

```text
Give user access to account, preferences and controls.
```

Includes:

```text
Profile
Plan
Push Preferences
Mental Detox
Wearables
Uploads
Daily Stack
Subscriber Benefits if visible
Privacy
Terms
Account
Logout
```

This is not the central operating surface.

Home remains central.

---

## Profile Settings

Purpose:

```text
Allow user to edit profile baseline.
```

Fields:

```text
Name
Age
Height
Weight
Biological sex
Language
Timezone
Relevant optional context
```

---

## Push Preferences

Purpose:

```text
Allow user to control notification behavior.
```

Includes:

```text
Push enabled
Mental Detox
Frequency preferences
Quiet hours if implemented
Category preferences if implemented
```

Push must be optional.

---

## Mental Detox Settings

Purpose:

```text
Allow user to reduce notification noise.
```

Controls may include:

```text
Reduce Wellbine notifications
Pause nonessential guidance
Quiet period
Focus mode support
```

---

## Plan Settings

Purpose:

```text
Show current active plan and related controls.
```

May include:

```text
Active plan
Plan start date
Plan summary
Change plan if supported
Restart plan if supported
```

Changing plans should be handled carefully.

---

# Privacy / Legal Screens

## Privacy Policy

Purpose:

```text
Show or link to Privacy Policy.
```

Required for release.

Must be accessible from:

```text
Signup
Settings
App metadata
```

---

## Terms of Use

Purpose:

```text
Show or link to Terms of Use.
```

Required for release.

Must be accessible from:

```text
Signup
Settings
App metadata
```

---

## AI Explanation

Purpose:

```text
Explain AI-assisted guidance.
```

May be a section inside Settings or onboarding.

Should clarify:

```text
AI supports wellness guidance.
AI does not provide medical diagnosis or emergency care.
```

---

# Account Screens

## Account

Purpose:

```text
Manage account-level actions.
```

Includes:

```text
Email
Account status
Subscription status if visible
Delete Account
Logout
```

---

## Delete Account

Purpose:

```text
Allow account deletion.
```

Flow:

```text
Open Delete Account
↓
Read warning
↓
Confirm
↓
Call delete_account
↓
Show result
```

This is release-critical.

---

# Error / Fallback Screens

## Loading State

Used when:

```text
Auth checking
Data loading
Plan activation
Home loading
Daily loading
Upload processing
Benefit loading
```

Should not be blank.

---

## Empty State

Used when:

```text
No active plan
No Daily actions
No Stack items
No uploads
No wearable connected
No benefit available
```

Should include a next action.

---

## Error State

Used when:

```text
Data fails to load
Action fails
Upload fails
External link fails
Plan activation fails
```

Should include:

```text
Clear message
Retry action
Safe fallback
```

---

## Offline / Poor Connection State

Purpose:

```text
Handle weak network.
```

Should avoid:

```text
Data loss
Duplicate actions
User being trapped
Blank screens
```

---

# Screen Priority

Priority 1:

```text
Splash / Loading
Auth
Welcome
Profile Baseline
Plan Selection
Plan Activation Loading
Home
Daily
Pillar Detail
Settings / Personal Center
Privacy Policy
Terms of Use
Account
Delete Account
```

Priority 2:

```text
Adaptive Summary
Pillar Quick Panel
Daily Action Detail
Daily Adjustment
Daily Stack
Push Preferences
Mental Detox Settings
```

Priority 3:

```text
Wearable Manager
Upload Manager
Commerce Benefit Detail
Subscriber Benefits
Ask Wellbine
```

Priority 4:

```text
Advanced analytics
Advanced recommendations
Advanced wearable insights
Advanced commerce flows
```

---

# Screens To Avoid In MVP

Avoid:

```text
Fixed Store tab
Large dashboard screen
Complex analytics screen
Medical report interpretation screen
Complex wearable analytics
Large plan marketplace
Social feed
Community feed
Gamification hub
Complex achievement system
```

These can distract from the operating loop.

---

# Screen Map Summary

Recommended MVP screen flow:

```text
Splash
↓
Auth
↓
Welcome
↓
Profile Baseline
↓
Optional Wearable
↓
Mental Detox / Push Explanation
↓
Goals
↓
Plan Selection
↓
Plan Activation
↓
Home
↓
Daily
↓
Pillar Detail
↓
Settings / Personal Center
```

Contextual screens:

```text
Daily Stack
Wearable Manager
Upload Manager
Commerce Benefit Detail
Ask Wellbine
Privacy
Terms
Delete Account
```

---

# Success Criteria

The Screen Map is successful when:

- Home is clearly central
- Daily is easy to access
- Pillars are understandable
- Settings are easy to find
- Account deletion is accessible
- Optional features do not block the user
- Commerce is contextual
- Wearables are optional
- Uploads are optional
- Push is optional
- The user always knows what to do next

---

# Current Status

Screen Map is currently a draft.

Next steps:

- Build FlutterFlow page list
- Define reusable components
- Create navigation actions
- Connect Supabase queries
- Add loading states
- Add empty states
- Add error states
- Test routing logic
- Validate against MVP Build Sequence

---

# Related Documents

- PRODUCTS/WELLBINE/PRODUCT.md
- PRODUCTS/WELLBINE/ONBOARDING.md
- PRODUCTS/WELLBINE/HOME.md
- PRODUCTS/WELLBINE/DAILY.md
- PRODUCTS/WELLBINE/PUSH.md
- PRODUCTS/WELLBINE/PILLARS.md
- PRODUCTS/WELLBINE/STACK.md
- PRODUCTS/WELLBINE/WEARABLES.md
- PRODUCTS/WELLBINE/COMMERCE_BRIDGE.md
- PRODUCTS/WELLBINE/FLUTTERFLOW_BUILD_GUIDE.md
- PRODUCTS/WELLBINE/MVP_BUILD_SEQUENCE.md
