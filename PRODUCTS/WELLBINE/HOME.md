# Wellbine Home

**Version:** 0.1.0

**Status:** Active

**Last Updated:** July 2026

---

# Purpose

This document defines the Wellbine Home experience.

Home is the main visual and operational entry point of the Wellbine app.

Home should not behave like a generic dashboard.

Home should not behave like one tab among many.

Home should become the central operating surface of Wellbine.

Home should help the user understand the current state of the system, the most relevant context and the next best action with minimal cognitive effort.

Home should answer:

```text
What matters now?
```

and:

```text
What is my next best action?
```

---

# Official Definition

**Wellbine Home is the main visual and operational surface of the app, designed to present the user's current context, adaptive summary, relevant pillar state and Next Best Action without relying on fixed bottom navigation.**

---

# Core Principle

Home is not a data wall.

Home is not a full dashboard.

Home is not a checklist.

Home is not a tab.

Home is the calm intelligence layer of Wellbine.

The user should be able to open the app, understand the current state, take one relevant action and leave.

---

# Relationship With AAI

Home is where AAI becomes visible to the user.

AAI uses Home to present:

- Current context
- Adaptive summary
- Next Best Action
- Relevant pillar state
- Recovery opportunity
- Daily status
- Push result
- Active plan state
- Ask Wellbine entry point

Home should not expose internal complexity.

The user should experience intelligence as clarity.

---

# Relationship With BCAS

Home must follow BCAS logic.

The screen should prioritize biological context over fixed clock time.

Examples of possible current contexts:

- Morning Reset
- Wake Window
- Feeding Window
- Movement Window
- Recovery Window
- Hydration Opportunity
- Sleep Preparation Window
- Daily Stack Window

Home should not simply tell the user what time it is.

Home should show what biological context matters now.

---

# Relationship With Daily

Home and Wellbine Daily must remain synchronized.

Daily is the deeper execution layer.

Home is the simplified operating surface.

Home should surface only the most relevant information from Daily.

Examples:

- Current Biological Context
- Next Best Action
- Active sequence
- Pending pillar action
- Recovery status
- Current protocol
- Active plan
- Daily Stack status
- Sleep plan status
- Hydration trend

The user may open Daily when deeper execution detail is needed.

Home should remain simple.

Daily should provide operational depth.

Daily does not need to exist as a fixed bottom navigation item.

Daily should be accessible through contextual Home actions.

---

# Relationship With Push

Home must reflect what happens through Push.

When the user confirms, adjusts or delays a Push sequence, Home should update automatically.

Examples:

- If the user confirms a morning plan by Push, Home should reflect the updated state.
- If the user taps Later, Home should show the relevant sequence as pending.
- If the user adjusts a plan, Home should reflect the new active sequence.
- If Push identifies a recovery need, Home should show the recovery context.
- If Push updates Hydration, Sleep, Meal, Movement, Mind, Sun or Stack, Home should reflect the relevant pillar state.

Home, Daily and Push must operate as one connected system.

---

# Relationship With Pillars

Home should not display pillars as static icons only.

Pillars are operational modules.

Home should show pillar information only when it is relevant to the current context.

Current operational pillars:

- Mind
- Sun
- Hydration
- Sleep
- Meal / Nutrition
- Movement
- Daily Stack

Home should not force the user to inspect every pillar every time.

Home should highlight:

- The active pillar
- The most relevant pending pillar
- The pillar affecting recovery
- The pillar connected to the Next Best Action

---

# Relationship With Plan Templates

Home must support users with or without an active plan.

If the user already has an active plan, Home should show the current state of that plan.

If the user has no active plan, Home should enter First Activation Mode.

Plan Templates are defined outside Home.

Home only displays the result of the active plan or routes the user to choose one.

Future related documents:

```text
PRODUCTS/WELLBINE/PLAN_TEMPLATES.md
PRODUCTS/WELLBINE/ONBOARDING.md
```

---

# Home Entry Paths

Home must support three different entry paths:

1. First Access Entry
2. Direct App Entry
3. Push Entry

These paths should not behave the same way.

---

