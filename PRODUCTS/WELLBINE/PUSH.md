# Wellbine Push

**Version:** 0.1.0

**Status:** Active

**Last Updated:** July 2026

---

# Purpose

This document defines the Push system of Wellbine.

Push is not a generic reminder layer.

Push is an operational extension of Adaptive Alignment Intelligence (AAI), designed to guide the user throughout the day with a small number of intelligent, context-aware interactions.

The objective is not to send more notifications.

The objective is to send fewer, smarter and more useful Push sequences.

---

# Official Definition

**Wellbine Push is the interactive daily orchestration layer that allows AAI to collect context, interpret the user's state and deliver the next sequence of actions without requiring the app to be opened.**

---

# Core Objective

The objective of Wellbine Push is to help the user move through the day with minimal cognitive effort.

A good Push should:

- Collect useful context.
- Interpret previous behavior.
- Suggest the next action sequence.
- Reduce the need to open the app.
- Update Wellbine Daily.
- Feed AAI learning.
- Support recovery without punishment.

Push should not behave like isolated reminders.

Push should behave like short intelligent checkpoints.

---

# Push Cadence

Wellbine should use a small number of Push cycles per day.

Default target:

**3 to 4 main Push cycles per day.**

Preferred daily structure:

1. Morning Activation
2. Midday Alignment
3. Evening Alignment
4. Night Reset

This cadence may adapt based on:

- User preferences
- Wearable availability
- Recovery state
- Protocol mode
- Notification fatigue
- User engagement
- Current biological context

The system should avoid sending many isolated notifications throughout the day.

---

# Push Cycle Structure

Each Push cycle should follow a simple sequence.

```text
Context Question

↓

User Response

↓

AAI Interpretation

↓

Next Action Sequence

↓

User Confirmation

↓

Daily Flow Update
```

A Push cycle may include one initial question and one follow-up plan.

The follow-up plan should summarize the next sequence of actions.

The user should be able to confirm, adjust or delay.

---

# Core Principle

Push should not ask isolated questions unless the answer directly improves the next sequence.

Bad logic:

```text
Did you drink water?

Yes
No
```

Better logic:

```text
Good morning, Victor.

How did you wake up today?

Rested
Okay
Tired
```

Then, after the response:

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

This structure is stronger because the first answer informs the next plan.

---

# Daily Push Architecture

Wellbine Push should be organized around four major daily cycles.

---

# 1. Morning Activation

The Morning Activation Push starts the day.

Its purpose is to understand the user's wake state and deliver the morning plan.

---

## Morning Context Question

Example:

```text
Good morning, Victor.

How did you wake up today?

Rested
Okay
Tired
```

This answer may help infer:

- Sleep quality
- Recovery state
- Previous-day intensity
- Late eating
- Stress
- Screen exposure
- Sleep duration
- Readiness for exercise
- Need for lower intensity

---

## Morning Plan Push

After the user responds, AAI should deliver the morning sequence.

Example:

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

The plan should adapt to the user's answer.

Example:

If the user answers **Tired**, the plan may change:

```text
Your recovery plan:

Hydration
10 min sunlight
Light breakfast
Vitamin B
Omega 3
5 min breathing
Skip HIIT for now

Ok?

Confirm
Adjust
Later
```

---

# 2. Midday Alignment

The Midday Alignment Push happens before or around lunch.

Its purpose is to review the morning, identify what was completed and deliver the lunch / early afternoon plan.

---

## Midday Review Question

Example:

```text
How did your morning plan go?

Complete
Partial
Not today
```

This answer helps AAI understand:

- Morning adherence
- Energy consistency
- Friction points
- Recovery needs
- Whether the daily plan should be adjusted

---

## Midday Plan Push

After the response, Wellbine sends the next sequence.

Example:

```text
Your midday plan:

Planned lunch
Hydration
Post-meal walk
Magnesium reminder, if scheduled
3 min reset meditation

Ok?

Confirm
Adjust
Later
```

If the morning was partial, the plan may include recovery:

```text
You can still stabilize today.

Midday recovery plan:

Planned lunch
Hydration
5 min walk
Complete missing Daily Stack item
3 min breathing

Ok?

Confirm
Adjust
Later
```

---

# 3. Evening Alignment

The Evening Alignment Push happens late afternoon or early evening.

Its purpose is to guide movement, hydration and dinner decisions.

