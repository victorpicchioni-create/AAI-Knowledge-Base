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

Plan Templates

↓

Home + Daily + Push + Operational Pillars
```

Plan Templates define the user's starting configuration.

Home is the main operating surface.

Daily is the deeper execution layer.

Push operates outside the app.

Pillars organize operational behavior.

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

This cycle supports Daily guidance, Push sequences, pillar behavior, recovery logic, plan adaptation and personalization.

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

# Current Wellbine Documents

The current Wellbine documentation includes:

- PRODUCT.md
- BCAS.md
- PLAN_TEMPLATES.md
- ONBOARDING.md
- HOME.md
- DAILY.md
- PUSH.md
- PILLARS.md
- STACK.md
- ADMIN.md
- DATA_MODEL.md
- IMPLEMENTATION_PLAN.md
- WEARABLES.md
- APP_RELEASE.md
- COMMERCE_BRIDGE.md
- SUPABASE_SCHEMA.md
- QA_PLAN.md
- PRIVACY_POLICY_DRAFT.md
- TERMS_DRAFT.md
- APP_RELEASE_CHECKLIST.md
- FLUTTERFLOW_BUILD_GUIDE.md
- SUPABASE_IMPLEMENTATION.md
- EDGE_FUNCTIONS.md
- ADMIN_BUILD_GUIDE.md
  
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

## Plan Templates

Defined in:

```text
PLAN_TEMPLATES.md
```

This document defines flexible admin-managed plan templates.

Plan Templates activate and organize the Wellbine experience across:

- Home
- Daily
- Push
- Pillars
- Wearables
- Settings
- User guidance
- Content
- Recommendations

Plan Templates should be database-driven and editable without code changes through Supabase or an Admin Panel.

---

## Onboarding

Defined in:

```text
ONBOARDING.md
```

This document defines the first activation flow of Wellbine.

Onboarding collects essential user context, supports wearable and upload options, activates a Recommended or Adapted Plan, configures Pillars, Daily, Push and Home, and moves the user into the first 7-Day Sync Plan.

---

## Home

Defined in:

```text
HOME.md
```

This document defines the main app operating surface.

Home is not just a tab.

Home should centralize the user's current state, Adaptive Summary, pillar signals, Current Insight, Next Best Action, Ask Wellbine and contextual access points.

Home should not depend on fixed Bottom Navigation.

---

## Daily

Defined in:

```text
DAILY.md
```

This document defines the daily execution flow of Wellbine.

Daily is the deeper operational layer of the day.

---

## Push

Defined in:

```text
PUSH.md
```

This document defines how Wellbine operates outside the app through intelligent daily Push cycles.

Push should not behave like generic reminders.

Push should work as contextual checkpoints that connect user response to the next sequence.

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

They are operational behavior modules connected to AAI, BCAS, Daily, Push and Home.

---

## Daily Stack

Defined in:

```text
STACK.md
```

This document defines medications, vitamins, supplements, nutraceuticals, stock control and intake confirmation.

Daily Stack is one operational pillar, not the only operational pillar.

---

## Admin

Defined in:

```text
ADMIN.md
```

This document defines the internal management system of Wellbine.

Admin allows authorized operators to configure and update Plans, Onboarding, Home, Daily, Push, Pillars, Stack, Wearables, Settings, Uploads, Content, Recommendations, Users, Analytics and Publishing without code changes.

Admin is the operational control layer of Wellbine.

---

## Data Model

Defined in:

```text
DATA_MODEL.md
```

This document defines the initial conceptual and operational data model for Wellbine.

The Data Model translates the product architecture into database-ready structures for Supabase, FlutterFlow and Admin implementation.

It covers Users, Plan Templates, User Active Plans, Pillars, Daily, Push, Home, Stack, Wearables, Settings, Uploads, Content, Recommendations, Admin, AAI Context and Events.

---

## Implementation Plan

Defined in:

```text
IMPLEMENTATION_PLAN.md
```

This document defines the staged execution roadmap for building Wellbine.

The Implementation Plan connects Supabase, FlutterFlow, Data Model, Authentication, Onboarding, Plan Templates, Home, Daily, Push, Pillars, Wearables, Uploads, Admin, AAI Context, Commerce Bridge, App Store and Google Play readiness, QA and Production Launch.

It defines the practical build order for turning the Wellbine architecture into an operational product.

---

## Wearables

Defined in:

```text
WEARABLES.md
```

This document defines the optional wearable connectivity layer of Wellbine.

Wearables improve automation, personalization and adaptive guidance by providing permissioned context from devices and health platforms.

The Wearables layer connects sleep, recovery, movement, heart trends, HRV, respiratory signals, oxygen saturation, temperature trends, stress signals and readiness to Home, Daily, Push, Pillars and AAI Context.

Wearables improve the system, but Wellbine must work without wearables.

---

## App Release

Defined in:

```text
APP_RELEASE.md
```

This document defines the App Store and Google Play release readiness plan for Wellbine.

The App Release plan covers iOS and Android approval, TestFlight, Google internal testing, health data permissions, wearable permissions, Push notifications, Privacy Policy, Terms of Use, account deletion, AI explanation, subscription language, external commerce, health claims, app screenshots, review notes, QA and production launch.

App Store and Google Play approval should be considered during product design, not only before launch.

---

## Commerce Bridge

Defined in:

```text
COMMERCE_BRIDGE.md
```

This document defines the subscriber benefit and external commerce connection layer of Wellbine.

Commerce Bridge allows eligible users to access coupons, offers or product-related benefits inside Wellbine and complete purchases through external e-commerce platforms.

The MVP Commerce Bridge uses one primary action that copies the benefit code automatically and opens the external commerce destination.

Commerce Bridge supports monetization without turning Wellbine into an in-app store or making commerce the center of the product experience.

---

## Supabase Schema

Defined in:

```text
SUPABASE_SCHEMA.md
```

This document defines the practical Supabase schema direction for Wellbine.

The Supabase Schema translates the conceptual Data Model into an operational backend structure for Supabase, FlutterFlow, Admin and AAI services.

It covers core tables, approximate fields, relationships, JSON configuration fields, Row Level Security direction, Storage buckets, Edge Functions, Admin publishing, event tracking and implementation phases.

Supabase is the source of truth. FlutterFlow is the interface layer.

---

---

## QA Plan

Defined in:

```text
QA_PLAN.md
```

This document defines the structured testing and validation process for Wellbine.

The QA Plan verifies that Wellbine works safely, reliably and coherently across product experience, backend logic, user data, admin configuration, app release and privacy-sensitive flows.

---

## Privacy Policy Draft

Defined in:

```text
PRIVACY_POLICY_DRAFT.md
```

This document defines the first internal draft of the Wellbine Privacy Policy.

The Privacy Policy Draft aligns product, data, app release, user trust and legal review before publication.

It covers account data, profile data, wellness context, wearable data, uploads, AI-assisted guidance, Push interactions, Daily activity, Daily Stack data, Commerce Bridge activity and app usage information.

---

## Terms Draft

Defined in:

```text
TERMS_DRAFT.md
```

This document defines the first internal draft of the Wellbine Terms of Use.

The Terms Draft clarifies product boundaries, user responsibilities, wellness guidance limits, AI-assisted guidance, subscriptions, Daily Stack, Wearables, Uploads, Commerce Bridge and external services.

---

## App Release Checklist

Defined in:

```text
APP_RELEASE_CHECKLIST.md
```

This document defines the practical verification checklist for publishing Wellbine on iOS and Android.

The App Release Checklist translates the release strategy into concrete validation items for App Store review, Google Play review, internal testing, beta testing and controlled production launch.

---

## FlutterFlow Build Guide

Defined in:

```text
FLUTTERFLOW_BUILD_GUIDE.md
```

This document defines the practical implementation guide for building the Wellbine mobile app interface, user flows, screen logic, Supabase connections and adaptive user experience in FlutterFlow.

FlutterFlow is the product interface layer, not the source of truth.

---

## Supabase Implementation

Defined in:

```text
SUPABASE_IMPLEMENTATION.md
```

This document defines the practical backend setup process that turns the Wellbine data model and schema blueprint into a working Supabase environment for the mobile app, Admin layer and AAI services.

Supabase should be built as the source of truth before building complex frontend behavior.

---

## Edge Functions

Defined in:

```text
EDGE_FUNCTIONS.md
```

This document defines the secure backend functions used to process sensitive, multi-step and adaptive workflows that should not live entirely inside the FlutterFlow frontend.

The core Edge Functions rule is: frontend triggers, backend decides.

---

## Admin Build Guide

Defined in:

```text
ADMIN_BUILD_GUIDE.md
```

This document defines the practical implementation guide for creating the internal control system used to configure, publish, manage and monitor the Wellbine product experience.

Admin controls product behavior. The app executes published configuration.

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
- Update Pillars
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

# Home-First Product Principle

Wellbine should not rely on fixed Bottom Navigation.

Home should become the central operating surface of the app.

Previous navigation areas should be absorbed into Home when possible:

- Hub becomes pillar visibility through Orbs and Quick Panels.
- Stats become Adaptive Summary, Sync and pillar percentages.
- Store becomes contextual recommendations or external flow.
- Profile becomes Personal Center or Settings access.
- Daily remains accessible through contextual actions.

The product should reduce navigation, not multiply tabs.

---

# Plan Template Principle

Plan Templates are flexible starting configurations.

The admin should be able to create, edit, duplicate, publish, archive and reorganize plans without changing code.

Plan Templates may configure:

- Pillars
- Daily
- Push
- Home
- Wearables
- Settings
- Content
- Recommendations
- Protocol rules

The engine is built once.

Plans are managed as content and configuration.

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
- Home as central operating surface
- Daily execution
- Push orchestration
- Operational pillars
- Plan Templates
- Low-friction user experience
- Context-aware guidance
- Recovery-based behavior
- Admin-managed configuration

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
- PRODUCTS/WELLBINE/PLAN_TEMPLATES.md
- PRODUCTS/WELLBINE/STACK.md
- PRODUCTS/WELLBINE/ADMIN.md
- PRODUCTS/WELLBINE/IMPLEMENTATION_PLAN.md
- PRODUCTS/WELLBINE/WEARABLES.md
- PRODUCTS/WELLBINE/APP_RELEASE.md
- PRODUCTS/WELLBINE/COMMERCE_BRIDGE.md
- PRODUCTS/WELLBINE/SUPABASE_SCHEMA.md
- PRODUCTS/WELLBINE/QA_PLAN.md
- PRODUCTS/WELLBINE/PRIVACY_POLICY_DRAFT.md
- PRODUCTS/WELLBINE/TERMS_DRAFT.md
- PRODUCTS/WELLBINE/APP_RELEASE_CHECKLIST.md
- PRODUCTS/WELLBINE/FLUTTERFLOW_BUILD_GUIDE.md
- PRODUCTS/WELLBINE/SUPABASE_IMPLEMENTATION.md
- PRODUCTS/WELLBINE/EDGE_FUNCTIONS.md
- PRODUCTS/WELLBINE/ADMIN_BUILD_GUIDE.md
