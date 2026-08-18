# Wellbine Supabase SQL MVP

**Version:** 0.1.0

**Status:** Draft

**Last Updated:** July 2026

---

# Purpose

This document defines the first practical SQL blueprint for the Wellbine MVP Supabase database.

The goal is to move from conceptual schema into an initial executable database structure.

This document covers:

- Required MVP tables
- Suggested SQL structure
- User-owned data
- Admin-managed data
- Plan Templates
- Plan Versions
- Active Plans
- Pillars
- Daily Plans
- Daily Actions
- Home State
- Feature Flags
- Basic Admin Roles
- Row Level Security direction
- Seed data
- Implementation order

This is not the final production migration.

This is the MVP SQL starting point.

---

# Official Definition

**Wellbine Supabase SQL MVP is the initial practical SQL blueprint used to create the minimum database foundation required for the first working version of Wellbine.**

---

# Core Principle

The core SQL MVP rule is:

```text
Create only what is necessary to prove the operating loop.
```

The operating loop is:

```text
Signup
↓
Profile
↓
Onboarding
↓
Plan Activation
↓
Home
↓
Daily
↓
Action
↓
State Update
```

The MVP database should support this loop before expanding into advanced analytics, commerce, wearables, uploads or complex AI automation.

---

# Important Notes

This SQL should be reviewed before production.

Before running in production, confirm:

- Table names
- Field names
- RLS policies
- Admin role strategy
- App environment
- FlutterFlow compatibility
- Edge Function requirements
- Legal and privacy requirements
- Account deletion behavior

This file is intentionally practical, but still a blueprint.

---

# MVP Table Scope

The MVP SQL should create these core tables first:

```text
user_profiles
user_settings
user_roles

plan_templates
plan_template_versions
user_active_plans

pillar_definitions
user_pillar_states

daily_plans
daily_actions

user_home_state

feature_flags
content_modules

admin_audit_log
```

Strong next layer:

```text
push_events
stack_items
```

Optional later:

```text
wearable_connections
wearable_metric_snapshots
user_uploads
commerce_benefits
user_commerce_benefits
commerce_events
user_aai_context
recommendations
```

---

# SQL Setup

```sql
-- ============================================================
-- Wellbine Supabase SQL MVP
-- Version: 0.1.0
-- Status: Draft
-- ============================================================

-- Enable UUID generation if needed.
create extension if not exists "pgcrypto";
```

---

# Updated At Trigger Function

```sql
-- ============================================================
-- updated_at helper
-- ============================================================

create or replace function public.set_updated_at()
returns trigger
language plpgsql
as $$
begin
  new.updated_at = now();
  return new;
end;
$$;
```

---

# User Roles

Purpose:

```text
Stores internal role assignments for admin access.
```

```sql
-- ============================================================
-- user_roles
-- ============================================================

create table if not exists public.user_roles (
  id uuid primary key default gen_random_uuid(),
  user_id uuid not null references auth.users(id) on delete cascade,
  role text not null default 'viewer',
  status text not null default 'active',
  metadata_json jsonb not null default '{}'::jsonb,
  created_at timestamptz not null default now(),
  updated_at timestamptz not null default now(),

  constraint user_roles_unique_user_role unique (user_id, role)
);

create trigger set_user_roles_updated_at
before update on public.user_roles
for each row
execute function public.set_updated_at();
```

Suggested roles:

```text
owner
admin
editor
support
viewer
```

---

# Admin Helper Function

Purpose:

```text
Checks whether authenticated user has an active admin role.
```

```sql
-- ============================================================
-- admin helper
-- ============================================================

create or replace function public.is_admin()
returns boolean
language sql
security definer
set search_path = public
as $$
  select exists (
    select 1
    from public.user_roles
    where user_id = auth.uid()
      and status = 'active'
      and role in ('owner', 'admin')
  );
$$;
```

Important:

```text
This is a basic helper.
Review carefully before production.
```

---

# User Profiles

Purpose:

```text
Stores the user profile baseline required for Wellbine activation.
```

```sql
-- ============================================================
-- user_profiles
-- ============================================================

create table if not exists public.user_profiles (
  id uuid primary key default gen_random_uuid(),
  user_id uuid not null unique references auth.users(id) on delete cascade,

  name text,
  biological_sex text,
  age integer,
  height_cm numeric,
  weight_kg numeric,
  country text,
  language text default 'en',
  timezone text,

  relevant_comorbidities_json jsonb not null default '[]'::jsonb,

  onboarding_completed boolean not null default false,
  onboarding_completed_at timestamptz,

  status text not null default 'active',
  metadata_json jsonb not null default '{}'::jsonb,

  created_at timestamptz not null default now(),
  updated_at timestamptz not null default now()
);

create trigger set_user_profiles_updated_at
before update on public.user_profiles
for each row
execute function public.set_updated_at();
```

---

# User Settings

Purpose:

```text
Stores user preferences, Push controls, Mental Detox and app-level settings.
```