---

## Evening Context Question

Example:

```text
How does your body feel now?

Ready
Tense
Drained
```

This answer may help infer:

- Readiness for strong movement
- Stress accumulation
- Recovery state
- Hydration need
- Need for lower intensity
- Dinner strategy

---

## Evening Plan Push

After the response, Wellbine sends the evening sequence.

Example:

```text
Your evening plan:

Strong movement
Hydration
Light dinner
Protein focus
Short cooldown

Ok?

Confirm
Adjust
Later
```

If the user answers **Drained**, the plan changes:

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

---

# 4. Night Reset

The Night Reset Push happens before sleep.

Its purpose is to close the day, understand the user's final state and suggest a sleep preparation sequence.

---

## Night Check-In

Example:

```text
How are you feeling at the end of the day?

Calm
Wired
Exhausted
```

This answer may help infer:

- Stress level
- Sleep readiness
- Recovery need
- Screen exposure
- Exercise timing impact
- Dinner impact
- Need for meditation or breathing

---

## Night Plan Push

After the response, Wellbine sends the night sequence.

Example:

```text
Your night reset:

Dim screens
Prepare tomorrow's stack
5 min meditation
Sleep ritual

Ok?

Confirm
Adjust
Later
```

If the user answers **Wired**, the plan may change:

```text
Your sleep downshift:

No more screens
Low light
Breathing exercise
Short meditation
Sleep ritual

Ok?

Confirm
Adjust
Later
```

---

# Push Action Logic

Each Push plan should provide clear action buttons.

Default action buttons:

- Confirm
- Adjust
- Later

These buttons must have specific operational behavior.

---

## Confirm

When the user taps **Confirm**, the app should not open.

Confirm means the user accepts the proposed sequence.

The system should automatically update the related internal pillars inside Wellbine Daily.

Depending on the Push type, Confirm may:

- Mark a planned sequence as accepted.
- Mark scheduled actions as active.
- Mark completed actions as done.
- Update pillar status.
- Update Daily Flow.
- Update Sync.
- Feed AAI learning.

Example:

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

If the user taps **Confirm**, Wellbine should internally update the related pillars without opening the app.

Possible internal updates:

- Sunlight confirmed in the morning plan
- Nutrition confirmed or scheduled
- Daily Stack confirmed or scheduled
- Hydration confirmed or scheduled
- Movement confirmed or scheduled
- Daily Flow updated
- Sync updated
- AAI learning updated

Confirm should reduce app opening.

The user should feel that the plan was accepted and the system handled the internal organization automatically.

---

## Adjust

When the user taps **Adjust**, the app should open directly on the relevant adjustment screen.

Adjust means the user does not want to follow the proposed sequence exactly.

The user may need to:

- Remove an action
- Change timing
- Change intensity
- Change food plan
- Change Daily Stack status
- Switch protocol
- Select a lighter plan
- Manually edit the current sequence

Adjust should not open the generic Home screen.

It should open the specific screen related to that Push sequence.

Examples:

- A Morning Plan Push should open the Morning Plan adjustment screen.
- A Midday Plan Push should open the Midday Plan adjustment screen.
- An Evening Movement Push should open the Movement adjustment screen.
- A Night Reset Push should open the Night Reset adjustment screen.

Adjust is the only default Push action that should open the app.

---

## Later

When the user taps **Later**, the app should not open.

Later means the user is not ready to act now.

The system should register this response and schedule a follow-up Push.

Default follow-up timing:

**Approximately 1 hour later**

Example:

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

If the user taps **Later**, Wellbine should:

- Register the delay
- Keep the sequence pending
- Recalculate the active context window if needed
- Send a follow-up Push approximately one hour later
- Avoid treating the action as failed
- Avoid punitive language

If the biological context changes before the follow-up, AAI may adjust the next Push.

Example:

If the user delays the morning plan and it becomes too late for HIIT, the next Push may suggest a lighter recovery plan instead.

---

# Button Logic Summary

```text
Confirm
↓
Accept sequence
↓
Update internal pillars
↓
No app opening

Adjust
↓
Open relevant app screen
↓
User edits sequence

Later
↓
Register delay
↓
Follow up by Push in approximately 1 hour
```

---

# Product Rule

Push buttons must reduce friction.

Confirm should update internal pillars without opening the app.

