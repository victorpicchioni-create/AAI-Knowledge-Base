# Wellbine Onboarding

**Version:** 0.1.0

**Status:** Active

**Last Updated:** July 2026

---

# Purpose

This document defines the Wellbine Onboarding experience.

Onboarding is the first activation flow of Wellbine.

Its purpose is to help the user move from a blank state to an active personalized operating experience with minimal friction.

Onboarding should activate:

- User profile basics
- Initial health context
- Initial goal
- Plan Template
- Pillar defaults
- Daily flow
- Push logic
- Home state
- Wearable preference
- Settings defaults
- Document and data upload options
- First Next Best Action

Onboarding should not feel like a long questionnaire.

It should feel like activating a personal system.

---

# Official Definition

**Wellbine Onboarding is the first activation flow that transforms a new user into an active Wellbine user by collecting essential profile data, selecting or adapting a starting plan, setting preferences and activating Home, Daily, Push and Pillars.**

---

# Core Principle

Onboarding should be short, adaptive and action-oriented.

The goal is not to collect every possible detail.

The goal is to collect enough essential context to activate the system safely and intelligently.

Wellbine should collect the minimum necessary information to start.

More details can be collected later through:

- Push check-ins
- Ask Wellbine
- Settings
- Pillar panels
- Daily adjustments
- Plan adjustments
- Wearable data
- Document upload
- Exam upload
- User history

This approach is called progressive profiling.

---

# Product Rule

Onboarding should not delay value.

The user should reach an active Home state quickly.

The ideal outcome of Onboarding is:

```text
User completes basic profile

↓

User selects goal and plan

↓

Wellbine activates the first 7-Day Sync Plan

↓

Home opens with Current Insight and Next Best Action
```

---

# Relationship With AAI

AAI uses Onboarding to establish the user's initial context.

Onboarding provides the first structured signals:

- Name
- Biological sex
- Age
- Height
- Weight
- Relevant comorbidities
- Goal
- Plan
- Preferences
- Constraints
- Wake / sleep pattern
- Push permission
- Wearable status
- Initial pillar priorities
- Uploaded documents or exams, if available

AAI should treat Onboarding as a starting point, not as a permanent truth.

The system should evolve after observing real behavior.

---

# Relationship With BCAS

Onboarding should support BCAS by collecting enough context to identify useful biological windows.

Examples:

- Wake time
- Sleep time
- Meal preference
- Movement preference
- Hydration preference
- Recovery need
- Fasting preference
- Daily rhythm
- Biological sex
- Age
- Weight
- Relevant conditions
- Wearable signals, if available

The system should not overfit to fixed times.

Onboarding should create starting assumptions that BCAS can later adapt.

---

# Relationship With Plan Templates

Plan Templates are central to Onboarding.

The user should not need to build a full plan from scratch.

The user should be able to choose between:

1. Recommended Plan
2. Adapted Plan

---

## Recommended Plan

Recommended Plan is an initial preconfigured plan suggested by Wellbine based on the information collected during onboarding.

Example:

```text
User profile:

Female
48 years old
1.60 m
60 kg
No reported comorbidities
Primary goal: Longevity
```

Possible recommendation:

```text
Recommended Plan

LONG40
```

The plan name, logic and available templates should be admin-managed.

The recommendation should be generated from:

- User profile
- Primary goal
- Biological sex
- Age
- Height
- Weight
- Relevant comorbidities
- Preferences
- Available Plan Templates
- Admin-defined rules

---

## Adapted Plan

Adapted Plan allows the user to customize the starting plan before activation.

The user may adjust:

- Pillar priority
- Nutrition preference
- Movement intensity
- Sleep target
- Hydration preference
- Push frequency
- Wearable usage
- Daily Stack interest
- Recovery focus
- Personal restrictions

Adapted Plan should not require the user to build everything manually.

It should start from a template and allow simple adjustments.

---

# Relationship With Home

If the user has no active plan, Home should enter First Activation Mode.

