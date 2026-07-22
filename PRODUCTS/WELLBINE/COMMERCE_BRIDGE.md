# Wellbine Commerce Bridge

**Version:** 0.1.0

**Status:** Draft

**Last Updated:** July 2026

---

# Purpose

This document defines the Commerce Bridge layer of Wellbine.

Commerce Bridge connects Wellbine subscribers to external commerce experiences without turning Wellbine into an in-app store.

The primary use case is:

```text
Active subscriber
↓
Receives subscriber benefit
↓
Uses benefit inside Wellbine
↓
External e-commerce opens
↓
Subscriber completes purchase outside Wellbine
```

Commerce Bridge may support nutraceuticals, wellness products, Daily Stack-related products, partner products, refill flows and subscriber benefits.

Commerce Bridge should support monetization without making commerce the center of the Wellbine experience.

---

# Official Definition

**Wellbine Commerce Bridge is the subscriber benefit and external commerce connection layer that allows eligible users to access coupons, offers or product-related benefits inside Wellbine and complete purchases through external e-commerce platforms.**

---

# Core Principle

The core Commerce Bridge rule is:

```text
Reduce friction without making commerce the center of the app.
```

Commerce should support the Wellbine experience.

Commerce should not dominate the Wellbine experience.

Wellbine should guide first.

Commerce should appear when relevant.

---

# Product Boundary

Commerce Bridge is not a full in-app store for the MVP.

Commerce Bridge is not the core product.

Commerce Bridge is not the main navigation structure.

Commerce Bridge is a contextual benefit layer.

Preferred framing:

```text
Subscriber Benefits
```

```text
Plan Benefits
```

```text
Daily Stack Benefit
```

```text
Monthly Benefit
```

Avoid framing the MVP around:

```text
Store as the main app destination
```

```text
Commerce as the primary user journey
```

```text
Shopping before guidance
```

---

# Core User Flow

The recommended MVP flow is:

```text
User is an active subscriber
↓
Wellbine shows available subscriber benefit
↓
User taps one primary action
↓
Coupon is copied automatically
↓
External commerce opens
↓
User completes purchase outside Wellbine
```

The user should not need to choose between multiple commerce actions when one action can handle the flow.

---

# Primary Action Rule

Commerce Bridge should use one primary action whenever possible.

Recommended button:

```text
Use Benefit
```

Alternative button labels:

```text
Use Monthly Benefit
Use My Benefit
Use Discount
Open Benefit
```

The primary button should perform two actions:

```text
Copy benefit code to clipboard
+
Open external commerce destination
```

Example behavior:

```text
User taps Use Benefit
↓
Coupon is copied
↓
External store opens
```

Optional confirmation message:

```text
Benefit copied. Opening store.
```

---

# Coupon Fallback Rule

Even if the external commerce platform supports automatic coupon application, Wellbine should still copy the coupon as fallback.

Recommended logic:

```text
If automatic coupon application is supported:
    copy coupon
    open store with coupon applied

If automatic coupon application is not supported:
    copy coupon
    open store destination

If automatic coupon application fails:
    user can paste copied coupon manually
```

This reduces friction while protecting the user experience.

---

# Automatic Coupon Application

Some commerce platforms may support automatic coupon application through:

- Checkout link
- Cart link
- Product link
- Discount URL
- Coupon parameter
- Platform-specific rule
- Campaign link
- API-generated checkout

Commerce Bridge should support this when available.

However, the system should not depend entirely on it.

Recommended rule:

```text
Automatic coupon application is preferred when supported, but copied coupon fallback should remain available.
```

---

# MVP Commerce Behavior

The MVP should remain simple.

MVP behavior:

- Show benefit inside Wellbine
- Show coupon or benefit code if applicable
- Use one primary action
- Copy code automatically
- Open external commerce link
- Track benefit shown
- Track benefit used / clicked
- Track coupon copied
- Track external link opened

The MVP should not require deep commerce integration.

---

# What The MVP Should Not Require

The MVP should not require:

- Internal checkout
- Product catalog inside Wellbine
- Cart inside Wellbine
- Payment processing inside Wellbine
- Fulfillment inside Wellbine
- Real-time inventory sync
- Full coupon API
- Redemption verification
- Advanced attribution
- Complex subscription-commerce sync
- Store as fixed navigation

These may be added later.

They should not block the core Wellbine product.

---

# User Experience Principle

