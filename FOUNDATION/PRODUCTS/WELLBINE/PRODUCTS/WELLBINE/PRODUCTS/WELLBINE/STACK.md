# Wellbine Stack

**Version:** 0.1.0

**Status:** Active

**Last Updated:** July 2026

---

# Purpose

This document defines the Wellbine Stack module.

The Wellbine Stack is the system responsible for organizing, tracking and supporting the user's daily intake of medications, vitamins, supplements, nutraceuticals and related health routines.

It replaces the older concept of a simple Wakeup routine.

The Stack is not just a reminder list.

It is an operational layer connected to AAI, BCAS, Wellbine Daily and Push.

---

# Official Definition

**Wellbine Stack is the daily intake management system of Wellbine, designed to organize medications, vitamins, supplements and related routines through context-aware guidance, Push confirmation and internal tracking.**

---

# Core Objective

The objective of Wellbine Stack is to help the user follow their daily intake routine with minimal friction.

The system should answer:

**What should the user take now, in this context, and how can this be confirmed with the least effort?**

The Stack should reduce forgetfulness, improve consistency and integrate intake behavior into the broader Wellbine Daily flow.

---

# What The Stack Includes

Wellbine Stack may include:

- Medications
- Vitamins
- Supplements
- Nutraceuticals
- Functional compounds
- Electrolytes
- Hydration-related items
- Protocol-based items
- User-defined health items

Examples:

- Vitamin B
- Omega 3
- Magnesium
- Creatine
- Melatonin
- CoQ10
- NAD+
- Medication prescribed by a doctor
- Electrolytes during fasting
- Protein supplement
- Custom user item

---

# Relationship With AAI

AAI uses Stack data to:

- Understand adherence patterns
- Identify missed or delayed intake
- Anticipate routine friction
- Adapt Daily guidance
- Adjust Push timing
- Improve future recommendations
- Connect intake behavior with energy, sleep, recovery and performance patterns

AAI should not simply remind the user.

AAI should learn from how the user follows or struggles with the Stack.

---

# Relationship With BCAS

The Stack should follow biological context, not only fixed clock time.

Some items may be time-based.

Others may be context-based.

Examples:

- Morning vitamins after waking
- Omega 3 with breakfast
- Magnesium in the evening
- Electrolytes during fasting
- Melatonin during Sleep Preparation Window
- Protein after Movement Window
- Hydration after Wake Window

The system should ask:

**What is the right context for this item?**

not only:

**What time is it?**

---

# Relationship With Daily

Wellbine Stack is part of Wellbine Daily.

Stack items may appear as:

- Next Best Action
- Daily Flow item
- Morning plan
- Midday plan
- Evening plan
- Night reset plan
- Push confirmation
- Protocol-specific recommendation

When a Stack item is confirmed, Wellbine Daily should update automatically.

---

# Relationship With Push

Push is one of the main ways the user interacts with Stack.

Stack should not require the user to open the app every time.

Example:

```text
Your morning stack:

Vitamin B
Omega 3
Hydration

Ok?

Confirm
Adjust
Later
```

Button logic:

- Confirm updates Stack and related pillars without opening the app.
- Adjust opens the relevant Stack adjustment screen.
- Later schedules a follow-up Push approximately one hour later.

---

# Stack Item Structure

Each Stack item should support the following fields:

- Name
- Category
- Dosage
- Unit
- Frequency
- Context Window
- Preferred timing
- With food / without food
- Active / inactive
- Photo
- Notes
- Stock quantity
- Refill threshold
- Reminder rules
- Protocol rules
- Safety notes

---

# Stack Categories

Recommended categories:

- Medication
- Vitamin
- Supplement
- Nutraceutical
- Hydration
- Electrolyte
- Protein
- Sleep support
- Recovery support
- Custom

---

# Context Windows

Stack items should be assigned to one or more context windows.

Examples:

## Wake Window

Items commonly taken after waking.

Examples:

- Hydration
- Vitamin B
- Morning supplements
- Medication

---

## Feeding Window

Items taken with food.

Examples:

- Omega 3
- Fat-soluble vitamins
- Digestive support
- Meal-related supplements

---

## Movement Window

Items related to movement, training or recovery.

Examples:

- Creatine
- Protein
- Electrolytes
- Recovery supplements

---

## Recovery Window

Items related to recovery, fatigue or stress.

Examples:

- Magnesium
- Electrolytes
- Adaptogens
- Recovery support

---

## Sleep Preparation Window

Items related to sleep preparation.

Examples:

- Magnesium
- Melatonin
- Night supplements
- Sleep support protocol

---

# Protocol Awareness

Stack must respect the user's current protocol.

Examples:

- Fasting
- OMAD
- Low carb
- Keto
- Vegetarian
- Normal day
- Recovery day
- Day off

Example rule:

If the user is fasting, the system should not suggest items that require food unless the user confirms an exception.

If the user is in a Sleep Preparation Window, the system should prioritize night-related Stack items.

If the user is on a Recovery Day, the system may reduce performance-related suggestions and prioritize recovery support.

---

# Stack Confirmation Logic

Stack confirmation should be simple.

The user should be able to confirm:

- One item
- A group of items
- A full Stack sequence

Example:

```text
Morning Stack complete?

Complete
Partial
Later
```

If the user chooses **Complete**, all related Stack items may be marked as done.

If the user chooses **Partial**, the app should open the relevant Stack screen to select what was taken.

If the user chooses **Later**, the system should follow up by Push.

---

# Push Button Logic

Default Stack Push buttons:

- Confirm
- Adjust
- Later

---

## Confirm

