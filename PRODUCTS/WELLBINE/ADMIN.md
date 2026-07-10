# Wellbine Admin

**Version:** 0.1.0

**Status:** Active

**Last Updated:** July 2026

---

# Purpose

This document defines the Wellbine Admin system.

The Admin system is the operational control layer of Wellbine.

Its purpose is to allow the business, product and operations team to configure, manage, publish, update and adjust the Wellbine experience without changing app code.

Admin should control:

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
- Internal notes

The Admin system should make Wellbine flexible, fast to operate and easy to evolve.

---

# Official Definition

**Wellbine Admin is the internal management system that allows authorized operators to configure and update the Wellbine experience across Plans, Onboarding, Home, Daily, Push, Pillars, Wearables, Settings, Uploads, Content and Recommendations without code changes.**

---

# Core Principle

The Admin system must not make the business rigid.

The Admin system should not create unnecessary friction.

The Admin system should make Wellbine easier to operate, not harder.

The product engine should be built once.

Business logic, content, plans, sequences, recommendations and user-facing configurations should be managed through data.

---

# Main Admin Rule

The Admin system should follow one rule:

```text
Business configuration should not require code changes.
```

The admin should be able to update the product experience quickly.

Examples:

- Add a new plan
- Edit an existing plan
- Change Onboarding text
- Reorder recommended plans
- Change Push copy
- Update pillar behavior
- Enable or disable a content module
- Change Home insight priority
- Adjust wearable fallback behavior
- Update Daily Stack guidance
- Add a recommendation
- Archive an old plan
- Publish a new version

without asking a developer to redeploy the app.

---

# Admin Philosophy

The Admin system should be:

- Flexible
- Fast
- Practical
- Clear
- Modular
- Database-driven
- Easy to operate
- Safe enough without becoming restrictive

Admin should feel like operating a business system, not programming.

The goal is not to create a complex enterprise dashboard.

The goal is to give the Wellbine team direct control over the product experience.

---

# Relationship With AAI

AAI is the intelligence architecture.

Admin is the control layer that defines what AAI can use, configure, display and activate.

Admin may define:

- Available Plan Templates
- Initial contexts
- Pillar priorities
- Push sequences
- User-facing content
- Recommendations
- Settings defaults
- Content modules
- Safety notes
- Internal instructions

AAI then uses these configurations to personalize and adapt the user experience.

Admin defines the starting environment.

AAI adapts within that environment.

---

# Relationship With POPAE

POPAE is the operating cycle of AAI:

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

Admin supports POPAE by allowing operators to define:

- What the system prepares
- What signals matter
- What predictions are useful
- What actions can be suggested
- What feedback should update future behavior

Admin should not expose POPAE complexity to normal users.

Admin should allow the product team to configure how POPAE becomes visible through Wellbine.

---

# Relationship With BCAS

BCAS organizes Wellbine around biological context.

Admin should allow the team to configure context-based logic.

Examples:

- Wake Window
- Feeding Window
- Movement Window
- Recovery Window
- Sleep Preparation Window
- Hydration Opportunity
- Daily Stack Window

Admin should support both:

- Time-based rules
- Context-based rules

The system should not force every flow into rigid times.

Admin should allow flexible biological context rules where useful.

---

# Admin Architecture

Recommended architecture:

```text
Admin Panel

↓

Supabase Database

↓

Wellbine App

↓

User Experience

↓

AAI Learning
```

The Admin Panel should update the same database-driven configuration that the app reads.

Supabase remains the direct database management layer.

The Admin Panel is the preferred operational interface.

---

# Admin Management Paths

Wellbine should support two valid administration paths.

---

## 1. Admin Panel

The Admin Panel is the preferred interface for daily operation.

It should be simple, visual and organized by product areas.

Possible route:

```text
/admin
```

or:

```text
Admin → Dashboard
```

The Admin Panel should allow the team to manage Wellbine without touching code.

---

## 2. Direct Supabase Management

Supabase may also be used directly.

This is useful for:

- Advanced data control
- Emergency fixes
- Internal testing
- Technical corrections
- Fast database-level updates

Supabase gives full control.

The Admin Panel gives safer and easier control.

Both should update the same system.

---

# Admin Usability Principle

The Admin interface should be easy to use.

Admin should not require technical knowledge for normal operations.

Good Admin experience:

```text
Create
Edit
Preview
Publish
Archive
Duplicate
Reorder
Save Draft
```

Bad Admin experience:

```text
Edit JSON manually for every change
Understand backend logic
Wait for developer deployment
Use hardcoded app rules
Break user experience accidentally
```

The Admin Panel should hide complexity when possible.

Advanced controls can exist, but daily operations should remain simple.

---

# Admin Dashboard

