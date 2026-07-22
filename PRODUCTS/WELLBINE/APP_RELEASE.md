# Wellbine App Release

**Version:** 0.1.0

**Status:** Draft

**Last Updated:** July 2026

---

# Purpose

This document defines the App Store and Google Play release readiness plan for Wellbine.

The goal is to prepare Wellbine for iOS and Android approval, testing and production release.

This document covers:

- Apple App Store readiness
- Google Play readiness
- TestFlight
- Google internal testing
- Health data permissions
- Wearable permissions
- Push notifications
- Privacy Policy
- Terms of Use
- Account deletion
- AI explanation
- Subscription language
- External commerce / coupon behavior
- Health and wellness claims
- App screenshots
- Review notes
- QA requirements
- Production launch

App release readiness should be considered during product design, not only before submission.

---

# Official Definition

**Wellbine App Release is the operational process that prepares, tests, submits and launches Wellbine on iOS and Android while respecting health data, privacy, AI, wearable, push, subscription and external commerce requirements.**

---

# Core Principle

The core release rule is:

```text
App Store and Google Play approval should be considered during product design, not only before launch.
```

Wellbine should not wait until the final build to think about:

- Health claims
- Wearable permissions
- Push permission copy
- AI explanation
- Privacy Policy
- Terms of Use
- Account deletion
- Data deletion
- External commerce links
- Subscription language
- User consent
- Screenshots
- Review notes

Release readiness starts early.

---

# Product Boundary

Wellbine should be positioned as an adaptive health alignment and wellness system.

Wellbine should not be positioned as:

- Medical diagnosis
- Medical treatment
- Emergency care
- Disease detection
- Clinical monitoring device
- Replacement for doctors
- Replacement for licensed medical advice

Preferred positioning:

```text
Wellbine helps users align daily routines, habits and wellness behaviors through adaptive guidance.
```

Avoid positioning:

```text
Wellbine diagnoses health conditions.
```

```text
Wellbine treats disease.
```

```text
Wellbine replaces medical care.
```

---

# App Store Risk Areas

Wellbine has several areas that may affect app review:

- Health and wellness claims
- Wearable data access
- HealthKit / Apple Health permissions
- Google Health Connect permissions
- Push notifications
- AI-generated guidance
- Supplements / nutraceutical references
- External e-commerce links
- Coupons and subscriber benefits
- Subscription or paid access
- Personal data collection
- Sensitive health-related uploads
- Account deletion
- Data deletion
- Privacy disclosures

These areas should be handled carefully.

---

# Apple App Store Readiness

Apple release preparation should include:

- Apple Developer account
- Bundle ID
- App signing
- App icon
- App display name
- App category
- App description
- Keywords
- Screenshots
- App preview video if needed
- Privacy Policy URL
- Terms of Use URL
- Support URL
- Marketing URL if needed
- Account deletion mechanism
- TestFlight testing
- App Review notes
- Health data explanation
- Push notification explanation
- AI guidance explanation
- External commerce explanation if applicable
- Subscription configuration if applicable

Apple review should receive enough context to understand what Wellbine does and what it does not do.

---

# Google Play Readiness

Google Play release preparation should include:

- Google Play Console account
- Android package name
- App signing
- App icon
- App name
- Short description
- Full description
- Feature graphic
- Screenshots
- Privacy Policy URL
- Terms of Use URL
- Support contact
- Data Safety form
- Health data disclosure
- Push notification disclosure
- AI guidance disclosure
- Wearable data disclosure
- Account deletion mechanism
- Internal testing
- Closed testing if needed
- Production release track
- Review notes if applicable

Google Play release should be prepared with clear data usage and permission explanations.

---

# TestFlight

TestFlight should be used before iOS public release.

TestFlight should validate:

- Signup
- Login
- Account deletion
- Onboarding
- Plan activation
- Home
- Daily
- Push
- Pillars
- Daily Stack
- Wearable optional connection
- Manual fallback
- Uploads
- Settings
- Subscriber benefits
- External links
- App stability
- Crash behavior
- Performance
- iOS permission prompts

TestFlight should include internal testers before external testers.

---

# Google Internal Testing

Google internal testing should be used before Android public release.

Internal testing should validate:

- Signup
- Login
- Account deletion
- Onboarding
- Plan activation
- Home
- Daily
- Push
- Pillars
- Daily Stack
- Wearable optional connection
- Manual fallback
- Uploads
- Settings
- Subscriber benefits
- External links
- Android permissions
- Android performance
- Crash behavior

After internal testing, Wellbine may move to closed testing or production depending on readiness.

---

# Health Data Permissions

Wellbine may request access to health-related data.

Health permission explanations must be clear.

The user should understand:

- What data is requested
- Why it is requested
- How it improves the experience
- That wearable connection is optional
- That Wellbine is not a diagnostic tool
- That permissions can be changed later

Example copy:

```text
Wellbine uses sleep and movement data to personalize your daily guidance.
```

Avoid vague copy:

```text
Allow all health data.
```

Health permission copy should be specific, minimal and user-friendly.

---

# Wearable Permissions

Wearable access should be optional.

Supported direction may include:

- Apple Health / HealthKit
- Google Health Connect
- Garmin
- Oura
- WHOOP
- Fitbit
- Manual fallback

Release readiness should confirm which providers are actually implemented before submission.

Do not claim support for providers that are not active.

Example:

```text
Wearable connection is optional.

Wellbine works through check-ins and manual input if no device is connected.
```

---

# Push Notification Permission

Push should be explained before requesting permission.

The user should understand that Push is used for adaptive guidance, not spam.

Preferred copy:

```text
Wellbine can guide your day through intelligent check-ins.

You can pause or reduce Push anytime with Mental Detox Mode.
```

Push should be optional.

If the user denies Push permission, Wellbine should still work through:

- Home
- Daily
- Ask Wellbine
- Manual check-ins

Push permission should not block onboarding.

---

# AI Explanation

Wellbine should explain AI usage clearly.

AI should be positioned as adaptive guidance, not medical authority.

Possible explanation:

```text
Wellbine uses AI to help organize your daily wellness context and suggest practical next actions.
```

Avoid:

```text
Wellbine AI diagnoses your health.
```

```text
Wellbine AI replaces medical advice.
```

The app should include a clear boundary:

```text
Wellbine provides wellness guidance and does not provide medical diagnosis or emergency care.
```

---

# Health And Wellness Claims

Wellbine should use careful language.

Preferred language:

- May help
- Supports
- Guides
- Suggests
- Encourages
- Helps organize
- Helps align
- Wellness routine
- Daily behavior
- Lifestyle guidance
- Recovery-aware guidance

Avoid hard medical claims:

- Diagnoses
- Treats
- Cures
- Prevents disease
- Detects disease
- Guarantees results
- Medical-grade
- Clinically proven unless properly substantiated
- Replaces doctor
- Replaces therapy
- Replaces medication

Claims should be reviewed before store submission.

---

# Nutraceutical And Supplement Language

Wellbine may include Daily Stack and Commerce Bridge features.

This creates additional review sensitivity.

Wellbine should avoid suggesting that supplements or nutraceuticals diagnose, treat, cure or prevent disease.

Preferred framing:

```text
Daily Stack helps organize your supplement, vitamin, nutraceutical or medication routine.
```

```text
Subscriber benefits may include discounts for external wellness products.
```

Avoid:

```text
This supplement treats your condition.
```

```text
This nutraceutical cures disease.
```

Daily Stack should support routine and adherence.

It should not provide medical prescription.

---

# External Commerce And Coupons

Wellbine may include Commerce Bridge / Subscriber Benefits.

This should be handled carefully.

Core logic:

```text
Active subscriber
↓
Accesses monthly benefit inside Wellbine
↓
Copies coupon
↓
Uses coupon on external e-commerce checkout
```

Commerce should be contextual.

Commerce should not dominate the app.

Do not make Store a fixed primary navigation item in the MVP.

Possible locations:

- Personal Center
- Subscriber Benefits
- Daily Stack
- Recommendations
- Plan Benefits
- Home contextual card

Important rule:

```text
Commerce Bridge is a subscriber benefit layer, not the core app experience.
```

External commerce behavior should be reviewed against current Apple and Google rules before release.

---

# Subscription Language

If Wellbine uses subscriptions, subscription language must be clear.

The app should clearly explain:

- Price
- Billing period
- What is included
- Renewal behavior
- Cancellation path
- Trial rules if any
- Subscriber benefits
- Coupon benefits if any
- Difference between app subscription and external product purchases

Avoid unclear language around:

- Free trials
- Auto-renewal
- Refunds
- External purchases
- Discounts
- Health outcomes

Subscription copy should be reviewed before release.

---

# Privacy Policy

Wellbine needs a Privacy Policy before store submission.

The Privacy Policy should cover:

- Account data
- Profile data
- Health-related data
- Wearable data
- Push data
- Daily actions
- Pillar states
- Uploads
- AI processing
- Data storage
- Data sharing
- Third-party services
- Analytics
- External commerce links
- User rights
- Data deletion
- Contact information

The Privacy Policy should be consistent with actual implementation.

Do not claim data practices that are not true.

---

# Terms Of Use

Wellbine needs Terms of Use before store submission.

Terms should cover:

- Product purpose
- Wellness guidance boundary
- No medical diagnosis
- No emergency use
- User responsibilities
- Subscription terms if applicable
- External commerce disclaimer
- Coupon terms if applicable
- Account rules
- Content ownership
- Service changes
- Limitation of liability
- Contact information

Terms should be reviewed before production launch.

---

# Account Deletion

App stores may require a clear way for users to delete their account.

Wellbine should provide an account deletion path.

Possible implementation:

```text
Settings
↓
Account
↓
Delete Account
↓
Confirmation
↓
Account deletion request
```

Deletion should consider:

- User profile
- User settings
- Active plans
- Daily history
- Push events
- Wearable connections
- Uploads
- Stack items
- Subscriber status
- Audit requirements
- Legal retention requirements

Deletion behavior should be clearly described in Privacy Policy.

---

# Data Deletion

Users should be able to understand what happens to their data.

Data deletion should cover:

- Profile data
- Health-related context
- Wearable connections
- Uploaded files
- Daily actions
- Push history
- Stack items
- Recommendations
- AAI context
- Account metadata

If some data must be retained for legal or audit reasons, the policy should say so clearly.

---

# Uploads And Sensitive Files

Uploads create review and privacy sensitivity.

Supported upload types may include:

- Lab exams
- Blood tests
- Medical reports
- Nutrition plans
- Fitness assessments
- Sleep reports
- Wearable exports
- PDF files
- Images
- Supplement lists
- Medication lists
- Personal notes

Upload should be optional.

Upload should not be required for onboarding.

The app should explain:

- Why upload exists
- What files are accepted
- That upload is optional
- How uploaded data may be used
- How the user can delete uploaded files

---

# Screenshots

App screenshots should show the product clearly without making excessive claims.

Recommended screenshot themes:

- Onboarding activation
- Home operating surface
- Current Insight
- Next Best Action
- Daily sequence
- Push-style guidance
- Pillar overview
- Daily Stack organization
- Wearable optional connection
- Subscriber benefits if included
- Settings / privacy control

Avoid screenshots that imply medical diagnosis or guaranteed health outcomes.

---

# App Description

The app description should be clear and careful.

Possible positioning:

```text
Wellbine is an adaptive wellness guidance system designed to help users organize daily routines across sleep, movement, hydration, nutrition, mind, sunlight and daily stack.
```

Include:

- Adaptive daily guidance
- Home operating surface
- Daily plan
- Push check-ins
- Pillars
- Optional wearables
- Optional uploads
- Subscriber benefits if active

Avoid:

- Diagnosis claims
- Disease treatment claims
- Guaranteed outcomes
- Unsupported clinical claims

---

# Review Notes

App review notes should explain sensitive areas clearly.

Possible review note topics:

- Wellbine is a wellness guidance app
- It does not provide medical diagnosis
- Wearable connection is optional
- Push is used for user-controlled guidance
- Mental Detox can reduce notifications
- Uploads are optional
- External commerce links, if present, are subscriber benefits
- Account deletion is available in Settings
- Test account credentials
- Any feature flags or hidden screens

Review notes should reduce reviewer confusion.

---

# Test Account

A test account should be prepared for app review.

The test account should allow reviewers to access:

- Onboarding completed state
- Active plan state
- Home
- Daily
- Pillars
- Settings
- Wearables screen
- Upload screen
- Subscriber benefits if visible
- Account deletion path

Avoid requiring real payment, real wearable connection or real sensitive data for reviewer access.

---

# Build Readiness Checklist

Before submission, verify:

```text
App builds successfully
No major crashes
Auth works
Logout works
Account deletion path exists
Privacy Policy URL works
Terms URL works
Support URL works
Push permission copy is clear
Health permission copy is clear
Wearable connection is optional
Manual fallback works
Onboarding works
Plan activation works
Home is not blank
Daily works
Pillars work
Settings work
Uploads are optional
External links work
Subscriber benefit copy is clear
No unsupported medical claims
Screenshots are ready
App description is ready
Review notes are ready
Test account is ready
```

---

# QA Before Submission

QA should test:

- New user
- Returning user
- User without Push
- User with Push
- User without wearable
- User with wearable placeholder or connection
- User without upload
- User with upload
- User with active plan
- User with no active plan
- User with subscriber benefit visible
- User with Mental Detox enabled
- User deleting account
- User changing settings
- App offline or poor connection
- App restart
- App update

QA should test both iOS and Android.

---

# Release Tracks

Recommended release path:

```text
Internal build
↓
TestFlight / Google Internal Testing
↓
Closed beta
↓
Controlled production launch
↓
Public launch
```

Avoid full public launch before validating:

- Activation
- Retention
- Push response
- App stability
- Store compliance
- User comprehension
- Subscription flow if applicable
- Commerce bridge if visible

