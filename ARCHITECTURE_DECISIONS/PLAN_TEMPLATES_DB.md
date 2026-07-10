# Plan Templates As Database-Driven Configuration

**Status:** Active

**Date:** July 2026

---

# Context

Wellbine uses Plan Templates as one of the main structures for activating the user experience.

A Plan Template is not just a content page.

A Plan Template defines how the Wellbine experience starts for a user.

It may activate and configure:

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
- User guidance
- First 7-Day Sync Plan

If Plan Templates are hardcoded into the app, every business update would require developer work and app redeployment.

That would make Wellbine slow, rigid and difficult to operate.

Wellbine needs the ability to create, edit, duplicate, preview, publish, archive and adjust plans quickly.

For this reason, Plan Templates must be database-driven and admin-managed.

---

# Decision

Plan Templates must be database-driven configurations.

Plan Templates should be editable without code changes through Supabase or an Admin Panel.

The app should read Plan Template configuration from the database and use it to activate the correct user experience.

Plan Templates should not be hardcoded into the application.

---

# Official Rule

```text
Plan Templates are database-driven configurations.
```

```text
Plan Templates should be admin-managed.
```

```text
Normal Plan Template updates should not require code changes.
```

---

# Rationale

Wellbine needs business flexibility.

The product team should be able to create and adjust plans without waiting for app development.

Examples:

- Add a longevity plan
- Add a recovery plan
- Add a metabolic plan
- Duplicate an existing plan
- Change plan copy
- Change pillar priority
- Change Push frequency
- Change Daily sequence
- Change Home starting state
- Change wearable defaults
- Change recommendations
- Archive an old plan
- Publish a new version

These are product and business operations.

They should not require code deployment.

A database-driven Plan Template system allows Wellbine to evolve faster.

---

# What Plan Templates Configure

A Plan Template may configure:

- Plan name
- Plan description
- Plan category
- Plan goals
- Plan duration
- Featured status
- Home starting state
- Daily sequence
- Push cycles
- Pillar defaults
- Daily Stack defaults
- Wearable behavior
- Settings defaults
- Upload options
- Content modules
- Recommendations
- Internal notes
- Admin metadata
- Version status
- Publishing status

Plan Templates should be flexible enough to support different business models, user goals and product strategies.

---

# Relationship With Admin

Admin is the operational control layer for Plan Templates.

The Admin system should allow authorized operators to manage Plan Templates without code changes.

Admin should support:

- Create Plan
- Edit Plan
- Duplicate Plan
- Preview Plan
- Publish Plan
- Archive Plan
- Reorder Plans
- Feature Plans
- Assign categories
- Edit descriptions
- Edit pillar configuration
- Edit Daily configuration
- Edit Push configuration
- Edit Home configuration
- Edit Wearable behavior
- Edit Settings defaults
- Edit Content modules
- Edit Recommendations
- Add internal notes

The Admin Panel is the preferred operational interface.

Supabase remains a valid direct management path for advanced control.

---

# Relationship With Supabase

Supabase may act as the source of truth for Plan Template data.

The app should read Plan Template configuration from Supabase or from a backend layer connected to Supabase.

Supabase may store:

- Plan templates
- Plan versions
- User active plan snapshots
- Plan events
- Pillar configuration
- Push configuration
- Daily configuration
- Home configuration
- Content modules
- Recommendations
- Settings defaults

Supabase gives full database control.

The Admin Panel gives safer and easier operational control.

Both should remain consistent.

---

# Relationship With User Active Plan Snapshot

When a user activates a Plan Template, Wellbine should create a user active plan snapshot.

The snapshot represents the user's personal version of the plan.

This is important because the user's plan may evolve after activation.

Example:

```text
Plan Template
↓
User activates plan
↓
User Active Plan Snapshot is created
↓
User adjustments modify the snapshot
↓
Original Plan Template remains unchanged
```

This prevents individual user behavior from changing the original template.

It also allows the same template to serve many users while still supporting personalization.

---

# Template Versus Snapshot

Plan Template:

```text
The reusable starting configuration.
```

User Active Plan Snapshot:

```text
The user's personalized active version of that configuration.
```

Example:

```text
LONG40 Template
↓
Victor's LONG40 Snapshot
```

The template remains stable.

The snapshot adapts.

---

# Relationship With Onboarding

Onboarding uses Plan Templates to activate the first user experience.

The user may choose:

- Recommended Plan
- Adapted Plan

Recommended Plan is suggested from user profile and goals.

Adapted Plan starts from a template and allows simple adjustments before activation.

Onboarding should not force the user to build a plan from zero.

Plan Templates provide the starting structure.

Onboarding activates it.

---

# Relationship With Home

Plan Templates should configure the initial Home state.

A Plan Template may define:

- Active plan display
- First Current Insight
- First Next Best Action
- Pillar visibility
- Pillar priority
- Adaptive Summary emphasis
- Quick Actions
- First Activation transition
- Contextual Access Points

After plan activation, Home should not be blank.

Home should immediately show the user's active plan and next useful action.

---

# Relationship With Daily

Plan Templates should configure the initial Daily flow.

A Plan Template may define:

- Morning sequence
- Midday sequence
- Evening sequence
- Night sequence
- Recovery logic
- Meal / Nutrition logic
- Hydration checkpoints
- Movement defaults
- Sleep planning defaults
- Mind reset defaults
- Sunlight guidance
- Daily Stack timing

Daily should start from the active plan configuration.

The user should not need to manually assemble the day.

---

# Relationship With Push

Plan Templates should configure starting Push behavior.

A Plan Template may define:

- Push cycles
- Push frequency
- Push timing windows
- Push copy
- Push tone
- Push response options
- Confirm behavior
- Adjust destination
- Later behavior
- Mental Detox defaults
- Pillar-specific Push
- Daily Stack Push
- Recovery Push