# 1. First Access Entry

When the user opens Wellbine for the first time and has no active plan, Home should not show the full operational state.

Instead, Home should enter:

```text
First Activation Mode
```

First Activation Mode should guide the user to choose a starting plan.

Example:

```text
Start your first Wellbine plan.

Choose a plan to activate your Daily, Push and Pillars.
```

Possible actions:

- Choose Plan
- Continue Setup
- Ask Wellbine

After the user selects a plan, Wellbine should activate:

- Daily
- Push logic
- Pillar defaults
- Home state
- Sync baseline
- Initial guidance

The full onboarding logic should be defined in a dedicated Onboarding document.

Home should only define how the first access state appears.

---

# 2. Direct App Entry

When the user opens Wellbine directly, without coming from a Push, the app should open the main Home experience.

The main Home should preserve the current premium dark layout and Orb-based visual identity.

The preferred Home composition is:

```text
Top Status Area

↓

Central Main Orb

↓

Static smaller Pillar Orbs

↓

Current Insight / Next Best Action

↓

Ask Wellbine input

↓

Contextual Access Points
```

The Home should not become a dashboard.

The user should be able to understand the current state quickly.

---

# 3. Push Entry

When the user enters Wellbine through a Push action, the app should route according to the Push action selected.

---

## Confirm

If the user taps Confirm, the app should not open.

Confirm should update internal pillar states, Daily, Sync and AAI learning in the background.

---

## Later

If the user taps Later, the app should not open.

Later should register delay and schedule a follow-up Push approximately one hour later.

---

## Adjust

If the user taps Adjust, Wellbine should not open the generic Home screen.

It should deep-link directly into the relevant operational screen.

The most common destination is a Sync Control or adjustment screen related to the Push sequence.

Example Push:

```text
Your morning plan:

10 min sunlight
Breakfast
Vitamin B
Omega 3
Hydration
15 min HIIT

Ok?

Confirm
Adjust
Later
```

If the user taps Adjust, Wellbine should open a Sync Control screen for that sequence.

The user should be able to enable, disable or adjust each item in the proposed plan.

Example adjustment items:

- Sunlight
- Breakfast
- Vitamin B
- Omega 3
- Hydration
- HIIT

The adjustment screen should allow the user to:

- Enable an action
- Disable an action
- Change intensity
- Change timing
- Replace an action
- Confirm the adjusted plan

After the user confirms the adjusted plan, Wellbine should update:

- Daily
- Push state
- Relevant pillars
- Sync
- AAI learning

Push Adjust should always deep-link into the relevant screen.

It should not require the user to manually search for the correct pillar.

---

# Core Screen Structure

The Home screen should include:

1. Top Status Area
2. Central Main Orb
3. Static Pillar Orbs
4. Pillar Orb Quick Panel
5. Adaptive Summary
6. Current Insight
7. Next Best Action
8. Ask Wellbine
9. Quick Actions
10. Contextual Access Points

Home should not use fixed Bottom Navigation.

All primary app shortcuts should be accessible from Home itself.

---

# 1. Top Status Area

The top status area should remain minimal.

Possible elements:

- Settings
- Wearable connection status
- Sync indicator
- Profile / Personal Center access
- Current date
- Current time

Avoid placing too much information at the top.

The top area should support orientation, not dominate the screen.

---

# 2. Central Main Orb

The Central Main Orb is the main visual identity of Wellbine.

It should remain visually consistent with the current premium dark design.

The infinity symbol may remain the central brand element.

However, the Central Main Orb should no longer function only as a logo button that opens Wellbine Daily.

The Central Main Orb should become the main summary gateway of the app.

When tapped, the Central Main Orb should open an Adaptive Summary Screen.

The Orb should represent the user's current system state.

---

# Central Main Orb Behavior

The Central Main Orb may communicate status through:

- Glow intensity
- Color gradient
- Motion intensity
- Recovery state
- Sync state
- System state
- Subtle visual feedback

The Orb should remain premium and calm.

Avoid:

- Excessive animation
- Confusing visual states
- Gamified noise
- Overloaded data inside the Orb