First Activation Mode should route the user into Onboarding.

Example:

```text
Start your first Wellbine plan.

Choose a plan to activate your Daily, Push and Pillars.
```

After Onboarding is complete, Home should open with:

- Active Plan
- Current Insight
- Next Best Action
- Pillar states
- Adaptive Summary
- Ask Wellbine
- Quick Actions

Home should not show a blank dashboard.

---

# Relationship With Daily

Onboarding should activate the first Daily flow.

Daily should receive:

- First day sequence
- Current plan
- Pillar defaults
- First active windows
- Recovery logic
- Daily Stack defaults, if applicable
- Hydration defaults
- Sleep planning defaults
- Movement defaults
- Meal / Nutrition defaults
- Mind defaults
- Sun defaults

Daily should not require the user to manually configure everything after Onboarding.

---

# Relationship With Push

Onboarding should request Push permission clearly.

Push is central to Wellbine because the product should create value even when the app is not opened.

However, Push permission should not feel forced.

Preferred approach:

```text
Enable Wellbine Push?

Wellbine uses intelligent check-ins to guide your day without requiring you to open the app.
```

If the user allows Push, Wellbine activates Push cycles.

If the user denies Push, Wellbine should still work through Home, Daily and Ask Wellbine.

The user should be able to enable Push later.

---

# Mental Detox Push Control

Wellbine should clearly explain that Push can be paused or disabled.

This is important because the app should not create notification fatigue.

The user should have an easy path to:

- Pause Push
- Reduce Push frequency
- Disable Push
- Enable mental detox mode
- Reactivate Push later

Example copy:

```text
You can pause Wellbine Push anytime.

Use Mental Detox Mode if you want fewer interruptions.
```

Mental Detox Mode should not punish the user.

It should simply reduce or pause external prompts while preserving Home and Daily functionality.

---

# Relationship With Pillars

Onboarding should not ask the user to configure every pillar manually.

Instead, the selected Plan Template should activate pillar defaults.

Current pillars:

- Mind
- Sun
- Hydration
- Sleep
- Meal / Nutrition
- Movement
- Daily Stack

The user may adjust pillar preferences during or after Onboarding.

The system should not require full manual configuration before delivering value.

---

# Pillar Preference Dashboard

After choosing a Recommended Plan or Adapted Plan, the user should be able to define pillar preferences in a simple Dashboard-style screen.

This screen should allow the user to adjust the emphasis of each pillar.

Example pillars:

- Mind
- Sun
- Hydration
- Sleep
- Meal / Nutrition
- Movement
- Daily Stack

Possible preference levels:

- High priority
- Normal
- Low priority
- Disabled for now

The Dashboard should not feel technical.

It should feel like adjusting the plan before activation.

Example:

```text
Adjust your plan focus.

Hydration: High
Sleep: High
Movement: Normal
Mind: Normal
Meal / Nutrition: High
Sun: Normal
Daily Stack: Optional
```

These preferences should update the user active plan snapshot.

They should not change the original Plan Template.

---

# Relationship With Wearables

Wearables should be optional during Onboarding.

The user should be invited to connect a wearable, but not blocked if they do not have one.

Preferred copy:

```text
You have the opportunity to connect a wearable device, if you want.

This can help Wellbine understand your sleep, movement and recovery more automatically.
```

Actions:

- Connect wearable
- Skip for now

If skipped:

```text
No problem. Wellbine will adapt through simple check-ins.
```

Wearables may improve:

- Sleep detection
- Sleep duration estimation
- Sleep quality estimation
- Recovery estimation
- Movement tracking
- Inactivity detection
- Heart rate trends
- Resting heart rate trends
- HRV signals
- Stress signals
- Readiness
- Cycle-related insights when supported
- Premenstrual period estimation when supported
- Temperature-related trends when supported
- Respiratory rate trends when supported
- Oxygen saturation trends when supported
- Push personalization
- Automatic context detection