```sql
-- ============================================================
-- user_settings
-- ============================================================

create table if not exists public.user_settings (
  id uuid primary key default gen_random_uuid(),
  user_id uuid not null unique references auth.users(id) on delete cascade,

  push_enabled boolean not null default false,
  mental_detox_enabled boolean not null default true,

  preferred_units text default 'metric',
  preferred_language text default 'en',
  preferred_timezone text,
  wake_time_preference time,
  sleep_time_preference time,
  rhythm_anchor_source text default 'assumed',
  notification_preferences_json jsonb not null default '{}'::jsonb,
  privacy_preferences_json jsonb not null default '{}'::jsonb,
  accessibility_preferences_json jsonb not null default '{}'::jsonb,
  commerce_preferences_json jsonb not null default '{}'::jsonb,

  metadata_json jsonb not null default '{}'::jsonb,

  created_at timestamptz not null default now(),
  updated_at timestamptz not null default now()
);

create trigger set_user_settings_updated_at
before update on public.user_settings
for each row
execute function public.set_updated_at();
```

---

# Plan Templates

Purpose:

```text
Stores admin-managed starting plan models.
```

```sql
-- ============================================================
-- plan_templates
-- ============================================================

create table if not exists public.plan_templates (
  id uuid primary key default gen_random_uuid(),

  name text not null,
  slug text not null unique,
  description text,
  status text not null default 'draft',
  category text,
  audience text,

  is_featured boolean not null default false,
  sort_order integer not null default 0,

  current_version_id uuid,

  metadata_json jsonb not null default '{}'::jsonb,

  created_by uuid references auth.users(id),
  updated_by uuid references auth.users(id),

  created_at timestamptz not null default now(),
  updated_at timestamptz not null default now()
);

create trigger set_plan_templates_updated_at
before update on public.plan_templates
for each row
execute function public.set_updated_at();
```

---

# Plan Template Versions

Purpose:

```text
Stores versioned configuration for Plan Templates.
```

```sql
-- ============================================================
-- plan_template_versions
-- ============================================================

create table if not exists public.plan_template_versions (
  id uuid primary key default gen_random_uuid(),

  plan_template_id uuid not null references public.plan_templates(id) on delete cascade,

  version_number integer not null default 1,
  status text not null default 'draft',

  configuration_json jsonb not null default '{}'::jsonb,
  pillar_defaults_json jsonb not null default '{}'::jsonb,
  daily_rules_json jsonb not null default '{}'::jsonb,
  push_rules_json jsonb not null default '{}'::jsonb,
  home_rules_json jsonb not null default '{}'::jsonb,
  wearable_rules_json jsonb not null default '{}'::jsonb,
  commerce_rules_json jsonb not null default '{}'::jsonb,
  content_rules_json jsonb not null default '{}'::jsonb,

  created_by uuid references auth.users(id),
  published_at timestamptz,

  created_at timestamptz not null default now(),
  updated_at timestamptz not null default now(),

  constraint plan_template_versions_unique_version unique (plan_template_id, version_number)
);

create trigger set_plan_template_versions_updated_at
before update on public.plan_template_versions
for each row
execute function public.set_updated_at();

alter table public.plan_templates
add constraint plan_templates_current_version_fk
foreign key (current_version_id)
references public.plan_template_versions(id);
```

Important:

```text
Users should activate a specific published version.
Existing user snapshots should not break when a template changes.
```

---

# User Active Plans

Purpose:

```text
Stores the user's active plan snapshot.
```

```sql
-- ============================================================
-- user_active_plans
-- ============================================================

create table if not exists public.user_active_plans (
  id uuid primary key default gen_random_uuid(),

  user_id uuid not null references auth.users(id) on delete cascade,
  plan_template_id uuid not null references public.plan_templates(id),
  plan_template_version_id uuid not null references public.plan_template_versions(id),

  status text not null default 'active',

  started_at timestamptz not null default now(),
  ended_at timestamptz,

  active_configuration_json jsonb not null default '{}'::jsonb,
  activation_source text default 'onboarding',

  metadata_json jsonb not null default '{}'::jsonb,

  created_at timestamptz not null default now(),
  updated_at timestamptz not null default now()
);

create trigger set_user_active_plans_updated_at
before update on public.user_active_plans
for each row
execute function public.set_updated_at();

create index if not exists idx_user_active_plans_user_id
on public.user_active_plans(user_id);

create index if not exists idx_user_active_plans_user_status
on public.user_active_plans(user_id, status);
```

Recommended MVP rule:

```text
Only one active primary plan per user.
```

This can be enforced in Edge Function logic first.

---

# Pillar Definitions

Purpose:

```text
Stores Wellbine operational pillars.
```

```sql
-- ============================================================
-- pillar_definitions
-- ============================================================

create table if not exists public.pillar_definitions (
  id uuid primary key default gen_random_uuid(),

  name text not null,
  slug text not null unique,
  description text,
  status text not null default 'active',
  sort_order integer not null default 0,

  default_configuration_json jsonb not null default '{}'::jsonb,
  metadata_json jsonb not null default '{}'::jsonb,

  created_at timestamptz not null default now(),
  updated_at timestamptz not null default now()
);

create trigger set_pillar_definitions_updated_at
before update on public.pillar_definitions
for each row
execute function public.set_updated_at();
```