The Orb should feel intelligent, not busy.

---

# 3. Static Pillar Orbs

The smaller Pillar Orbs should remain part of the visual identity.

However, they should not float or orbit unpredictably around the Central Main Orb.

The smaller Orbs should become static or predictably positioned.

They should use a consistent spatial organization so the user builds visual memory over time.

The Orbs may represent:

- Mind
- Sun
- Hydration
- Sleep
- Meal / Nutrition
- Movement
- Daily Stack

---

# Static Pillar Orb Layout

The smaller Pillar Orbs should follow a fixed and predictable spatial layout.

They should preserve the current Home visual style while borrowing the clarity of the Hub Orb structure.

Each Pillar Orb may show:

- Pillar icon
- Pillar name
- Percentage
- Status
- Glow intensity
- Completion state

Example:

```text
SUN
100%
```

```text
HYDRO
82%
```

```text
STACK
33%
```

```text
SLEEP
0%
```

The smaller Orbs should help the user understand system state without opening every pillar.

The Orbs should be informational first, but a tap should open the Pillar Orb Quick Panel for fast action.

---

# 4. Pillar Orb Quick Panel

When the user taps a smaller Pillar Orb, Home should open a quick contextual popup instead of immediately opening the full pillar screen.

The Pillar Orb Quick Panel should provide fast actions related to that pillar without forcing the user to leave Home.

This panel should behave like a lightweight operational shortcut.

Example:

```text
RECOVERY

Evening Recovery

Gentle movement for recovery

Mark done
Open pillar
Next
```

Another example:

```text
DONE TODAY

Midday Movement

Break sedentary time with motion

Done today
Open pillar
Next
```

The Pillar Orb Quick Panel should be contextual.

It should reflect the selected pillar and the current state of the day.

---

# Pillar Orb Quick Panel Structure

The quick panel may include:

- Pillar icon
- Status chip
- Action title
- Short description
- Primary action button
- Open pillar shortcut
- Next shortcut
- Close button

Example status chips:

- Recovery
- Done Today
- Pending
- Active
- Next
- Window Closed
- Adjusted

---

# Pillar Orb Quick Panel Actions

## Primary Action

The primary action depends on the pillar state.

Examples:

- Mark done
- Done today
- Start
- Confirm
- Adjust
- Resume
- Recover

If the user taps the primary action, the app should update the related pillar, Daily, Sync and AAI learning without requiring full navigation when possible.

Example:

```text
Mark done

↓

Update pillar

↓

Update Daily

↓

Update Sync

↓

Show confirmation feedback
```

---

## Open Pillar

Open pillar should take the user to the full pillar screen.

This is used when the user wants more detail or manual control.

Examples:

- Open Hydration panel
- Open Sleep panel
- Open Movement panel
- Open Meal / Nutrition panel
- Open Mind panel
- Open Daily Stack panel

---

## Next

Next should move the user to the next relevant pillar action or suggested sequence.

It should not randomly cycle through pillars.

Next should be context-aware.

Example:

If Movement is done and Hydration is behind, Next may surface Hydration.

If Recovery is active, Next may surface Mind or Sleep Preparation.

---

# Product Rule

Mini Pillar Orbs and the Central Main Orb must have different behaviors.

```text
Mini Pillar Orb

↓

Pillar Orb Quick Panel
```

```text
Central Main Orb

↓

Adaptive Summary Screen
```

The user should be able to act quickly from Home without being forced into deep navigation.

---

# Pillar Orb States

Pillar Orbs may show state through subtle visual treatment.

Possible states:

- Active
- Pending
- Done
- Upcoming
- Window Closed
- Locked
- Adjusted
- Partial

Preferred visual treatments:

- Glow intensity
- Opacity
- Small completion indicator
- Subtle border
- Soft highlight
- Percentage
- Short status label

Avoid:

- Constant movement
- Uncontrolled floating animations
- Excessive orbit effects
- Distracting transitions
- Dashboard clutter

---

# 5. Adaptive Summary

The Adaptive Summary is the high-level intelligence summary of the user's current state.