Push should not be hardcoded globally for all users.

Push should respect plan context.

---

# Relationship With Pillars

Plan Templates should configure Pillar defaults.

Current pillars:

- Mind
- Sun
- Hydration
- Sleep
- Meal / Nutrition
- Movement
- Daily Stack

A Plan Template may define for each pillar:

- Active / inactive
- Priority
- Target
- Starting behavior
- Daily behavior
- Push behavior
- Home visibility
- Quick Panel behavior
- Content modules
- Recommendations

Pillars should become operational when a plan is activated.

---

# Relationship With Wearables

Plan Templates may define wearable behavior.

Examples:

- Wearable optional
- Wearable recommended
- Wearable-specific insights enabled
- Manual fallback enabled
- Sleep signal usage
- Movement signal usage
- Recovery signal usage
- HRV usage
- Resting heart rate usage
- Temperature trend usage
- Respiratory rate usage
- Oxygen saturation usage
- Cycle-related signal usage when supported

Wearables should improve the plan.

Wearables should not be required for the plan to work.

---

# Relationship With Settings

Plan Templates may define default settings.

Examples:

- Language
- Time zone
- Units
- Push frequency
- Mental Detox default
- Wake preference
- Sleep preference
- Dietary preference
- Training level
- Wearable preference
- Upload preference

User settings should be editable.

The template defines the starting defaults.

The user active plan snapshot and user settings may override them.

---

# Relationship With Content

Plan Templates may activate specific content modules.

Examples:

- Educational cards
- Breathing sessions
- Meditation sessions
- Movement sequences
- Sleep guidance
- Hydration guidance
- Nutrition guidance
- Daily Stack instructions
- Recovery explanations
- Weekly summaries

Content should be reusable across multiple plans.

The same content module may appear in different templates.

---

# Relationship With Recommendations

Plan Templates may define recommendation logic.

Recommendations may include:

- Content
- Daily actions
- Pillar actions
- Store items
- Refill reminders
- Plan upgrades
- Partner offers
- External links

Recommendations should remain contextual.

They should not dominate the product experience.

The plan may define what is eligible.

AAI and user behavior may define when it appears.

---

# Versioning

Plan Templates should support versioning when useful.

Versioning allows Wellbine to preserve history and control updates.

Possible statuses:

```text
Draft
Published
Archived
```

A published plan may later receive a new version.

Existing users may:

- Keep their current snapshot
- Be offered an update
- Be migrated manually
- Be migrated by selected group
- Receive update only if admin chooses

Plan updates should not automatically disrupt active users unless intentionally configured.

---

# Publishing

Publishing should be simple.

Admin should be able to:

- Save draft
- Preview
- Publish
- Archive

Minimum publishing requirements may include:

- Plan name
- Status
- At least one active pillar
- Basic Home state
- Basic Daily logic

Publishing should not require excessive bureaucracy.

The goal is to make the business faster, not slower.

---

# Archiving

Published or previously used plans should generally be archived, not deleted.

Archive preserves history and avoids breaking references.

Delete may be allowed only for:

- Test plans
- Unused drafts
- Mistaken entries with no user dependency

Archiving should be the safer default.

---

# Admin Flexibility

The Admin system should not impose unnecessary business restrictions on Plan Templates.

Admin should not hardcode:

- Plan names
- Plan categories
- Campaign structure
- Marketing angle
- Plan positioning
- Plan order
- Featured plans
- Recommendation types

These should remain configurable.

Business decisions should be made by the product and business team.

The software should support them.

---

# Data Model Direction

A future implementation may include tables such as:

```text
plan_templates
plan_template_versions
user_active_plans
plan_events
```

Additional related tables may include:

```text
plan_pillar_configs
plan_push_configs
plan_daily_configs
plan_home_configs
plan_content_modules
plan_recommendations
plan_settings_defaults
```

The exact implementation may evolve.

The architectural direction is that Plan Templates should be represented as data, not hardcoded behavior.

---

# Consequences

This decision means:

- Plan Templates must be managed as data.
- Normal plan updates should not require code changes.
- Admin must be able to create, edit, duplicate, publish and archive plans.
- Supabase may serve as the direct data management layer.
- Admin Panel should become the preferred operational interface.
- Plan activation should create a user active plan snapshot.
- User personalization should modify the snapshot, not the original template.
- Home, Daily, Push, Pillars, Wearables, Settings, Content and Recommendations should be configurable from the plan.
- Plan updates should support versioning and controlled rollout.

---

# What This Prevents

This decision prevents:

- Hardcoded plans
- Developer dependency for normal plan updates
- Slow product iteration
- Inflexible business logic
- One-size-fits-all user experience
- Plan edits affecting users unintentionally
- User personalization changing the original template
- Admin Panel and Supabase becoming inconsistent
- Plan Templates becoming only static content pages

---

# Related Documents

- README.md
- ARCHITECTURE_DECISIONS/README.md
- ARCHITECTURE_DECISIONS/HOME_CENTRAL.md
- ARCHITECTURE_DECISIONS/PUSH_ORCHESTRATION.md
- PRODUCTS/WELLBINE/README.md
- PRODUCTS/WELLBINE/PLAN_TEMPLATES.md
- PRODUCTS/WELLBINE/ADMIN.md
- PRODUCTS/WELLBINE/ONBOARDING.md
- PRODUCTS/WELLBINE/HOME.md
- PRODUCTS/WELLBINE/DAILY.md
- PRODUCTS/WELLBINE/PUSH.md
- PRODUCTS/WELLBINE/PILLARS.md
- PRODUCTS/WELLBINE/STACK.md
