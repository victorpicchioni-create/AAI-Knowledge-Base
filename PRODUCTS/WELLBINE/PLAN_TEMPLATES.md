# Wellbine Plan Templates

**Version:** 0.1.0

**Status:** Active

**Last Updated:** July 2026

---

# Purpose

This document defines Plan Templates in Wellbine.

Plan Templates are predefined, admin-managed starting points that allow users to activate a complete health, performance or longevity experience without building everything manually.

A Plan Template should activate:

- Pillar defaults
- Daily guidance
- Push sequences
- Home state
- Wearable behavior
- Settings defaults
- Protocol rules
- Content modules
- Product or service recommendations when relevant

Plan Templates should be database-driven and editable without code changes.

---

# Official Definition

**Wellbine Plan Templates are flexible admin-managed configurations that activate and organize the Wellbine experience across Home, Daily, Push, Pillars, Wearables, Settings and user guidance.**

---

# Core Principle

Plan Templates should not be hardcoded.

Plans should be managed as flexible content and configuration.

The admin should be able to create, edit, duplicate, publish, archive and reorganize plans without changing app code.

The engine should be built once.

Plans should be managed through data.

---

# Flexibility Principle

The Plan Template system must remain flexible.

The admin should not be blocked by unnecessary restrictions.

The admin should be able to define:

- Plan name
- Plan category
- Plan goal
- Plan duration
- Plan description
- Pillar behavior
- Push behavior
- Daily behavior
- Home behavior
- Wearable behavior
- Settings defaults
- Content modules
- Store or external recommendations
- Safety notes
- Internal notes
- Display order
- Featured status
- Availability status

The panel should be simple to use.

The plan system should support business decisions without becoming a technical bottleneck.

---

# Admin Control Principle

The plan system should be database-driven.

The admin should be able to update plans through:

- Supabase
- Admin Panel

Both paths should control the same plan data.

The Admin Panel is the preferred operational interface.

Supabase remains a direct database management path.

The admin should not need to redeploy the app to update plans.

---

# Plan Template Architecture

Recommended architecture:

```text
Admin Management Layer

↓

Supabase Database

↓

Wellbine App

↓

User selects plan

↓

User Active Plan Snapshot is created

↓

Home + Daily + Push + Pillars + Wearables + Settings activate automatically
```

The app should read active Plan Templates from the database.

The app should not require code changes when plans are created, edited, published or archived.

---

# Admin Management Options

Wellbine should support two valid administration paths:

1. Direct Supabase management
2. Administrative Panel management

Both paths should update the same database-driven plan system.

---

## Direct Supabase Management

The admin may manage Plan Templates directly through Supabase.

This path is useful for:

- Fast edits
- Advanced data control
- Emergency fixes
- Internal testing
- Database-level corrections

Direct Supabase management gives full control.

---

## Administrative Panel Management

The preferred operational experience is an internal Admin Panel.

Possible route:

```text
Admin → Plan Templates
```

The Admin Panel should allow:

- Create Plan
- Edit Plan
- Duplicate Plan
- Preview Plan
- Publish Plan
- Archive Plan
- Reorder Plans
- Feature Plans
- Edit Pillars
- Edit Push
- Edit Daily
- Edit Home
- Edit Wearables
- Edit Settings
- Edit Content
- Edit Store or External Recommendations
- Edit Safety Notes
- Edit Internal Notes

The Admin Panel should make plan management faster, safer and easier.

The admin should not need to touch code.

---

# Admin Usability Principle

The admin experience should be simple.

A plan should feel like editing a structured content object, not like programming.

The admin should be able to build a plan by selecting and editing sections.

Recommended sections:

```text
Basic Info
Goals
Audience
Pillars
Daily
Push
Home
Wearables
Settings
Content
Recommendations
Safety Notes
Internal Notes
Publish
Preview
```

The admin should be able to save partial progress.

The admin should be able to duplicate existing plans and modify them quickly.

---

# Plan Status Lifecycle

Plan Templates should use simple status management.

Recommended statuses:

- Draft
- Published
- Archived

---