---

# User Pillar States

Purpose:

```text
Stores the current user-specific state for each pillar.
```

```sql
-- ============================================================
-- user_pillar_states
-- ============================================================

create table if not exists public.user_pillar_states (
  id uuid primary key default gen_random_uuid(),

  user_id uuid not null references auth.users(id) on delete cascade,
  pillar_id uuid not null references public.pillar_definitions(id),
  active_plan_id uuid references public.user_active_plans(id) on delete set null,

  status text not null default 'active',
  score numeric,

  state_json jsonb not null default '{}'::jsonb,

  last_action_at timestamptz,
  last_evaluated_at timestamptz,

  created_at timestamptz not null default now(),
  updated_at timestamptz not null default now(),

  constraint user_pillar_states_unique_user_pillar_plan unique (user_id, pillar_id, active_plan_id)
);

create trigger set_user_pillar_states_updated_at
before update on public.user_pillar_states
for each row
execute function public.set_updated_at();

create index if not exists idx_user_pillar_states_user_id
on public.user_pillar_states(user_id);

create index if not exists idx_user_pillar_states_active_plan
on public.user_pillar_states(active_plan_id);
```

---

# Daily Plans

Purpose:

```text
Stores the user's daily execution plan.
```

```sql
-- ============================================================
-- daily_plans
-- ============================================================

create table if not exists public.daily_plans (
  id uuid primary key default gen_random_uuid(),

  user_id uuid not null references auth.users(id) on delete cascade,
  active_plan_id uuid references public.user_active_plans(id) on delete set null,

  plan_date date not null,
  status text not null default 'planned',

  daily_summary text,
  daily_context_json jsonb not null default '{}'::jsonb,
  schedule_json jsonb not null default '{}'::jsonb,

  created_by text default 'system',
  generated_at timestamptz default now(),

  created_at timestamptz not null default now(),
  updated_at timestamptz not null default now(),

  constraint daily_plans_unique_user_date unique (user_id, plan_date)
);

create trigger set_daily_plans_updated_at
before update on public.daily_plans
for each row
execute function public.set_updated_at();

create index if not exists idx_daily_plans_user_date
on public.daily_plans(user_id, plan_date);

create index if not exists idx_daily_plans_active_plan
on public.daily_plans(active_plan_id);
```

---

# Daily Actions

Purpose:

```text
Stores individual actions inside a Daily plan.
```

```sql
-- ============================================================
-- daily_actions
-- ============================================================

create table if not exists public.daily_actions (
  id uuid primary key default gen_random_uuid(),

  user_id uuid not null references auth.users(id) on delete cascade,
  daily_plan_id uuid not null references public.daily_plans(id) on delete cascade,
  pillar_id uuid references public.pillar_definitions(id) on delete set null,

  action_type text,
  title text not null,
  description text,

  status text not null default 'upcoming',

  scheduled_window_start timestamptz,
  scheduled_window_end timestamptz,

  completed_at timestamptz,
  skipped_at timestamptz,
  delayed_until timestamptz,

  source text default 'plan_template',

  metadata_json jsonb not null default '{}'::jsonb,

  created_at timestamptz not null default now(),
  updated_at timestamptz not null default now()
);

create trigger set_daily_actions_updated_at
before update on public.daily_actions
for each row
execute function public.set_updated_at();

create index if not exists idx_daily_actions_user_id
on public.daily_actions(user_id);

create index if not exists idx_daily_actions_daily_plan
on public.daily_actions(daily_plan_id);

create index if not exists idx_daily_actions_user_status
on public.daily_actions(user_id, status);
```

Recommended statuses:

```text
upcoming
active
completed
adjusted
delayed
skipped
expired
```

---

# User Home State

Purpose:

```text
Stores the user's current Home operating state.
```

```sql
-- ============================================================
-- user_home_state
-- ============================================================

create table if not exists public.user_home_state (
  id uuid primary key default gen_random_uuid(),

  user_id uuid not null unique references auth.users(id) on delete cascade,
  active_plan_id uuid references public.user_active_plans(id) on delete set null,

  current_insight text,
  next_best_action text,

  adaptive_summary_json jsonb not null default '{}'::jsonb,
  pillar_orbs_json jsonb not null default '[]'::jsonb,

  home_status text not null default 'active',
  last_updated_at timestamptz default now(),

  metadata_json jsonb not null default '{}'::jsonb,

  created_at timestamptz not null default now(),
  updated_at timestamptz not null default now()
);

create trigger set_user_home_state_updated_at
before update on public.user_home_state
for each row
execute function public.set_updated_at();
```

Important:

```text
Home should not calculate everything inside FlutterFlow.
Supabase should store the current operating state.
```

---

