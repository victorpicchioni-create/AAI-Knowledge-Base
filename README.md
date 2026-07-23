# ◉ Adaptive Alignment Intelligence (AAI)

## Official Core Documentation

This repository is the official knowledge base for the Adaptive Alignment Intelligence (AAI) framework.

It serves as the Single Source of Truth (SSOT) for every permanent concept, framework, methodology, product specification and architectural decision related to AAI.

---

# Repository Structure

```text
AAI-Knowledge-Base/

README.md

ARCHITECTURE_DECISIONS/
    README.md
    HOME_CENTRAL.md
    PUSH_ORCHESTRATION.md
    PLAN_TEMPLATES_DB.md
    ADMIN_CONTROL_LAYER.md
    ONBOARDING_ACTIVATION.md

FOUNDATION/
    AAI_CONSTITUTION.md
    AAI_GLOSSARY.md
    AAI_PRINCIPLES.md

FRAMEWORKS/
    POPAE.md

PRODUCTS/
    WELLBINE/
        README.md
        PRODUCT.md
        BCAS.md
        PLAN_TEMPLATES.md
        ONBOARDING.md
        HOME.md
        DAILY.md
        PUSH.md
        PILLARS.md
        STACK.md
        ADMIN.md
        DATA_MODEL.md
        IMPLEMENTATION_PLAN.md
        WEARABLES.md
        APP_RELEASE.md
        COMMERCE_BRIDGE.md
        SUPABASE_SCHEMA.md
        QA_PLAN.md
        PRIVACY_POLICY_DRAFT.md
        TERMS_DRAFT.md
        APP_RELEASE_CHECKLIST.md
        FLUTTERFLOW_BUILD_GUIDE.md
        SUPABASE_IMPLEMENTATION.md
        EDGE_FUNCTIONS.md
        ADMIN_BUILD_GUIDE.md
        MVP_BUILD_SEQUENCE.md
        SCREEN_MAP.md
        FEATURE_FLAGS.md
        SUPABASE_SQL_MVP.md
        FLUTTERFLOW_ACTIONS.md
        EDGE_FUNCTION_PAYLOADS.md
              
```
     
---

# Repository Purpose

This repository stores the official documentation of the AAI framework.

Every document follows one simple rule:

- One document
- One subject
- One official truth

Documentation is written primarily for AI systems and secondarily for humans.

---

# Repository Organization

## FOUNDATION

Permanent concepts that define AAI.

Current documents:

- AAI_CONSTITUTION.md
- AAI_GLOSSARY.md
- AAI_PRINCIPLES.md

---

## FRAMEWORKS

Generic frameworks developed under AAI.

Current framework:

- POPAE.md

Frameworks in this section must be product-independent.

---

## PRODUCTS

Products built using the AAI framework.

Current product:

- Wellbine

---

## PRODUCTS / WELLBINE

Wellbine is the first product built using AAI.

Current documents:

Current documents:

- README.md
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
- MVP_BUILD_SEQUENCE.md
- SCREEN_MAP.md
- FEATURE_FLAGS.md
- SUPABASE_SQL_MVP.md
- FLUTTERFLOW_ACTIONS.md
- EDGE_FUNCTION_PAYLOADS.md
  
Each product contains its own independent documentation, including product-specific methodologies, screens, flows, pillars, plan templates and implementation rules.

---

## ARCHITECTURE_DECISIONS

This folder stores official architecture decisions for AAI, Wellbine and related systems.

Architecture decisions are used to record important product, technical and structural choices that should not be lost, forgotten or accidentally reversed.

Current documents:

- README.md
- HOME_CENTRAL.md
- PUSH_ORCHESTRATION.md
- PLAN_TEMPLATES_DB.md
- ADMIN_CONTROL_LAYER.md
- ONBOARDING_ACTIVATION.md
  
---

# Current Architecture

The current Wellbine architecture follows this direction:

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

Onboarding

↓

Home + Daily + Push + Operational Pillars
```

---

# Current Product Focus

Wellbine is being structured around:

- Home as the central operating surface
- Onboarding as the first activation flow
- Daily as the deeper execution layer
- Push as the outside-app orchestration layer
- Operational Pillars as behavior modules
- Plan Templates as admin-managed starting configurations
- Admin as the operational control layer
- Data Model as the structural foundation for implementation
- Implementation Plan as the staged execution roadmap
- Wearables as optional context enhancers
- App Release as the iOS and Android approval readiness layer
- Commerce Bridge as the subscriber benefit and external commerce connection layer
- Supabase Schema as the operational backend structure
- QA Plan as the product validation and testing layer
- Privacy Policy Draft as the privacy alignment layer
- Terms Draft as the usage rules and product boundary layer
- App Release Checklist as the practical launch verification layer
- FlutterFlow Build Guide as the mobile app implementation layer
- Supabase Implementation as the backend execution layer
- Edge Functions as the secure backend workflow layer
- Admin Build Guide as the internal control implementation layer
- MVP Build Sequence as the ordered construction roadmap
- Screen Map as the mobile app structure blueprint
- Feature Flags as the operational visibility and rollout control layer
- Supabase SQL MVP as the practical database starting point
- FlutterFlow Actions as the frontend interaction logic layer
- Edge Function Payloads as the backend contract layer
- BCAS as the biological context alignment methodology
- AAI as the intelligence architecture
  
---

# Working Method

Every concept follows the same lifecycle.

```text
Idea

↓

Discussion

↓

Validation

↓

Official Documentation

↓

Repository
```

Only validated concepts become part of this repository.

If a concept is not documented here, it is not considered part of the official AAI framework.

---

# Current Status

Framework Version

**0.1.0**

Status

**Foundation Phase**

Primary Product

**Wellbine**

---

# Guiding Principle

Technology changes.

Products evolve.

The framework remains.
