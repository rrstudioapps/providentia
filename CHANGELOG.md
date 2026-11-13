# Changelog

All notable changes to this project are documented in this file.
The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) and the project uses
[Semantic Versioning](https://semver.org/).

## [1.2.0] — 2026-11-13

### Added

- Theme configurator in Settings → Appearance: six accent colors (indigo, blue, emerald, violet,
  rose, orange), all WCAG AA in light and dark mode, and comfortable / compact density. Saved in the
  browser and applied before Angular boots, with no flash.
- Users: edit an account (name, company, email, plan, status, seats, country), delete it with a
  confirmation, and delete the selected accounts in bulk. New `UsersApi.update()` and
  `UsersApi.delete()`, in both the mock and the HTTP implementation.
- `docs/openapi.yaml`: OpenAPI 3.1 contract of every endpoint the HTTP mode expects (paths,
  parameters, JSON schemas, error codes), also published as an API reference page.

### Fixed

- Danger buttons (delete, cancel plan) are readable in dark mode: new `--app-bad-ink` token.

### Changed

- New endpoints for your backend: `PATCH /users/:id` and `POST /users/delete` `{ ids }`.

## [1.1.0] — 2026-11-13

### Added

- Users and invoices on phones: card lists with the key fields instead of wide tables, a "Sort by"
  menu and 44px tap targets.
- Settings → Appearance → **Mock API** switches to simulate a slow network or failing requests,
  with a banner while they are on: loading and error states can be tried without a backend.
- Error state with Retry on the Settings pages (profile, notifications, security), and one shared
  `<app-load-error>` component for every page.
- `demo` build configuration (`ng build --configuration production,demo`): visitors are signed in
  with the demo account, so every page of a public demo can be linked and indexed. Off by default.
- Themed checkboxes and select chevrons, bigger switches, red border on fields with an error.

### Fixed

- Billing page no longer breaks when billing data fails to load.
- Demo data: the Users list matches the Overview (paying accounts and MRR per plan), and every
  customer has a different name.
- Dark mode: brighter indigo accent, readable on its soft background (WCAG AA).
- Reports: churn rate change shown in percentage points; a change that rounds to zero is "Stable".
- Cohort retention: first column shows the cohort size and the colors span the real retention range.
- Active users chart fills its card; axis labels no longer overflow on phones.
- Status tabs show a fade when they scroll; table headers stay on one line; settings tabs and the
  phone icon in active sessions are clearer; route changes only cross-fade the page content.

### Changed

- `ReportResult.change` for `percent` metrics (churn rate) is now a difference in percentage points.
  If you connected your own API, update that value in `POST /reports/run`.

## [1.0.1] — 2026-11-13

### Fixed

- Demo data: Overview, Reports and the sign-in panel now share one revenue history
  (`core/mock/revenue-history.ts`), so MRR, growth and churn match on every page.
- Secondary text (`--app-muted`) darkened in light mode to meet WCAG AA contrast (4.5:1) on all
  surfaces; chart axis labels follow.
- Sign-in pages: promo panel uses the new `--app-brand-panel` token and brighter text, readable in
  both themes.
- Notifications menu no longer overflows the screen on phones.

### Added

- "Skip to content" link; focus moves to the page content when opening another section.
- Failed page loads (e.g. after a new deploy) reload the page once, then show an error toast
  instead of failing silently.
- KPI cards: a change that rounds to zero is shown as neutral, and churn rate changes are shown in
  percentage points (`deltaUnit: 'points'`).

### Changed

- `Kpi.delta` for `churnRate` is now a difference in percentage points (current − previous),
  not a % change. If you connected your own API, update that value in `GET /analytics/overview`.

## [1.0.0] — 2026-11-13

First public release.

### Added

- Overview page: KPI cards with sparklines, MRR growth, revenue by plan, active users,
  MRR movements and cohort retention heatmap, date range filter and CSV export.
- Users page: status tabs, search, plan and country filters, sorting and pagination kept in the
  URL, bulk CSV export, invite dialog, customer detail drawer and "view as customer".
- Reports page: report builder with chart and table, saved reports and CSV export.
- Billing page: current plan, usage meters, payment method form, plan comparison, plan change and
  cancel/resume flows, invoice history.
- Settings: profile with photo upload, notifications, appearance and security tabs.
- Auth: login, registration, forgot/reset password, onboarding wizard, guards and HTTP interceptor.
- Command palette (Ctrl/⌘ K), notification feed, in-app 404 page.
- Light, dark and system themes; responsive layout with collapsible sidebar and mobile drawer.
- Swappable API layer (mock data or HttpClient) with one switch in `app.config.ts`.
- Unit tests (Vitest) and end-to-end tests (Playwright).
- "Support rrstudio" button (Ko-fi) and optional "Download free" button, configured in
  `src/app/config/links.ts`.