# Feature Flags

Purpose:

```text
Controls feature visibility and rollout.
```

```sql
-- ============================================================
-- feature_flags
-- ============================================================

create table if not exists public.feature_flags (
  id uuid primary key default gen_random_uuid(),

  flag_key text not null,
  description text,
  status text not null default 'active',

  scope text not null default 'global',
  scope_id text,

  enabled boolean not null default false,

  rules_json jsonb not null default '{}'::jsonb,
  metadata_json jsonb not null default '{}'::jsonb,

  created_by uuid references auth.users(id),
  updated_by uuid references auth.users(id),

  created_at timestamptz not null default now(),
  updated_at timestamptz not null default now(),

  constraint feature_flags_unique_scope_key unique (flag_key, scope, scope_id)
);

create trigger set_feature_flags_updated_at
before update on public.feature_flags
for each row
execute function public.set_updated_at();

create index if not exists idx_feature_flags_key
on public.feature_flags(flag_key);

create index if not exists idx_feature_flags_scope
on public.feature_flags(scope, scope_id);
```

---

# Content Modules

Purpose:

```text
Stores admin-managed content used by onboarding, Home, Daily, Pillars and other flows.
```

```sql
-- ============================================================
-- content_modules
-- ============================================================

create table if not exists public.content_modules (
  id uuid primary key default gen_random_uuid(),

  title text not null,
  slug text not null unique,
  content_type text not null,
  status text not null default 'draft',
  language text not null default 'en',

  body_markdown text,
  content_json jsonb not null default '{}'::jsonb,
  tags_json jsonb not null default '[]'::jsonb,

  created_by uuid references auth.users(id),
  updated_by uuid references auth.users(id),
  published_at timestamptz,

  created_at timestamptz not null default now(),
  updated_at timestamptz not null default now()
);

create trigger set_content_modules_updated_at
before update on public.content_modules
for each row
execute function public.set_updated_at();

create index if not exists idx_content_modules_status_type
on public.content_modules(status, content_type);
```

---

# Admin Audit Log

Purpose:

```text
Records important admin actions.
```

```sql
-- ============================================================
-- admin_audit_log
-- ============================================================

create table if not exists public.admin_audit_log (
  id uuid primary key default gen_random_uuid(),

  admin_user_id uuid references auth.users(id),

  action text not null,
  entity_type text,
  entity_id uuid,

  before_json jsonb not null default '{}'::jsonb,
  after_json jsonb not null default '{}'::jsonb,
  metadata_json jsonb not null default '{}'::jsonb,

  created_at timestamptz not null default now()
);

create index if not exists idx_admin_audit_log_admin_user
on public.admin_audit_log(admin_user_id);

create index if not exists idx_admin_audit_log_entity
on public.admin_audit_log(entity_type, entity_id);
```

---

# Optional MVP Table — Push Events

Purpose:

```text
Stores Push orchestration events and responses.
```

```sql
-- ============================================================
-- push_events
-- Optional MVP
-- ============================================================

create table if not exists public.push_events (
  id uuid primary key default gen_random_uuid(),

  user_id uuid not null references auth.users(id) on delete cascade,
  daily_plan_id uuid references public.daily_plans(id) on delete set null,
  daily_action_id uuid references public.daily_actions(id) on delete set null,

  push_type text,
  title text,
  body text,

  status text not null default 'scheduled',
  response text,

  scheduled_for timestamptz,
  sent_at timestamptz,
  responded_at timestamptz,

  deep_link text,
  payload_json jsonb not null default '{}'::jsonb,

  created_at timestamptz not null default now(),
  updated_at timestamptz not null default now()
);

create trigger set_push_events_updated_at
before update on public.push_events
for each row
execute function public.set_updated_at();

create index if not exists idx_push_events_user_id
on public.push_events(user_id);

create index if not exists idx_push_events_user_status
on public.push_events(user_id, status);
```

---

# Optional MVP Table — Stack Items

Purpose:

```text
Stores Daily Stack routine items.
```

```sql
-- ============================================================
-- stack_items
-- Optional MVP
-- ============================================================

create table if not exists public.stack_items (
  id uuid primary key default gen_random_uuid(),

  user_id uuid not null references auth.users(id) on delete cascade,

  name text not null,
  item_type text default 'other',
  status text not null default 'active',

  dosage_text text,
  frequency_json jsonb not null default '{}'::jsonb,
  timing_json jsonb not null default '{}'::jsonb,
  instructions text,

  refill_tracking_enabled boolean not null default false,
  refill_context_json jsonb not null default '{}'::jsonb,

  safety_notes text,
  source text default 'user',

  metadata_json jsonb not null default '{}'::jsonb,

  created_at timestamptz not null default now(),
  updated_at timestamptz not null default now()
);

create trigger set_stack_items_updated_at
before update on public.stack_items
for each row
execute function public.set_updated_at();

create index if not exists idx_stack_items_user_id
on public.stack_items(user_id);
```

---

# Enable Row Level Security

