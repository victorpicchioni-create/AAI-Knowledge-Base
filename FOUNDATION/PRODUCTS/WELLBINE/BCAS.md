# Wellbine BCAS

**Version:** 0.1.0

**Status:** Active

**Last Updated:** July 2026

---

# Purpose

This document defines BCAS inside Wellbine.

BCAS means:

**Biological Context Alignment System**

BCAS is the product-specific methodology used by Wellbine to organize guidance, routines, interventions and Push interactions based on the user's biological context.

---

# Official Definition

**BCAS is the Wellbine methodology that aligns user guidance with biological context instead of rigid clock-based routines.**

---

# Core Concept

Wellbine should not organize the user's day only by fixed time.

The system should not ask only:

**What time is it?**

The system should ask:

**What biological context is the user experiencing now?**

This allows Wellbine to adapt to real life instead of forcing the user into a fixed schedule.

---

# Scientific Position

BCAS does not reject circadian science.

BCAS extends circadian science.

Circadian rhythm remains important, but fixed clock time is not the only driver of user guidance.

In BCAS:

- Time is a variable.
- Biological context is the priority.
- User state matters.
- Behavior matters.
- Feedback matters.
- Routine flexibility matters.

---

# Scientific Foundations

BCAS is based on principles from:

- Chronobiology
- Lifestyle Medicine
- Human Physiology
- Behavioral Science
- Context-aware systems

The objective is to deliver the right guidance at the most relevant biological moment.

---

# Biological Context

A biological context is the current physiological or behavioral state of the user.

Examples:

- The user just woke up.
- The user has been inactive for several hours.
- The user finished a meal.
- The user is fasting.
- The user completed exercise.
- The user needs recovery.
- The user is preparing for sleep.
- The user has not hydrated for a long period.
- The user is under stress.
- The user has low energy.

Each biological context creates an opportunity for alignment.

---

# Biological Context Windows

BCAS uses Biological Context Windows instead of rigid time blocks.

A Biological Context Window opens when a relevant biological or behavioral event occurs.

---

## Wake Window

Triggered when the user wakes up.

Possible guidance:

- Hydration
- Sunlight exposure
- Breathing
- Meditation
- Morning reset
- First meal, when appropriate

---

## Feeding Window

Triggered by meal timing, fasting state, hunger signals or nutritional protocol.

Possible guidance:

- Confirm planned meal
- Log meal
- Adjust meal guidance
- Respect fasting state
- Avoid food suggestions during fasting windows

---

## Movement Window

Triggered by inactivity, planned movement, wearable data or contextual opportunity.

Possible guidance:

- Short walk
- Mobility
- Strength training
- Sedentary break
- Lower intensity movement

---

## Recovery Window

Triggered after physical effort, poor sleep, fatigue or elevated stress.

Possible guidance:

- Rest
- Hydration
- Breathing
- Lower intensity
- Recovery protocol
- Sleep support

---

## Sleep Preparation Window

Triggered when the user enters the biological or behavioral context of preparing for sleep.

Possible guidance:

- Screen reduction
- Night reset
- Breathing
- Meditation
- Sleep ritual
- Wake planning

---

# Relationship With AAI

AAI is the intelligence architecture.

BCAS is the Wellbine methodology for biological context.

In simple terms:

**AAI interprets.**

**BCAS organizes.**

**Wellbine delivers.**

---

# Relationship With POPAE

BCAS operates inside the POPAE cycle.

```text
Prepare
↓
Observe
↓
Predict
↓
Align
↓
Evolve
```

In Wellbine:

- Prepare: reduce noise and identify user state.
- Observe: collect user behavior, feedback and biological signals.
- Predict: anticipate the next relevant biological need.
- Align: deliver the next best action.
- Evolve: learn from response and outcomes.

---

# Wellbine Daily Implementation

BCAS replaces the older fixed-time daily routine.

Wellbine Daily should not be treated as a simple schedule.

It should operate as a context-aware execution system.

The system should identify:

- Current Biological Context
- Active Context Window
- Next Best Action
- Relevant Guidance
- User Feedback
- Recovery Opportunity

---

# Next Best Action

The main output of BCAS inside Wellbine is the Next Best Action.

The user should not need to decide what to do next.

The system should identify the most relevant action based on context and present it clearly.

Examples:

- Have your planned lunch.
- Take a 5-minute walk.
- Drink water now.
- Start your Night Reset.
- Lower intensity today.
- Complete your Daily Stack.
- Take your supplement.
- Begin your sleep ritual.

---

# Recovery Principle

BCAS should prevent the user from feeling that the day is lost.

If the user wakes up late, skips an action or changes routine, the system should adjust around the new context.

The user should always be guided toward the next possible alignment opportunity.

Preferred language:

- Window Closed
- Still Recoverable
- Next Best Action
- Continue From Here

Avoid:

- Missed
- Failed
- Penalty
- Lost Day

---

# Push Integration

BCAS is designed to work both inside and outside the app.

Push notifications should be treated as operational extensions of AAI.

Whenever possible, Push should be interactive and allow the user to respond without opening the application.

Examples:

```text
Did you have your planned lunch?

Yes
Not yet
Skip today
```

```text
How is your energy now?

High
Normal
Low
```

```text
Did you drink water recently?

Yes
Not yet
Remind me later
```

These responses feed AAI and improve future personalization.

---

# Diet And Protocol Awareness

Wellbine must allow the user to indicate the current diet or daily protocol.

Examples:

- Fasting
- OMAD
- Low carb
- Keto
- Vegetarian
- Normal day
- Recovery day
- Day off

This prevents the system from suggesting inappropriate actions.

Example:

If the user is fasting, Wellbine should not suggest food during the fasting window.

---

# Product Rules

BCAS inside Wellbine must follow these rules:

- Context comes before clock time.
- Clock time is a variable, not the main driver.
- Biological context determines relevance.
- The system adapts to the user's real routine.
- Guidance must be short, useful and actionable.
- The system avoids unnecessary interruption.
- Push reduces app dependency.
- The user always has a path forward.
- Recovery is preferred over punishment.

---

# What BCAS Is Not

BCAS is not a calendar system.

BCAS is not a habit checklist.

BCAS is not a rigid circadian schedule.

BCAS is not a medical diagnosis system.

BCAS is not a replacement for professional health guidance.

BCAS is the Wellbine methodology for biological context alignment.

---

# Current Status

BCAS is currently the central methodology guiding the redesign of Wellbine.

The main areas affected are:

- Home
- Wellbine Daily
- Push
- Daily Stack
- Score
- User Recovery Flow
- AAI Context Engine

---

# Future Evolution

BCAS should evolve toward increasingly accurate context detection.

Future inputs may include:

- Wearables
- Sleep data
- Movement data
- Hydration patterns
- Nutrition patterns
- User feedback
- Location context
- Calendar context
- Environmental signals

The objective is to make interventions more timely, relevant and effortless.

---

# Related Documents

- FOUNDATION/AAI_CONSTITUTION.md
- FOUNDATION/AAI_GLOSSARY.md
- FOUNDATION/AAI_PRINCIPLES.md
- FRAMEWORKS/POPAE.md
- PRODUCTS/WELLBINE/PRODUCT.md
- PRODUCTS/WELLBINE/DAILY.md
- PRODUCTS/WELLBINE/PUSH.md