Wearable-based cycle or premenstrual insights should only be used when supported by the device, user permissions and available data.

Wearables should not be treated as medical diagnosis tools.

Without wearables, Wellbine should rely on:

- Push answers
- Manual input
- Daily behavior
- Plan configuration
- Interaction history

Wearables improve automation.

They should not be required for value.

---

# Relationship With Settings

Onboarding may define initial settings.

Settings may include:

- Language
- Time zone
- Units
- Push preference
- Wake time
- Sleep time
- Dietary preference
- Training level
- Wearable preference
- Privacy preference
- Mental Detox preference
- Upload preference

Settings should remain editable after Onboarding.

Onboarding settings are starting defaults, not permanent restrictions.

---

# Relationship With Uploads

Onboarding should include or offer access to an upload environment.

The user may upload documents, exams, wearable exports or relevant personal data.

This should be optional.

The upload environment may support:

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

Upload should not be required to start.

Preferred copy:

```text
Have exams or health documents?

You can upload them now or later.
```

Actions:

- Upload now
- Skip for now

Uploaded files may help AAI better understand context, but they should not delay activation.

Document upload should respect privacy, security and user consent.

---

# Onboarding Entry Paths

Onboarding may be triggered by:

1. First user access
2. No active plan
3. User chooses to start a new plan
4. User resets their plan
5. Admin or system requires reactivation
6. Major product update requiring new setup

---

# First User Access Flow

The first access flow should collect essential profile information before the main integration flow.

This creates enough context for Wellbine to recommend a starting plan.

Recommended first access profile flow:

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

Profile Baseline Complete
```

This profile flow should be short.

It should not feel like a medical intake form.

---

# Profile Baseline Fields

## Name

The user's name helps personalize communication.

Example:

```text
What should Wellbine call you?
```

---

## Biological Sex

Biological sex may help Wellbine personalize guidance related to physiology, recovery, cycle-related insights and health context.

Example options:

- Female
- Male
- Prefer not to say

Future versions may support more detailed identity and health profile options, but biological sex should be treated as a physiological field.

---

## Age

Age helps guide plan recommendations and recovery expectations.

---

## Height

Height helps support body composition, hydration and metabolic context.

---

## Weight

Weight helps support plan recommendations, hydration estimates, movement context and body composition tracking.

---

## Relevant Comorbidities

The user may optionally inform relevant comorbidities.

This should be handled carefully.

Example:

```text
Do you have any relevant health conditions Wellbine should consider?

None
Yes
Prefer not to say
```

If the user selects Yes, the app may allow structured selection or free text.

This information should support safer personalization.

It should not turn onboarding into medical diagnosis.

---

# Main Integration Flow

After the profile baseline is complete, the user enters the main integration flow.

Recommended flow:

```text
Connect wearable device, optional

↓

Mental Detox and Push controls explanation

↓

Activate Wellbine Push, optional

↓

Choose primary goals

↓

Choose Plan Model

↓

Define pillar preferences in Dashboard

↓

Activate 7-Day Sync Plan

↓

Enter Home
```

---

# Step 1 — Connect Wearable Device

The user has the opportunity to connect a wearable device.

Example:

```text
You have the opportunity to connect a wearable device, if you want.

This helps Wellbine personalize sleep, movement and recovery.
```

Actions:

- Connect wearable
- Skip for now

The user should not be blocked if they skip.

---

# Step 2 — Mental Detox And Push Controls

Before asking for Push permission, Wellbine should explain that notifications remain under user control.

Example:

```text
Wellbine can guide your day through intelligent Push.

You can pause or reduce Push anytime with Mental Detox Mode.
```

Actions:

- Continue
- Learn more

This reduces resistance and builds trust.

---

# Step 3 — Activate Wellbine Push

Wellbine should request Push permission after explaining the value and control.

Example:

```text
Enable Wellbine Push?