```sql
-- ============================================================
-- Enable RLS
-- ============================================================

alter table public.user_roles enable row level security;
alter table public.user_profiles enable row level security;
alter table public.user_settings enable row level security;

alter table public.plan_templates enable row level security;
alter table public.plan_template_versions enable row level security;
alter table public.user_active_plans enable row level security;

alter table public.pillar_definitions enable row level security;
alter table public.user_pillar_states enable row level security;

alter table public.daily_plans enable row level security;
alter table public.daily_actions enable row level security;

alter table public.user_home_state enable row level security;

alter table public.feature_flags enable row level security;
alter table public.content_modules enable row level security;

alter table public.admin_audit_log enable row level security;

alter table public.push_events enable row level security;
alter table public.stack_items enable row level security;
```

---

# RLS Policies — User-Owned Tables

## user_profiles

```sql
create policy "Users can read own profile"
on public.user_profiles
for select
to authenticated
using (user_id = auth.uid());

create policy "Users can insert own profile"
on public.user_profiles
for insert
to authenticated
with check (user_id = auth.uid());

create policy "Users can update own profile"
on public.user_profiles
for update
to authenticated
using (user_id = auth.uid())
with check (user_id = auth.uid());
```

---

## user_settings

```sql
create policy "Users can read own settings"
on public.user_settings
for select
to authenticated
using (user_id = auth.uid());

create policy "Users can insert own settings"
on public.user_settings
for insert
to authenticated
with check (user_id = auth.uid());

create policy "Users can update own settings"
on public.user_settings
for update
to authenticated
using (user_id = auth.uid())
with check (user_id = auth.uid());
```

---

## user_active_plans

```sql
create policy "Users can read own active plans"
on public.user_active_plans
for select
to authenticated
using (user_id = auth.uid());

create policy "Users can insert own active plans"
on public.user_active_plans
for insert
to authenticated
with check (user_id = auth.uid());

create policy "Users can update own active plans"
on public.user_active_plans
for update
to authenticated
using (user_id = auth.uid())
with check (user_id = auth.uid());
```

Important:

```text
For production, plan activation should preferably happen through Edge Function.
```

---

## user_pillar_states

```sql
create policy "Users can read own pillar states"
on public.user_pillar_states
for select
to authenticated
using (user_id = auth.uid());

create policy "Users can insert own pillar states"
on public.user_pillar_states
for insert
to authenticated
with check (user_id = auth.uid());

create policy "Users can update own pillar states"
on public.user_pillar_states
for update
to authenticated
using (user_id = auth.uid())
with check (user_id = auth.uid());
```

---

## daily_plans

```sql
create policy "Users can read own daily plans"
on public.daily_plans
for select
to authenticated
using (user_id = auth.uid());

create policy "Users can insert own daily plans"
on public.daily_plans
for insert
to authenticated
with check (user_id = auth.uid());

create policy "Users can update own daily plans"
on public.daily_plans
for update
to authenticated
using (user_id = auth.uid())
with check (user_id = auth.uid());
```

---

## daily_actions

```sql
create policy "Users can read own daily actions"
on public.daily_actions
for select
to authenticated
using (user_id = auth.uid());

create policy "Users can insert own daily actions"
on public.daily_actions
for insert
to authenticated
with check (user_id = auth.uid());

create policy "Users can update own daily actions"
on public.daily_actions
for update
to authenticated
using (user_id = auth.uid())
with check (user_id = auth.uid());
```

---

## user_home_state

```sql
create policy "Users can read own home state"
on public.user_home_state
for select
to authenticated
using (user_id = auth.uid());

create policy "Users can insert own home state"
on public.user_home_state
for insert
to authenticated
with check (user_id = auth.uid());

create policy "Users can update own home state"
on public.user_home_state
for update
to authenticated
using (user_id = auth.uid())
with check (user_id = auth.uid());
```

---

## push_events

```sql
create policy "Users can read own push events"
on public.push_events
for select
to authenticated
using (user_id = auth.uid());

create policy "Users can insert own push events"
on public.push_events
for insert
to authenticated
with check (user_id = auth.uid());

create policy "Users can update own push events"
on public.push_events
for update
to authenticated
using (user_id = auth.uid())
with check (user_id = auth.uid());
```

---

## stack_items

```sql
create policy "Users can read own stack items"
on public.stack_items
for select
to authenticated
using (user_id = auth.uid());

create policy "Users can insert own stack items"
on public.stack_items
for insert
to authenticated
with check (user_id = auth.uid());

create policy "Users can update own stack items"
on public.stack_items
for update
to authenticated
using (user_id = auth.uid())
with check (user_id = auth.uid());

create policy "Users can delete own stack items"
on public.stack_items
for delete
to authenticated
using (user_id = auth.uid());
```

---

# RLS Policies — Admin-Managed Tables

## plan_templates

