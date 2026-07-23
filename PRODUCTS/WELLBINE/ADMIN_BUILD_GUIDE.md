# Wellbine Admin Build Guide

**Version:** 0.1.0

**Status:** Draft

**Last Updated:** July 2026

---

# Purpose

This document defines the practical Admin build guide for Wellbine.

The goal is to create an operational control layer where internal users can manage product behavior without changing app code for every business rule, plan, copy, content, recommendation or commerce update.

This document connects:

- Admin
- Supabase
- Plan Templates
- Onboarding
- Home
- Daily
- Push
- Pillars
- Daily Stack
- Wearables
- Uploads
- Commerce Bridge
- App Release
- QA
- Edge Functions

Admin is the operational control layer of Wellbine.

Supabase remains the source of truth.

FlutterFlow consumes the configured experience.

---

# Official Definition

**Wellbine Admin Build Guide is the practical implementation guide for creating the internal control system used to configure, publish, manage and monitor the Wellbine product experience.**

---

# Core Principle

The core Admin rule is:

```text
Admin controls product behavior. The app executes published configuration.
```

The Admin layer should allow the team to change important operational elements without app redeployment where practical.

Admin should control:

- Plan Templates
- Plan Template Versions
- Onboarding copy and structure
- Pillar definitions
- Pillar defaults
- Home content
- Daily rules
- Push copy
- Push rules
- Content modules
- Recommendations
- Commerce Benefits
- Feature visibility
- Publishing status
- Review status
- Internal notes
- Audit logs

---

# What Admin Is

Admin is the internal management layer for Wellbine.

Admin allows authorized users to:

- Create
- Edit
- Duplicate
- Preview
- Publish
- Archive
- Disable
- Reorder
- Review
- Monitor

product configuration.

Admin is not the user app.

Admin is not the source of user experience by itself.

Admin configures Supabase.

FlutterFlow reads the published configuration.

---

# What Admin Should Not Be

Admin should not be:

- A second version of the user app
- A place where unsafe changes bypass review
- A public interface
- A replacement for Supabase security
- A place where service role access is exposed casually
- A place where draft content appears to users
- A fragile spreadsheet that controls production without audit
- A blocker for basic MVP execution

Admin should be powerful, but controlled.

---

# Recommended Admin Stack

Possible Admin implementation options:

```text
Softr
Retool
Supabase Studio
Custom Admin Panel
Internal FlutterFlow Admin
```

Recommended direction:

```text
Start with the fastest reliable Admin tool.
Keep Supabase as source of truth.
Move to custom Admin only when needed.
```

For MVP, a no-code or low-code Admin can be enough if it controls the right tables safely.

---

# Admin Build Priorities

Recommended Admin build order:

```text
1. Admin authentication / access control
2. Plan Templates management
3. Plan Template Versions management
4. Pillar Definitions management
5. Content Modules management
6. Feature visibility controls
7. Commerce Benefits management
8. Push copy and rules management
9. Recommendations management
10. User support view
11. Publishing workflow
12. Audit logs
13. App Release content review
```

Do not start by building a large admin dashboard with many charts.

Start with the controls that affect the product.

---

# Admin Roles

Recommended roles:

```text
owner
admin
editor
support
viewer
```

---

## owner

Can manage:

- All settings
- Admin users
- Publishing
- Production-critical configuration
- Commerce Benefits
- Plan Templates
- Feature visibility
- Audit logs

---

## admin

Can manage:

- Plan Templates
- Content
- Push
- Pillars
- Commerce Benefits
- Recommendations
- Publishing

May not manage owner-level permissions.

---

## editor

Can create and edit drafts.

May not publish to production unless approved.

---

## support

Can view limited user support data.

May not edit product configuration.

May not access sensitive health uploads unless explicitly authorized.

---

## viewer

Can view configuration and reports.

Cannot edit or publish.

---

# Access Control Rule

Admin access must be protected.

Regular users must never access Admin.

Admin actions should require:

```text
Authenticated admin user
+
Valid role
+
Allowed action
```