Commerce Bridge should feel like a benefit, not an interruption.

Good experience:

```text
Your subscriber benefit is available.

Use it when you need it.
```

Bad experience:

```text
Buy now.
Limited time.
Don't miss this.
```

Wellbine should avoid aggressive commerce pressure inside the health experience.

The product should remain trust-first.

---

# Possible Placement Inside App

Commerce Bridge may appear in contextual areas such as:

- Personal Center
- Subscriber Benefits
- Plan Benefits
- Daily Stack
- Recommendations
- Home contextual card
- Settings / Subscription area
- Relevant pillar panel
- Refill context
- Plan completion screen

Commerce Bridge should not require a fixed Store tab in the MVP.

---

# Home Placement Rule

Home may show Commerce Bridge only when contextually relevant.

Examples:

- Subscriber benefit available
- Daily Stack refill context
- Plan-related recommendation
- User asks for product support
- Admin enables contextual benefit card
- Active plan includes subscriber benefit visibility

Home should not become a shopping surface.

Home remains the central operating surface.

---

# Daily Stack Relationship

Daily Stack is a natural commerce bridge entry point.

Commerce may support:

- Supplement refill
- Nutraceutical refill
- Vitamin refill
- Product-related routine support
- Plan-related product recommendation
- Subscriber benefit access

Important rule:

```text
Daily Stack should organize routine and adherence, not aggressively sell products.
```

Commerce should appear when useful.

---

# Recommendations Relationship

Commerce Bridge may connect to Recommendations.

Recommendations may include:

- Product suggestions
- Refill suggestions
- External checkout links
- Partner offers
- Subscriber benefits
- Plan-related products
- Daily Stack-related products

Recommendations should be contextual and admin-managed.

They should not dominate the user experience.

---

# Subscriber Eligibility

Commerce Bridge should support eligibility rules.

Eligibility may depend on:

- Active subscription
- Plan type
- Subscription tier
- Region
- Campaign
- Benefit availability
- User status
- Admin configuration
- Time period
- Partner rules
- Product category
- Prior redemption status

Eligibility rules should be configurable.

They should not be hardcoded.

---

# Benefit Types

Commerce Bridge may support different benefit types.

Possible benefit types:

- Coupon code
- Discount link
- Free shipping
- Bundle access
- Exclusive product access
- Subscription discount
- Refill benefit
- Partner benefit
- Plan-specific offer
- Monthly benefit
- One-time benefit
- Trial benefit
- Renewal benefit

The system should remain flexible.

Do not hardcode a single benefit model.

---

# Business Rule Flexibility

Commerce Bridge should not hardcode:

- Discount percentage
- Coupon value
- Campaign type
- Platform
- Product category
- Benefit name
- Benefit frequency
- Eligibility rules
- Renewal logic
- Redemption limits
- External checkout behavior
- Product positioning
- Region rules

These should be configurable through Admin where practical.

---

# Admin Role

Admin should control Commerce Bridge behavior.

Admin may manage:

- Benefit campaigns
- Coupon codes
- External URLs
- Platform type
- Eligibility rules
- Visibility rules
- Active / inactive status
- Start date
- End date
- Benefit frequency
- Benefit copy
- Button label
- Placement inside app
- Plan association
- Product category
- Partner association
- Redemption notes
- Internal notes
- Review status

Admin should be able to update benefits without app redeployment where practical.

---

# Commerce Platforms

Commerce Bridge may connect to external commerce platforms.

Possible future integrations:

- Shopify
- CartPanda
- WooCommerce
- Atomicat
- Custom checkout
- Coupon API
- Subscription platform
- Fulfillment partner
- Partner commerce platform

The system should not depend on a single commerce provider.

---

# Platform-Agnostic Rule

Commerce Bridge should be platform-agnostic.

The internal Wellbine logic should not assume that every commerce platform behaves the same way.

Different platforms may support:

- Manual coupon
- Automatic discount link
- Checkout URL
- Cart URL
- Product URL
- Coupon API
- Order webhook
- Subscription sync
- Redemption callback

Commerce Bridge should support a flexible configuration model.

---

# External Store Opening Rule

Commerce Bridge should open the external commerce destination outside the core Wellbine app flow.

Possible destinations:

- Product page
- Collection page
- Cart page
- Checkout page
- Campaign page
- Partner landing page

Preferred destination:

```text
The most direct useful destination available.
```

Avoid:

```text
Generic store homepage when a more relevant destination exists.
```

