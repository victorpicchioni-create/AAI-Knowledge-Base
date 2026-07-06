# Wellbine

**Version:** 0.1.0

**Status:** Active

**Last Updated:** July 2026

---

# Purpose

This document introduces Wellbine, the first product built using the Adaptive Alignment Intelligence (AAI) framework.

Wellbine applies AAI to health, performance and longevity through context-aware guidance, intelligent routines, adaptive intervention and operational daily pillars.

---

# Official Product Definition

**Wellbine is an Adaptive Human Operating System designed to help users improve health, performance and longevity with minimal cognitive effort.**

Wellbine is not just:

- A habit tracker
- A health app
- A wellness dashboard
- A meditation app
- A supplement tracker
- An AI chatbot

Wellbine is the first product implementation of AAI.

---

# Product Architecture

Wellbine follows this architecture:

```text
AAI

↓

POPAE

↓

Wellbine

↓

BCAS

↓

Daily + Push

↓

Operational Pillars
```

---

# Relationship With AAI

AAI is the intelligence architecture behind Wellbine.

AAI allows Wellbine to:

- Understand user context
- Learn from behavior
- Anticipate needs
- Align recommendations
- Optimize outcomes
- Reduce cognitive load

Wellbine is the product experience.

AAI is the intelligence layer.

---

# Relationship With POPAE

POPAE is the operating cycle used by AAI.

In Wellbine, POPAE works as:

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

This cycle supports the user's daily guidance, Push sequences, pillar behavior, recovery logic and personalization.

---

# Relationship With BCAS

BCAS is the Wellbine methodology for biological context alignment.

BCAS helps Wellbine move away from rigid clock-based routines and toward context-aware guidance.

Wellbine should not ask only:

```text
What time is it?
```

It should ask:

```text
What biological context is the user in now?
```

---

# Core Product Documents

The current Wellbine documentation includes:

- PRODUCT.md
- BCAS.md
- HOME.md
- DAILY.md
- PUSH.md
- PILLARS.md
- STACK.md

---

# Core Product Areas

## Product Overview

Defined in:

```text
PRODUCT.md
```

This document defines the product vision, direction, boundaries and core rules.

---

## Biological Context Alignment

Defined in:

```text
BCAS.md
```

This document defines how Wellbine aligns guidance with biological context.

---

## Home

Defined in:

```text
HOME.md
```

This document defines the main app entry point and how Wellbine presents current context and Next Best Action.

---

## Daily

Defined in:

```text
DAILY.md
```

This document defines the daily execution flow of Wellbine.

---

## Push

Defined in:

```text
PUSH.md
```

This document defines how Wellbine operates outside the app through 3 to 4 intelligent daily Push cycles.

---

## Pillars

Defined in:

```text
PILLARS.md
```

This document defines the operational pillars of Wellbine.

Current pillars:

- Mind
- Sun
- Hydration
- Sleep
- Meal / Nutrition
- Movement
- Daily Stack

Pillars are not just icons or habits.

They are operational behavior modules connected to AAI, BCAS, Daily and Push.

---

## Daily Stack

Defined in:

```text
STACK.md
```

This document defines medications, vitamins, supplements, nutraceuticals, stock control and intake confirmation.

Daily Stack is one operational pillar, not the only operational pillar.

---

# Push-First Principle

Wellbine should generate value even when the app is not opened.

Push should not behave like generic reminders.

Push should work as intelligent checkpoints.

Default daily Push cycles:

1. Morning Activation
2. Midday Alignment
3. Evening Alignment
4. Night Reset

Each Push cycle may:

- Collect context
- Interpret the previous state
- Suggest the next sequence
- Confirm actions
- Update Daily
- Feed AAI learning

---

# Confirm / Adjust / Later

Wellbine uses a simple default action logic.

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

# Product Principle

Wellbine should reduce cognitive load.

The user should not need to analyze complex dashboards to know what to do.

The product should answer:

```text
What matters now?
```

and:

```text
What is the next best action?
```

---

# Current Technical Direction

Current stack direction:

- FlutterFlow
- Supabase
- Firebase Cloud Messaging for Push Notifications

The technical stack may evolve, but the product principles should remain stable.

---

# Current Status

Wellbine is in the product foundation phase.

Current focus:

- AAI alignment
- BCAS logic
- Daily execution
- Push orchestration
- Operational pillars
- Low-friction user experience
- Context-aware guidance
- Recovery-based behavior

---

# Related Documents

- FOUNDATION/AAI_CONSTITUTION.md
- FOUNDATION/AAI_GLOSSARY.md
- FOUNDATION/AAI_PRINCIPLES.md
- FRAMEWORKS/POPAE.md
- PRODUCTS/WELLBINE/PRODUCT.md
- PRODUCTS/WELLBINE/BCAS.md
- PRODUCTS/WELLBINE/HOME.md
- PRODUCTS/WELLBINE/DAILY.md
- PRODUCTS/WELLBINE/PUSH.md
- PRODUCTS/WELLBINE/PILLARS.md
- PRODUCTS/WELLBINE/STACK.md
