# Admin As Operational Control Layer

**Status:** Active

**Date:** July 2026

---

# Context

Wellbine needs to evolve quickly.

The product will depend on many configurable areas:

- Plan Templates
- Onboarding
- Home
- Daily
- Push
- Pillars
- Daily Stack
- Wearables
- Settings
- Uploads
- Content
- Recommendations
- Users
- Analytics
- Publishing

If these areas are hardcoded, every normal business change would require developer work.

That would make the product slow, rigid and difficult to operate.

Wellbine should not depend on code changes for normal business updates.

The Admin system should act as the operational control layer of Wellbine.

---

# Decision

Admin is the operational control layer of Wellbine.

The Admin system should allow authorized operators to configure, update, publish, archive and manage the Wellbine experience without changing app code.

Admin should control business configuration.

Code should provide the product engine.

Admin should control the product behavior, content and configuration that change over time.

---

# Official Rule

```text
Admin is the operational control layer of Wellbine.
```

```text
Normal business configuration should not require code changes.
```

```text
The app should be built as an engine that reads Admin-managed configuration.
```

---

# Rationale

Wellbine is not a static app.

It needs to support:

- New plans
- New onboarding flows
- New Push sequences
- New pillar configurations
- New content modules
- New recommendations
- New settings
- New user journeys
- New commercial strategies
- New operational rules

These changes should be fast.

The product team should not need to wait for app redeployment every time a plan, Push, content module or recommendation changes.

Admin allows Wellbine to operate as a living system.

---

# Admin Versus App Code

App code should define:

- Core product engine
- Security rules
- Authentication
- Data access
- Rendering logic
- Core flows
- System integrations
- Technical infrastructure

Admin should define:

- Plan content
- Plan configuration
- Onboarding copy
- Onboarding structure
- Push copy
- Push timing
- Pillar defaults
- Daily sequences
- Home messages
- Content modules
- Recommendations
- Publishing status
- Business metadata

The product should separate stable engine logic from changing business configuration.

---

# Relationship With Supabase

Supabase may act as the direct database management layer.

Admin Panel should act as the preferred operational interface.

Both should manage the same underlying configuration.

Recommended relationship:

```text
Admin Panel
↓
Supabase Database
↓
Wellbine App
↓
User Experience
```

Supabase gives technical control.

Admin Panel gives operational control.

They should not become separate sources of truth.

---

# Relationship With Plan Templates

Plan Templates should be managed through Admin.

Admin should allow operators to:

- Create plans
- Edit plans
- Duplicate plans
- Preview plans
- Publish plans
- Archive plans
- Reorder plans
- Feature plans
- Configure pillars
- Configure Daily
- Configure Push
- Configure Home
- Configure Wearables
- Configure Settings
- Configure Content
- Configure Recommendations

Plan Templates are defined in:

```text
PRODUCTS/WELLBINE/PLAN_TEMPLATES.md
```

The architecture decision for database-driven plans is defined in:

```text
ARCHITECTURE_DECISIONS/PLAN_TEMPLATES_DB.md
```

---

# Relationship With Onboarding

Onboarding should be configurable through Admin.

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
- First Activation Mode copy

Onboarding should not require code changes for normal copy, option or flow adjustments.

---

# Relationship With Push

Push should be configurable through Admin.

Admin may control:

- Push cycles
- Push copy
- Push timing
- Push frequency
- Push response options
- Confirm behavior
- Adjust destination
- Later behavior
- Mental Detox mode
- Plan-specific Push
- Pillar-specific Push
- Recovery Push
- Daily Stack Push

Push should not become hardcoded generic reminders.

Push should remain an orchestration layer controlled by product logic and Admin configuration.

---

# Relationship With Home

Home should be configurable through Admin.

Admin may control:

- Current Insight templates
- Next Best Action templates
- Adaptive Summary priority
- Pillar visibility
- Pillar Orb Quick Panel options
- First Activation Mode copy
- Active Plan display
- Quick Actions
- Contextual Access Points