Adjust should open the app only when editing is necessary.

Later should preserve the user's path forward without penalty.

---

# Relationship With AAI

AAI uses Push to:

- Understand the user's state.
- Compare current answers with previous behavior.
- Detect changes in context.
- Anticipate needs.
- Adjust the next sequence.
- Update Wellbine Daily.
- Improve future guidance.

Push is not separate from AAI.

Push is one of the ways AAI operates outside the app.

---

# Relationship With BCAS

Push should follow BCAS logic.

This means Push should be based on biological context and daily state, not only fixed time.

Clock time may help trigger a Push, but context should determine the content.

Example:

A morning Push is not just sent because it is 7:00 AM.

It is sent because the user is entering the Morning Activation context.

---

# Relationship With Daily

Push and Wellbine Daily must operate as one connected system.

When the user answers a Push:

- Daily Flow updates.
- Actions may become Done.
- Current Biological Context may change.
- Next Best Action may change.
- Recovery logic may activate.
- Score and Sync may update.
- AAI learning improves.

The app and Push should always reflect the same state.

---

# Wearable-Aware Push Logic

Wellbine Push must behave differently depending on whether the user has a wearable connected.

---

## With Wearable

When a wearable is connected, Push should rely more on automatic context detection and less on manual questioning.

Wearable data may help identify:

- Wake time
- Sleep duration
- Sleep quality
- HRV
- Resting heart rate
- Movement
- Inactivity
- Exercise
- Recovery state
- Stress signals

With wearable data, Push should focus more on:

- Interpretation
- Guidance
- Confirmation
- Adjustment
- Recovery suggestions

Example:

```text
Your recovery looks lower today.

Suggested plan:

Sunlight
Hydration
Light movement
No HIIT
Early night reset

Ok?

Confirm
Adjust
Later
```

---

## Without Wearable

When no wearable is connected, Push becomes the primary context collection layer.

However, the system should not ask many questions.

It should ask fewer and better questions.

Without wearable data, each Push question should reveal multiple parameters.

Example:

```text
How did you wake up today?

Rested
Okay
Tired
```

This answer is more valuable than asking:

```text
Did you wake up?
```

The goal is not to replace sensors with noise.

The goal is to replace missing sensor data with high-signal user input.

---

# High-Signal Question Design

Wellbine Push questions must be high-signal.

A good Push question should:

- Be easy to answer.
- Use binary or ternary options.
- Reveal more than one parameter.
- Help AAI understand context.
- Reduce the need for future questions.
- Support the next action sequence.

Avoid obvious questions.

Bad examples:

```text
Did you wake up?
```

```text
Did you open the app?
```

Good examples:

```text
How did you wake up today?

Rested
Okay
Tired
```

```text
How does your body feel now?

Ready
Tense
Drained
```

```text
How did your last meal feel?

Light
Heavy
Still hungry
```

```text
How are you feeling at the end of the day?

Calm
Wired
Exhausted
```

The goal is not to ask more questions.

The goal is to ask better questions.

---

# Push Plan Design

A Push plan should summarize the next sequence of actions.

It should be short, clear and actionable.

A good Push plan should include:

- 3 to 6 actions maximum.
- The most relevant actions for the current context.
- Protocol-aware adjustments.
- Recovery logic when needed.
- One clear confirmation.

Example:

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

Avoid long plans with too many items.

Avoid generic advice.

Avoid forcing the user to open the app unless necessary.

---

# Push Categories

Wellbine Push should be organized into four main categories.

---

## 1. Context Push

Used to understand the user's current state.

Example:

```text
How did you wake up today?

Rested
Okay
Tired
```

---

## 2. Plan Push

Used to deliver the next sequence.

Example:

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

---

## 3. Recovery Push

Used when the system identifies a need to adjust the day.

Example:

```text
You can still stabilize today.

Choose the lighter plan?

Yes
Keep original
Later
```

---

## 4. Confirmation Push

Used to confirm completion of a sequence.

Example:

```text
Morning plan complete?

Complete
Partial
Not today
```

---

# Push Frequency Rules

Default maximum:

**3 to 4 main Push cycles per day.**

The system may reduce frequency when:

- The user ignores Push notifications.
- The user has a wearable connected.
- Context can be inferred automatically.
- The user prefers fewer notifications.
- Notification fatigue is detected.