The Admin Dashboard should provide a high-level overview.

Possible sections:

- Plans
- Onboarding
- Home
- Daily
- Push
- Pillars
- Stack
- Wearables
- Settings
- Uploads
- Content
- Recommendations
- Users
- Analytics
- Publishing

The dashboard should show:

- Active plans
- Draft plans
- Recently updated items
- Published content
- Archived items
- User activity signals
- Pending uploads
- Push performance
- Onboarding completion
- Plan activation
- Key alerts

The dashboard should help the admin know what needs attention.

---

# Core Admin Modules

The Admin system should include the following modules.

---

# 1. Plan Templates Admin

Plan Templates are one of the most important Admin areas.

The admin should be able to manage plans without code changes.

Actions:

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
- Edit goals
- Edit plan duration
- Edit pillar configuration
- Edit Daily configuration
- Edit Push configuration
- Edit Home configuration
- Edit Wearable behavior
- Edit Settings defaults
- Edit Content modules
- Edit Recommendations
- Add internal notes

Plan Templates should remain flexible.

The Admin system should not impose unnecessary naming, category or campaign restrictions.

Business rules should be configurable by the admin.

Plan Templates are defined in:

```text
PLAN_TEMPLATES.md
```

---

# 2. Onboarding Admin

The admin should be able to manage Onboarding content and structure.

Editable areas:

- Welcome copy
- Profile baseline questions
- Goal options
- Recommended Plan logic
- Adapted Plan options
- Wearable connection copy
- Push permission copy
- Mental Detox explanation
- Upload step copy
- Pillar preference Dashboard
- Plan preview copy
- First Activation Mode
- First 7-Day Sync Plan activation copy

The admin should be able to modify Onboarding without redeploying the app.

Onboarding should be configurable but not overcomplicated.

Onboarding is defined in:

```text
ONBOARDING.md
```

---

# 3. Home Admin

The admin should be able to configure key Home behavior.

Editable areas:

- Current Insight templates
- Next Best Action templates
- Adaptive Summary priorities
- Pillar visibility rules
- Home copy
- First Activation Mode copy
- Active Plan display
- Mini Orb behavior
- Pillar Orb Quick Panel options
- Contextual Access Points
- Quick Actions
- Personal Center access
- Sync Control entry points

Admin should not turn Home into a dashboard.

Home should remain the central operating surface.

Home is defined in:

```text
HOME.md
```

---

# 4. Daily Admin

The admin should be able to configure Daily flows.

Editable areas:

- Morning sequence
- Midday sequence
- Evening sequence
- Night sequence
- Recovery sequence
- Context windows
- Daily Stack timing
- Meal timing
- Hydration checkpoints
- Movement logic
- Sleep planning logic
- Mind reset logic
- Sunlight guidance
- Window Closed behavior
- Recovery language
- Next Best Action logic

Daily is the execution layer.

Daily should be configurable through plans and Admin rules.

Daily is defined in:

```text
DAILY.md
```

---

# 5. Push Admin

The admin should be able to configure Push behavior.

Push should not behave like generic reminders.

Editable areas:

- Push cycles
- Push timing windows
- Push copy
- Push response options
- Confirm behavior
- Adjust destination
- Later timing
- Follow-up logic
- Deep links
- Context questions
- Tone
- Frequency
- Mental Detox behavior
- User opt-down logic

Default Push cycles:

```text
Morning Activation
Midday Alignment
Evening Alignment
Night Reset
```

Default action logic:

```text
Confirm
↓
Update internal state without opening app

Adjust
↓
Open relevant screen

Later
↓
Schedule follow-up later
```

Push is defined in:

```text
PUSH.md
```

---

# 6. Pillars Admin

The admin should be able to configure operational pillars.

Current pillars:

- Mind
- Sun
- Hydration
- Sleep
- Meal / Nutrition
- Movement
- Daily Stack

Editable areas per pillar:

- Active / inactive
- Priority
- Default behavior
- User-facing copy
- Target
- Context windows
- Daily behavior
- Push behavior
- Home visibility
- Quick Panel behavior
- Recovery logic
- Manual adjustment rules
- Content modules
- Recommendations

Pillars should be operational modules, not simple icons.

Pillars are defined in:

```text
PILLARS.md
```

---

# 7. Daily Stack Admin

Daily Stack requires dedicated Admin controls because it may involve:

- Medications
- Vitamins
- Supplements
- Nutraceuticals
- Stock control
- Intake confirmation
- Refill reminders
- Protocol-based timing
- Food-related timing
- User-specific adjustments

Editable areas:

- Stack item types
- Item names
- Timing
- Instructions
- With food / without food
- Stock tracking
- Low stock threshold
- Refill recommendations
- Confirmation logic
- Push reminders
- Daily integration
- Home integration
- Plan integration

