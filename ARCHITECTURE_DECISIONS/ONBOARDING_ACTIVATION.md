# Onboarding As First Activation Flow

**Status:** Active

**Date:** July 2026

---

# Context

Wellbine should not treat onboarding as a simple registration form.

A traditional onboarding flow usually collects account information, asks a few questions and then sends the user into a generic app screen.

That is not enough for Wellbine.

Wellbine is designed to operate as an adaptive daily guidance system.

For this reason, onboarding must do more than collect data.

Onboarding must activate the first usable version of the Wellbine experience.

It should move the user from a blank state into an active operating state with:

- Basic profile context
- Primary goal
- Recommended or Adapted Plan
- Initial pillar preferences
- Optional wearable connection
- Optional Push activation
- Optional document upload
- First 7-Day Sync Plan
- Active Home state
- Current Insight
- Next Best Action

Onboarding is the first activation flow of Wellbine.

---

# Decision

Onboarding is the first activation flow of Wellbine.

Onboarding should not be treated as a long questionnaire, a passive intake form or a generic account setup.

Onboarding should collect only the essential context needed to activate the first user experience.

After onboarding, the user should enter Home with an active plan, visible guidance and a clear Next Best Action.

---

# Official Rule

```text
Onboarding is not just registration.
```

```text
Onboarding is the first activation flow of Wellbine.
```

```text
Onboarding should move the user from blank state to active plan state.
```

---

# Rationale

Wellbine needs to deliver value quickly.

The user should not feel like they are filling out a medical form before seeing the product work.

The system should collect enough information to start, then continue learning progressively through:

- Push check-ins
- Daily behavior
- Home interactions
- Ask Wellbine
- Pillar adjustments
- Wearable data
- Uploaded documents
- User feedback
- Plan evolution

This approach reduces friction.

It also matches the AAI principle of adapting over time instead of assuming that all context must be known immediately.

---

# Core Activation Flow

The onboarding activation flow should follow this direction:

```text
Welcome
↓
Basic profile baseline
↓
Optional wearable connection
↓
Push and Mental Detox explanation
↓
Optional Push activation
↓
Primary goal selection
↓
Recommended Plan or Adapted Plan
↓
Pillar preference Dashboard
↓
Optional document upload
↓
Activate 7-Day Sync Plan
↓
Enter Home
```

This flow may evolve, but the purpose should remain the same:

```text
Activate the first usable Wellbine experience.
```

---

# Profile Baseline

Onboarding should first collect essential profile context.

Recommended baseline:

- Name
- Biological sex
- Age
- Height
- Weight
- Relevant comorbidities

The profile baseline should be short.

It should not become a full medical intake.

The goal is to create enough context for a safe and useful initial recommendation.

---

# Biological Sex

Biological sex may be collected as a physiological personalization field.

Possible options:

- Female
- Male
- Prefer not to say

This field may support personalization related to:

- Recovery
- Cycle-related insights when applicable
- Premenstrual period estimation when supported
- Energy patterns
- Sleep context
- Health context

This should not be treated as an identity statement.

It should be handled as a physiological field for personalization.

---

# Relevant Comorbidities

Relevant comorbidities may be collected carefully.

Possible options:

- None
- Yes
- Prefer not to say

If the user selects Yes, the app may allow structured selection or free text.

This information should support safer personalization.

It should not turn onboarding into medical diagnosis.

---

# Recommended Plan

Onboarding should support a Recommended Plan.

A Recommended Plan is an initial preconfigured plan suggested by Wellbine based on the user profile and goals.

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
Recommended Plan:

LONG40
```

The logic, available plans and plan names should be admin-managed.

The recommendation may consider:

- User goal
- Biological sex
- Age
- Height
- Weight
- Relevant comorbidities
- Preferences
- Available Plan Templates
- Admin-defined mapping
- Future AAI recommendation logic

---

# Adapted Plan

Onboarding should also support an Adapted Plan.

An Adapted Plan allows the user to adjust the starting plan before activation.

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

The user should not need to build everything manually.

Adapted Plan should start from a template and allow simple adjustments.

---

# Pillar Preference Dashboard

After selecting a Recommended Plan or Adapted Plan, the user should be able to adjust pillar preferences.

Current pillars:

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

These preferences should update the user active plan snapshot.

They should not modify the original Plan Template.

---

# Wearable Connection

Wearable connection should be optional.

The user should be invited to connect a wearable, but the product should not block activation if the user skips it.

Preferred logic:

```text
Connect wearable
↓
Use wearable signals when available
```

```text
Skip wearable
↓
Use Push check-ins, manual input and Daily behavior
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
- Temperature trends when supported
- Respiratory rate trends when supported
- Oxygen saturation trends when supported
- Push personalization
- Automatic context detection

Wearables should improve automation.

They should not be required for value.

---

# Push Activation

Onboarding should explain Push before requesting permission.

Push should not feel forced.

The user should understand:

- What Wellbine Push does
- Why Push matters
- That Push is optional
- That Push can be paused
- That Mental Detox mode exists
- That the app still works without Push

If Push is enabled, Wellbine can activate outside-app orchestration.

If Push is denied, Wellbine should still work through:

- Home
- Daily
- Ask Wellbine
- Manual check-ins

The user should be able to enable Push later.

---

# Mental Detox Explanation

Onboarding should explain Mental Detox before asking for Push permission.

Mental Detox gives the user control over interruptions.

The user should be able to:

- Pause Push
- Reduce Push frequency
- Disable Push
- Enable Mental Detox mode
- Reactivate Push later

Mental Detox should not punish the user.

It should reduce interruption while preserving the plan inside Home and Daily.

---

# Upload Environment

