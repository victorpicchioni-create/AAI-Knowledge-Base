# Wellbine Daily

**Version:** 0.1.0

**Status:** Active

**Last Updated:** July 2026

---

# Purpose

This document defines the Wellbine Daily module.

Wellbine Daily is the main execution flow of the Wellbine app.

Its purpose is to guide the user through the day using biological context, Next Best Action logic, recovery opportunities, wearable-aware automation and intelligent Push feedback.

Wellbine Daily should not behave like a simple habit checklist or rigid schedule.

---

# Official Definition

**Wellbine Daily is the context-aware daily execution system of Wellbine, designed to identify the user's current biological context and guide the next best action.**

---

# Core Objective

The objective of Wellbine Daily is to answer one question:

**What is the next best action now?**

The user should not need to interpret dashboards, scores or complex timelines to know what to do.

The system should guide the user clearly, calmly and intelligently.

---

# Relationship With AAI

Wellbine Daily uses AAI to:

- Understand the user's current context
- Learn from behavior and feedback
- Anticipate needs
- Identify the next best action
- Adjust guidance over time
- Improve outcomes

AAI is responsible for intelligence and interpretation.

---

# Relationship With BCAS

Wellbine Daily uses BCAS as its operating methodology.

BCAS replaces rigid clock-based daily routines with biological context-based guidance.

The flow should prioritize:

- Current Biological Context
- Active Context Window
- Next Best Action
- Recovery Opportunity
- User Feedback
- Push Interaction

Clock time may still exist, but it should not be the primary driver.

---

# Wearable-Aware Operation

Wellbine Daily must work with or without wearable devices.

The system should never depend entirely on wearables to deliver value.

However, the level of automation changes depending on whether the user has a wearable connected.

---

## With Wearable

When a wearable is connected, Wellbine Daily should rely more on automatic context detection and less on manual user input.

Wearable data may help identify:

- Wake time
- Sleep duration
- Sleep quality
- Resting heart rate
- HRV
- Movement
- Inactivity
- Exercise
- Recovery state
- Stress signals
- Energy patterns

In this mode, the system should reduce unnecessary Push check-ins because many biological and behavioral signals can be detected automatically.

The user experience should feel more automatic, predictive and effortless.

Example:

```text
Wearable detects poor sleep and elevated recovery need.

↓

Wellbine adjusts the day.

↓

Next Best Action:

Lower intensity today.
```

---

## Without Wearable

When no wearable is connected, Wellbine Daily must remain simple and useful.

In this mode, the system should use fewer but smarter interactive Push check-ins.

Push questions should not ask obvious questions.

They should ask about states that reveal multiple possible signals.

The objective is to collect high-value context with minimal user effort.

Bad example:

```text
Did you wake up?

Yes
Not yet
Remind me later
```

This question is weak because if the user is answering, the user is already awake.

Better example:

```text
How did you wake up today?

Rested
Okay
Tired
```

This answer may help infer:

- Sleep quality
- Recovery state
- Late eating
- Previous-day exercise intensity
- Stress
- Screen exposure
- Sleep duration
- Readiness for the day

Examples of smart Push check-ins:

```text
How did you wake up today?

Rested
Okay
Tired
```

```text
How is your energy and focus right now?

Sharp
Normal
Low
```

```text
How did your last meal feel?

Light
Heavy
Still hungry
```

```text
How does your body feel right now?

Ready
Tense
Drained
```

```text
How was your morning routine?

Complete
Partial
Not started
```

Without wearable data, Push becomes the primary context collection layer.

However, the system should avoid excessive questioning.

Each Push should collect context that can inform more than one parameter.

The experience should remain light, fast and low-friction.

---

## Product Rule

Wearables increase automation.

Push check-ins replace missing sensors.

Without wearables, the system should not ask more questions by default.

It should ask better questions.

Both modes must support the same objective:

**Identify the user's current context and guide the Next Best Action with minimal cognitive effort.**

---

# Core Screen Structure

The Wellbine Daily screen should be structured around five main areas:

1. Daily Status
2. Current Biological Context
3. Next Best Action
4. Guidance
5. Daily Flow

---

# Daily Status

The top area of the screen should communicate the current state of the day in simple human language.

Preferred message:

**Your day is still recoverable.**

Supporting text:

**Complete the next 3 actions to stabilize your Sync.**

The system should avoid displaying raw penalties, negative scores or overly technical metrics in the main view.

Avoid:

- Raw -7.0
- Penalty
- Missed score
- Negative projections
- Overly complex calculations

The math may exist internally, but the user should receive clear guidance.

---

# Current Biological Context

The screen should show the user's current biological context when relevant.

Examples:

- Morning Reset
- Feeding Window
- Movement Window
- Recovery Window
- Sleep Preparation Window
- Hydration Opportunity
- Daily Stack Window

The context should explain why the current action matters.

Example:

**Current Context:** Feeding Window

---

# Next Best Action

The main action card should be called:

**Next Best Action**

It should present one clear action.

Example:

```text
Next Best Action

Lunch

Have your planned lunch.

Done
```

The button should use direct action language.

Preferred buttons:

- Done
- Start
- Log
- Confirm
- Skip Today
- Remind Me Later

Avoid vague buttons such as:

- Continue Today
- Go
- Proceed
- Next

---

# Guidance

Guidance should be short, useful and specific.

Example:

**Eat sitting down — even five minutes counts.**

Guidance should feel intelligent, not motivational.

Avoid generic motivational phrases.

Good guidance should be:

- Practical
- Calm
- Context-aware
- Short
- Actionable

---

# Daily Flow

The Daily Flow shows the user's day, but it should not feel like a punishment checklist.

The flow should show actions by state.

Official states:

- Done
- Now
- Upcoming
- Window Closed
- Locked

---

# State Definitions

## Done

The action was completed.

Example:

**Lunch — Done**

---

## Now

The action is currently active and relevant.

Example:

**Hydration — Now**

---

## Upcoming

The action is expected later, depending on context.

Example:

**Sleep Ritual — Upcoming**

---

## Window Closed

The biological context window has passed.

This should replace negative language such as "Missed".

Example:

**Morning Sunlight — Window Closed**

Window Closed means the opportunity passed, but the day is still recoverable.

---

## Locked

The action is not available yet because the required context has not occurred.

Example:

**Night Reset — Locked**

---

# Language Rules

Preferred language:

- Your day is still recoverable
- Next Best Action
- Window Closed
- Continue From Here
- Stabilize your Sync
- Current Context
- Upcoming
- Done
- Now

Avoid:

- Missed
- Failed
- Penalty
- Lost
- Bad score
- You failed
- You are behind

---

# Recovery Logic

Wellbine Daily must always preserve a path forward.

If the user wakes up late, skips an action or changes routine, the system should not treat the entire day as failed.

Instead, the system should identify the next possible alignment opportunity.

Example:

Instead of:

```text
Morning Meditation — Missed
Sunlight — Missed
Breakfast — Missed
```

Use:

```text
Current Context

Late Morning Reset

Next Best Action

Hydrate and get 5 minutes of sunlight.
```

Recovery is not an exception.

Recovery is part of the system.

---

# Context-Based Flow

The Wellbine Daily flow should be organized by biological context, not only by clock time.

Example flow:

```text
Wake

↓

Morning Reset

↓

Feeding Window

↓

Work / Focus Period

↓

Movement Window

↓

Recovery Window

↓

Evening Nutrition

↓

Sleep Preparation

↓

Sleep
```

This allows Wellbine to adapt to different users:

- Early risers
- Late risers
- Night workers
- Parents
- Travelers
- Professionals with irregular schedules

---

# Diet And Protocol Mode

Wellbine Daily must allow the user to indicate the current diet or daily protocol.

This exists so the system avoids inappropriate suggestions.

Examples:

- Fasting
- OMAD
- Low carb
- Keto
- Vegetarian
- Normal day
- Recovery day
- Day off

Example rule:

If the user is fasting, Wellbine should not suggest a meal during the fasting window.

This section may appear as:

**Today's Protocol**

or

**Today's Mode**

Current preferred label:

**Today's Protocol**

---

# Push Integration

Wellbine Daily should work both inside the app and through interactive Push Notifications.

The long-term goal is that the user does not need to open the app for every action.

Push should not be treated as a simple reminder system.

Push is an operational extension of AAI.

Push responses should update the Daily Flow, feed AAI learning and help infer broader patterns.

A single Push answer should be useful for more than one interpretation whenever possible.

