# Home As Central Operating Surface

**Status:** Active

**Date:** July 2026

---

# Context

Wellbine needs a clear product architecture for how users interact with the app.

The early app structure included multiple navigation areas such as:

- Home
- Hub
- Store
- Stats
- Profile

This created a risk of fragmentation.

If each area becomes a separate fixed destination, the user may not know where to act, where to inspect status, where to follow guidance or where to adjust the plan.

Wellbine is not intended to behave like a generic wellness dashboard.

Wellbine is intended to operate as an adaptive daily guidance system.

For this reason, the main product surface needs to prioritize:

- Current user state
- Adaptive Summary
- Current Insight
- Next Best Action
- Pillar signals
- Daily execution
- Push continuation
- Ask Wellbine
- Contextual access points

The product should guide the user toward action, not force the user to browse multiple disconnected sections.

---

# Decision

Home is the central operating surface of Wellbine.

Home should be the main place where the user understands what is happening now, what matters next and what action should be taken.

Wellbine should not depend on a fixed Bottom Navigation as the main structure of the product.

Home should absorb or contextualize the functions that were previously separated into fixed areas such as Hub, Stats, Store and Profile.

---

# Official Rule

```text
Home is the main operating surface of Wellbine.
```

```text
Bottom Navigation should not define the core architecture of Wellbine.
```

```text
Navigation should follow user context, not force the user into static app sections.
```

---

# Rationale

Wellbine is built around adaptive guidance.

The user should not need to decide where to go first.

The system should show:

- What is happening now
- What the body/context suggests
- What the next action is
- Which pillars need attention
- What can be confirmed immediately
- What can be adjusted when needed

Home is the right surface for this because it can combine:

- AAI context
- BCAS windows
- Plan Template state
- Onboarding result
- Daily execution
- Push continuation
- Pillar status
- Adaptive Summary
- Ask Wellbine

A fixed Bottom Navigation would make the product feel like a traditional app with separate tabs.

That is not the intended experience.

Wellbine should feel like an intelligent operating surface.

---

# What Home Should Include

Home should include:

- Top Status Area
- Central Main Orb
- Static Pillar Orbs
- Pillar Orb Quick Panel
- Adaptive Summary
- Current Insight
- Next Best Action
- Ask Wellbine
- Quick Actions
- Contextual Access Points
- Active Plan state
- First Activation Mode when no plan exists

---

# Central Main Orb

The Central Main Orb represents the main intelligence state of Wellbine.

It may include the infinity / brand identity.

The Central Main Orb should not only open Daily.

Tapping the Central Main Orb should open an Adaptive Summary screen.

The Adaptive Summary may include:

- Body
- Mind
- Recovery
- Today Sync
- 7-Day Sync

The summary should be adaptive and based on the current user context.

It should not be random decoration.

---

# Pillar Orbs

Mini Pillar Orbs should be static or predictably positioned.

They should not float randomly or behave like uncontrolled visual elements.

Each Pillar Orb may show:

- Icon
- Name
- Percentage
- Status
- Glow or visual intensity
- Current relevance

Tapping a Pillar Orb should open a Pillar Orb Quick Panel before forcing the user into a deeper screen.

---

# Pillar Orb Quick Panel

The Pillar Orb Quick Panel should provide fast action without unnecessary navigation.

It may include:

- Status chip
- Pillar title
- Short explanation
- Primary action
- Open pillar
- Next
- Close

Example:

```text
Recovery

Evening Recovery

Gentle movement can help your recovery window.

Mark done
Open pillar
Next
```

The primary action should update the relevant internal state when possible.

Example:

```text
Mark done
↓
Update Pillar
↓
Update Daily
↓
Update Home
↓
Update AAI context
```

---

# Hub Decision

Hub should not duplicate Home.

If Hub exists only to show the same pillar and status information as Home, it should be absorbed into Home.

Home should become the main inspection and action surface.

A separate Hub should only exist if it has a clear purpose that Home does not already serve.

---

# Stats Decision

Stats should not require a separate primary tab.

Stats should be integrated into Home through:

- Adaptive Summary
- Sync status
- Pillar percentages
- Recovery status
- 7-Day Sync
- Plan progress
- Current Insight

Detailed stats may exist deeper in the product, but they should not define the main navigation structure.

---

# Store Decision

Store should not be a fixed primary navigation item by default.

Store access should be contextual.

Store may appear when relevant through:

- Recommendations
- Daily Stack refill
- Plan-related suggestions
- Content modules
- Partner offers
- User intent
- Admin configuration

Store should not dominate the Wellbine experience.

The product should guide first.

Recommendations and commerce should appear when useful.

---

# Profile Decision

Profile should not compete with Home as a primary destination.

Profile or Personal Center should be accessible through a clear top-level entry such as:

- Avatar
- Settings icon
- Personal Center shortcut

Profile should include account and personal configuration.

Home should remain the daily operating surface.

---

# Push Continuation

If the user enters the app from a Push notification, Home should not always open generically.

When the user taps Adjust from Push, the app should deep-link to the relevant adjustment panel.

Examples:

- Hydration adjustment
- Sleep adjustment
- Daily Stack adjustment
- Movement adjustment
- Recovery adjustment
- Meal / Nutrition adjustment
- Mind reset adjustment

The user should continue the same context that started in Push.

Push should connect directly to Home, Daily or the relevant Pillar panel depending on context.

---

# First Activation Mode

If the user has no active plan, Home should enter First Activation Mode.

Home should not show a full operating state before activation.

First Activation Mode should guide the user toward:

- Onboarding
- Plan selection
- Ask Wellbine
- First 7-Day Sync Plan activation

Example:

```text
Start your first Wellbine plan.

Choose a plan to activate your Daily, Push and Pillars.
```

After activation, Home should show:

- Active Plan
- Current Insight
- Next Best Action
- Pillar states
- Adaptive Summary
- Ask Wellbine
- Quick Actions

---

# Navigation Principle

Wellbine navigation should be contextual.

The product should not force the user to think in terms of static sections.

The user should be guided by:

- Current state
- Current need
- Biological context
- Active plan
- Pillar priority
- Push response
- Daily sequence
- Next Best Action

The app should behave like an adaptive operating system for personal health behavior, not like a generic tab-based tracker.

---

# Consequences

This decision means:

- Home becomes the central product surface.
- Fixed Bottom Navigation should not be the main architecture.
- Hub should not duplicate Home.
- Stats should be integrated into Home and deeper summaries.
- Store should be contextual, not dominant.
- Profile should be accessible but not compete with Home.
- Push should deep-link into relevant context.
- Pillar Orbs should support quick action.
- Daily should remain the deeper execution layer.
- Onboarding should activate Home, not just complete a form.
- Plan Templates should configure the initial Home state.
- Admin should manage Home-related content and behavior.

---

# What This Prevents

This decision prevents:

- Home becoming only a decorative dashboard
- Hub duplicating Home
- Store dominating the main navigation
- Stats becoming disconnected from action
- Bottom Navigation controlling the product structure
- Users getting lost between unrelated tabs
- Push opening generic screens instead of contextual actions
- Pillars becoming only icons without operational behavior

---

# Related Documents

- README.md
- PRODUCTS/WELLBINE/README.md
- PRODUCTS/WELLBINE/HOME.md
- PRODUCTS/WELLBINE/DAILY.md
- PRODUCTS/WELLBINE/PUSH.md
- PRODUCTS/WELLBINE/PILLARS.md
- PRODUCTS/WELLBINE/PLAN_TEMPLATES.md
- PRODUCTS/WELLBINE/ONBOARDING.md
- PRODUCTS/WELLBINE/ADMIN.md
