# Push As Orchestration Layer

**Status:** Active

**Date:** July 2026

---

# Context

Wellbine uses Push as one of its most important product surfaces.

Push should not behave like generic reminders.

A generic reminder simply tells the user to do something:

```text
Drink water.
Take your supplement.
Go walk.
Prepare for sleep.
```

This is not enough for Wellbine.

Wellbine is designed to be an adaptive guidance system.

Push should help the user continue the day without needing to open the app all the time.

Push should:

- Ask simple context questions
- Capture user state
- Interpret the answer
- Suggest the next sequence
- Update Daily
- Update Pillars
- Update Home
- Update AAI context
- Continue the user's plan outside the app

Push is not a notification layer only.

Push is an orchestration layer.

---

# Decision

Push is an outside-app orchestration layer for Wellbine.

Push should not be treated as a generic reminder system.

Push should guide the user through contextual checkpoints across the day and connect each answer to the next useful sequence.

Push should operate with simple interactions, but adaptive logic.

The user should be able to respond without opening the app when possible.

---

# Official Rule

```text
Push is not a reminder.
```

```text
Push is an orchestration layer.
```

```text
Push should connect user response to the next adaptive sequence.
```

---

# Core Push Flow

The standard Push flow should follow this logic:

```text
Push asks a simple question

↓

User responds

↓

Wellbine interprets context

↓

The next sequence is adjusted

↓

Daily, Pillars, Home and AAI context are updated
```

Example:

```text
How did you wake up today?

Good
Tired
Very tired
```

If the user selects:

```text
Tired
```

Wellbine may adjust the morning sequence:

```text
Sunlight
Hydration
Light breakfast or coffee
Vitamin B
Omega 3
Gentle activation
Avoid intense HIIT immediately
```

Push should not only remind.

Push should adapt.

---

# Interaction Principle

Push questions should be:

```text
Open in interpretation.
Closed in interaction.
```

This means the question may reveal useful context, but the response should remain simple.

Good example:

```text
How did you wake up today?

Good
Tired
Very tired
```

Bad example:

```text
Describe in detail your sleep, mood, energy, pain level, stress level, dream quality and morning motivation.
```

Push should reduce friction.

The user should be able to answer quickly.

---

# Core Push Actions

Push should support three main actions:

```text
Confirm
Adjust
Later
```

---

# Confirm

Confirm means the user accepts or completes the suggested action.

Confirm should update the system without forcing the user to open the app.

Example:

```text
Morning hydration ready?

Confirm
Adjust
Later
```

If the user taps:

```text
Confirm
```

The system should update:

```text
Hydration pillar
Daily sequence
Home state
AAI context
Plan progress
```

Confirm should be fast.

Confirm should reduce friction.

---

# Adjust

Adjust means the user needs to change the suggested action.

Adjust should open the relevant app screen or adjustment panel.

It should not open a generic Home screen when the context is specific.

Examples:

```text
Adjust hydration
↓
Open Hydration adjustment panel
```

```text
Adjust sleep
↓
Open Sleep planner
```

```text
Adjust Daily Stack
↓
Open Stack adjustment panel
```

```text
Adjust movement
↓
Open Movement adjustment panel
```

Adjust should preserve context.

The user should continue the same flow that started in Push.

---

# Later

Later means the user is not ready now.

Later should log delay and schedule a contextual follow-up.

Default behavior:

```text
Later
↓
Log delay
↓
Follow up about one hour later
```

The follow-up should not shame the user.

Example:

```text
Still a good moment to complete your hydration check?
```

Later should support recovery, not punishment.

---

# Push Cycles

Wellbine should not overload the user with excessive Push notifications.

The default model should use 3 to 4 major Push cycles per day.

Recommended cycles:

```text
Morning Activation
Midday Alignment
Evening Alignment
Night Reset
```

These cycles may vary by plan, user preference, Mental Detox mode and context.

---

# Morning Activation

Morning Activation helps start the day.

Possible functions:

- Ask how the user woke up
- Confirm sleep quality
- Confirm wake state
- Suggest sunlight
- Suggest hydration
- Suggest breakfast or coffee timing
- Suggest Daily Stack timing
- Suggest movement intensity
- Adjust the first Daily sequence

Example:

```text
How did you wake up today?

Good
Tired
Very tired
```

Possible follow-up:

```text
Start with sunlight, hydration and a light activation sequence.
```

---

# Midday Alignment

Midday Alignment helps correct the day while it is still recoverable.