It may appear when the user taps the Central Main Orb or as the primary Main Orb detail state.

It should summarize the most important state of the user.

Possible summary areas:

- Body
- Mind
- Recovery
- Today Sync
- 7-Day Sync

The Adaptive Summary should not be random.

It should prioritize the most relevant insight based on current context.

Example:

- If recovery is low, Recovery appears first.
- If hydration is low, Body or Hydration may appear first.
- If sleep planning is active, Sleep or Recovery may appear first.
- If the day is going well, Today Sync may appear first.
- If the weekly trend matters, 7-Day Sync may appear first.

---

# Adaptive Summary Screen

The Adaptive Summary Screen may use a gauge-style interface.

Example:

```text
Today Sync

1.6

Medium
```

Other possible summaries:

```text
Body

Low Recovery
```

```text
Mind

Stable
```

```text
Recovery

Needs Attention
```

```text
7-Day Sync

Improving
```

Preferred naming:

```text
Adaptive Summary
```

Avoid naming this behavior:

```text
Random screen
```

The intelligence should feel intentional.

---

# 6. Current Insight

Below the Orb area, Home should show the most relevant current message.

Example:

```text
A few areas need attention.

Log a meal to refocus.
```

Another example:

```text
Your recovery is lower today.

Choose a lighter movement plan.
```

Another example:

```text
Hydration is behind.

Drink water now.
```

Current Insight should be:

- Short
- Context-aware
- Useful
- Actionable
- Calm

Avoid generic motivational messages.

---

# 7. Next Best Action

The main action card should be called:

```text
Next Best Action
```

It should present one clear action.

Example:

```text
Next Best Action

Have your planned lunch.

Done
Adjust
Later
```

Another example:

```text
Next Best Action

Hydrate now.

Done
Later
```

Another example:

```text
Next Best Action

Confirm your sleep plan.

Confirm
Adjust
Later
```

The action should be direct and easy to understand.

Avoid vague buttons such as:

- Continue Today
- Go
- Proceed
- Next

Preferred buttons:

- Done
- Start
- Confirm
- Adjust
- Later
- Open Daily

---

# Active Sequence

Home may show the current active sequence when relevant.

Example:

```text
Morning Plan

10 min sunlight
Breakfast
Vitamin B
Omega 3
Hydration
15 min HIIT
```

The active sequence should be short.

It should not become a long checklist.

Recommended maximum:

```text
3 to 6 actions
```

If more detail is needed, the user should open Daily.

---

# 8. Ask Wellbine

Ask Wellbine should remain available from Home.

It should function as the user's direct conversational entry point.

Ask Wellbine is not the same as AAI.

Ask Wellbine is the conversational interface.

AAI is the intelligence architecture behind the system.

Suggested prompts:

- What should I do now?
- Organize my day
- Help me recover today
- I feel tired
- Adjust my plan
- How is my progress?
- Plan my sleep
- What should I eat?
- Help me move today

---

# 9. Quick Actions

The plus button should function as Quick Actions.

Quick Actions may include:

- Log meal
- Log water
- Log movement
- Log mood
- Log supplement
- Log medication
- Adjust protocol
- Open Daily Stack
- Start meditation
- Adjust sleep plan
- Change active plan

Quick Actions should not become a large menu.

They should provide fast access to common actions.

---

# 10. Contextual Access Points

Wellbine should not rely on fixed Bottom Navigation.

The Home screen should become the central operating surface of the app.

The previous bottom navigation items should be absorbed or replaced by contextual access points inside Home.

---

## Home

Home is the primary operating surface.

It is not just one tab among many.

Home should contain:

- Central Main Orb
- Static Pillar Orbs
- Adaptive Summary
- Current Insight
- Next Best Action
- Ask Wellbine
- Quick Actions
- Pillar Orb Quick Panels

---

## Hub

Hub should not exist as a separate primary navigation tab if it repeats Home.

The current Hub function should be absorbed into Home through:

- Static Pillar Orbs
- Pillar Orb Quick Panels
- Adaptive Summary
- Pillar state percentages
- Contextual pillar access