```sql
create policy "Users can read published plan templates"
on public.plan_templates
for select
to authenticated
using (status = 'published' or public.is_admin());

create policy "Admins can insert plan templates"
on public.plan_templates
for insert
to authenticated
with check (public.is_admin());

create policy "Admins can update plan templates"
on public.plan_templates
for update
to authenticated
using (public.is_admin())
with check (public.is_admin());

create policy "Admins can delete plan templates"
on public.plan_templates
for delete
to authenticated
using (public.is_admin());
```

---

## plan_template_versions

```sql
create policy "Users can read published plan template versions"
on public.plan_template_versions
for select
to authenticated
using (status = 'published' or public.is_admin());

create policy "Admins can insert plan template versions"
on public.plan_template_versions
for insert
to authenticated
with check (public.is_admin());

create policy "Admins can update plan template versions"
on public.plan_template_versions
for update
to authenticated
using (public.is_admin())
with check (public.is_admin());

create policy "Admins can delete plan template versions"
on public.plan_template_versions
for delete
to authenticated
using (public.is_admin());
```

---

## pillar_definitions

```sql
create policy "Users can read active pillar definitions"
on public.pillar_definitions
for select
to authenticated
using (status = 'active' or public.is_admin());

create policy "Admins can insert pillar definitions"
on public.pillar_definitions
for insert
to authenticated
with check (public.is_admin());

create policy "Admins can update pillar definitions"
on public.pillar_definitions
for update
to authenticated
using (public.is_admin())
with check (public.is_admin());

create policy "Admins can delete pillar definitions"
on public.pillar_definitions
for delete
to authenticated
using (public.is_admin());
```

---

## feature_flags

```sql
create policy "Users can read active feature flags"
on public.feature_flags
for select
to authenticated
using (status = 'active' or public.is_admin());

create policy "Admins can insert feature flags"
on public.feature_flags
for insert
to authenticated
with check (public.is_admin());

create policy "Admins can update feature flags"
on public.feature_flags
for update
to authenticated
using (public.is_admin())
with check (public.is_admin());

create policy "Admins can delete feature flags"
on public.feature_flags
for delete
to authenticated
using (public.is_admin());
```

---

## content_modules

```sql
create policy "Users can read published content modules"
on public.content_modules
for select
to authenticated
using (status = 'published' or public.is_admin());

create policy "Admins can insert content modules"
on public.content_modules
for insert
to authenticated
with check (public.is_admin());

create policy "Admins can update content modules"
on public.content_modules
for update
to authenticated
using (public.is_admin())
with check (public.is_admin());

create policy "Admins can delete content modules"
on public.content_modules
for delete
to authenticated
using (public.is_admin());
```

---

## admin_audit_log

```sql
create policy "Admins can read audit log"
on public.admin_audit_log
for select
to authenticated
using (public.is_admin());

create policy "Admins can insert audit log"
on public.admin_audit_log
for insert
to authenticated
with check (public.is_admin());
```

---

## user_roles

```sql
create policy "Admins can read user roles"
on public.user_roles
for select
to authenticated
using (public.is_admin());

create policy "Admins can insert user roles"
on public.user_roles
for insert
to authenticated
with check (public.is_admin());

create policy "Admins can update user roles"
on public.user_roles
for update
to authenticated
using (public.is_admin())
with check (public.is_admin());

create policy "Admins can delete user roles"
on public.user_roles
for delete
to authenticated
using (public.is_admin());
```

Important:

```text
Initial owner role may need to be inserted manually through Supabase SQL editor or secure backend process.
```

---

# Seed Data — Pillar Definitions

```sql
-- ============================================================
-- Seed initial pillar definitions
-- ============================================================

insert into public.pillar_definitions
(name, slug, description, status, sort_order, default_configuration_json)
values
('Mind', 'mind', 'Supports mental state, breathing, focus and meditation.', 'active', 10, '{}'::jsonb),
('Sun', 'sun', 'Supports sunlight exposure and circadian alignment.', 'active', 20, '{}'::jsonb),
('Hydration', 'hydration', 'Supports hydration behavior and daily fluid rhythm.', 'active', 30, '{}'::jsonb),
('Sleep', 'sleep', 'Supports sleep preparation, recovery and sleep consistency.', 'active', 40, '{}'::jsonb),
('Nutrition', 'nutrition', 'Supports meal, fasting and nutrition context.', 'active', 50, '{}'::jsonb),
('Movement', 'movement', 'Supports movement, training and recovery-aware activity.', 'active', 60, '{}'::jsonb),
('Daily Stack', 'daily_stack', 'Supports supplements, vitamins, nutraceuticals, medications and routine items.', 'active', 70, '{}'::jsonb)
on conflict (slug) do update
set
  name = excluded.name,
  description = excluded.description,
  status = excluded.status,
  sort_order = excluded.sort_order,
  updated_at = now();
```

---

# Seed Data — Feature Flags