Admin role may be managed through:

```text
user_roles table
custom claims
Admin platform permissions
protected backend
```

---

# Admin Audit Rule

Important admin actions should be logged.

Use:

```text
admin_audit_log
```

Audit log should record:

```text
admin_user_id
action
entity_type
entity_id
before_json
after_json
metadata_json
created_at
```

Audit matters for:

- Plan changes
- Publishing
- Commerce Benefits
- Push copy
- Feature visibility
- Content changes
- User support actions
- Release-sensitive configuration

---

# Core Admin Sections

Recommended Admin sections:

```text
Dashboard
Plans
Plan Versions
Pillars
Onboarding
Home
Daily
Push
Daily Stack
Wearables
Uploads
Content
Recommendations
Commerce Bridge
Feature Flags
Users
Support
Analytics
Publishing
Audit Logs
Release Review
Settings
```

For MVP, not all sections need to be deep.

---

# Admin Dashboard

The Admin Dashboard should show operational status.

Possible widgets:

```text
Published plans
Draft plans
Active users
Onboarding completions
Plan activations
Daily action activity
Push activity
Commerce Bridge visibility
Active Commerce Benefits
Broken configuration warnings
Upcoming benefit expirations
Recent admin changes
Release checklist status
```

The Dashboard should help the team see whether the system is ready and stable.

---

# Plans Admin

Plans Admin manages:

```text
plan_templates
```

Admin should be able to:

- Create Plan Template
- Edit Plan Template
- Duplicate Plan Template
- Archive Plan Template
- Reorder Plan Templates
- Feature Plan Template
- Change category
- Change audience
- Add internal notes
- View current published version
- View draft versions

Plan Template fields may include:

```text
name
slug
description
status
category
audience
is_featured
sort_order
current_version_id
metadata_json
```

Important rule:

```text
Plan Templates should not hardcode all business logic inside the app.
```

---

# Plan Versions Admin

Plan Versions Admin manages:

```text
plan_template_versions
```

Admin should be able to:

- Create draft version
- Edit draft version
- Preview version
- Publish version
- Archive version
- Compare versions
- See publishing history
- Add internal notes

Plan Version configuration may include:

```text
configuration_json
pillar_defaults_json
daily_rules_json
push_rules_json
home_rules_json
wearable_rules_json
commerce_rules_json
content_rules_json
```

Important rule:

```text
Published Plan Versions should remain stable for users who already activated them.
```

---

# Plan Publishing Flow

Recommended flow:

```text
Create draft
↓
Edit configuration
↓
Preview
↓
QA check
↓
Publish
↓
Make available to users
```

When publishing:

```text
Validate required fields
Set version status to published
Update plan_templates.current_version_id
Write admin_audit_log
```

Publishing should preferably use:

```text
admin_publish_plan Edge Function
```

---

# Pillars Admin

Pillars Admin manages:

```text
pillar_definitions
```

Initial pillars:

```text
mind
sun
hydration
sleep
nutrition
movement
daily_stack
```

Admin should be able to:

- Edit pillar name
- Edit description
- Edit sort order
- Enable / disable pillar
- Edit default configuration
- Edit user-facing copy
- Edit related content
- Edit icon or visual metadata
- Control visibility

Important rule:

```text
Pillars should be stable enough for the user and configurable enough for the product.
```

---

# Onboarding Admin

Onboarding Admin manages onboarding structure and copy.

Admin may control:

- Step title
- Step description
- Step order
- Optional / required status
- Available options
- Helper copy
- Skip behavior
- Plan recommendation copy
- Upload explanation
- Wearable explanation
- Push explanation
- Mental Detox explanation

Important rules:

```text
Wearables must remain optional.
Uploads must remain optional.
Push must remain optional.
Onboarding should not feel like a medical exam.
```

---

# Home Admin

Home Admin manages Home configuration.

Admin may control:

- Current Insight copy patterns
- Next Best Action copy patterns
- Home contextual cards
- Pillar Orb visibility
- Adaptive Summary sections
- Commerce card visibility
- Recommendation placements
- Empty state copy
- Error state copy
- First Activation state

