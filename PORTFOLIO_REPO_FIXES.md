# Portfolio Repository Audit & Manual Fix Register

**Audit date:** 5 October 2026  
**Account:** Masterleeaus  
**Repositories scanned:** 27

This register tracks issues that remain after the portfolio-wide evidence, branding, security-policy, contribution-policy and CI cleanup pass.

## Status vocabulary

- **Fixed** — changed directly on `main`.
- **Rerun** — source/configuration was repaired; a new CI or deployment run is required for fresh evidence.
- **Decision** — a product, schema, licensing or architecture decision is required before changing code safely.
- **Environment** — requires credentials, provider access, a deployed host, external service, or another environment-specific dependency.
- **Benchmark** — implementation exists, but the claimed property needs a reproducible evaluation rather than more documentation.

---

# Fixed automatically

## Portfolio-wide

- Scanned every accessible repository README and current positioning.
- Verified the primary checked-in banner/image path for the portfolio READMEs; checked assets were present.
- Added root `SECURITY.md` and/or `CONTRIBUTING.md` to serious repositories that were missing them, except where repository-local versions already existed.
- Standardised support docs around evidence labels: Implemented, Tested, Evaluated, Experimental and Planned.
- Restored the engineering portfolio banner in the profile README.
- Added the current commercial Titan naming map to the profile:
  - Titan Zero
  - Titan Core
  - Titan Build — blue
  - Titan Desk — red
  - Titan Field — yellow
  - Titan Pay — green
- Corrected a broken emphasis marker in the Uniquely README.

## Branding

- **ZeroPay README → Titan Pay** customer-facing identity. Repository/module slug remains `ZeroPay` for compatibility.
- **Titan-Zero-Field-Service-Workforce README → Titan Field** customer-facing identity. Repository slug remains unchanged for compatibility.
- Profile selected-project naming now uses **Titan Field**.

## Clean-Hub

Fixed directly on `main`:

- Removed the incompatible Tailwind 4 `@tailwindcss/vite` plugin from the root Vite config because the host is Tailwind 3 + PostCSS.
- Updated Titan Zero source verification to the canonical archived PWA plan path.
- Updated the source-verifier regression fixture to the same canonical plan path.
- Adjusted the secret baseline to permit the deliberately deterministic test-only APP keys in `.env.testing` and `.env.verification` while continuing to reject populated keys elsewhere.
- Updated README/evaluation docs so repaired failures are not still presented as current defects.

## Titan Business Operating System

- Fixed the MySQL CI environment setup. The workflow now removes both commented and active DB variables and appends one explicit testing database block rather than attempting to `sed` values that are commented out in `.env.example`.
- Updated README/evaluation status to distinguish that repair from still-unverified migration health.

## Uniquely

- Codecov upload is now supplemental. A Codecov authentication/upload problem no longer converts passing tests, static analysis and the coverage gate into a red project test result.

## zero

- Replaced the realtime mobile endpoint's reversible master-key fragments with a server-minted short-lived OpenAI Realtime client secret.
- Preserved the existing mobile `key1` / `key2` / `key3` response shape by splitting only the ephemeral secret.
- Replaced the retired preview-model fallback with a current configurable Realtime model fallback.
- Added safe provider-failure behavior and a source regression guard preventing reintroduction of master-key splitting.
- Updated README, security and evaluation documents.

---

# P0 — fix before calling the repositories reproducibly healthy

## Clean-Hub — Composer lock reconciliation

**Status:** Decision / Environment

`composer.json` requires:

```text
phpoffice/phpspreadsheet ^5.8
```

but the reviewed lock file contains 4.5.0.

### Required action

Run dependency resolution in a normal networked development environment and review the resulting transitive changes:

```bash
composer update phpoffice/phpspreadsheet --with-all-dependencies
composer validate --strict
composer test
```

Do not hand-edit `composer.lock`.

---

## Clean-Hub — 15 Titan verifier failures

**Status:** Code / Architecture

Last executed verifier result:

```text
42,917 passed
15 failed
42,932 total checks
```

Remaining failures from the reviewed run:

1. incomplete WorkCore Rewind remains quarantined
2. incomplete WorkCore Intelligence remains quarantined
3. WorkCore registers canonical Documents module
4. WorkCore registers canonical Assurance module
5. WorkCore registers governed read executor
6. Titan operations interface has a named route
7. company setup fallback route exists
8. Titan operations routes require authentication and active company
9. company model permits required public identifier creation
10. presence channel is company scoped
11. presence authorization verifies active company membership
12. conversation broadcast authorization is company scoped
13. private user broadcast channel is company scoped
14. `/.worktrees` is protected in `.gitignore`
15. `/storage/integration-evidence` is protected in `.gitignore`

Several are straightforward, but they touch runtime ownership/route/tenancy decisions and should be corrected deliberately rather than making the verifier less strict.

---