Examples:

```text
How did you wake up today?

Rested
Okay
Tired
```

```text
How is your energy and focus right now?

Sharp
Normal
Low
```

```text
How did your last meal feel?

Light
Heavy
Still hungry
```

```text
How does your body feel right now?

Ready
Tense
Drained
```

```text
How was your morning routine?

Complete
Partial
Not started
```

---

# Push Question Design

Wellbine Push questions should follow a high-signal design.

The system should avoid asking questions that are obvious, redundant or too narrow.

Bad example:

```text
Did you wake up?
```

This question is weak because if the user is answering, the user is already awake.

Better example:

```text
How did you wake up today?

Rested
Okay
Tired
```

This answer may help infer sleep quality, recovery state, late eating, stress, previous-day intensity and readiness.

A good Push question should:

- Be easy to answer
- Offer binary or ternary choices
- Reveal more than one parameter
- Help AAI understand context
- Reduce the need for multiple future questions
- Support the Next Best Action

The goal is not to ask more questions.

The goal is to ask better questions.

---

# User Interaction Rules

The user should be able to:

- Complete an action inside the app
- Complete an action through Push
- Skip an action
- Delay an action
- Register an action within the current day
- Change the current protocol
- Recover part of the day through later actions
- Use wearable data when available to reduce manual check-ins
- Use interactive Push check-ins when wearable data is unavailable

---

# Score Presentation

Score should exist, but it should not dominate the screen.

The user should understand progress without needing to interpret complex calculations.

Preferred score language:

- Stabilize your Sync
- Improve today
- Recoverable
- Strong day
- Needs attention

Avoid exposing raw internal math as the main message.

---

# Current UI Changes

The current Wellbine Daily screen should be updated as follows:

## Keep

- Dark premium interface
- Daily execution structure
- Guidance area
- Daily action list
- Protocol selector

## Change

- Replace fixed-time logic with BCAS context logic
- Replace "Missed" with "Window Closed"
- Replace technical score language with human guidance
- Replace "Continue Today" with direct action buttons
- Make Next Best Action the main focus
- Reduce negative or punitive language
- Support wearable-based automation
- Support Push-based context collection when wearables are unavailable
- Replace low-value Push questions with high-signal Push questions

## Remove or Hide

- Penalty labels
- Excessive raw score data
- Repeated missed indicators
- Overly technical projections in the main view
- Obvious Push questions
- Redundant check-ins

---

# Primary Screen Copy

Recommended main copy:

```text
Your day is still recoverable.

Complete the next 3 actions to stabilize your Sync.
```

Recommended action card:

```text
Next Best Action

Lunch

Have your planned lunch.

Done
```

Recommended guidance example:

```text
Eat sitting down — even five minutes counts.
```

---

# What Wellbine Daily Is Not

Wellbine Daily is not a calendar.

Wellbine Daily is not a punishment system.

Wellbine Daily is not a rigid habit checklist.

Wellbine Daily is not a dashboard.

Wellbine Daily is not dependent only on clock time.

Wellbine Daily is not dependent on wearables to create value.

Wellbine Daily is the daily execution layer of Wellbine.

---

# Current Status

Wellbine Daily is being redesigned from a time-based routine flow into a BCAS-based context-aware execution flow.

The next implementation priorities are:

- Current Biological Context
- Next Best Action
- Window states
- Recovery language
- Interactive Push connection
- Protocol awareness
- Wearable-aware automation
- High-signal Push question design
- Push-based context collection for users without wearables

---

# Future Evolution

Future versions of Wellbine Daily may include:

- Wearable-based context detection
- Automatic wake detection
- Automatic recovery recommendations
- Personalized context windows
- Predictive Daily Flow
- Dynamic Push timing
- Context-aware score adjustment
- Wearable-aware automation
- Manual-to-automatic context transition

---

# Related Documents

- FOUNDATION/AAI_CONSTITUTION.md
- FOUNDATION/AAI_GLOSSARY.md
- FOUNDATION/AAI_PRINCIPLES.md
- FRAMEWORKS/POPAE.md
- PRODUCTS/WELLBINE/PRODUCT.md
- PRODUCTS/WELLBINE/BCAS.md
- PRODUCTS/WELLBINE/PUSH.md
- PRODUCTS/WELLBINE/STACK.md