The user should land as close as possible to the intended purchase path.

---

# Single Button Flow

The preferred MVP interaction is:

```text
User sees benefit
↓
User taps one button
↓
Coupon is copied
↓
External commerce opens
```

Recommended logic:

```text
Primary Action:
Copy benefit code
Open external URL
Track event
```

Events:

```text
benefit_viewed
benefit_button_tapped
coupon_copied
external_store_opened
```

Optional future events:

```text
checkout_started
coupon_applied
purchase_completed
redemption_confirmed
```

---

# Fallback UX

If the external link fails:

```text
Show coupon code
Allow copy again
Allow open store again
```

If coupon copy fails:

```text
Show coupon code visibly
Allow manual copy
Open store if possible
```

If user returns from store:

```text
Do not interrupt the user.
Keep benefit available if still eligible.
```

Commerce Bridge should fail gracefully.

---

# Tracking

Commerce Bridge should track basic events.

MVP tracking:

- Benefit shown
- Button tapped
- Coupon copied
- External URL opened

Future tracking:

- Checkout started
- Coupon applied
- Purchase completed
- Redemption confirmed
- Revenue attributed
- Campaign performance
- Benefit expiration
- User eligibility change

Tracking should respect privacy and platform rules.

---

# Data Model Direction

Commerce Bridge may require future tables.

Possible tables:

```text
commerce_benefits
commerce_campaigns
user_commerce_benefits
commerce_events
commerce_platforms
commerce_redemptions
```

---

## commerce_benefits

Possible fields:

```text
id
name
description
benefit_type
status
code
external_url
platform
button_label
placement
eligibility_rules_json
visibility_rules_json
starts_at
ends_at
metadata_json
created_at
updated_at
```

---

## user_commerce_benefits

Possible fields:

```text
id
user_id
commerce_benefit_id
status
shown_at
used_at
copied_at
opened_at
expires_at
metadata_json
created_at
updated_at
```

---

## commerce_events

Possible fields:

```text
id
user_id
commerce_benefit_id
event_type
event_payload
created_at
```

Possible event types:

```text
benefit_viewed
benefit_button_tapped
coupon_copied
external_store_opened
checkout_started
coupon_applied
purchase_completed
redemption_confirmed
expired
```

---

# Relationship With Subscriptions

Commerce Bridge may depend on subscription status.

Possible subscriber statuses:

```text
active
trialing
past_due
cancelled
expired
free
```

Eligibility should define which statuses qualify for each benefit.

Example:

```text
active subscribers only
```

or:

```text
active and trialing users
```

or:

```text
specific plan tier only
```

These rules should be configurable.

---

# Relationship With App Release

Commerce Bridge may affect App Store and Google Play review.

Before release, decide:

```text
Is Commerce Bridge visible in this release?
```

If visible, prepare:

- Clear benefit explanation
- External commerce explanation
- Coupon terms
- Privacy Policy coverage
- Terms of Use coverage
- Review notes
- Safe product language
- No unsupported health claims
- Working external links

If not ready, Commerce Bridge should remain hidden through configuration.

---

# Product Claim Boundary

Commerce Bridge must avoid unsupported health claims.

Preferred language:

- Supports routine
- Wellness product
- Subscriber benefit
- Daily Stack support
- Product discount
- External store
- Partner offer
- Nutraceutical product

Avoid unsupported claims:

- Treats disease
- Cures disease
- Prevents disease
- Medical-grade outcome
- Guaranteed result
- Replaces medication
- Replaces doctor

Commerce language should be reviewed before launch.

---

# Relationship With AAI

AAI may help determine when a benefit is relevant.

AAI may consider:

- Active plan
- Pillar state
- Daily Stack context
- User preferences
- User behavior
- Recommendation eligibility
- Benefit availability
- User intent

AAI should not aggressively push commerce.

AAI should surface commerce only when contextually useful.

---

# Relationship With Home

Home may show Commerce Bridge through contextual cards.

Example triggers:

- Benefit available
- Refill context
- Daily Stack relevance
- Plan benefit
- Subscriber status
- User intent

Home should not become a storefront.

Home should remain focused on:

- Current Insight
- Next Best Action
- Adaptive Summary
- Pillar state
- Daily alignment

---

# Relationship With Daily

Daily may surface Commerce Bridge when relevant.

Examples:

- Daily Stack refill context
- Plan-specific benefit
- User asks about product support
- Recommendation connected to active plan