Daily Stack is defined in:

```text
STACK.md
```

---

# 8. Wearables Admin

The admin should be able to configure wearable behavior.

Wearables should improve automation but should not be required for value.

Editable areas:

- Supported devices
- Connected providers
- Signal usage
- Sleep data usage
- Movement data usage
- Recovery data usage
- Heart rate usage
- HRV usage
- Resting heart rate usage
- Temperature trend usage
- Respiratory rate usage
- Oxygen saturation usage
- Stress signal usage
- Cycle-related signal usage when supported
- Premenstrual period estimation when supported
- Manual fallback behavior
- Wearable connection copy
- Wearable permission copy
- Wearable error states

Example:

```text
If wearable connected:
Use sleep and recovery data.

If no wearable:
Use Push check-ins and manual input.
```

Wearables should not create a dependency.

They should improve context.

---

# 9. Settings Admin

The admin should be able to manage Settings defaults.

Settings may include:

- Language
- Time zone
- Units
- Push frequency
- Mental Detox mode
- Wake preference
- Sleep preference
- Dietary preference
- Training level
- Wearable preference
- Privacy preference
- Upload preference
- Notification tone
- Default plan behavior

Settings should be user-editable.

Admin defines defaults.

User personalization overrides defaults.

---

# 10. Uploads Admin

The admin should be able to manage uploaded files and data flows.

Upload types may include:

- Lab exams
- Blood tests
- Medical reports
- Nutrition plans
- Fitness assessments
- Sleep reports
- Wearable exports
- PDF files
- Images
- Historical health documents
- Supplement lists
- Medication lists
- Personal notes

Admin may need to see:

- Upload status
- Processing status
- File type
- User association
- Extracted data status
- Internal notes
- Error state
- User permission state

Upload should remain optional for users.

Uploaded files may help personalize Wellbine, but they should not block activation.

---

# 11. Content Admin

The admin should be able to manage reusable content modules.

Content modules may include:

- Educational cards
- Guided meditations
- Breathing sessions
- Movement videos
- Nutrition guidance
- Sleep guidance
- Hydration guidance
- Daily Stack instructions
- Recovery explanations
- Weekly summaries
- Onboarding explanations
- Plan-specific content
- Pillar-specific content

Content should be reusable across:

- Plans
- Pillars
- Daily
- Push
- Home
- Onboarding

Content should not require code deployment.

---

# 12. Recommendations Admin

The admin should be able to manage recommendations.

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
- Partner offers

Recommendations should be optional and contextual.

Examples:

- Daily Stack refill
- Electrolyte suggestion
- Protein support
- Sleep support
- Meditation content
- Movement sequence
- Nutrition guide

Recommendations should not dominate the user experience.

They should appear when relevant.

---

# 13. Users Admin

The admin should be able to view and manage user-level information with appropriate permissions.

Possible user admin areas:

- User profile
- Active plan
- Plan history
- Pillar status
- Push status
- Wearable status
- Upload status
- Daily activity
- Stack status
- Settings
- Notes
- Support state
- Account status

User management should be practical.

Admin should not expose unnecessary sensitive detail to every role.

Permissions may vary by admin role.

---

# 14. Analytics Admin

The admin should be able to understand what is working.

Possible analytics:

- Onboarding completion
- Plan activation
- Plan completion
- Push response rate
- Push opt-out
- Mental Detox usage
- Pillar engagement
- Daily activity
- Home interaction
- Upload usage
- Wearable connection rate
- Recommendation clicks
- Stack adherence
- Retention
- Drop-off points

Analytics should help improve the product.

Analytics should not overload the admin dashboard.

---

# 15. Publishing Admin

Publishing should be simple.

Admin should support:

- Draft
- Published
- Archived

These statuses may apply to:

- Plan Templates
- Content modules
- Onboarding modules
- Push sequences
- Recommendations
- Home messages
- Pillar configurations

Publishing should not be painful.

The admin should be able to preview before publishing when useful.

---

# Preview Mode

The Admin system should support preview mode.

Preview may show:

- Home first state
- Onboarding flow
- Plan activation
- Daily sequence
- Push examples
- Pillar state
- Recommendations
- Content modules

Preview helps the admin understand what users will see.

Preview should be useful but not mandatory for every small edit.

---

# Duplicate Function

The Admin system should support duplication.

Duplication is important for speed.

Admin should be able to duplicate:

- Plans
- Push sequences
- Content modules
- Recommendations
- Pillar configurations
- Onboarding modules

Example:

```text
Duplicate Metabolic Support Plan

↓

Rename

↓

Adjust pillars

↓

Publish new version
```