Possible functions:

- Check hydration
- Check meal timing
- Check movement
- Check energy
- Check stress
- Adjust afternoon plan
- Suggest recovery action
- Prevent the user from feeling the day is lost

Example:

```text
How was your hydration this morning?

2+ cups
Less than 2
Forgot
```

Possible follow-up:

```text
Still recoverable. Add 2 cups before your next meal.
```

---

# Evening Alignment

Evening Alignment helps transition the user toward recovery.

Possible functions:

- Check movement
- Check meal timing
- Check Daily Stack
- Check stress
- Suggest light walk
- Suggest recovery sequence
- Suggest lower stimulation
- Prepare sleep window

Example:

```text
How is your energy now?

Stable
Low
Overstimulated
```

Possible follow-up:

```text
Use a lighter evening sequence and start reducing stimulation.
```

---

# Night Reset

Night Reset helps close the day and prepare sleep.

Possible functions:

- Confirm sleep plan
- Confirm wind-down
- Confirm hydration finish
- Confirm Daily Stack completion
- Suggest sleep preparation
- Adjust next morning expectations
- Create tomorrow's starting context

Example:

```text
Ready to start your sleep preparation?

Confirm
Adjust
Later
```

Possible follow-up:

```text
Your target sleep window starts soon. Begin your night reset.
```

---

# Push And BCAS

Push should operate inside BCAS.

BCAS means Wellbine should consider biological context, not only clock time.

Push should account for:

- Wake Window
- Feeding Window
- Movement Window
- Recovery Window
- Sleep Preparation Window
- Hydration Opportunity
- Daily Stack timing

Example:

```text
It is not just 7:00 AM.

It is the user's Wake Window.
```

Example:

```text
It is not just 10:00 PM.

It is the user's Sleep Preparation Window.
```

Push should use timing, but it should not be trapped by rigid time.

---

# Push And AAI

AAI should use Push as a context collection and alignment mechanism.

Push provides important signals:

- Energy
- Sleep quality
- Hydration status
- Meal status
- Movement status
- Stress state
- Recovery state
- User delay
- User resistance
- User preference
- Plan friction
- Completion signals

AAI should use these signals to improve:

- Daily guidance
- Home insights
- Pillar state
- Plan adaptation
- Next Best Action
- Future Push timing
- User personalization

Push is one of the main ways AAI observes and aligns behavior.

---

# Push And Daily

Push should extend Daily outside the app.

Daily is the deeper execution layer.

Push is the outside-app continuation layer.

Example:

```text
Daily defines the sequence.

Push checks and advances the sequence.
```

Push should be able to:

- Start a Daily sequence
- Confirm a Daily action
- Adjust a Daily action
- Delay a Daily action
- Recover a missed window
- Move the user to the next useful step

Push should not operate separately from Daily.

---

# Push And Home

Push should update Home.

When a user responds to Push, Home should reflect the updated state.

Examples:

```text
User confirms hydration
↓
Home updates Hydration pillar
```

```text
User delays movement
↓
Home updates Movement status
```

```text
User reports poor sleep
↓
Home updates Recovery and Next Best Action
```

Home should not ignore Push responses.

Push and Home should share context.

---

# Push And Pillars

Push should connect directly to Pillars.

Current pillars:

- Mind
- Sun
- Hydration
- Sleep
- Meal / Nutrition
- Movement
- Daily Stack

Push may ask questions, confirm actions or open adjustment panels for any pillar.

Example:

```text
Hydration
↓
How was your hydration this morning?
```

Example:

```text
Movement
↓
Ready for a 7-minute activation?
```

Example:

```text
Sleep
↓
Do you want to keep your planned sleep window?
```

Example:

```text
Daily Stack
↓
Confirm your evening stack?
```

Push should make pillars operational outside the app.

---

# Push And Plan Templates

Plan Templates should define starting Push behavior.

A plan may define:

- Active Push cycles
- Push frequency
- Push tone
- Push timing windows
- Pillar priority
- Default questions
- Default response options
- Recovery logic
- Mental Detox defaults
- Daily Stack Push behavior
- Sleep Push behavior
- Hydration Push behavior

The user active plan snapshot may later adapt based on real behavior.

Plan Templates provide the starting configuration.

Push evolves after usage.

---

# Push And Onboarding

Onboarding should explain Push before asking permission.

The user should understand:

- Why Push matters
- What kind of Push Wellbine sends
- That Push can be paused
- That Mental Detox mode exists
- That Push is optional