---

# Production Launch Metrics

Track:

- Install
- Signup
- Onboarding start
- Onboarding completion
- Plan activation
- Home first view
- Daily first action
- Push permission acceptance
- Push response rate
- Pillar engagement
- Daily Stack engagement
- Wearable connection attempt
- Upload attempt
- Subscriber benefit view
- Coupon copy
- External commerce click
- Account deletion
- Crashes
- App review feedback
- Retention

These metrics help decide what to improve after launch.

---

# App Release And Data Model

App release depends on the Data Model.

Important areas:

- user_profiles
- user_settings
- user_active_plans
- user_home_state
- daily_plans
- daily_actions
- user_pillar_states
- push_events
- wearable_connections
- user_uploads
- stack_items
- recommendations
- admin_audit_log
- user_aai_context

Release should not happen if core data flows are unstable.

---

# App Release And Admin

Admin affects app release because app behavior may be configuration-driven.

Before launch, Admin should control:

- Published plans
- Onboarding copy
- Push copy
- Home messages
- Pillar defaults
- Content modules
- Recommendations
- Subscriber benefits if active
- Feature visibility
- Publishing state

App review should not see broken draft content.

Only published, launch-ready content should appear.

---

# App Release And Commerce Bridge

Commerce Bridge may affect review.

Before launch, decide:

```text
Is Commerce Bridge visible in this release?
```

If yes, prepare:

- Clear subscriber benefit explanation
- External checkout explanation
- Coupon terms
- No misleading supplement claims
- No unsupported health claims
- Working external links
- Privacy and Terms coverage
- Review notes explanation

If no, keep Commerce Bridge hidden behind configuration.

Do not expose incomplete commerce flows to reviewers.

---

# App Release And Wearables

Wearables may affect review.

Before launch, decide:

```text
Which wearable integrations are active?
```

For each active integration, prepare:

- Permission explanation
- Provider connection flow
- Data usage explanation
- Manual fallback
- Error handling
- Privacy coverage
- Review notes

Do not claim support for devices or platforms not actually connected.

---

# App Release And AAI

AAI may affect review because it uses AI-driven guidance.

Before launch, prepare:

- AI explanation
- Wellness boundary
- No diagnosis statement
- No emergency use statement
- User control
- Escalation language if needed
- Privacy coverage

AAI should make the product more useful, not create unclear medical claims.

---

# What App Release Should Not Do

App release should not:

- Submit before onboarding works
- Submit before account deletion works
- Submit with broken permission flows
- Submit with unsupported medical claims
- Submit with incomplete external commerce
- Submit with hidden required functionality
- Submit with unclear AI claims
- Submit with unclear health data usage
- Submit with mandatory wearable connection
- Submit with a blank Home after onboarding
- Submit with draft content visible to users
- Submit without test credentials
- Submit without Privacy Policy and Terms

---

# Success Criteria

App release is successful when:

- iOS build is accepted
- Android build is accepted
- Onboarding works
- Plan activation works
- Home opens with useful state
- Daily works
- Push works or gracefully degrades
- Wearables are optional
- Uploads are optional
- Account deletion exists
- Privacy and Terms are live
- Claims are safe
- Review notes are clear
- Test accounts work
- No critical crashes occur
- The product can enter controlled launch

---

# Current Status

App Release is currently in planning.

The next implementation steps are:

- Define release scope
- Confirm whether subscriptions are included in first release
- Confirm whether Commerce Bridge is visible in first release
- Confirm active wearable integrations
- Prepare Privacy Policy
- Prepare Terms of Use
- Prepare account deletion flow
- Prepare iOS build process
- Prepare Android build process
- Prepare TestFlight
- Prepare Google internal testing
- Prepare screenshots
- Prepare app description
- Prepare review notes
- Prepare QA checklist

---

# Future Documents

Related future documents may include:

```text
PRODUCTS/WELLBINE/PRIVACY_POLICY_DRAFT.md
PRODUCTS/WELLBINE/TERMS_DRAFT.md
PRODUCTS/WELLBINE/QA_PLAN.md
PRODUCTS/WELLBINE/COMMERCE_BRIDGE.md
PRODUCTS/WELLBINE/WEARABLES.md
```

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
- ARCHITECTURE_DECISIONS/HOME_CENTRAL.md
- ARCHITECTURE_DECISIONS/PUSH_ORCHESTRATION.md
- ARCHITECTURE_DECISIONS/PLAN_TEMPLATES_DB.md
- ARCHITECTURE_DECISIONS/ADMIN_CONTROL_LAYER.md
- ARCHITECTURE_DECISIONS/ONBOARDING_ACTIVATION.md
