# Wellbine Wearables

**Version:** 0.1.0

**Status:** Draft

**Last Updated:** July 2026

---

# Purpose

This document defines the Wearables layer of Wellbine.

Wearables are optional context enhancers that may improve automation, personalization and adaptive guidance.

Wearables should help Wellbine understand:

- Sleep
- Recovery
- Movement
- Inactivity
- Heart trends
- HRV
- Respiratory signals
- Oxygen saturation
- Temperature trends
- Stress signals
- Readiness
- Cycle-related insights when supported

Wearables should improve the product.

Wearables should not be required for the product to work.

---

# Official Definition

**Wellbine Wearables is the optional device connectivity layer that allows Wellbine to use permissioned wearable and health data to improve Home, Daily, Push, Pillars and AAI Context without making wearable access mandatory.**

---

# Core Principle

The core wearable rule is:

```text
Wearables improve automation, but Wellbine must work without wearables.
```

Users without wearables should still receive value through:

- Onboarding
- Push check-ins
- Manual inputs
- Daily behavior
- Pillar updates
- Ask Wellbine
- Settings
- Plan configuration
- Uploads

Wearables should reduce friction.

They should not create dependency.

---

# Product Role

Wearables should support the Wellbine operating system.

They should not become the product itself.

Wearables help answer:

```text
What is the user's biological context right now?
```

Examples:

- Did the user sleep enough?
- Is recovery low?
- Is movement too low?
- Has the user been inactive?
- Is resting heart rate elevated?
- Is HRV lower than usual?
- Is there a possible stress signal?
- Is there a temperature trend?
- Is the user in a lower readiness state?

Wearables provide signals.

AAI interprets context.

Wellbine suggests action.

---

# Relationship With AAI

AAI should use wearable signals as one input layer.

Wearables may provide:

- Passive observation
- Reduced manual input
- Context validation
- Trend detection
- Recovery estimation
- Sleep consistency
- Movement patterns
- Stress-related signals
- Readiness context

AAI should never treat wearable data as perfect truth.

Wearable data should be interpreted together with:

- User answers
- Daily actions
- Pillar states
- Plan context
- Push responses
- Uploads
- Settings
- Historical behavior

AAI should use wearable data to improve alignment, not to overrule the user blindly.

---

# Relationship With BCAS

Wearables support BCAS by helping estimate biological context.

BCAS should use wearable signals to improve:

- Wake Window
- Recovery Window
- Movement Window
- Sleep Preparation Window
- Hydration Opportunity
- Daily Stack timing
- Stress / recovery context

Example:

```text
User slept poorly
↓
Recovery Window becomes more important
↓
Daily adjusts movement intensity
↓
Push suggests lighter activation
↓
Home updates Current Insight
```

BCAS should not rely only on fixed clock time.

Wearables help the system understand the user's body state.

---

# Relationship With Home

Home should reflect wearable context when available.

Wearable data may update:

- Adaptive Summary
- Current Insight
- Next Best Action
- Recovery state
- Sleep state
- Movement state
- Pillar percentages
- Readiness indication
- Today Sync
- 7-Day Sync

Example:

```text
Wearable detects short sleep
↓
Home shows Recovery priority
↓
Next Best Action changes
```

If no wearable is connected, Home should use manual and Push-based signals.

Home should not show a broken state just because wearable data is missing.

---

# Relationship With Daily

Daily should adapt using wearable context when available.

Wearable data may influence:

- Morning Activation
- Movement intensity
- Recovery sequence
- Sleep planning
- Hydration prompts
- Mind reset
- Daily Stack timing
- Meal / Nutrition timing
- Night Reset

Example:

```text
Low recovery signal
↓
Daily reduces intensity
↓
Movement shifts from HIIT to light walk
↓
Mind reset becomes higher priority
```

Daily should always have a fallback.

---

# Relationship With Push

Push should become more personalized when wearable data exists.

Wearable data may affect:

- Push timing
- Push copy
- Push urgency
- Push frequency
- Push questions
- Confirm / Adjust / Later logic
- Recovery language
- Deep-link destination

Example:

```text
Wearable shows low sleep duration
↓
Morning Push asks recovery-focused question
```