Confirm means the user accepts or completes the proposed Stack sequence.

The app should not open.

Internal updates may include:

- Stack items marked as taken
- Daily Stack pillar updated
- Daily Flow updated
- Sync updated
- Stock reduced
- AAI learning updated

---

## Adjust

Adjust means the user needs to edit the Stack sequence.

The app should open directly on the relevant Stack screen.

The user may need to:

- Remove an item
- Mark only some items as taken
- Change dosage
- Change timing
- Skip one item
- Add a note
- Update stock
- Change protocol

---

## Later

Later means the user is not ready now.

The app should not open.

The system should:

- Register the delay
- Keep the Stack sequence pending
- Send a follow-up Push approximately one hour later
- Avoid punitive language
- Adjust if the biological context changes

---

# Stock Control

Wellbine Stack should support simple stock control.

For each item, the user may define:

- Current quantity
- Unit type
- Quantity used per intake
- Refill alert threshold
- Purchase reminder
- Photo of product
- Notes

When the user confirms an item, the system may reduce stock automatically.

Example:

If the user confirms Omega 3 and dosage is 2 capsules, the stock decreases by 2.

When stock reaches the refill threshold, the system may notify the user.

Example:

```text
Omega 3 is running low.

Add to refill list?

Add
Later
Ignore
```

---

# Photos

Each Stack item should allow a photo.

Photos help the user recognize the correct product quickly.

Possible photo types:

- Front label
- Dosage label
- Product bottle
- Box
- Custom image

Photos are especially useful when the user has multiple similar supplements or medications.

---

# Safety Rules

Wellbine Stack is not a medical prescription system.

The system should not prescribe medication.

The system should not replace medical advice.

The system may help the user track what they already take.

For medications, the system should use careful language.

Avoid:

- You should take this medication.
- Increase your dosage.
- Stop this medication.

Preferred language:

- Scheduled medication
- Your registered medication
- Confirm if taken
- Follow your medical prescription
- Consult your doctor before changes

---

# Daily Stack Pillar

Daily Stack is one of the Wellbine pillars.

It should contribute to the user's daily consistency and Sync.

However, Stack scoring should avoid harsh punishment.

Preferred states:

- Done
- Partial
- Pending
- Window Closed
- Skipped
- Adjusted

Avoid:

- Failed
- Penalty
- Missed
- Bad adherence

---

# Stack And Recovery

If the user skips or delays Stack items, the system should support recovery.

Example:

```text
Your morning stack is still pending.

Take it now?

Confirm
Adjust
Later
```

If the context has changed, the system may adjust.

Example:

If a morning item requires food but the user is now fasting, the system should not blindly suggest it.

It should ask the user to adjust or defer.

---

# Stack And Wearables

Wearables do not directly confirm most Stack items.

However, wearable data may influence Stack guidance.

Examples:

- Poor sleep may trigger a recovery-focused Stack.
- High stress may trigger breathing or recovery support.
- Heavy training may trigger recovery Stack.
- Low recovery may reduce performance Stack intensity.

With wearables, fewer manual check-ins may be needed.

Without wearables, Push may collect more high-signal feedback to guide Stack timing.

---

# User Interaction Rules

The user should be able to:

- Add Stack items
- Edit Stack items
- Upload photos
- Define dosage
- Define frequency
- Define timing or context window
- Confirm individual items
- Confirm grouped Stack sequences
- Skip items
- Delay items
- Adjust current protocol
- Track stock
- Receive refill alerts
- Review Stack history

---

# Current UI / Product Changes

## Keep

- Daily Stack as a core pillar
- Alarms and reminders
- Quantity control
- Product photos
- Medication / vitamin / supplement tracking
- Historical records

---

## Change

- Stack should become context-aware
- Stack should integrate with Push
- Stack should integrate with Wellbine Daily
- Stack should support grouped confirmation
- Stack should support stock reduction
- Stack should respect protocol mode
- Stack should reduce app opening through Confirm / Adjust / Later logic

---

## Remove or Avoid

- Treating Stack as only a morning checklist
- Generic reminders without context
- Excessive notifications
- Medical prescription language
- Punitive adherence language
- Forcing the app open for simple confirmations

---

# What Wellbine Stack Is Not

Wellbine Stack is not a prescription system.

Wellbine Stack is not a medical diagnosis tool.

Wellbine Stack is not only a reminder list.

Wellbine Stack is not limited to the morning.

Wellbine Stack is not disconnected from Daily.

Wellbine Stack is the intake management layer of Wellbine.

---

# Current Status

Wellbine Stack is being redesigned from a simple reminder feature into a context-aware intake management system.

The next implementation priorities are:

- Stack item structure
- Context Window assignment
- Push confirmation
- Stock control
- Photos
- Protocol awareness
- Daily integration
- Confirm / Adjust / Later logic

---

# Future Evolution

Future versions of Wellbine Stack may include:

- Barcode scanning
- AI product recognition
- Refill marketplace
- Drug / supplement interaction warnings
- Wearable-informed Stack suggestions
- Smart timing optimization
- Personalized intake plans
- Automatic reorder reminders
- Pharmacy or supplement store integration

---

# Related Documents

- FOUNDATION/AAI_CONSTITUTION.md
- FOUNDATION/AAI_GLOSSARY.md
- FOUNDATION/AAI_PRINCIPLES.md
- FRAMEWORKS/POPAE.md
- PRODUCTS/WELLBINE/PRODUCT.md
- PRODUCTS/WELLBINE/BCAS.md
- PRODUCTS/WELLBINE/DAILY.md
- PRODUCTS/WELLBINE/PUSH.md