If a deeper Hub-like view exists in the future, it should be treated as a secondary view, not a main navigation item.

---

## Store

Store should not be a fixed in-app bottom navigation item.

Commercial flows should be external or context-triggered.

Store access may appear through:

- Stack refill recommendations
- Plan Template recommendations
- Product suggestions linked to a protocol
- External checkout
- Admin-managed offers
- Ask Wellbine suggestions when appropriate

Store should not compete with the daily operating experience.

---

## Stats

Stats should not be a fixed bottom navigation item.

Stats should be integrated into Home through:

- Adaptive Summary
- Today Sync
- 7-Day Sync
- Pillar percentages
- Recovery state
- Current Insight
- Progress cards when relevant

The user should not need to open a separate Stats tab to understand progress.

---

## Profile

Profile should not be a fixed bottom navigation item.

Profile, account, personal records and settings should be accessible through a single clear entry point.

Possible access points:

- Top Status Area
- Settings icon
- User avatar
- Personal Center shortcut

Profile access should not duplicate the same destination as another icon unless intentionally designed as a Personal Center.

---

# Navigation Rule

Wellbine should minimize persistent navigation.

The app should avoid competing sections at the bottom of the screen.

Primary navigation should happen through:

```text
Central Main Orb
↓
Adaptive Summary

Mini Pillar Orb
↓
Pillar Orb Quick Panel

Ask Wellbine
↓
Conversational assistance

Plus Button
↓
Quick Actions

Push Adjust
↓
Relevant Sync Control screen

Top Status / Avatar
↓
Personal Center or Settings
```

The user should not need a fixed bottom menu to operate Wellbine.

Home should contain the app's main operating logic.

---

# Home, Hub And Daily Separation

Home, Hub and Daily should not compete with each other.

They have different roles.

---

## Home

Home shows the current state, Adaptive Summary, relevant pillar signal, Current Insight and Next Best Action.

Home answers:

```text
What matters now?
```

---

## Hub

Hub should not be a primary tab if it simply repeats Home.

Hub may exist only as a secondary pillar inspection view if needed.

Hub answers:

```text
What is happening across my pillars?
```

---

## Daily

Daily is the execution layer.

Daily shows the deeper operational flow of the day, including sequences, windows, recovery, actions and pillar progression.

Daily answers:

```text
How is my day being executed?
```

Product rule:

```text
Home = act now

Hub = inspect pillars, only if needed

Daily = execute the day
```

---

# Home Information Hierarchy

Home should combine four layers.

---

## 1. Visual State

The Orb system shows the user's overall state.

This includes:

- Central Main Orb
- Static Pillar Orbs
- Color
- Glow
- Percentage
- Status

---

## 2. Adaptive Summary

The Central Main Orb opens or displays the Adaptive Summary.

The Adaptive Summary may include:

- Body
- Mind
- Recovery
- Today Sync
- 7-Day Sync

---

## 3. Current Insight

Home shows the most relevant current message.

Example:

```text
A few areas need attention.

Log a meal to refocus.
```

---

## 4. Direct Interaction

Home provides immediate action.

Examples:

- Confirm
- Adjust
- Later
- Done
- Ask Wellbine
- Quick Actions
- Pillar Orb Quick Panel
- Sync Control from Push Adjust

The user should not need to interpret complex data or navigate through tabs before acting.

---

# Home Copy Logic

Home copy should be short, calm and useful.

Examples:

```text
Your day is still recoverable.

Complete the next 3 actions to stabilize your Sync.
```

```text
Current Context

Recovery Window

Next Best Action

Lower intensity today.
```

```text
Current Context

Morning Reset

Next Best Action

Hydrate and get 10 minutes of sunlight.
```

Avoid:

- Generic motivational copy
- Excessive metrics
- Negative language
- Punitive language
- Competing instructions

---

# Home Is Not A Dashboard

Home should not be a traditional dashboard.

Avoid:

- Too many cards
- Too many metrics
- Complex charts
- Competing priorities
- Medical-style data display
- Fitness dashboard clutter
- Social feed behavior
- Full pillar checklist

Home should feel like an intelligent operating surface.