## Titan Business Operating System — canonical invoice-table ownership

**Status:** Architecture / Schema decision

The full test suite cascaded to **724 failures / 13 passes** from repeated SQLite:

```text
table "invoices" already exists
```

The host has:

```text
database/migrations/2026_04_10_180009_create_invoices_table.php
```

and the application also depends on invoice packages/modules.

### Required decision

Choose the canonical owner of the core `invoices` table:

- host application migration, or
- installed invoice package/module.

Then migrate the non-owner to an extension/alteration model.

**Do not** simply wrap the host create migration in `Schema::hasTable()`: that can hide a collision while leaving the wrong schema active.

---

## zero — Composer / YooKassa dependency chain

**Status:** Environment / Dependency decision

The reviewed CI dependency install fails on the YooKassa validator package because the locked dist archive returns GitHub 404 and source fallback is disabled. Older repository evidence also references a `git.yoomoney.ru` transitive dependency source.

### Required action

Choose one supported path:

- upgrade YooKassa to a release whose complete dependency graph is publicly resolvable;
- replace/remove the integration if no longer used;
- or provide an intentional authenticated/private dependency source.

Then regenerate and commit the lock file and rerun CI.

Do not bypass this by disabling Composer validation.

---

# P1 — rerun verification after fixes already made

## Clean-Hub

**Status:** Rerun

Rerun these workflows on current `main`:

- Repository Baseline
- Titan Zero Source Verification
- Laravel CI

The rerun should determine whether the repaired Vite config, source-plan path and synthetic-key policy are now green.

The historical frontend install also reported **39 npm vulnerabilities**:

- 2 low
- 4 moderate
- 33 high

Run:

```bash
npm audit
npm outdated
```

Review upgrades individually; do not use `npm audit fix --force` blindly on this application.

## Titan Business Operating System

**Status:** Rerun

Rerun CI after the MySQL environment fix.

The fresh-migration job should now reach the migration layer, exposing the next actual migration error rather than failing because Laravel ignored commented DB values.

## Uniquely

**Status:** Rerun

Rerun the Tests workflow. The previous audited application result was:

```text
203 passed
12 skipped
670 assertions
```

with Composer validation, dependency audit, Pint and PHPStan passing before Codecov caused the overall failure.

A new run should establish current-head evidence now that Codecov is non-blocking.

The historical Docker workflow also failed from GitHub API rate limiting; rerun before treating that as a repository defect.

## zero — realtime credentials

**Status:** Rerun / Environment

After Composer is repaired:

- run the new realtime credential regression test;
- test successful client-secret issuance;
- test provider failure;
- verify expiry in the mobile client;
- verify authenticated user/company/conversation binding end to end;
- verify replay/session reuse behavior.

Only then close the live-verification portion of issue #263.

---

# P1 — repository-specific engineering gaps already documented by the codebase

## CleanPro

**Status:** Code

TitanGo's local mutation item ID is not persisted as a server-side idempotency key for every mutation type.

An ambiguous network failure after a successful server write can therefore allow a duplicated replay in some paths.

**Fix:** carry the local operation ID/idempotency key through every mutating field API and persist/replay-check it server-side.

## Titan Builder

**Status:** Code / CI

The repository's documented full-verification snapshot failed before root verification because of:

- six inherited workflow-policy violations;
- duplicate `braces@3.0.3` lockfile mapping.

Resolve the workflow-policy violations and regenerate/reconcile the lock graph, then rerun `pnpm verify`.

## Titan Core

**Status:** Architecture

The runtime audit records direct AI paths that still bypass the intended central model gateway.

The repo should not be treated as a single production runtime authority until those direct paths are consolidated or explicitly designated exceptions.

## Field-Flux-Pro

**Status:** Environment

The module has focused source/test evidence but no proven synchronized host lockfile + clean installed host + green full suite.

Install it into the target Laravel host and capture exact-head verification before claiming host readiness.

## WorkCore ERP Modules

**Status:** Environment / Provenance

Some extraction/build tests require the original consolidated source archive or retained legacy release ZIPs and are intentionally skipped when those sources are unavailable.

Preserve those source inputs and hashes if full extraction reproducibility is important.

## Climate Crew

**Status:** Benchmark

The evaluation runner's system integration is currently mocked for the offline lane.

Do not claim scientific-performance improvement until the real multi-agent orchestration is connected to a labelled evaluation and compared against a useful baseline.

## ForgeMesh

**Status:** Benchmark

The corpus/compiler is reproducible, but there is no benchmark showing that the selected specialist team improves downstream engineering task quality.

If this becomes a primary portfolio project, add task-level ablation:

```text
generic agent set
vs
ForgeMesh-selected minimum team
```

## Titan Themes

**Status:** Benchmark

Structural validators exist, but browser visual regression and accessibility conformance are not established.

Add:

- screenshot/visual-diff lane;
- keyboard/focus tests;
- automated accessibility checks;
- host rendering check for each supported surface.

## Tenant-Forge

**Status:** Benchmark / Security

Foundation tests do not establish cross-tenant query isolation or Stripe webhook/payment correctness.

Add tenant-isolation negative tests and webhook replay/idempotency tests before presenting it as a hardened SaaS foundation.

## Delivery Management Platform

**Status:** Provenance / Scope

This is best presented as an attributed reference architecture, not original AI infrastructure.

Keep tenant-boundary evidence prominent and preserve upstream attribution.

---

# P2 — branding decisions / assets

## Titan Pay

**Current README:** aligned.

Still uses legacy repository/module/image names containing `ZeroPay`.

### Decide

- keep repo slug `ZeroPay` permanently as engineering history; or
- rename repository to `Titan-Pay` and update external links.

### Asset work

Replace legacy ZeroPay logo/banner graphics with Titan Pay green brand assets. Do not remove compatibility asset paths until references are migrated.

## Titan Field

**Current README:** aligned.

Repository slug remains:

```text
Titan-Zero-Field-Service-Workforce
```

Legacy banner/logo filenames still use the old product identity.

### Decide

- keep repository slug as historical engineering name; or
- rename it to a Titan Field repository after auditing links/actions/deployments.

### Asset work

Create/replace customer-facing Titan Field graphics using the yellow field brand.

## TitanPro

The repo is technically strong, but **TitanPro is not part of the current commercial four-app naming model**.

Decide whether it is:

- a legacy portfolio engineering project;
- an internal/technical platform name;
- or intended to map into Titan Core/Desk.

Do not mass-rename code until that decision is explicit.

## Titan-Core

The repository name overlaps the current **Titan Core** commercial name, but its README describes an AI/platform kernel, while current Titan Core is the suite/system-management surface.

Decide whether:

- the repo becomes the implementation of current Titan Core;
- or it remains an infrastructure/kernel repo with a clearer technical qualifier.

## Titan Business Operating System

The repository contains historical surface names and architecture generations.

Decide whether this repo is:

- a historical/platform engineering repository; or
- the canonical implementation of the current suite.

If canonical, reconcile historical product-language docs with current:

```text
Titan Zero
Titan Core
Titan Build
Titan Desk
Titan Field
Titan Pay
```

without renaming internal modules that still need compatibility.

## Tradie Smart

The README is professional but does not currently lead with a portfolio banner like most of the rest of the suite.

If it remains a prominent pinned repo, add a restrained architecture/identity banner consistent with the current portfolio visual system.

---

# P2 — licensing / provenance decisions

Do **not** auto-add licenses to these repositories until source provenance is reviewed.

Public/engineering repositories found without a root `LICENSE` during this audit:

- predictive-analytics-module
- Delivery-Management-Platform
- zero
- Tradie-Smart
- Clean-Hub
- CleanPro
- Titan Pay / ZeroPay
- Tenant-Forge
- Uniquely
- Titan-Core
- Field-Flux-Pro
- Titan-themes
- WorkCore-ERP-Modules
- Smart-Sellers
- Interaction-engine
- Titan Field / Titan-Zero-Field-Service-Workforce
- Commerce-Crew
- Developer-Workforce-Extension-
- Trust-Engine

The profile repository also has no root license, which is generally not important unless profile assets/text are intended for reuse.

Repositories observed with a root `LICENSE`:

- Titan-Business-Operating-System
- TitanPro
- AI-Coding-Studio
- Titan-Builder
- Climate-crew
- ForgeMesh
- decision-engine

### Special provenance caution

Titan-Business-Operating-System's root MIT file carries upstream copyright text. Review whether that license accurately covers repository-local additions and every retained/imported component before presenting the entire repository as uniformly authored/licensed.

---

# Strong repositories that should not be churned without evidence

These already have unusually good portfolio evidence and should be improved through real evaluation/runtime work rather than cosmetic README rewrites:

- decision-engine
- Interaction-engine
- Trust-Engine
- Uniquely
- AI-Coding-Studio
- Titan-Builder
- ForgeMesh
- WorkCore-ERP-Modules
- Smart-Sellers
- Commerce-Crew
- TitanPro
- Titan Themes

---

# Portfolio priorities

If the goal is employability and engineering credibility, the highest-return order is:

1. **Get Clean-Hub CI green** and convert its governed-action mechanism into an adversarial benchmark.
2. **Resolve Titan BOS invoice ownership**, then rerun migrations/tests/module verification.
3. **Repair zero Composer dependencies**, then verify the new Realtime credential boundary.
4. **Rerun Uniquely** and publish current-head test evidence.
5. **Add/resolve root licensing** only after provenance review.
6. **Finish visual brand assets** for Titan Pay and Titan Field.
7. Keep Decision Engine, Interaction Engine and Trust Engine as the measured-control-plane proof points.