Receive your daily plan, check-ins and adjustments without opening the app.
```

Actions:

- Enable Push
- Not now

If the user selects Not now, the product should continue.

---

# Step 4 — Choose Primary Goals

The user should choose the primary goal.

Example options:

- Improve energy
- Lose weight
- Build performance
- Improve sleep
- Reduce stress
- Support recovery
- Improve longevity
- Follow a nutrition protocol
- Support medication routine
- Start simple

The user should be able to select one main goal.

Optional later version:

- Allow secondary goals
- Allow AI recommendation
- Allow Ask Wellbine to help choose

---

# Step 5 — Choose Plan Model

The user should choose between:

1. Recommended Plan
2. Adapted Plan

Example:

```text
Choose how you want to start.

Recommended Plan
Adapted Plan
```

---

## Recommended Plan

Recommended Plan is generated from the user's profile baseline, primary goal and available Plan Templates.

Example:

```text
Recommended for you:

LONG40

Designed for longevity, recovery and daily consistency.
```

The user may:

- Accept Recommended Plan
- View details
- Choose another plan
- Switch to Adapted Plan

---

## Adapted Plan

Adapted Plan lets the user start from a plan and adjust key preferences before activation.

Example:

```text
Adapt your plan before starting.
```

The user may adjust:

- Pillar emphasis
- Nutrition preference
- Movement intensity
- Sleep target
- Hydration preference
- Push frequency
- Wearable use
- Daily Stack interest
- Recovery focus

---

# Step 6 — Define Pillar Preferences In Dashboard

The user should review pillar preferences before activation.

This should happen in a simple Dashboard-like screen.

Example:

```text
Define your pillar focus.
```

Pillars:

- Mind
- Sun
- Hydration
- Sleep
- Meal / Nutrition
- Movement
- Daily Stack

Possible actions:

- Increase priority
- Reduce priority
- Disable for now
- Keep recommended

The user should not need to understand the full system.

They should only make simple preference choices.

---

# Step 7 — Upload Documents, Optional

The user may upload documents before activation or skip this step.

Example:

```text
Upload documents or exams?

You can add lab tests, health files or wearable data now or later.
```

Actions:

- Upload now
- Skip for now

The upload area should support:

- Exams
- Reports
- Wearable exports
- Images
- PDFs
- Medication lists
- Supplement lists
- Notes

This step should be optional.

---

# Step 8 — Activate 7-Day Sync Plan

When the user activates the plan, Wellbine should create:

- User profile baseline
- Active plan snapshot
- First Daily flow
- First Push cycle
- Pillar defaults
- Home state
- Initial Sync baseline
- Initial AAI context
- Settings defaults
- Wearable state
- Upload state

Activation copy:

```text
Your 7-Day Sync Plan is active.
```

Next:

```text
Go to Home
```

---

# Step 9 — Enter Home

After Onboarding, the user should land on Home.

Home should show:

- Active Plan
- Current Insight
- Next Best Action
- Pillar states
- Ask Wellbine
- Quick Actions

Example:

```text
Active Plan

LONG40

Next Best Action

Hydrate and prepare your first recovery window.
```

---

# First Activation Mode

If no active plan exists, Home should show First Activation Mode.

Example:

```text
Start your first Wellbine plan.

Choose a plan to activate your Daily, Push and Pillars.
```

Actions:

- Choose Plan
- Ask Wellbine
- Continue Setup

First Activation Mode should be simple.

It should not show a full Home state because the system has not been activated yet.

---

# Progressive Profiling

Wellbine should not ask everything during Onboarding.

Instead, it should learn progressively.

Examples of information collected later:

- Mood patterns
- Meal timing
- Hydration habits
- Movement preference
- Sleep consistency
- Supplement adherence
- Stress patterns
- Recovery response
- Plan friction
- Food preferences
- Push timing preference
- Cycle-related patterns, if applicable
- Wearable trends
- Uploaded document insights

This reduces first-use friction.

---

# Onboarding Questions

Onboarding questions should be:

- Short
- Useful
- Easy to answer
- Connected to plan activation
- Avoid unnecessary detail
- Avoid medical complexity unless user chooses it

Good question:

```text
What is your main focus right now?
```

Bad question:

```text
Fill out your complete health profile before starting.
```

Good question:

```text
How intense should your plan start?
```

Bad question:

```text
Enter your complete weekly training periodization.
```

---

# Onboarding With Ask Wellbine

Ask Wellbine may help during Onboarding.

Possible use cases:

- Help choose a plan
- Explain plan differences
- Adjust preferences
- Translate user intent into a plan suggestion
- Answer questions about how Wellbine works
- Help understand uploaded documents, when available

Example:

```text
Not sure which plan to choose?