The user enters, sees what matters, acts and leaves.

---

# Wearable-Aware Home

Home should work with or without wearables.

---

## With Wearable

When a wearable is connected, Home may reflect automatically detected context.

Examples:

- Poor sleep
- Low recovery
- Elevated stress
- Inactivity
- Completed movement
- Sleep preparation readiness
- Recovery need

Home should use these signals to adjust Current Context, Adaptive Summary and Next Best Action.

Example:

```text
Current Context

Low Recovery

Next Best Action

Choose a lighter movement plan.
```

---

## Without Wearable

When no wearable is connected, Home should rely more on:

- Push responses
- Manual input
- Interaction history
- Protocol settings
- Daily behavior

The user should not feel punished for not having a wearable.

Wearables improve automation.

They should not be required for value.

---

# Protocol Awareness

Home must respect the user's current protocol.

Examples:

- Fasting
- OMAD
- Low carb
- Keto
- Vegetarian
- Normal day
- Recovery day
- Day off
- GLP-1 Support
- Performance
- Recovery

Example:

If the user is fasting, Home should not suggest breakfast during the fasting window.

Instead, it may show:

```text
Current Context

Fasting Window

Next Best Action

Hydrate and continue your fasting plan.
```

---

# Plan Awareness

Home should display the active plan when relevant.

Example:

```text
Active Plan

GLP-1 Support Plan

Next Best Action

Hydration + protein meal planning.
```

Another example:

```text
Active Plan

Elite Performance Plan

Next Best Action

Strong movement window starts today.
```

Plan awareness should not dominate Home.

The plan should guide the current state quietly.

---

# Pillar Examples On Home

## Hydration

```text
Current Context

Hydration Opportunity

Next Best Action

Drink water now.
```

---

## Sleep

```text
Current Context

Sleep Preparation Window

Next Best Action

Confirm your sleep plan.
```

---

## Meal / Nutrition

```text
Current Context

Feeding Window

Next Best Action

Have your planned lunch.
```

---

## Movement

```text
Current Context

Movement Window

Next Best Action

Start strong movement.
```

If recovery is low:

```text
Current Context

Recovery Window

Next Best Action

Choose light movement.
```

---

## Mind

```text
Current Context

Stress Reset

Next Best Action

Start 3 min breathing.
```

---

## Sun

```text
Current Context

Morning Reset

Next Best Action

Get 10 min natural light.
```

---

## Daily Stack

```text
Current Context

Daily Stack Window

Next Best Action

Confirm your morning stack.
```

---

# Updated Primary Flow

The ideal direct app flow:

```text
User opens Wellbine directly.

↓

Home shows the Orb-based system state.

↓

Central Main Orb summarizes Body, Mind, Recovery, Today Sync or 7-Day Sync.

↓

Static Pillar Orbs show pillar status.

↓

User may tap a mini Pillar Orb to open the Pillar Orb Quick Panel.

↓

Home identifies the current context.

↓

Home shows the Current Insight or Next Best Action.

↓

User confirms, adjusts, opens a pillar, uses Quick Actions or asks Wellbine.

↓

Home updates.

↓

User leaves.
```

The ideal Push Adjust flow:

```text
User receives Push.

↓

User taps Adjust.

↓

Wellbine opens the relevant Sync Control panel.

↓

User enables, disables or adjusts plan items.

↓

User confirms adjusted plan.

↓

Daily, Push, Pillars, Sync and AAI are updated.

↓

User leaves.
```

The ideal first access flow:

```text
User opens Wellbine for the first time.

↓

Home enters First Activation Mode.

↓

User chooses a starting plan.

↓

Wellbine activates Daily, Push and Pillars.

↓

Home shows the initial system state.

↓

User receives the first Next Best Action.
```

Home should reduce the need for fixed navigation.

The user should be able to operate the app from Home.

---

# Current UI Changes

The current Home screen should be updated as follows.

---

## Keep

- Dark premium interface
- Central Orb
- Infinity brand identity
- Ask Wellbine input
- Minimal design language
- Orb-based visual system

---

## Change