Important rule:

```text
Home must remain the central operating surface, not a storefront or dashboard maze.
```

---

# Daily Admin

Daily Admin manages Daily experience configuration.

Admin may control:

- Daily action templates
- Daily sequence rules
- Recovery-aware copy
- Action categories
- Window behavior
- Confirm / Adjust / Later behavior
- Plan-specific Daily rules
- Fasting-aware rules
- Sleep-aware rules
- Movement-aware rules
- Daily empty states
- Daily fallback copy

Important rule:

```text
Daily should help the user continue from the current state, not punish missed actions.
```

---

# Push Admin

Push Admin manages Push copy and rules.

Admin may control:

- Push templates
- Push timing windows
- Push frequency
- Push eligibility
- Push category
- Deep link destination
- Confirm / Adjust / Later payload
- Mental Detox compatibility
- Commerce Push visibility
- Recovery-aware follow-up
- Plan-specific Push rules

Important rules:

```text
Push is orchestration, not spam.
Push should not become a promotional channel.
Push should respect Mental Detox.
```

---

# Daily Stack Admin

Daily Stack Admin may control stack-related settings.

Admin may manage:

- Item categories
- Default timing options
- Default frequency options
- Safety copy
- Refill tracking options
- Commerce Bridge connection rules
- Daily Stack education content
- Product category mapping

Important rule:

```text
Daily Stack organizes routines. It does not prescribe medication.
```

---

# Wearables Admin

Wearables Admin may control wearable-related configuration.

Admin may manage:

- Active providers
- Provider visibility
- Provider status
- Coming soon providers
- Permission copy
- Data usage copy
- Manual fallback copy
- Error copy
- Supported metric mapping
- Last sync display rules

Important rules:

```text
Do not show providers as active if integration is not implemented.
Wearables are optional.
Wellbine must work without wearables.
```

---

# Uploads Admin

Uploads Admin may control upload-related configuration.

Admin may manage:

- Accepted file types
- Upload categories
- Upload explanation copy
- Extraction status copy
- File size limits
- Storage behavior
- Delete upload copy
- Upload privacy copy
- Processing rules
- Upload summary visibility

Important rules:

```text
Uploads are optional.
Uploads should not imply diagnosis.
Private files must not be publicly accessible.
```

---

# Content Admin

Content Admin manages:

```text
content_modules
```

Admin should be able to:

- Create content
- Edit content
- Preview content
- Publish content
- Archive content
- Tag content
- Link content to plans
- Link content to pillars
- Link content to onboarding
- Link content to Daily Stack
- Link content to Commerce Bridge

Content types:

```text
education
guidance
plan_content
pillar_content
stack_content
commerce_content
onboarding_content
faq
```

Important rule:

```text
Do not hardcode content that will change frequently.
```

---

# Recommendations Admin

Recommendations Admin manages recommendation logic and visibility.

Admin may control:

- Recommendation templates
- Placement
- Priority
- Status
- Related pillar
- Related plan
- Related content
- Related commerce benefit
- CTA label
- CTA destination
- Visibility rules
- Suppression rules

Recommendation placements:

```text
home
daily
pillar
stack
personal_center
commerce
```

Important rule:

```text
Recommendations should be contextual, not noise.
```

---

# Commerce Bridge Admin

Commerce Bridge Admin manages:

```text
commerce_benefits
user_commerce_benefits
commerce_events
```

Admin should be able to:

- Create benefit
- Edit benefit
- Archive benefit
- Enable / disable benefit
- Define eligibility
- Define visibility
- Define external URL
- Define benefit code if applicable
- Define button label
- Define placement
- Define campaign dates
- Define partner metadata
- Define platform type
- Review performance events

Important rules:

```text
Do not hardcode discount amounts.
Do not hardcode platform dependency.
One primary action should copy the benefit code and open the external destination.
Commerce Bridge must be hideable.
Commerce should not become the center of the app.
```

---

# Feature Flags Admin

Feature Flags Admin controls visibility.