```sql
-- ============================================================
-- Seed initial feature flags
-- ============================================================

insert into public.feature_flags
(flag_key, description, scope, scope_id, enabled, status)
values
('onboarding_enabled', 'Controls onboarding visibility.', 'global', 'default', true, 'active'),
('home_enabled', 'Controls Home visibility.', 'global', 'default', true, 'active'),
('daily_enabled', 'Controls Daily visibility.', 'global', 'default', true, 'active'),
('pillars_enabled', 'Controls Pillars visibility.', 'global', 'default', true, 'active'),
('daily_stack_enabled', 'Controls Daily Stack visibility.', 'global', 'default', true, 'active'),
('push_enabled', 'Controls Push orchestration visibility.', 'global', 'default', false, 'active'),
('wearables_enabled', 'Controls Wearables visibility.', 'global', 'default', false, 'active'),
('uploads_enabled', 'Controls Uploads visibility.', 'global', 'default', false, 'active'),
('commerce_bridge_enabled', 'Controls Commerce Bridge visibility.', 'global', 'default', false, 'active'),
('ask_wellbine_enabled', 'Controls Ask Wellbine visibility.', 'global', 'default', false, 'active'),
('subscriptions_enabled', 'Controls subscription features.', 'global', 'default', false, 'active'),
('recommendations_enabled', 'Controls recommendation visibility.', 'global', 'default', false, 'active'),
('app_review_mode', 'Controls app review mode.', 'global', 'default', false, 'active'),
('beta_mode', 'Controls beta mode.', 'global', 'default', true, 'active')
on conflict (flag_key, scope, scope_id) do update
set
  enabled = excluded.enabled,
  status = excluded.status,
  description = excluded.description,
  updated_at = now();
```

---

# Seed Data — Example Plan Template

This is an example internal starter plan.

It should be edited through Admin later.

```sql
-- ============================================================
-- Seed initial MVP plan template
-- ============================================================

insert into public.plan_templates
(name, slug, description, status, category, audience, is_featured, sort_order)
values
(
  '7-Day Sync Plan',
  '7-day-sync-plan',
  'A simple starter plan designed to activate the Wellbine operating loop.',
  'published',
  'starter',
  'general',
  true,
  10
)
on conflict (slug) do update
set
  name = excluded.name,
  description = excluded.description,
  status = excluded.status,
  category = excluded.category,
  audience = excluded.audience,
  is_featured = excluded.is_featured,
  sort_order = excluded.sort_order,
  updated_at = now();
```

---

# Seed Data — Example Plan Version

```sql
-- ============================================================
-- Seed initial MVP plan version
-- ============================================================

with selected_plan as (
  select id
  from public.plan_templates
  where slug = '7-day-sync-plan'
  limit 1
),
inserted_version as (
  insert into public.plan_template_versions
  (
    plan_template_id,
    version_number,
    status,
    configuration_json,
    pillar_defaults_json,
    daily_rules_json,
    push_rules_json,
    home_rules_json,
    wearable_rules_json,
    commerce_rules_json,
    content_rules_json,
    published_at
  )
  select
    selected_plan.id,
    1,
    'published',
    '{
      "duration_days": 7,
      "objective": "activate_daily_alignment",
      "mode": "starter"
    }'::jsonb,
    '{
      "mind": {"enabled": true},
      "sun": {"enabled": true},
      "hydration": {"enabled": true},
      "sleep": {"enabled": true},
      "nutrition": {"enabled": true},
      "movement": {"enabled": true},
      "daily_stack": {"enabled": true}
    }'::jsonb,
    '{
      "daily_cycles": ["morning", "midday", "evening", "night"],
      "allow_confirm": true,
      "allow_adjust": true,
      "allow_later": true
    }'::jsonb,
    '{
      "push_optional": true,
      "max_major_cycles_per_day": 4
    }'::jsonb,
    '{
      "show_main_orb": true,
      "show_pillar_orbs": true,
      "show_next_best_action": true
    }'::jsonb,
    '{
      "wearables_optional": true
    }'::jsonb,
    '{
      "commerce_bridge_enabled": false
    }'::jsonb,
    '{}'::jsonb,
    now()
  from selected_plan
  on conflict (plan_template_id, version_number) do update
  set
    status = excluded.status,
    configuration_json = excluded.configuration_json,
    pillar_defaults_json = excluded.pillar_defaults_json,
    daily_rules_json = excluded.daily_rules_json,
    push_rules_json = excluded.push_rules_json,
    home_rules_json = excluded.home_rules_json,
    wearable_rules_json = excluded.wearable_rules_json,
    commerce_rules_json = excluded.commerce_rules_json,
    content_rules_json = excluded.content_rules_json,
    published_at = excluded.published_at,
    updated_at = now()
  returning id, plan_template_id
)
update public.plan_templates
set current_version_id = inserted_version.id,
    updated_at = now()
from inserted_version
where public.plan_templates.id = inserted_version.plan_template_id;
```

---

# MVP Edge Function Dependency

The SQL above supports these mandatory functions:

```text
activate_plan
update_home_state
process_daily_action
delete_account
```

The database can exist before the functions.

But the MVP experience becomes reliable only when these workflows are controlled.

---

# First Activation Logic