Daily should not interrupt execution with unrelated commerce.

Commerce should be secondary.

---

# Relationship With Push

Push may mention Commerce Bridge only when useful and allowed by user settings.

Push should not become promotional spam.

Possible Push use cases:

- Subscriber benefit available
- Benefit expiring soon
- Refill-related reminder
- User-requested product reminder

Push should respect:

- Mental Detox mode
- Push frequency preference
- User relevance
- Admin configuration

---

# Relationship With Admin

Admin should define Commerce Bridge configuration.

Admin should control:

- Campaigns
- Benefits
- Eligibility
- Copy
- Links
- Placement
- Timing
- Frequency
- Status
- Tracking
- Partner rules
- Review status

Admin should be able to disable Commerce Bridge quickly if needed.

---

# Relationship With Plan Templates

Plan Templates may define commerce eligibility or visibility.

Examples:

- Plan has no commerce benefits
- Plan includes monthly subscriber benefit
- Plan includes Daily Stack benefit
- Plan includes partner product recommendation
- Plan hides commerce entirely
- Plan shows commerce only in Personal Center

Plan Templates should not hardcode specific discount amounts.

They should reference configurable benefits.

---

# Relationship With Implementation Plan

Commerce Bridge is planned as a later implementation layer.

It should not block MVP core activation.

The core Wellbine sequence remains:

```text
Onboarding
↓
Plan Activation
↓
Home
↓
Daily
↓
Push
↓
Pillars
```

Commerce Bridge should be planned now, but built in simple MVP form when the core experience is stable.

---

# MVP Scope

Commerce Bridge MVP should include:

- Subscriber benefit visibility
- One primary benefit action
- Automatic coupon copy
- External commerce opening
- Basic event tracking
- Admin-managed benefit configuration
- Ability to hide Commerce Bridge
- Basic Terms / Privacy coverage
- Safe language

MVP should not include:

- Full internal store
- Internal checkout
- Cart inside Wellbine
- Complex product catalog
- Full redemption verification
- Deep API integration
- Aggressive promotional flows
- Store tab as primary navigation

---

# Future Scope

Future versions may include:

- Dynamic coupons
- Unique user coupons
- Monthly benefit automation
- Coupon expiration rules
- Redemption verification
- Purchase attribution
- External checkout API integration
- Subscription-commerce synchronization
- Product recommendations
- Refill automation
- Partner dashboards
- Revenue analytics
- Campaign analytics
- A/B testing
- Region-specific benefit rules
- Tier-based benefits
- Plan-specific benefits

---

# Success Criteria

Commerce Bridge is successful when:

- Subscribers understand the benefit
- The benefit is easy to use
- One tap can copy the coupon and open the store
- External commerce does not confuse the user
- The app does not become commerce-first
- Admin can manage benefit rules
- Commerce can be hidden or changed quickly
- App review risk is controlled
- Claims remain safe
- The core Wellbine experience remains the priority

---

# What Commerce Bridge Should Not Do

Commerce Bridge should not:

- Become the main app experience
- Replace Home
- Become fixed Bottom Navigation
- Interrupt Daily unnecessarily
- Turn Push into promotional spam
- Require complex checkout integration for MVP
- Hardcode discount rules
- Hardcode platform dependency
- Make unverified health claims
- Confuse app subscription with external product purchase
- Block core product launch

Commerce Bridge should support monetization without weakening trust.

---

# Current Status

Commerce Bridge is currently planned as a subscriber benefit layer.

The recommended MVP approach is:

```text
One primary action
↓
Copy coupon automatically
↓
Open external commerce destination
↓
Use copied coupon as fallback if automatic application is unavailable
```

The next implementation steps are:

- Define subscriber benefit model
- Define Admin configuration fields
- Define first benefit placements
- Define external commerce platform
- Define coupon behavior
- Define event tracking
- Define safe copy
- Define App Release impact
- Define Privacy and Terms coverage

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
- ARCHITECTURE_DECISIONS/HOME_CENTRAL.md
- ARCHITECTURE_DECISIONS/PUSH_ORCHESTRATION.md
- ARCHITECTURE_DECISIONS/PLAN_TEMPLATES_DB.md
- ARCHITECTURE_DECISIONS/ADMIN_CONTROL_LAYER.md
- ARCHITECTURE_DECISIONS/ONBOARDING_ACTIVATION.md