## Draft

The plan is being created or edited.

It does not appear to users unless preview mode is enabled.

---

## Published

The plan is live and available for users.

---

## Archived

The plan is no longer available for new users.

Archived plans should preserve history.

---

# Delete Rule

Plan deletion should be possible only when safe.

Preferred default action:

```text
Archive
```

Delete may be used for:

- Test plans
- Unused drafts
- Admin cleanup

Published or previously activated plans should generally be archived rather than deleted.

---

# Plan Versioning

Plan Templates may support versioning.

Versioning allows the admin to improve plans over time while preserving user history.

Example:

```text
Metabolic Support Plan v1

↓

Metabolic Support Plan v2
```

Versioning should help the system:

- Preserve history
- Compare plan performance
- Avoid breaking user data
- Allow controlled updates

---

# Plan Snapshot Rule

When a user activates a Plan Template, Wellbine should create a user-specific plan snapshot.

Recommended logic:

```text
Plan Template

↓

User activates plan

↓

User Active Plan Snapshot is created

↓

User follows the snapshot
```

This allows the user to personalize a plan without changing the original template.

---

# Plan Update Rule

When the admin updates a Plan Template, the system should support flexible update behavior.

Possible update modes:

- Apply only to new users
- Offer update to existing users
- Apply to selected user groups
- Apply manually through admin
- Keep existing users on their current snapshot

The admin should be able to choose the correct behavior when needed.

---

# Relationship With AAI

AAI uses Plan Templates as structured starting points.

A Plan Template gives AAI an initial operating context.

AAI then learns from user behavior and adapts over time.

Plan Templates may provide:

- Initial goals
- Initial pillar priorities
- Initial protocol rules
- Initial Daily sequences
- Initial Push logic
- Initial Home state
- Initial wearable expectations
- Initial settings defaults
- Initial content guidance
- Initial recovery assumptions

A Plan Template is the starting configuration.

AAI provides adaptation.

---

# Relationship With BCAS

Plan Templates should support BCAS.

This means plans should be configurable around biological context, not only fixed time.

Examples:

- Sleep actions may align with Sleep Preparation Window.
- Meal actions may align with Feeding Windows.
- Sun actions may align with Wake Window or Morning Reset.
- Movement may depend on readiness, recovery and energy.
- Hydration may adapt to protocol, fasting, movement and recovery.
- Daily Stack may respect food, timing, medication and supplement context.

The admin should be able to define both:

- Time-based rules
- Context-based rules

The system should support both when useful.

---

# Relationship With Pillars

Plan Templates activate and configure operational pillars.

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
- Default behavior
- Target
- Context windows
- Push behavior
- Daily behavior
- Home visibility
- Recovery logic
- Manual adjustment rules
- Content modules
- Linked recommendations

Pillars should be configurable from the plan.

A plan should define how the pillars work together.

---

# Pillar Configuration

Each pillar may have its own configuration block.

Example:

```text
Hydration

Active: Yes
Unit: Cups
Electrolytes: Enabled
Morning reminder: Yes
Midday check-in: Yes
Evening check-in: Yes
Home visibility: High
```

Another example:

```text
Sleep

Active: Yes
Sleep planning: Enabled
Alarm sync option: Enabled
Recovery estimate: Enabled
Night Reset: Enabled
Home visibility: High
```

Another example:

```text
Movement

Active: Yes
Intensity: Adaptive
Strong movement: Optional
Recovery movement: Enabled
Post-meal walk: Enabled
Home visibility: Medium
```

The admin should be able to adjust these configurations without code.

---

# Relationship With Daily

Plan Templates should define the user's initial Daily flow.

A plan may define:

- Morning sequence
- Midday sequence
- Evening sequence
- Night sequence
- Recovery sequence
- Active Context Windows
- Next Best Action logic
- Window Closed logic
- Daily Stack timing
- Meal timing
- Movement intensity
- Hydration checkpoints
- Sleep planning logic
- Mind reset timing
- Sunlight guidance

Daily should execute the plan without overwhelming the user.

---

# Relationship With Push

