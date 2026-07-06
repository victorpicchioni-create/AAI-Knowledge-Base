# Wellbine Pillars

**Version:** 0.1.0

**Status:** Active

**Last Updated:** July 2026

---

# Purpose

This document defines the operational pillars of Wellbine.

The pillars are not just icons, habits or visual categories.

The pillars are operational behavior modules connected to AAI, BCAS, Wellbine Daily and Push.

Each pillar can collect context, guide actions, receive confirmation, update Daily, influence Sync and support recovery logic.

---

# Official Definition

**Wellbine Pillars are operational modules that organize the user's daily health, performance and longevity behaviors into context-aware systems.**

---

# Core Principle

A pillar is not a visual shortcut.

A pillar is an operational system.

Each pillar may:

- Appear in Wellbine Daily
- Be included in Push sequences
- Use Confirm / Adjust / Later logic
- Collect user feedback
- Update internal state
- Influence Sync
- Influence Recovery
- Feed AAI learning
- Adapt to biological context
- Work without requiring the user to open the app

---

# Current Pillars

The current Wellbine pillars are:

- Mind
- Sun
- Hydration
- Sleep
- Meal / Nutrition
- Movement
- Daily Stack

These pillars may evolve over time, but this is the current official structure.

---

# Relationship With AAI

AAI uses the pillars to understand the user's daily reality.

The pillars provide structured signals about:

- Behavior
- Energy
- Recovery
- Nutrition
- Sleep
- Hydration
- Movement
- Mental state
- Supplement and medication adherence
- Routine friction
- User preferences

AAI should not treat pillars as isolated checkboxes.

AAI should understand how the pillars interact.

Example:

Poor sleep may affect movement intensity.

Late meal may affect sleep quality.

Low hydration may affect energy and recovery.

Strong movement may increase hydration and recovery needs.

---

# Relationship With BCAS

The pillars operate through BCAS.

This means pillar actions should be guided by biological context, not only fixed clock time.

Examples:

- Sun belongs mainly to the Wake Window or Morning Reset.
- Meal belongs to Feeding Windows.
- Movement depends on energy, readiness and recovery.
- Sleep belongs to Sleep Preparation and Recovery logic.
- Hydration may be active throughout the day but measured through simple checkpoints.
- Daily Stack depends on timing, food, protocol and user plan.
- Mind may activate during stress, focus, recovery or sleep preparation.

Clock time may help trigger actions, but biological context should define relevance.

---

# Relationship With Daily

Wellbine Daily is the execution layer.

Pillars appear in Daily as:

- Current context
- Next Best Action
- Daily Flow item
- Pending action
- Completed action
- Recovery opportunity
- Protocol adjustment
- Push sequence result

Daily should not show pillars as a static checklist.

Daily should show what matters now.

---

# Relationship With Push

Push is the outside-app orchestration layer for pillars.

Pillar actions should be included in the 3 to 4 main Push cycles of the day.

Default daily Push cycles:

1. Morning Activation
2. Midday Alignment
3. Evening Alignment
4. Night Reset

Push should avoid many isolated notifications.

Instead, Push should collect context and suggest the next sequence of pillar actions.

Example:

```text
Good morning, Victor.

How did you wake up today?

Rested
Okay
Tired
```

Then:

```text
Your morning plan:

10 min sunlight
Breakfast
Vitamin B
Omega 3
Hydration
15 min HIIT

Ok?

Confirm
Adjust
Later
```

---

# Confirm / Adjust / Later Logic

All pillars may use the same default Push action logic.

---

## Confirm

Confirm accepts the proposed sequence.

The app should not open.

The system should update the related internal pillar states automatically.

Possible updates:

- Pillar marked as done
- Pillar marked as planned
- Pillar marked as active
- Daily Flow updated
- Sync updated
- Recovery estimate updated
- AAI learning updated

Confirm should reduce friction.

---

## Adjust

Adjust opens the app directly on the relevant adjustment screen.

Adjust means the user wants to modify the proposed sequence.

The user may need to:

- Change timing
- Change intensity
- Change meal
- Change protocol
- Change sleep plan
- Change Stack item
- Remove an action
- Select a lighter option
- Edit what was completed

Adjust should not open the generic Home screen.

It should open the specific screen related to that pillar or sequence.

---

## Later

Later does not open the app.

Later registers a delay and schedules a follow-up Push.

Default follow-up timing:

**Approximately 1 hour later**

If the biological context changes before the follow-up, AAI may adjust the next recommendation.

Later should never be treated as failure.

---

# Pillar States

Each pillar may use the following states:

- Done
- Active
- Pending
- Upcoming
- Adjusted
- Partial
- Window Closed
- Locked
- Skipped

Avoid punitive states.

Do not use:

- Failed
- Bad
- Penalty
- Lost
- Missed

Preferred language:

- Window Closed
- Still Recoverable
- Continue From Here
- Adjusted
- Partial
- Next Best Action

---

# 1. Mind

Mind is the pillar responsible for mental state, breathing, meditation, focus, stress regulation and emotional reset.

Mind may support:

- Stress reduction
- Focus
- Breathing
- Meditation
- Emotional reset
- Sleep preparation
- Recovery
- Short pauses during the day

Mind should not feel like a generic meditation library.

Mind should offer context-aware mental regulation.

Example Push:

```text
How is your state of mind right now?

Calm
Anxious
Overwhelmed

```

Possible follow-up:

```text
Quick reset plan:

3 min breathing
Screen pause
Hydration

Ok?

Confirm
Adjust
Later
```

Mind may appear in:

- Morning Activation
- Midday Alignment
- Recovery Window
- Night Reset
- Sleep Preparation Window

---

# 2. Sun

Sun is the pillar responsible for natural light exposure and circadian anchoring.

Sun may support:

- Morning energy
- Circadian rhythm
- Mood
- Sleep quality
- Day activation
- Biological alignment

Sun should be simple.

The user should not need to track sunlight in a complex way.

Example Push:

```text
Your morning plan:

10 min sunlight
Hydration
Breakfast
Daily Stack

Ok?

Confirm
Adjust
Later
```

Sun may be marked as done through:

- Manual confirmation
- Push confirmation
- Future wearable or location context
- Morning plan confirmation

Sun is mainly related to:

- Wake Window
- Morning Reset
- Sleep quality
- Energy regulation

---

# 3. Hydration

Hydration is the pillar responsible for fluid balance through simple serving-based tracking, context-aware reminders and protocol-based hydration support.

Hydration should not be a rigid milliliter-per-hour calculator.

The main user-facing unit should be:

**Cups**

The internal system may estimate:

```text
1 cup ≈ 250 ml
```

But the user should not be forced to think in milliliters.

---

## Hydration Units

Default rule:

```text
Water = cups

Electrolytes / functional hydration items = doses
```

Use **cups** for water.

Use **doses** for electrolytes, functional compounds or hydration-related supplements.

---

## Hydration Push Logic

Hydration should be included inside the main daily Push cycles.

It should not generate many isolated hourly reminders by default.

Morning example:

```text
Your morning plan:

10 min sunlight
Breakfast
Vitamin B
Omega 3
Hydration
15 min HIIT

Ok?

Confirm
Adjust
Later
```

Midday check-in:

```text
How was your hydration this morning?

2+ cups
Less than 2
Forgot
```

Evening check-in:

```text
How is your hydration today?

5+ cups
3+ cups
Forgot
```

Night check-in, if needed:

```text
How did your hydration finish today?

6+ cups
3+ cups
Low
```

---

## Hydration Panel

The Hydration pillar panel may include:

- Daily cup goal
- Cups consumed today
- Simple history
- Electrolytes enabled / disabled
- Functional drinks enabled / disabled
- Juice enabled / disabled
- Protocol-based hydration rules
- Manual adjustment
- Fasting support
- Training support
- Heat or climate support in the future

The user should not need to open the Hydration panel every day.

The pillar should still work through Push and Daily.

---

## Hydration Protocol Awareness

Hydration should adapt to the user's current protocol.

Examples:

### Normal Day

- Water active
- Electrolytes optional
- Functional drinks optional

### Fasting

- Water active
- Electrolytes active if included in the plan
- Caloric drinks disabled during fasting window
- Juice disabled during fasting window

### Strong Movement Day

- Water active
- Electrolytes active or suggested
- Post-movement hydration emphasized

### Weight Loss Protocol

- Water active
- Juice limited or disabled
- Electrolytes depending on context

The user may manually adjust these settings.

---

# 4. Sleep

Sleep is the pillar responsible for planning, guiding and tracking sleep through ideal bedtime, wake time, estimated recovery impact and optional phone alarm synchronization.

Sleep should not only ask how the user slept.

Sleep should help the user plan sleep before the night happens.

---

## Sleep Planning

The Sleep pillar should suggest:

- Ideal bedtime
- Ideal wake time
- Estimated sleep duration
- Estimated Recovery impact
- Night Reset sequence

Example:

```text
Ideal Sleep Plan

Go to bed: 23:30
Wake up: 07:00

Estimated sleep: 7h30
Recovery: 100%
```

---

## Manual Adjustment

The user may adjust bedtime and wake time manually.

Example:

```text
Adjusted Sleep Plan

Go to bed: 00:30
Wake up: 06:30

Estimated sleep: 6h00
Recovery: 70%
```

The system should recalculate Recovery in real time.

---

## Recovery Zones