The `activate_plan` function should use:

```text
plan_templates
plan_template_versions
pillar_definitions
user_active_plans
user_pillar_states
daily_plans
daily_actions
user_home_state
```

Minimum activation output:

```text
active plan created
pillar states created
daily plan created
daily actions created
home state created
```

---

# Initial Daily Actions Direction

For MVP, Daily actions may be generated from static starter rules.

Example starter actions:

```text
Morning check-in
Hydration check
Movement action
Nutrition check
Evening reset
Sleep preparation
```

These should later come from:

```text
daily_rules_json
AAI context
pillar states
wearable data
user behavior
```

---

# Account Deletion Direction

The SQL provides user-owned tables with `on delete cascade` from `auth.users`.

However, production deletion should be handled carefully.

Account deletion should consider:

```text
soft delete
hard delete
anonymization
legal retention
subscription records
commerce events
uploads
audit logs
```

Do not rely blindly on cascade deletion without confirming privacy and legal needs.

---

# Storage Not Included In This SQL

Storage buckets should be created separately in Supabase.

Recommended buckets:

```text
user_uploads
public_assets
admin_assets
```

Uploads are optional for first MVP.

Do not enable uploads before private bucket rules are ready.

---

# What This MVP SQL Does Not Yet Include

This MVP SQL does not fully include:

```text
wearable_connections
wearable_metric_snapshots
user_uploads
commerce_benefits
user_commerce_benefits
commerce_events
recommendations
user_aai_context
advanced subscriptions
advanced analytics
payment records
```

These should be added only when the core operating loop works.

---

# Implementation Order

Recommended SQL implementation order:

```text
1. Extensions
2. updated_at function
3. user_roles
4. is_admin helper
5. user_profiles
6. user_settings
7. plan_templates
8. plan_template_versions
9. user_active_plans
10. pillar_definitions
11. user_pillar_states
12. daily_plans
13. daily_actions
14. user_home_state
15. feature_flags
16. content_modules
17. admin_audit_log
18. optional push_events
19. optional stack_items
20. enable RLS
21. create RLS policies
22. seed pillar definitions
23. seed feature flags
24. seed starter plan
25. seed starter plan version
```

---

# QA After Running SQL

After running SQL, test:

```text
Can authenticated user create own profile?
Can authenticated user read own profile?
Can authenticated user update own profile?
Can user read published plan templates?
Can user read published plan versions?
Can user read active pillar definitions?
Can user not update plan templates?
Can user not update pillar definitions?
Can user not read another user's private data?
Can admin read admin-managed records?
Can admin update admin-managed records?
Can seed data appear correctly?
```

---

# FlutterFlow Connection Checklist

After SQL is created, connect FlutterFlow to:

```text
user_profiles
user_settings
plan_templates
plan_template_versions
user_active_plans
pillar_definitions
user_pillar_states
daily_plans
daily_actions
user_home_state
feature_flags
content_modules
```

FlutterFlow should use:

```text
Supabase URL
Supabase anon key
authenticated user session
RLS-protected access
```

FlutterFlow must not use:

```text
service role key
```

---

# What This SQL Should Not Do

This SQL should not:

- Be treated as final production legal architecture
- Skip Edge Functions for complex operations
- Replace privacy review
- Replace security review
- Replace app QA
- Hardcode all future business rules
- Force commerce into MVP
- Force wearables into MVP
- Force uploads into MVP
- Turn FlutterFlow into source of truth
- Expose admin write access to normal users

---

# Success Criteria

This SQL MVP is successful when:

- Core tables exist
- Seed pillars exist
- Starter plan exists
- Starter plan version exists
- RLS is enabled
- User-owned data is protected
- Published plans can be read
- Admin-managed tables are protected
- FlutterFlow can connect
- Plan Activation can be implemented
- Home can load state
- Daily can load actions
- The core operating loop can be tested

---

# Current Status

Supabase SQL MVP is currently a draft.

Next steps:

- Review SQL
- Run in development Supabase project
- Confirm no syntax errors
- Test RLS with normal user
- Create initial admin role manually
- Connect FlutterFlow
- Build Auth
- Build Profile
- Build Onboarding
- Build Plan Activation Edge Function
- Build Home
- Build Daily
- Test operating loop

---

# Related Documents

- PRODUCTS/WELLBINE/SUPABASE_SCHEMA.md
- PRODUCTS/WELLBINE/SUPABASE_IMPLEMENTATION.md
- PRODUCTS/WELLBINE/EDGE_FUNCTIONS.md
- PRODUCTS/WELLBINE/FLUTTERFLOW_BUILD_GUIDE.md
- PRODUCTS/WELLBINE/MVP_BUILD_SEQUENCE.md
- PRODUCTS/WELLBINE/SCREEN_MAP.md
- PRODUCTS/WELLBINE/FEATURE_FLAGS.md
- PRODUCTS/WELLBINE/QA_PLAN.md
- PRODUCTS/WELLBINE/APP_RELEASE_CHECKLIST.md
