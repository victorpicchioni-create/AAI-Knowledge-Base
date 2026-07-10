# Architecture Decisions

**Version:** 0.1.0

**Status:** Active

**Last Updated:** July 2026

---

# Purpose

This folder stores official architecture decisions for AAI and Wellbine.

Architecture decisions are used to record important product, technical and structural choices that should not be lost, forgotten or accidentally reversed.

This folder acts as a decision history for the project.

---

# Official Definition

**Architecture Decisions are permanent records of important structural choices made during the development of AAI, Wellbine and related systems.**

---

# Why This Exists

As the project grows, many decisions will affect multiple documents, screens, flows and systems.

Examples:

- Home as the central operating surface
- Push as an orchestration layer
- Plan Templates as database-driven configurations
- Admin as the operational control layer
- BCAS as the biological alignment methodology
- Wearables as optional context enhancers
- Onboarding as the first activation flow

These decisions should not remain only inside conversations.

They should be documented clearly.

---

# What Should Be Recorded Here

Use this folder to record decisions that affect:

- Product architecture
- User experience architecture
- Data structure
- Admin logic
- Intelligence architecture
- Navigation
- Core flows
- System behavior
- Product boundaries
- Long-term implementation direction

---

# What Should Not Be Recorded Here

This folder should not be used for:

- Temporary notes
- Random ideas
- Minor copy changes
- Small UI preferences
- Unapproved concepts
- Draft marketing copy
- Daily task lists

Only important decisions should become architecture decision records.

---

# Decision File Format

Each architecture decision should have its own file.

Recommended filename format:

```text
DECISION_NAME.md
```

Example:

```text
HOME_AS_CENTRAL_OPERATING_SURFACE.md
```

Each decision should include:

- Title
- Status
- Date
- Context
- Decision
- Rationale
- Consequences
- Related documents

---

# Decision Status

Possible statuses:

```text
Proposed
Accepted
Active
Deprecated
Replaced
```

Most official decisions should use:

```text
Active
```

---

# Recommended Template

```markdown
# Decision Title

**Status:** Active

**Date:** Month Year

---

# Context

Explain the problem, situation or product conflict that led to this decision.

---

# Decision

State the decision clearly.

---

# Rationale

Explain why this decision was made.

---

# Consequences

Explain what this decision changes or prevents.

---

# Related Documents

List documents affected by this decision.
```

---

# Current Decisions

The current active architecture decisions are:

```text
HOME_CENTRAL.md
PUSH_ORCHESTRATION.md
```

---

# Current Planned Decisions

The next planned architecture decisions are:

```text
PLAN_TEMPLATES_DB.md
ADMIN_CONTROL_LAYER.md
ONBOARDING_ACTIVATION.md
```

---

# Related Documents

- README.md
- FOUNDATION/AAI_CONSTITUTION.md
- FOUNDATION/AAI_GLOSSARY.md
- FOUNDATION/AAI_PRINCIPLES.md
- FRAMEWORKS/POPAE.md
- PRODUCTS/WELLBINE/README.md
- PRODUCTS/WELLBINE/HOME.md
- PRODUCTS/WELLBINE/PUSH.md
- PRODUCTS/WELLBINE/PLAN_TEMPLATES.md
- PRODUCTS/WELLBINE/ADMIN.md
- PRODUCTS/WELLBINE/ONBOARDING.md