Sleep Recovery may use three main zones.

### Green Zone

```text
7h+ sleep opportunity

Recovery 90–100%
```

Meaning:

```text
Ideal recovery window.
```

---

### Yellow Zone

```text
6h–7h sleep opportunity

Recovery 70–89%
```

Meaning:

```text
Acceptable, but not ideal.
```

---

### Orange Zone

```text
Less than 6h sleep opportunity

Recovery 40–69%
```

Meaning:

```text
Recovery will likely be reduced tomorrow.
```

Avoid showing negative recovery language such as:

```text
Recovery -60%
```

Preferred:

```text
Recovery 60%
```

or:

```text
High Recovery Impact
```

---

## Phone Alarm Sync

Sleep should include optional phone alarm synchronization.

Example setting:

```text
Sync with phone alarm

Enabled / Disabled
```

If enabled, Wellbine should attempt to create or update the phone alarm based on the selected wake time.

If disabled, Wellbine only suggests the sleep plan and does not change the phone alarm.

Product rule:

**Wellbine should support automatic alarm adjustment when allowed by the user's device and operating system.**

The system must respect operating system limitations and user permissions.

---

## Sleep Push Example

Night Push:

```text
Your ideal sleep plan:

Bed: 23:30
Wake: 07:00
Recovery: 100%

Confirm
Adjust
Later
```

Confirm:

- Confirms sleep plan
- Updates Sleep pillar
- Activates Night Reset
- Updates Daily
- Adjusts phone alarm if enabled and allowed

Adjust:

- Opens Sleep adjustment screen
- User changes bedtime or wake time
- Recovery recalculates

Later:

- Registers delay
- Sends follow-up Push approximately one hour later
- Recalculates Recovery if sleep opportunity changes

---

# 5. Meal / Nutrition

Meal / Nutrition is the pillar responsible for meals, nutrition protocols, food timing, meal feedback and post-meal response.

Meal / Nutrition is one of the most complex pillars.

It should not behave like a simple food diary.

It should guide eating behavior according to the user's protocol, biological context and daily plan.

Meal / Nutrition may support:

- Breakfast
- Lunch
- Dinner
- Snacks
- Fasting
- OMAD
- Low carb
- Keto
- Vegetarian
- Weight loss protocols
- Performance protocols
- Recovery protocols
- Post-meal feedback
- Meal planning
- Meal adjustment

---

## Meal Context

Meal / Nutrition should respect Feeding Windows and user protocol.

Example:

If the user is fasting, Wellbine should not suggest a meal during the fasting window.

Instead:

```text
How is your fasting window feeling?

Easy
Manageable
Hard
```

Then:

```text
Fasting support plan:

Hydration
Electrolytes, if scheduled
Light walk
No food suggestions now

Ok?

Confirm
Adjust
Later
```

---

## Meal Push Examples

Midday Push:

```text
How did your morning plan go?

Complete
Partial
Not today
```

Then:

```text
Your midday plan:

Planned lunch
Hydration
Post-meal walk
3 min reset meditation

Ok?

Confirm
Adjust
Later
```

Post-meal feedback:

```text
How did your last meal feel?

Light
Heavy
Still hungry
```

This answer may help infer:

- Meal size
- Satiety
- Digestion
- Energy stability
- Possible glucose response
- Need for walking
- Dinner adjustment

---

## Meal Adjustment

Adjust should open the relevant Meal screen.

The user may need to:

- Change meal
- Skip meal
- Register fasting
- Change protocol
- Mark meal as completed
- Mark meal as partial
- Add feedback
- Choose lighter option
- Add post-meal walk

Meal / Nutrition should influence:

- Energy
- Recovery
- Sleep
- Movement
- Hydration
- Sync

---

# 6. Movement

Movement is the pillar responsible for physical activity, training, walking, strength, mobility, HIIT, recovery movement and sedentary breaks.

Movement should not only track workouts.

It should help the user choose the right movement intensity for the current biological context.

Movement may support:

- Strong movement
- Light movement
- Walking
- HIIT
- Strength
- Mobility
- Stretching
- Post-meal walk
- Sedentary break
- Recovery movement

---

## Movement Readiness

Movement should adapt to:

- Sleep quality
- Energy
- Recovery
- Stress
- Hydration
- Meal timing
- Wearable data
- User feedback

Example Push:

```text
How does your body feel now?

Ready
Tense
Drained
```

If Ready:

```text
Your evening plan:

Strong movement
Hydration
Light dinner
Short cooldown

Ok?

Confirm
Adjust
Later
```

If Drained:

```text
Your recovery evening:

Light movement
Hydration
Simple dinner
No intense workout
5 min breathing

Ok?

Confirm
Adjust
Later
```

Movement should support recovery, not punishment.