Example:

```text
Wearable shows low movement
↓
Midday Push suggests movement window
```

If no wearable is connected, Push should ask simple check-ins.

---

# Relationship With Pillars

Wearables may support multiple pillars.

Current pillars:

- Mind
- Sun
- Hydration
- Sleep
- Meal / Nutrition
- Movement
- Daily Stack

Wearables directly support:

- Sleep
- Movement
- Mind / stress context
- Recovery
- Daily Stack timing when connected to routine context

Wearables indirectly support:

- Hydration
- Meal / Nutrition
- Sun
- Overall Daily alignment

Wearables should not replace pillar interaction.

They should improve pillar context.

---

# Relationship With Onboarding

Wearable connection should be offered during Onboarding.

It should be optional.

Preferred copy:

```text
You have the opportunity to connect a wearable device, if you want.

This can help Wellbine understand your sleep, movement and recovery more automatically.
```

Actions:

```text
Connect wearable
Skip for now
```

If skipped:

```text
No problem. Wellbine will adapt through simple check-ins.
```

Onboarding should not block activation if the user skips wearable connection.

---

# Relationship With Plan Templates

Plan Templates may define wearable behavior.

A Plan Template may configure:

- Wearable optional
- Wearable recommended
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
- Push personalization from wearable data
- Home summary from wearable data

Plan Templates should not require wearable access by default unless a specific plan explicitly depends on it.

---

# Relationship With Admin

Admin should configure wearable behavior.

Admin may control:

- Supported providers
- Enabled providers
- Wearable connection copy
- Permission explanation
- Data usage rules
- Fallback behavior
- Plan-specific wearable logic
- Pillar-specific wearable logic
- Home display rules
- Push behavior from wearable data
- Error messages
- Reconnect prompts

Admin should be able to adjust wearable behavior without changing app code where practical.

---

# Relationship With Data Model

Wearables are represented in the Data Model through:

```text
wearable_connections
wearable_daily_summaries
wearable_events
```

Potential data fields include:

```text
provider
status
connected_at
last_sync_at
permissions_json
sleep_duration_minutes
sleep_quality_score
resting_heart_rate
hrv_ms
steps
active_minutes
calories
spo2
respiratory_rate
temperature_delta
stress_score
readiness_score
raw_summary_json
```

Wearable data should be scoped, permissioned and stored carefully.

---

# Supported Provider Direction

The Wearables layer may support:

```text
Apple Health / HealthKit
Google Health Connect
Garmin
Oura
WHOOP
Fitbit
Other providers
Manual fallback
```

Implementation should verify provider availability, API access, review requirements and regional restrictions before launch.

Not every provider needs to be supported in MVP.

---

# MVP Provider Strategy

The MVP should not try to support every wearable provider immediately.

Recommended MVP direction:

```text
1. Manual fallback
2. Apple Health / HealthKit direction
3. Google Health Connect direction
4. Additional providers later
```

Garmin, Oura, WHOOP and Fitbit may be added later depending on:

- API access
- User demand
- Development cost
- App review requirements
- Business priority
- Market strategy

---

# Manual Fallback

Manual fallback is required.

Without wearable connection, Wellbine should still ask:

- How did you sleep?
- How did you wake up?
- How is your energy?
- How is your stress?
- Did you move today?
- How was hydration?
- Are you ready for sleep preparation?
- Did you complete your Daily Stack?

Manual fallback supports:

- Users without devices
- Users who deny permission
- Users with disconnected devices
- Users with incomplete data
- Users with privacy concerns

Manual fallback protects product value.

---

# Wearable Signals

Possible wearable signals:

```text
sleep_duration
sleep_quality
wake_time
bedtime
resting_heart_rate
heart_rate
hrv
steps
active_minutes
calories
respiratory_rate
oxygen_saturation
temperature_delta
stress_score
readiness_score
cycle_related_signals
premenstrual_estimation
```

Not all providers support all signals.

The system should treat every signal as optional.

---

# Signal Reliability

Wearable signals should be treated as estimates.

Wellbine should avoid assuming that every wearable measurement is exact.

Rules:

```text
Use trends more than isolated numbers.
```