Onboarding should offer an optional upload environment.

The user may upload:

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

Upload should be optional.

Upload should not block activation.

Uploaded files may improve personalization, but the user should be able to start without them.

---

# First 7-Day Sync Plan

Onboarding should activate the first 7-Day Sync Plan.

The 7-Day Sync Plan is the user's first operational plan cycle.

Activation should create:

- User profile baseline
- Active plan snapshot
- Initial Home state
- Initial Daily flow
- Initial Push logic
- Pillar defaults
- Settings defaults
- Wearable state
- Upload state
- Initial AAI context
- First Current Insight
- First Next Best Action

After activation, the user should land on Home.

---

# Relationship With Home

Onboarding should activate Home.

If no active plan exists, Home should show First Activation Mode.

After onboarding, Home should show:

- Active Plan
- Current Insight
- Next Best Action
- Pillar states
- Adaptive Summary
- Ask Wellbine
- Quick Actions

Home should not be blank after onboarding.

The user should immediately understand what to do next.

---

# Relationship With Daily

Onboarding should activate the first Daily flow.

Daily should receive:

- First day sequence
- Current plan
- Pillar defaults
- First active windows
- Recovery logic
- Daily Stack defaults when applicable
- Hydration defaults
- Sleep planning defaults
- Movement defaults
- Meal / Nutrition defaults
- Mind defaults
- Sun defaults

Daily should not require manual configuration after onboarding.

---

# Relationship With Push

Onboarding should activate Push logic if permission is granted.

Push should then operate as an orchestration layer.

Onboarding should define the starting Push state:

- Enabled or disabled
- Frequency preference
- Mental Detox preference
- Initial Push cycles
- Plan-specific Push logic
- Pillar-specific Push logic

If Push is disabled, the system should preserve the same logic inside Home and Daily where possible.

---

# Relationship With Plan Templates

Onboarding depends on Plan Templates.

The user should not build the product experience from zero.

Plan Templates provide the starting structure.

Onboarding selects, recommends or adapts the plan.

Plan activation should create a user active plan snapshot.

The original Plan Template should remain unchanged.

---

# Relationship With Admin

Onboarding should be admin-configurable.

Admin may control:

- Welcome copy
- Profile questions
- Goal options
- Recommended Plan logic
- Adapted Plan options
- Wearable connection copy
- Push permission copy
- Mental Detox explanation
- Upload step copy
- Pillar preference Dashboard
- Plan preview copy
- First Activation Mode copy
- First 7-Day Sync Plan activation copy

Normal onboarding changes should not require code changes.

---

# Relationship With AAI

AAI should use onboarding as the first structured context layer.

Onboarding provides initial signals.

AAI should treat onboarding data as a starting point, not a permanent truth.

The system should evolve as the user interacts with:

- Push
- Home
- Daily
- Pillars
- Wearables
- Uploads
- Ask Wellbine
- Settings
- Plan adjustments

Onboarding starts the intelligence loop.

It does not complete it.

---

# Relationship With BCAS

Onboarding should support BCAS by collecting enough context to initialize biological guidance.

Useful starting context may include:

- Wake preference
- Sleep preference
- Meal preference
- Movement preference
- Hydration preference
- Recovery need
- Fasting preference
- Daily rhythm
- Biological sex
- Age
- Weight
- Wearable status

BCAS should later adapt based on real behavior.

Onboarding creates starting assumptions.

BCAS improves them over time.

---

# Progressive Profiling

Onboarding should follow progressive profiling.

This means Wellbine should collect the minimum necessary information first and learn more later.

Do not ask everything upfront.

More details may be collected later through:

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

This reduces friction and increases activation.

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
- Send the user into a blank app state

Onboarding should activate the system.

---

# Consequences

This decision means:

- Onboarding becomes a core product flow.
- Onboarding must activate the first user experience.
- Onboarding must connect to Plan Templates.
- Onboarding must create a user active plan snapshot.
- Onboarding must initialize Home.
- Onboarding must initialize Daily.
- Onboarding must initialize Push when enabled.
- Onboarding must initialize Pillar defaults.
- Onboarding must support optional wearable connection.
- Onboarding must support optional upload.
- Onboarding must support Recommended Plan and Adapted Plan.
- Onboarding must remain short and action-oriented.
- Onboarding should be configurable through Admin.

---

# What This Prevents

This decision prevents:

- Onboarding becoming only registration
- Onboarding becoming a long questionnaire
- Users reaching a blank Home
- Users needing to build a plan manually from zero
- Wearables being required for activation
- Push being forced
- Uploads blocking activation
- Plan Templates being disconnected from user activation
- Daily starting without context
- Pillars starting without priority
- Admin being unable to update onboarding content
- AAI starting without structured initial context

---

# Related Documents

- README.md
- ARCHITECTURE_DECISIONS/README.md
- ARCHITECTURE_DECISIONS/HOME_CENTRAL.md
- ARCHITECTURE_DECISIONS/PUSH_ORCHESTRATION.md
- ARCHITECTURE_DECISIONS/PLAN_TEMPLATES_DB.md
- ARCHITECTURE_DECISIONS/ADMIN_CONTROL_LAYER.md
- PRODUCTS/WELLBINE/README.md
- PRODUCTS/WELLBINE/ONBOARDING.md
- PRODUCTS/WELLBINE/PLAN_TEMPLATES.md
- PRODUCTS/WELLBINE/HOME.md
- PRODUCTS/WELLBINE/DAILY.md
- PRODUCTS/WELLBINE/PUSH.md
- PRODUCTS/WELLBINE/PILLARS.md
- PRODUCTS/WELLBINE/ADMIN.md
- PRODUCTS/WELLBINE/BCAS.md