The system may temporarily increase interaction only when:

- The user explicitly requests support.
- A protocol requires closer follow-up.
- There is an important recovery opportunity.
- A key action needs confirmation.

Even in these cases, the system should remain low-friction.

---

# Push Tone

Push should sound calm, useful and intelligent.

It should not sound aggressive, motivational or punitive.

Preferred tone:

- Direct
- Calm
- Human
- Practical
- Low-pressure

Avoid:

- Guilt
- Shame
- Fear
- Excess urgency
- Over-motivation
- Punishment language

Avoid phrases such as:

- You missed it.
- You failed.
- You are behind.
- You lost your streak.
- You need to fix this now.

Preferred phrases:

- Continue from here.
- Your day is still recoverable.
- Want to adjust today?
- Lower intensity today?
- Start now?
- Confirm plan?
- Adjust plan?
- Later?

---

# Protocol Awareness

Push must respect the user's current protocol.

Examples:

- Fasting
- OMAD
- Low carb
- Keto
- Vegetarian
- Normal day
- Recovery day
- Day off

Example:

If the user is fasting, Push should not suggest breakfast or lunch during the fasting window.

Instead, it may send:

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

# Push And Recovery

Push should support recovery logic.

If the user skips, delays or partially completes a sequence, Push should not punish the user.

Instead, it should adjust the next plan.

Example:

```text
You can still stabilize today.

Recovery plan:

Hydration
5 min walk
Planned lunch
3 min breathing

Ok?

Confirm
Adjust
Later
```

The user should always have a path forward.

---

# Technical Direction

Current technical direction:

- FlutterFlow as the app layer
- Supabase as backend, database and authentication
- Firebase Cloud Messaging for Push delivery
- Supabase functions or backend logic for Push orchestration when needed

The Push architecture must support future interactive Push behavior.

---

# Current UI / Product Changes

The current Wellbine product direction requires Push to become a central part of the experience.

## Keep

- Daily Stack notifications
- Ritual reminders
- App-linked actions when necessary

## Change

- Push becomes sequence-based
- Push becomes interactive
- Push becomes context-aware
- Push sends 3 to 4 main cycles per day
- Push collects high-signal context
- Push suggests the next action sequence
- Push updates Wellbine Daily
- Push works differently with and without wearables
- Push supports recovery logic
- Confirm updates internal pillars without opening the app
- Adjust opens the relevant app adjustment screen
- Later schedules a follow-up Push approximately one hour later

## Remove or Avoid

- Many isolated reminders
- Excessive notifications
- Low-value check-ins
- Obvious questions
- Punitive language
- Push that forces the app open unnecessarily
- Asking one question for one narrow parameter

---

# What Wellbine Push Is Not

Wellbine Push is not a spam system.

Wellbine Push is not a generic reminder system.

Wellbine Push is not a marketing notification layer.

Wellbine Push is not a punishment mechanism.

Wellbine Push is not dependent only on clock time.

Wellbine Push is not a collection of disconnected questions.

Wellbine Push is an intelligent daily orchestration layer.

---

# Current Status

Wellbine Push is being redesigned as a sequence-based, context-aware extension of AAI.

The next implementation priorities are:

- 3 to 4 daily Push cycles
- Morning Activation
- Midday Alignment
- Evening Alignment
- Night Reset
- High-signal question design
- Push plan delivery
- Confirm / Adjust / Later button logic
- Daily Flow integration
- Wearable-aware Push logic
- Protocol-aware Push behavior
- Recovery-based Push guidance

---

# Future Evolution

Future versions of Wellbine Push may include:

- Dynamic Push timing
- Predictive Push
- Wearable-triggered Push
- Location-aware Push
- Calendar-aware Push
- Push fatigue detection
- Personalized notification cadence
- Adaptive question selection
- AI-generated Push suggestions with safety rules
- Fully autonomous daily plan generation

---

# Related Documents

- FOUNDATION/AAI_CONSTITUTION.md
- FOUNDATION/AAI_GLOSSARY.md
- FOUNDATION/AAI_PRINCIPLES.md
- FRAMEWORKS/POPAE.md
- PRODUCTS/WELLBINE/PRODUCT.md
- PRODUCTS/WELLBINE/BCAS.md
- PRODUCTS/WELLBINE/DAILY.md
- PRODUCTS/WELLBINE/STACK.md