This makes plan creation faster.

---

# Versioning

Versioning may be used when useful.

Versioning helps preserve history.

Versioning may apply to:

- Plan Templates
- Onboarding flows
- Push sequences
- Content modules
- Pillar configurations

The Admin system should not force complex versioning for every small change.

Versioning should support control, not create friction.

---

# Audit Trail

The Admin system should eventually maintain an audit trail.

Audit trail may record:

- Who changed something
- What changed
- When it changed
- Previous value
- New value
- Publish status
- Archive action

This helps with reliability and accountability.

Audit trail should run in the background.

It should not slow down normal Admin work.

---

# Admin Roles

Admin roles may evolve over time.

Possible roles:

- Owner
- Admin
- Editor
- Support
- Viewer

Role examples:

## Owner

Full control.

## Admin

Can manage product configuration.

## Editor

Can edit content and plans, but may not manage sensitive settings.

## Support

Can view user support information.

## Viewer

Can view information but not edit.

Roles should be practical.

They should not overcomplicate early operations.

---

# Safety Notes

Safety notes may exist inside Admin.

Safety notes should help the team organize sensitive information.

Safety notes should not make the Admin Panel difficult to use.

Examples:

- Internal caution
- User-facing disclaimer
- Medical relevance
- Needs review
- Region-specific note
- Product claim note

Detailed legal, medical or regulatory review may be handled separately when needed.

Admin should not become blocked by unnecessary complexity.

---

# Business Flexibility Rule

The Admin system must support business flexibility.

Admin should not hardcode:

- Plan names
- Plan categories
- Campaign logic
- Content structure
- Recommendation types
- Push labels
- Pillar emphasis
- Store access
- Onboarding copy

The product team should be able to test and change business decisions quickly.

Admin should serve the business.

The business should not be trapped by the Admin system.

---

# Data-Driven Product Rule

Wellbine should be data-driven where practical.

Admin-managed data may include:

- Plans
- Plan versions
- User active plan snapshots
- Onboarding modules
- Home messages
- Push sequences
- Pillar configurations
- Stack items
- Wearable rules
- Settings defaults
- Upload metadata
- Content modules
- Recommendations

The app should read this configuration and render the correct experience.

---

# Recommended Admin Sections

Recommended top-level Admin sections:

```text
Dashboard
Plans
Onboarding
Home
Daily
Push
Pillars
Stack
Wearables
Settings
Uploads
Content
Recommendations
Users
Analytics
Publishing
```

This structure may evolve.

The Admin system should remain modular.

---

# What Admin Should Not Do

Admin should not:

- Require code changes for normal business updates
- Force hardcoded plan categories
- Make plan creation difficult
- Turn every edit into a technical task
- Overload the admin with unnecessary rules
- Block simple business decisions
- Force every product area into separate complex workflows
- Make Supabase and Admin Panel inconsistent
- Make users depend on manual staff intervention
- Make the product rigid

Admin should make Wellbine easier to operate.

---

# Current Status

Wellbine Admin is being defined as the operational control layer for the product.

The next implementation priorities are:

- Plan Template management
- Onboarding management
- Push configuration
- Pillar configuration
- Home configuration
- Daily configuration
- Daily Stack management
- Wearable settings
- Upload management
- Content modules
- Recommendation management
- User support view
- Basic analytics
- Publish / archive workflow

---

# Future Evolution

Future versions of Admin may include:

- Full FlutterFlow Admin Panel
- AI-assisted plan creation
- AI-assisted content creation
- Plan preview simulator
- Push simulator
- Onboarding simulator
- Visual sequence builder
- Drag-and-drop plan builder
- Upload interpretation dashboard
- Wearable signal dashboard
- Cohort analytics
- A/B testing
- Region-specific configuration
- Language-specific configuration
- Admin approval workflows
- Advanced role permissions
- Advanced audit trail

---

# Related Documents

- FOUNDATION/AAI_CONSTITUTION.md
- FOUNDATION/AAI_GLOSSARY.md
- FOUNDATION/AAI_PRINCIPLES.md
- FRAMEWORKS/POPAE.md
- PRODUCTS/WELLBINE/README.md
- PRODUCTS/WELLBINE/PRODUCT.md
- PRODUCTS/WELLBINE/BCAS.md
- PRODUCTS/WELLBINE/PLAN_TEMPLATES.md
- PRODUCTS/WELLBINE/ONBOARDING.md
- PRODUCTS/WELLBINE/HOME.md
- PRODUCTS/WELLBINE/DAILY.md
- PRODUCTS/WELLBINE/PUSH.md
- PRODUCTS/WELLBINE/PILLARS.md
- PRODUCTS/WELLBINE/STACK.md