```text
Use wearable data as context, not diagnosis.
```

```text
Combine wearable data with user feedback.
```

```text
Do not overreact to a single abnormal signal.
```

Example:

```text
One poor HRV reading
↓
Suggest lighter recovery-aware guidance
↓
Do not make medical claims
```

---

# Permission Strategy

Wearable permissions should be clear and specific.

The user should understand:

- What data is requested
- Why it is useful
- How it improves guidance
- That connection is optional
- That permissions can be changed later

Permission copy should be simple.

Example:

```text
Wellbine uses sleep and movement data to personalize your daily guidance.
```

Avoid fear-based or overly technical language.

---

# Privacy Rule

Wearable data may be sensitive.

The system should follow these rules:

```text
Collect only useful data.
```

```text
Ask permission clearly.
```

```text
Respect user control.
```

```text
Do not expose wearable data unnecessarily.
```

```text
Do not use wearable data for diagnosis.
```

```text
Allow disconnecting wearable access.
```

---

# Disconnection Flow

Users should be able to disconnect a wearable.

When disconnected:

```text
Wearable connection status changes
↓
Data sync stops
↓
Manual fallback becomes active
↓
Home and Daily continue functioning
```

The user should not lose access to the core product.

---

# Error States

The product should handle wearable errors gracefully.

Possible error states:

- Not connected
- Permission denied
- Sync failed
- Provider unavailable
- Partial data
- Old data
- Token expired
- Reconnect required
- Unsupported provider
- No wearable detected

Example copy:

```text
Wearable data is not available right now.

Wellbine will continue with check-ins.
```

Do not make the user feel blocked.

---

# Data Freshness

Wearable data should have freshness awareness.

The system should know:

- Last sync time
- Data date
- Provider status
- Signal completeness
- Whether data is stale

Example:

```text
Last sync: 14 hours ago
```

If data is stale, Wellbine should avoid making strong adjustments based on it.

---

# Home Display Rules

Home should not overload the user with raw wearable data.

Home should translate wearable data into useful context.

Bad:

```text
HRV: 41ms
RHR: 72
SpO2: 96
Respiratory rate: 17
Temperature delta: +0.3
```

Better:

```text
Recovery may be lower today.

Use a lighter movement sequence and prioritize hydration.
```

Detailed metrics may be available in deeper views, but Home should focus on action.

---

# Daily Adjustment Rules

Daily should use wearable signals to adjust intensity.

Example rules:

```text
Low sleep duration
↓
Reduce morning intensity
```

```text
Low movement by midday
↓
Suggest short movement window
```

```text
High inactivity
↓
Trigger movement opportunity
```

```text
Low recovery
↓
Prioritize recovery, hydration and sleep preparation
```

Rules should remain configurable through Admin and Plan Templates.

---

# Push Adjustment Rules

Push may use wearable signals to personalize check-ins.

Example:

```text
Short sleep detected
↓
How is your energy this morning?

Stable
Low
Very low
```

Example:

```text
Low movement detected
↓
Ready for a short activation walk?

Confirm
Adjust
Later
```

Push should remain simple.

Wearable data should make Push smarter, not more annoying.

---

# Cycle-Related Insights

Wearables may support cycle-related insights when supported by the device, permissions and available data.

Possible use cases:

- Cycle-related recovery context
- Premenstrual period estimation
- Temperature trend awareness
- Energy guidance
- Sleep guidance
- Movement intensity adjustment

Rules:

```text
Use only when supported.
```

```text
Ask permission clearly.
```

```text
Avoid diagnosis.
```

```text
Use cautious language.
```

Example:

```text
Your recent pattern may suggest a lower-recovery window.

Consider a lighter movement sequence today.
```

---

# Medical Safety Boundary

Wearables should not turn Wellbine into a diagnostic product.

Wellbine should not claim to diagnose:

- Heart disease
- Sleep disorders
- Respiratory disease
- Fertility status
- Hormonal conditions
- Mental health disorders
- Medical emergencies

Wellbine may provide lifestyle guidance based on context.

If something appears concerning, the product may encourage professional consultation using cautious language.

---

# FlutterFlow Implementation Direction

FlutterFlow may be used to build:

- Wearable connection screen
- Permission explanation screen
- Wearable status screen
- Manual fallback screens
- Sync status components
- Wearable-based Home cards
- Wearable adjustment panels
- Settings and disconnect flow

FlutterFlow should not hardcode provider logic that belongs in Supabase/Admin configuration.

FlutterFlow should render connection status and context.

---

# Supabase Implementation Direction

Supabase should store:

- Wearable connection status
- Provider metadata
- Permission metadata
- Last sync timestamp
- Daily summaries
- Wearable events
- Manual fallback data
- AAI context updates

Supabase should enforce user-level access.

Users should only access their own wearable data.

Admin access should be role-controlled.

---

# Integration Layer Direction

Some wearable integrations may require custom backend logic.

Possible implementation paths:

- FlutterFlow native integration when available
- Custom actions
- Supabase Edge Functions
- External integration service
- Provider APIs
- Manual import
- User-uploaded wearable exports

The final technical path should depend on provider requirements and implementation cost.

---

# MVP Scope

MVP should include:

- Wearable optional connection concept
- Manual fallback
- Wearable status field
- Basic wearable connection screen
- Basic permission explanation
- Placeholder for future provider sync
- Basic data model support
- Home/Daily/Push logic prepared for wearable signals

MVP should not require:

- Full Garmin integration
- Full Oura integration
- Full WHOOP integration
- Full Fitbit integration
- Full Apple Health implementation before core product
- Full Google Health Connect implementation before core product
- Deep biometric analytics
- Medical interpretation

The MVP should be wearable-ready, not wearable-dependent.

---

# Future Scope

Future versions may include:

- Apple Health / HealthKit integration
- Google Health Connect integration
- Garmin integration
- Oura integration
- WHOOP integration
- Fitbit integration
- Wearable exports upload
- Advanced recovery modeling
- Sleep consistency modeling
- Cycle-aware personalization
- Stress pattern detection
- Readiness scoring
- Wearable-based Push timing
- Wearable-based Daily regeneration
- Provider-specific dashboards
- Data quality scoring
- Consent management
- FHIR-compatible mapping

---

# App Store And Google Play Impact

Wearables may affect app store review.

The product should prepare:

- Health data permission explanation
- Privacy Policy
- Terms of Use
- Account deletion
- Data deletion
- Health data usage description
- App review notes
- Screenshots showing permission context
- Clear statement that wearable connection is optional
- Clear statement that Wellbine is not a diagnostic tool

Wearables should be considered in:

```text
PRODUCTS/WELLBINE/APP_RELEASE.md
```

---

# What Wearables Should Not Do

Wearables should not:

- Be required for onboarding
- Be required for plan activation
- Replace user feedback
- Override user preference blindly
- Create medical diagnosis
- Overload Home with raw metrics
- Make Push too frequent
- Make Wellbine feel like a smartwatch dashboard
- Block the user when data is missing
- Become the central product identity

Wearables should support the system.

They should not become the system.

---

# Success Criteria

Wearables are successful when:

- Users can connect devices optionally
- Users without devices still receive value
- Home becomes more contextual
- Daily adapts more intelligently
- Push becomes more relevant
- Pillar states improve
- AAI context becomes richer
- The product remains simple
- Permissions are clear
- Privacy is respected
- App store review is not blocked by unclear health claims

---

# Current Status

Wearables are currently defined as an optional context enhancement layer.

The next implementation steps are:

- Confirm MVP wearable scope
- Define manual fallback
- Define wearable data fields
- Define wearable connection screen
- Define permission copy
- Define provider priority
- Define Supabase tables
- Define FlutterFlow implementation path
- Define app store requirements
- Connect wearable state to Home, Daily, Push and AAI Context

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
- ARCHITECTURE_DECISIONS/HOME_CENTRAL.md
- ARCHITECTURE_DECISIONS/PUSH_ORCHESTRATION.md
- ARCHITECTURE_DECISIONS/PLAN_TEMPLATES_DB.md
- ARCHITECTURE_DECISIONS/ADMIN_CONTROL_LAYER.md
- ARCHITECTURE_DECISIONS/ONBOARDING_ACTIVATION.md