Plan Templates should define Push behavior.

Default Push structure:

1. Morning Activation
2. Midday Alignment
3. Evening Alignment
4. Night Reset

A plan may define:

- Push timing windows
- Context questions
- Response options
- Follow-up plans
- Confirm behavior
- Adjust destination
- Later timing
- Recovery variations
- Frequency rules
- Push tone
- Push priority

Default target:

```text
3 to 4 main Push cycles per day
```

The admin should be able to adjust Push behavior by plan.

---

# Relationship With Home

Plan Templates should define the user's initial Home state.

Home may display:

- Active Plan
- Current Insight
- Next Best Action
- Pillar emphasis
- Adaptive Summary priority
- Recovery state
- First Activation completion state

Example:

```text
Active Plan

Metabolic Support Plan

Next Best Action

Hydration + protein meal planning.
```

Plan awareness should guide Home quietly.

The plan should not dominate the interface.

---

# Relationship With Wearables

Plan Templates should define how wearable data is used.

Wearable-related configuration may include:

- Wearable required / optional
- Wearable recommended message
- Sleep data usage
- HRV usage
- Resting heart rate usage
- Movement detection
- Inactivity detection
- Recovery estimation
- Stress signals
- Wearable-based Push reduction
- Manual fallback when no wearable is connected

Example:

```text
Wearable behavior

Wearable: Optional
Use sleep data: Yes
Use recovery data: Yes
Use movement data: Yes
If no wearable: Use Push check-ins
```

The user should not be punished for not having a wearable.

Plans should work with or without wearable data.

---

# Relationship With Settings

Plan Templates may define initial Settings defaults.

Settings may include:

- Push frequency
- Preferred wake time
- Preferred sleep time
- Units
- Language
- Time zone
- Measurement preferences
- Dietary preferences
- Training level
- Notification style
- Wearable preference
- Privacy preference

The user should always be able to adjust personal settings.

Plan settings are starting defaults, not permanent restrictions.

---

# Relationship With Content

Plan Templates may include content modules.

Content modules may include:

- Educational cards
- Guided meditations
- Breathing sessions
- Movement videos
- Meal guidance
- Sleep guidance
- Hydration guidance
- Daily Stack instructions
- Recovery explanations
- Weekly summaries
- Onboarding explanations

The admin should be able to attach content to a plan.

Content should be reusable across multiple plans.

---

# Relationship With Recommendations

Plan Templates may include recommendations.

Recommendations may include:

- Products
- Services
- Content
- Daily actions
- Pillar actions
- Plan upgrades
- External links
- Store items
- Refill reminders

Recommendations should be optional and contextual.

The admin should be able to enable or disable recommendations per plan.

---

# Relationship With Onboarding

Plan Templates are central to first access.

If a user opens Wellbine for the first time, the app should guide the user to choose a starting plan.

This belongs mainly to:

```text
ONBOARDING.md
```

But Plan Templates provide the options that Onboarding will display.

Example first access flow:

```text
Choose your main goal

↓

Suggested Plan Templates

↓

Select plan

↓

Adjust constraints

↓

Activate 7-Day Sync Plan

↓

Enter Home
```

---

# Relationship With Admin

Plan Template administration should eventually be defined in:

```text
ADMIN.md
```

This document defines what Plan Templates are and how they should behave.

The future Admin document should define the broader admin experience, including:

- Admin roles
- Admin permissions
- Plan management
- Pillar management
- Wearable settings
- Content management
- Push management
- User management
- Settings management
- Recommendations
- Analytics
- Publishing workflows

Plan Template administration should not require one separate document per action at this stage.

A single future `ADMIN.md` should be enough until the admin system becomes more complex.

---

# Suggested Database Structure

The exact database structure may evolve, but the recommended model is:

---

## plan_templates

Stores the main plan metadata.

Suggested fields:

- id
- name
- slug
- category
- short_description
- long_description
- status
- is_featured
- display_order
- duration_days
- difficulty_level
- goal_tags
- audience_tags
- internal_notes
- safety_notes
- created_at
- updated_at

---

## plan_template_versions