Push should not feel forced.

If the user denies Push permission, Wellbine should continue to work through:

- Home
- Daily
- Ask Wellbine
- Manual check-ins

The user should be able to enable Push later.

---

# Push And Mental Detox

Mental Detox mode allows the user to reduce or pause Push.

Mental Detox should not punish the user.

Mental Detox may:

- Reduce Push frequency
- Pause non-critical Push
- Keep only essential check-ins
- Disable Push temporarily
- Route guidance through Home instead

Example:

```text
Mental Detox Mode active.

Wellbine will reduce interruptions and keep your plan available inside Home.
```

Mental Detox should protect the user from notification fatigue.

---

# Push And Wearables

Wearables may improve Push personalization.

If wearable data is available, Push may use:

- Sleep duration
- Sleep quality
- Recovery
- Movement
- Inactivity
- Heart rate trends
- Resting heart rate
- HRV
- Stress signals
- Temperature trends
- Respiratory rate
- Oxygen saturation
- Cycle-related signals when supported
- Premenstrual period estimation when supported

If wearable data is not available, Push should rely on:

- User check-ins
- Daily behavior
- Manual input
- Plan settings
- Interaction history

Wearables should improve Push.

Wearables should not be required for Push.

---

# Push And Admin

Admin should be able to configure Push without code changes.

Admin may control:

- Push cycles
- Push copy
- Push timing
- Push response options
- Push frequency
- Push tone
- Push deep links
- Confirm behavior
- Adjust behavior
- Later behavior
- Mental Detox behavior
- Plan-specific Push
- Pillar-specific Push
- Recovery Push
- Daily Stack Push

Admin should allow fast iteration.

Push should be database-driven where practical.

---

# Push Frequency Rule

Push should be useful, not annoying.

Default recommendation:

```text
3 to 4 major Push cycles per day
```

Additional Push messages may exist only when justified by:

- User request
- Plan priority
- Safety-relevant routine
- Daily Stack timing
- Sleep window
- Recovery state
- Explicit user preference
- Admin configuration

Push should not become spam.

---

# Push Recovery Language

Push should avoid guilt-based language.

Avoid:

```text
You missed it.
You failed.
You lost the day.
Too late.
```

Prefer:

```text
Still recoverable.
Continue from here.
Next best action.
Window closed, next opportunity.
```

Push should help the user recover the day.

It should not create shame.

---

# Push Deep Linking

Push should deep-link to the correct context.

Examples:

```text
Adjust hydration
↓
Hydration panel
```

```text
Adjust sleep
↓
Sleep planner
```

```text
Adjust stack
↓
Daily Stack panel
```

```text
Adjust movement
↓
Movement panel
```

```text
View summary
↓
Adaptive Summary
```

```text
Start Daily
↓
Daily sequence
```

Push should not always open generic Home.

The destination should match the action.

---

# Consequences

This decision means:

- Push becomes a core product surface.
- Push is not just a notification layer.
- Push must connect to Daily, Home, Pillars and AAI.
- Push responses must update system state.
- Push must support Confirm, Adjust and Later.
- Push must support contextual deep links.
- Push should operate with 3 to 4 major cycles per day.
- Push should respect Mental Detox mode.
- Push should adapt based on user answers.
- Push should support recovery language.
- Admin should be able to configure Push behavior.
- Plan Templates should define starting Push logic.

---

# What This Prevents

This decision prevents:

- Push becoming generic reminders
- Excessive notification spam
- Push being disconnected from Daily
- Push being disconnected from Home
- Push being disconnected from Pillars
- User answers being ignored
- Adjust opening irrelevant screens
- Later being treated as failure
- Push becoming rigid clock-based messages only
- Push depending completely on wearables
- Push becoming hardcoded and difficult to update

---

# Related Documents

- README.md
- ARCHITECTURE_DECISIONS/README.md
- ARCHITECTURE_DECISIONS/HOME_CENTRAL.md
- PRODUCTS/WELLBINE/README.md
- PRODUCTS/WELLBINE/PUSH.md
- PRODUCTS/WELLBINE/DAILY.md
- PRODUCTS/WELLBINE/HOME.md
- PRODUCTS/WELLBINE/PILLARS.md
- PRODUCTS/WELLBINE/PLAN_TEMPLATES.md
- PRODUCTS/WELLBINE/ONBOARDING.md
- PRODUCTS/WELLBINE/ADMIN.md
- PRODUCTS/WELLBINE/BCAS.md