Possible flags:

```text
wearables_enabled
uploads_enabled
commerce_bridge_enabled
ask_wellbine_enabled
daily_stack_enabled
subscriptions_enabled
push_enabled
app_release_mode
beta_mode
```

Feature flags may apply globally, by plan, by user segment or by environment.

Important rule:

```text
Unfinished features should be hidden before app review.
```

---

# Users Admin

Users Admin should be limited and privacy-aware.

Admin may view:

- User ID
- Email if needed
- Account status
- Onboarding status
- Active plan status
- Subscription status
- Push enabled status
- Wearable connection status
- Upload count
- Commerce benefit status
- Last active timestamp

Admin should not casually expose sensitive health data.

Sensitive views should require stronger permission.

---

# Support Admin

Support Admin helps resolve user issues.

Support may need to see:

- Account status
- Onboarding completion
- Active plan
- Push settings
- Subscription status
- Upload status
- Commerce benefit eligibility
- Recent error state
- Device/app version if available

Support should not need full private health context for most cases.

---

# Analytics Admin

Analytics should be practical first.

Useful metrics:

```text
signup_completed
onboarding_started
onboarding_completed
plan_activated
home_viewed
daily_action_confirmed
daily_action_adjusted
daily_action_delayed
push_permission_granted
push_permission_denied
wearable_connected
upload_added
commerce_benefit_used
account_deleted
```

Analytics should answer:

```text
Are users activating?
Are users returning?
Are users acting?
Are Push messages useful?
Is Commerce helpful or intrusive?
Where do users drop off?
```

---

# Publishing Admin

Publishing Admin should manage release-sensitive content.

Publishing applies to:

- Plan Templates
- Plan Template Versions
- Content Modules
- Commerce Benefits
- Onboarding configuration
- Push copy
- Recommendations
- Feature flags

Recommended statuses:

```text
draft
review
published
paused
archived
```

Draft content should not appear to normal users.

---

# Release Review Admin

Release Review helps App Release readiness.

Admin may show:

- Visible features
- Published plans
- Active commerce benefits
- Active push templates
- Privacy link status
- Terms link status
- Account deletion status
- Health claim review status
- App Release Checklist status
- QA status

This helps prevent review submission with broken configuration.

---

# Configuration Validation

Admin should validate configuration before publishing.

Examples:

```text
Plan must have name
Plan must have published version
Published version must have configuration_json
Push template must have title and body
Commerce benefit must have external_url if visible
Commerce benefit must have eligibility rules if restricted
Content must have language
Feature must not expose incomplete screen
```

Validation should prevent obvious broken states.

---

# Admin Preview

Admin should support preview where possible.

Preview helps check:

- Plan card
- Onboarding step
- Home card
- Daily action
- Push message
- Commerce benefit
- Recommendation
- Content module

Preview reduces broken user-facing content.

---

# Draft / Published Separation

Admin must separate draft and published content.

Rules:

```text
Draft content is editable.
Published content is visible.
Archived content is hidden from new usage.
Active user snapshots should remain stable.
```

This is especially important for Plan Templates.

---

# Admin And Supabase

Admin should write to Supabase tables.

Important tables:

```text
plan_templates
plan_template_versions
pillar_definitions
content_modules
recommendations
commerce_benefits
admin_audit_log
```

Admin should not bypass security casually.

Admin should not use frontend keys for privileged operations without access control.

---

# Admin And Edge Functions

Admin should use Edge Functions for critical workflows.

Examples:

```text
admin_publish_plan
admin_archive_plan
admin_publish_content
admin_update_commerce_benefit
```

Edge Functions should validate admin permissions.

---

# Admin And FlutterFlow

FlutterFlow should consume published Admin configuration.

The user app should not show:

- Draft plans
- Draft content
- Archived benefits
- Inactive Push templates
- Disabled features
- Internal notes

FlutterFlow should read only what users are allowed to see.

---

# Admin And App Release

Admin affects release readiness.

Before App Store or Google Play submission, Admin should confirm:

```text
Only ready features are visible
Only published content is visible
Commerce Bridge is hidden or working
Wearables are optional
Uploads are optional
Push is optional
Account deletion path exists
Privacy and Terms links work
No unsafe claims are visible
Test account sees clean content
```

---

# Admin And Commerce Bridge

Commerce Admin should make Commerce Bridge flexible.

Do not hardcode:

- Discount amount
- Benefit name
- Campaign frequency
- Platform
- Product category
- External destination
- Button label
- Eligibility rules
- Region rules

Admin should allow future business rules without app rebuild.

---

# Admin And Privacy

Admin must respect privacy.

Admin should not make it easy for internal users to browse sensitive user data without reason.

Recommended practices:

```text
Role-based access
Limited support views
Audit logs
No unnecessary raw health data display
No unnecessary file access
Clear internal permissions
```

---

# Admin And QA

QA should test Admin configuration.

Test:

```text
Draft plan hidden
Published plan visible
Archived plan hidden
Commerce benefit hidden when inactive
Feature flag hides feature
Push template deep link works
Onboarding copy updates
Home content updates
Admin changes are logged
Non-admin cannot access Admin
```

---

# MVP Admin Scope

Minimum MVP Admin:

```text
Plan Templates
Plan Template Versions
Pillar Definitions
Content Modules
Feature Flags
Commerce Benefits
Basic User Support View
Publishing Status
Audit Log
```

Strong MVP Admin:

```text
Onboarding Configuration
Push Templates
Recommendations
Release Review
QA Status
```

Later Admin:

```text
Advanced analytics
Partner dashboard
Commerce performance
A/B testing
Automated approval workflow
Advanced role permissions
```

---

# What Admin Should Not Do

Admin should not:

- Expose draft content to users
- Allow regular users to edit product configuration
- Bypass RLS without control
- Expose service role keys
- Make unsafe health claims easy to publish
- Force app redeploy for every copy change
- Hardcode commerce business rules
- Hardcode plan categories forever
- Turn support into unrestricted health data browsing
- Publish incomplete Commerce Bridge flows
- Show unsupported wearable integrations as active

---

# Success Criteria

Admin is successful when:

- The team can create and publish plans
- The team can manage content
- The team can manage pillars
- The team can manage Commerce Bridge
- The team can control feature visibility
- Draft content stays hidden
- Published content appears correctly
- Admin actions are traceable
- User app behavior can evolve without app redeployment
- App release risk is reduced
- Sensitive data is protected
- Wellbine remains operationally flexible

---

# Current Status

Admin Build Guide is currently a draft.

Next steps:

- Choose Admin platform
- Define admin roles
- Create user_roles strategy
- Create Admin views for Plan Templates
- Create Admin views for Plan Versions
- Create Admin views for Pillars
- Create Admin views for Content
- Create Admin views for Commerce Benefits
- Add publishing workflow
- Add audit logging
- Add release review view
- Test Admin against QA Plan

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
- PRODUCTS/WELLBINE/ADMIN.md
- PRODUCTS/WELLBINE/DATA_MODEL.md
- PRODUCTS/WELLBINE/IMPLEMENTATION_PLAN.md
- PRODUCTS/WELLBINE/WEARABLES.md
- PRODUCTS/WELLBINE/APP_RELEASE.md
- PRODUCTS/WELLBINE/COMMERCE_BRIDGE.md
- PRODUCTS/WELLBINE/SUPABASE_SCHEMA.md
- PRODUCTS/WELLBINE/SUPABASE_IMPLEMENTATION.md
- PRODUCTS/WELLBINE/EDGE_FUNCTIONS.md
- PRODUCTS/WELLBINE/QA_PLAN.md
- PRODUCTS/WELLBINE/PRIVACY_POLICY_DRAFT.md
- PRODUCTS/WELLBINE/TERMS_DRAFT.md
- PRODUCTS/WELLBINE/APP_RELEASE_CHECKLIST.md
- PRODUCTS/WELLBINE/FLUTTERFLOW_BUILD_GUIDE.md