Stores versioned plan configurations.

Suggested fields:

- id
- plan_template_id
- version_number
- pillar_config
- push_config
- daily_config
- home_config
- wearable_config
- settings_config
- content_config
- recommendation_config
- protocol_rules
- onboarding_rules
- safety_notes
- internal_notes
- created_at
- published_at

---

## user_active_plans

Stores the user-specific activated plan snapshot.

Suggested fields:

- id
- user_id
- plan_template_id
- plan_template_version_id
- plan_snapshot
- status
- start_date
- end_date
- current_day
- created_at
- updated_at

---

## plan_events

Stores plan-related history.

Suggested events:

- Plan activated
- Plan paused
- Plan completed
- Plan changed
- Plan archived
- Plan adjusted
- Plan restarted
- Plan migrated

---

# Plan Template Fields

A Plan Template should support configurable areas.

---

## Basic Information

- Plan name
- Plan slug
- Category
- Short description
- Long description
- Duration
- Difficulty
- Main goal
- Suggested audience
- Internal notes
- Safety notes

---

## Pillar Configuration

- Mind
- Sun
- Hydration
- Sleep
- Meal / Nutrition
- Movement
- Daily Stack

For each pillar:

- Active / inactive
- Priority
- Default target
- Context windows
- Push behavior
- Daily behavior
- Home visibility
- Recovery logic
- Manual adjustment rules
- Content
- Recommendations

---

## Push Configuration

- Morning Activation
- Midday Alignment
- Evening Alignment
- Night Reset
- Timing windows
- Questions
- Response options
- Follow-up plans
- Confirm behavior
- Adjust destination
- Later behavior
- Recovery variations

---

## Daily Configuration

- Morning sequence
- Midday sequence
- Evening sequence
- Night sequence
- Recovery options
- Window states
- Daily Stack timing
- Meal timing
- Movement intensity
- Hydration checkpoints
- Sleep planning logic
- Mind reset logic
- Sunlight guidance

---

## Home Configuration

- Active Plan label
- First Current Insight
- First Next Best Action
- Pillar emphasis
- Adaptive Summary priority
- Recovery language
- First Activation state
- Home visibility rules

---

## Wearable Configuration

- Wearable optional / recommended / required
- Sleep data usage
- Recovery data usage
- Movement data usage
- HRV usage
- Stress signal usage
- Manual fallback logic

---

## Settings Configuration

- Push frequency
- Preferred wake time
- Preferred sleep time
- Units
- Language
- Time zone
- Diet preferences
- Training level
- Notification style
- Privacy defaults

---

## Content Configuration

- Educational content
- Meditation content
- Breathing content
- Movement content
- Nutrition content
- Sleep content
- Hydration content
- Recovery content

---

## Recommendation Configuration

- Store items
- External products
- Services
- Plan upgrades
- Refill reminders
- Educational links
- Partner offers

---

# Plan Categories

Plan categories should be admin-defined.

The system should not force a fixed category list.

The admin may create categories such as:

- Performance
- Weight Loss
- Longevity
- Recovery
- Nutrition
- Sleep
- Stress
- Metabolic Support
- Custom

Categories should help organize plans.

They should not restrict plan creation.

---

# Plan Naming

Plan names should be admin-defined.

The system should allow flexible naming.

The admin may use:

- Brand-owned names
- Protocol-style names
- Goal-based names
- Campaign names
- Internal test names
- Region-specific names
- Seasonal names

The app should not hardcode naming restrictions.

If needed, legal or compliance review can happen as a separate internal process.

Naming should not make the plan system harder to operate.

---

# Example Plan Template

Example:

```text
Metabolic Support Plan
```

Category:

```text
Metabolic Support
```

Primary pillars:

- Meal / Nutrition
- Hydration
- Movement
- Sleep
- Daily Stack
- Mind

Default rules:

- Protein focus
- Smaller meals
- Hydration checkpoints
- Electrolytes if included in protocol
- Strength preservation
- Gentle movement
- Sleep consistency
- Digestive comfort check-ins

Example Push:

```text
How is your energy and appetite today?

Stable
Low
Heavy
```

Follow-up plan:

```text
Today's support plan:

Hydration
Protein-focused meal
Light movement
Sleep plan
Daily Stack, if scheduled

Ok?

Confirm
Adjust
Later
```

---

# Plan Activation Logic

When a user selects a plan, Wellbine should activate:

- Plan snapshot
- Pillar defaults
- Daily flow
- Push sequence
- Home state
- Wearable behavior
- Settings defaults
- Sync baseline
- Recovery logic
- Protocol rules
- Content modules
- Recommendations, if enabled

Activation flow:

```text
User selects Plan Template

↓

Wellbine creates User Active Plan Snapshot

↓

Pillars receive default configuration

↓

Daily receives first execution flow

↓

Push receives first cycle logic

↓

Home enters active plan state

↓

Wearable and Settings defaults are applied

↓

AAI begins learning from behavior
```

---

# Plan Adjustment Logic

Users should be able to adjust their active plan without destroying the original template.

User adjustments should be stored in the user's active plan snapshot.

Examples of possible user adjustments:

- Change wake time
- Change sleep target
- Disable a pillar
- Change meal preference
- Change movement intensity
- Modify Daily Stack items
- Change Push frequency
- Change fasting preference
- Change wearable preference
- Change notification preference

These changes should affect the user snapshot, not the original template.

---

# Admin Preview

Before publishing a plan, the admin should be able to preview:

- Home first state
- Daily sequence
- Push cycles
- Pillar defaults
- Wearable behavior
- Settings defaults
- Content modules
- Recommendations
- User-facing description

Preview should help the admin understand the plan experience before publishing.

---

# Admin Publish Rules

Publishing should be simple.

A plan should be publishable when the admin decides it is ready.

Recommended minimum fields:

- Name
- Status
- At least one active pillar
- Basic Home state
- Basic Daily logic

The admin panel should help identify missing data, but it should not create unnecessary friction.

---

# Safety Notes

Safety notes may exist as metadata.

They should help the admin organize sensitive or important information.

Safety notes should not make the plan builder difficult to use.

Detailed medical, legal or regulatory controls should be defined later in a dedicated admin or safety document if needed.

---

# What Plan Templates Are

Plan Templates are:

- Flexible
- Editable
- Admin-managed
- Database-driven
- Configurable
- Reusable
- Duplicable
- Publishable without code
- Connected to Home, Daily, Push, Pillars, Wearables and Settings

Plan Templates are adaptive starting points.

---

# Current Status

Plan Templates are being defined as flexible admin-managed, database-driven starting points for Wellbine.

The next implementation priorities are:

- Database schema
- Admin Management Options
- Admin publish / archive logic
- Plan activation logic
- User active plan snapshot
- First Access integration
- Home active plan state
- Daily and Push configuration from plans
- Pillar default activation
- Wearable configuration
- Settings configuration
- Content configuration
- Recommendation configuration

---

# Future Evolution

Future versions of Plan Templates may include:

- Full Admin Panel
- Drag-and-drop plan builder
- AI-assisted plan creation
- Plan preview simulator
- Plan version comparison
- Plan performance analytics
- User cohort comparison
- Personalized plan recommendations
- Automatic plan adjustment
- Admin-managed offer integration
- Region-specific plan availability
- Content module library
- Wearable-specific plan variants

---

# Related Documents

- FOUNDATION/AAI_CONSTITUTION.md
- FOUNDATION/AAI_GLOSSARY.md
- FOUNDATION/AAI_PRINCIPLES.md
- FRAMEWORKS/POPAE.md
- PRODUCTS/WELLBINE/README.md
- PRODUCTS/WELLBINE/PRODUCT.md
- PRODUCTS/WELLBINE/BCAS.md
- PRODUCTS/WELLBINE/HOME.md
- PRODUCTS/WELLBINE/DAILY.md
- PRODUCTS/WELLBINE/PUSH.md
- PRODUCTS/WELLBINE/PILLARS.md
- PRODUCTS/WELLBINE/STACK.md