Home should remain the central operating surface.

Admin should help configure Home without turning it into a rigid dashboard.

---

# Relationship With Pillars

Pillars should be configurable through Admin.

Current pillars:

- Mind
- Sun
- Hydration
- Sleep
- Meal / Nutrition
- Movement
- Daily Stack

Admin may define for each pillar:

- Active / inactive
- Priority
- Target
- User-facing copy
- Daily behavior
- Push behavior
- Home visibility
- Quick Panel behavior
- Content modules
- Recommendations

Pillars should be operational modules, not hardcoded icons.

---

# Relationship With Content And Recommendations

Admin should control content and recommendations.

Content may include:

- Educational cards
- Guided meditations
- Breathing sessions
- Movement sequences
- Nutrition guidance
- Sleep guidance
- Hydration guidance
- Recovery explanations
- Plan-specific content

Recommendations may include:

- Daily actions
- Pillar actions
- Content
- Refill reminders
- Store items
- Partner offers
- External links

These should be configurable, reusable and contextual.

They should not require code deployment for normal updates.

---

# Relationship With Users

Admin may provide user-level operational visibility.

Possible user areas:

- User profile
- Active plan
- Plan history
- Push status
- Pillar status
- Wearable status
- Upload status
- Daily activity
- Stack status
- Settings
- Support state

User access should respect roles and permissions.

Not every admin role should see or edit every type of user information.

---

# Relationship With Publishing

Admin should support simple publishing states.

Recommended statuses:

```text
Draft
Published
Archived
```

These may apply to:

- Plan Templates
- Onboarding modules
- Push sequences
- Content modules
- Recommendations
- Pillar configurations
- Home messages

Publishing should make the product controllable without creating unnecessary bureaucracy.

---

# Business Flexibility Rule

The Admin system should not hardcode business decisions.

Admin should not hardcode:

- Plan names
- Plan categories
- Campaign logic
- Recommendation types
- Push labels
- Pillar emphasis
- Content structure
- Store access
- Onboarding copy

These should remain configurable.

The business should be able to test, adjust and evolve.

The software should support the business, not trap it.

---

# Consequences

This decision means:

- Admin becomes a central part of the product architecture.
- Normal business configuration should not require code changes.
- Plan Templates should be managed through Admin.
- Onboarding should be configurable through Admin.
- Push should be configurable through Admin.
- Home behavior should be configurable through Admin.
- Pillars should be configurable through Admin.
- Content and recommendations should be configurable through Admin.
- Supabase may serve as the direct data layer.
- Admin Panel should become the preferred operational interface.
- The app should read Admin-managed configuration where practical.

---

# What This Prevents

This decision prevents:

- Hardcoded business logic
- Slow plan iteration
- Developer dependency for normal product updates
- Static onboarding
- Static Push sequences
- Static pillar configuration
- Static recommendations
- Admin Panel and Supabase becoming inconsistent
- Wellbine becoming rigid
- Business decisions being blocked by code deployment

---

# Related Documents

- README.md
- ARCHITECTURE_DECISIONS/README.md
- ARCHITECTURE_DECISIONS/HOME_CENTRAL.md
- ARCHITECTURE_DECISIONS/PUSH_ORCHESTRATION.md
- ARCHITECTURE_DECISIONS/PLAN_TEMPLATES_DB.md
- PRODUCTS/WELLBINE/README.md
- PRODUCTS/WELLBINE/ADMIN.md
- PRODUCTS/WELLBINE/PLAN_TEMPLATES.md
- PRODUCTS/WELLBINE/ONBOARDING.md
- PRODUCTS/WELLBINE/HOME.md
- PRODUCTS/WELLBINE/DAILY.md
- PRODUCTS/WELLBINE/PUSH.md
- PRODUCTS/WELLBINE/PILLARS.md
- PRODUCTS/WELLBINE/STACK.md