---

# 7. Daily Stack

Daily Stack is the pillar responsible for medications, vitamins, supplements, nutraceuticals and functional items.

Daily Stack may include:

- Medications
- Vitamins
- Supplements
- Nutraceuticals
- Electrolytes
- Functional compounds
- Protein
- Sleep support items
- Recovery support items

Daily Stack should support:

- Dosage
- Timing
- Context Window
- With food / without food
- Photos
- Notes
- Stock control
- Refill reminders
- Push confirmation
- Protocol rules

Example Push:

```text
Your morning stack:

Vitamin B
Omega 3
Hydration

Ok?

Confirm
Adjust
Later
```

Confirm:

- Marks Stack sequence as accepted or completed
- Updates Daily Stack pillar
- Updates Daily Flow
- Updates stock if needed
- Feeds AAI learning

Adjust:

- Opens Daily Stack adjustment screen

Later:

- Sends follow-up Push approximately one hour later

---

## Safety Rule

Daily Stack is not a prescription system.

Wellbine should not prescribe medications.

For medications, the system should use careful language.

Preferred:

- Registered medication
- Scheduled medication
- Confirm if taken
- Follow your medical prescription
- Consult your doctor before changes

Avoid:

- Increase your dosage
- Stop this medication
- You should take this medication

---

# Pillars And Sync

Pillars contribute to the user's Sync.

Sync should represent overall alignment, not perfection.

A user can recover a day even after missing or delaying actions.

Sync should consider:

- Completed actions
- Partial completion
- Recovery actions
- Context relevance
- User effort
- Protocol adherence
- Sleep opportunity
- Hydration trend
- Movement readiness
- Meal consistency
- Mind regulation
- Daily Stack adherence

Avoid harsh penalties.

The system should communicate recovery paths.

---

# Pillars And Recovery

Every pillar should support recovery logic.

If a pillar action is delayed, skipped or partially completed, the system should ask:

**What is still useful now?**

Example:

Instead of:

```text
Hydration missed.
```

Use:

```text
You can still stabilize today.

Drink water now?
```

Instead of:

```text
Workout failed.
```

Use:

```text
Your body looks drained.

Choose a lighter movement plan?
```

Recovery is part of the product.

It is not an exception.

---

# Pillars And Home

Home should display pillar information only when relevant.

Home should not become a dashboard of all pillars.

Home should show:

- Current Context
- Next Best Action
- Relevant pillar state
- Recovery opportunity
- Sync status
- Ask Wellbine

The user should not need to interpret every pillar every time the app opens.

Home answers:

**What matters now?**

---

# Pillars And Wearables

Wearables may improve pillar automation.

With wearable data, Wellbine may infer:

- Sleep duration
- Sleep quality
- Recovery
- Movement
- Inactivity
- Stress
- Readiness
- Energy patterns

Without wearables, Wellbine should still work through:

- Push answers
- Manual input
- Interaction history
- Protocol settings
- Daily behavior

Wearables improve automation.

They should not be required for value.

---

# What Pillars Are Not

Pillars are not icons only.

Pillars are not static habits.

Pillars are not disconnected trackers.

Pillars are not a punishment system.

Pillars are not a dashboard category.

Pillars are not required to be opened every day.

Pillars are operational systems.

---

# Current Status

The Wellbine pillar system is being redesigned as a set of operational behavior modules connected to AAI, BCAS, Daily and Push.

The next implementation priorities are:

- Operational pillar definition
- Pillar states
- Push integration
- Daily integration
- Confirm / Adjust / Later logic
- Hydration redesign
- Sleep planning logic
- Meal / Nutrition complexity
- Movement readiness
- Daily Stack support
- Sync and Recovery integration

---

# Future Evolution

Future versions of the pillar system may include:

- Deeper individual pillar documents
- Advanced Meal / Nutrition engine
- Personalized Sleep optimization
- Automatic alarm integration
- Wearable-based readiness
- Adaptive hydration targets
- AI-guided movement planning
- Supplement and medication safety rules
- Context-aware pillar weighting
- Personalized Sync calculation
- Fully adaptive daily plan generation

---

# Related Documents

- FOUNDATION/AAI_CONSTITUTION.md
- FOUNDATION/AAI_GLOSSARY.md
- FOUNDATION/AAI_PRINCIPLES.md
- FRAMEWORKS/POPAE.md
- PRODUCTS/WELLBINE/README.md
- PRODUCTS/WELLBINE/PRODUCT.md
- PRODUCTS/WELLBINE/BCAS.md
- PRODUCTS/WELLBINE/HOME.md
- PRODUCTS/WELLBINE/DAILY.md
- PRODUCTS/WELLBINE/PUSH.md
- PRODUCTS/WELLBINE/STACK.md