Ask Wellbine.
```

Ask Wellbine should not replace the structured Onboarding flow.

It should assist it.

---

# Onboarding And Admin

Onboarding should eventually be admin-configurable.

The admin may define:

- Welcome copy
- Goal options
- Plan suggestions
- Question order
- Required fields
- Optional fields
- Default settings
- Push permission copy
- Mental Detox copy
- Wearable connection copy
- Upload step copy
- Plan preview content
- First Activation Mode copy

This allows the product team to adjust Onboarding without code changes.

---

# Admin-Controlled Onboarding

Onboarding may be managed through:

- Supabase
- Admin Panel

The admin should be able to update basic Onboarding content without redeploying the app.

This includes:

- Text
- Plan order
- Featured plans
- Goal-to-plan mapping
- Optional questions
- Default settings
- Upload options
- Push explanations
- First activation copy

The Onboarding engine should be stable.

The content should be editable.

---

# Onboarding Output

After Onboarding, Wellbine should have:

- User account
- Basic user context
- Selected Plan Template
- User Active Plan Snapshot
- Initial Home state
- Initial Daily flow
- Initial Push logic
- Initial pillar defaults
- Settings defaults
- Wearable status
- Upload status
- First Next Best Action

---

# What Onboarding Should Not Do

Onboarding should not:

- Feel like a long medical intake form
- Require too much data before value
- Force wearable connection
- Force Push permission
- Force full pillar configuration
- Force supplement or medication setup
- Force Store interaction
- Force document upload
- Force long reading
- Become a quiz without activation

Onboarding should activate the system.

---

# Success Criteria

Onboarding is successful when:

- The user understands what Wellbine does
- The user completes basic profile setup
- The user chooses a starting plan
- The user reaches Home quickly
- The user sees a clear Next Best Action
- The system has enough context to start
- The user does not feel overloaded
- The plan can evolve after real behavior

---

# Current Status

Wellbine Onboarding is being defined as the first activation flow connected to Plan Templates, Home, Daily, Push, Pillars, Wearables, Settings and Uploads.

The next implementation priorities are:

- First Activation Mode
- Basic profile setup
- Goal selection
- Recommended Plan logic
- Adapted Plan logic
- Pillar preference Dashboard
- Push permission flow
- Mental Detox Push control
- Wearable optional connection
- Upload environment
- First 7-Day Sync Plan activation
- Home activation state
- Admin-managed Onboarding content

---

# Future Evolution

Future versions of Onboarding may include:

- AI-assisted plan recommendation
- Dynamic question flow
- Region-specific onboarding
- Language-specific onboarding
- Wearable-aware onboarding
- Cycle-aware onboarding when applicable
- Medical-safe optional profile fields
- Plan comparison
- Onboarding analytics
- Drop-off optimization
- Admin-managed onboarding modules
- Personalized first week generation
- Deeper upload interpretation
- Adaptive onboarding based on previous answers

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
- PRODUCTS/WELLBINE/HOME.md
- PRODUCTS/WELLBINE/DAILY.md
- PRODUCTS/WELLBINE/PUSH.md
- PRODUCTS/WELLBINE/PILLARS.md
- PRODUCTS/WELLBINE/STACK.md