- Remove fixed Bottom Navigation
- Make Home the central operating surface of the app
- Absorb Hub functions into Home through static Pillar Orbs and Quick Panels
- Move Store out of fixed app navigation
- Integrate Stats into Home through Adaptive Summary, Sync and pillar percentages
- Move Profile access to one clear contextual entry point
- Make smaller Orbs static
- Use fixed and predictable pillar Orb positioning
- Remove uncontrolled floating / orbiting behavior
- Make the Central Main Orb open an Adaptive Summary Screen
- Use the Main Orb to summarize Body, Mind, Recovery, Today Sync and 7-Day Sync
- Show pillar percentage and state through smaller Orbs
- Make mini Pillar Orbs open the Pillar Orb Quick Panel
- Allow fast actions directly from the Pillar Orb Quick Panel
- Make Current Insight more visible
- Make Next Best Action more central
- Show only relevant pillar states
- Support First Activation Mode when no plan is active
- Deep-link Push Adjust actions into the relevant Sync Control screen
- Allow users to enable, disable or adjust Push sequence items from Sync Control
- Sync Home with Daily and Push
- Support wearable-aware context
- Support protocol-aware guidance
- Support active plan awareness
- Support Confirm / Adjust / Later logic

---

## Remove or Avoid

- Fixed Bottom Navigation
- Separate Hub tab that repeats Home
- Fixed in-app Store tab
- Separate Stats tab for information already shown on Home
- Duplicate Profile access points
- Persistent navigation competing with the Home operating surface
- Floating smaller Orbs around the Central Orb
- Constant Orb animation
- Excessive metrics
- Dashboard clutter
- Generic motivational messages
- Negative status language
- Too many competing actions
- Full pillar checklist on Home
- Opening generic Home after Push Adjust
- Random insight selection
- Forcing full pillar navigation for simple actions

---

# What Wellbine Home Is Not

Wellbine Home is not a dashboard.

Wellbine Home is not a social feed.

Wellbine Home is not a medical report.

Wellbine Home is not a data wall.

Wellbine Home is not a habit checklist.

Wellbine Home is not a full pillar control panel.

Wellbine Home is not the onboarding engine.

Wellbine Home is not one tab among many.

Wellbine Home is the calm intelligence layer of the Wellbine app.

---

# Current Status

Wellbine Home is being redesigned to align with AAI, BCAS, Daily, Push, Operational Pillars and future Plan Templates.

The next implementation priorities are:

- Remove fixed Bottom Navigation
- Home as central operating surface
- Static pillar Orbs
- Central Main Orb as Adaptive Summary gateway
- Adaptive Summary Screen
- Pillar Orb Quick Panel
- Current Insight area
- Next Best Action area
- Push Adjust deep-linking
- Sync Control entry from Push
- First Activation Mode
- Active plan awareness
- Daily synchronization
- Pillar state synchronization
- Wearable-aware context
- Protocol-aware guidance
- Reduced cognitive load

---

# Future Evolution

Future versions of Home may include:

- More precise wearable context
- Predictive context display
- Personalized Orb state behavior
- Adaptive Home copy
- Dynamic Daily summary
- Deeper Ask Wellbine integration
- Context-aware Quick Actions
- Personalized Home layouts
- AI-generated daily summary with safety rules
- Plan Template activation from Home
- Adaptive Sync Control screens
- Admin-managed Home content modules
- More advanced Pillar Orb Quick Panel actions
- Optional secondary Hub-like inspection view

---

# Related Documents

- FOUNDATION/AAI_CONSTITUTION.md
- FOUNDATION/AAI_GLOSSARY.md
- FOUNDATION/AAI_PRINCIPLES.md
- FRAMEWORKS/POPAE.md
- PRODUCTS/WELLBINE/README.md
- PRODUCTS/WELLBINE/PRODUCT.md
- PRODUCTS/WELLBINE/BCAS.md
- PRODUCTS/WELLBINE/DAILY.md
- PRODUCTS/WELLBINE/PUSH.md
- PRODUCTS/WELLBINE/PILLARS.md
- PRODUCTS/WELLBINE/STACK.md
