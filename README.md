<h1 align="center">Jason Lee</h1>
<p align="center"><strong>AI Systems Developer · Agent Reliability & Evaluation · Titan Zero</strong></p>
<p align="center">Melbourne, Australia · <a href="mailto:jason@titanzero.io">jason@titanzero.io</a></p>
<p align="center">BSc, Environmental Chemistry major — Griffith University (2015) · MBA — Australian Institute of Business (2018)</p>

I build AI-enabled software where model suggestions meet evidence, evaluation, and clear authority boundaries. My environmental chemistry background informs how I handle uncertainty, provenance, and reproducibility.

<strong>Target roles:</strong> AI Systems Engineer · Applied AI Engineer · Agent Reliability / Evaluation Engineer  
<strong>Primary:</strong> TypeScript / Node.js · <strong>Growth area:</strong> Python · PHP / Laravel project experience

## Measured test evidence

Three reference-engine evaluations completed successfully in GitHub Actions on 4 October 2026:

- **[Titan Decision Engine · 20 cases](https://github.com/Masterleeaus/decision-engine/actions/runs/37170763045):** 0/17 blocked or unresolved cases produced a ready handoff (two-sided 95% Wilson upper bound: **18.4%**); 0/2 wrong-company attempts created a request. A recommendation-only baseline treated 15/17 blocked or unresolved cases as actionable. The test covers request preparation, not host persistence, approval, or execution. [Method and report](https://github.com/Masterleeaus/decision-engine#reproducible-authority-handoff-evaluation).
- **[Titan Interaction Engine · 31 cases](https://github.com/Masterleeaus/Interaction-engine/actions/runs/37171514412):** 0/24 blocked requests were allowed (95% Wilson upper bound: **13.8%**); 0/7 valid requests were wrongly denied; 0/1 cross-tenant approval attempts passed. The test covers policy decisions, not adapters or downstream execution. [Method and report](https://github.com/Masterleeaus/Interaction-engine#reproducible-authority-policy-evaluation).
- **[Titan Trust Engine · 32 cases](https://github.com/Masterleeaus/Trust-Engine/actions/runs/37172099402):** 0/32 trust-level mismatches (95% Wilson upper bound: **10.7%**). The cases also exposed a limitation: all 3 GPS-present cases with missing accuracy still received a high signal, tagged no_accuracy. GPS does not prove attendance or truth. [Method and report](https://github.com/Masterleeaus/Trust-Engine#reproducible-trust-signal-evaluation).

These are small, bounded suites. The intervals describe the synthetic test counts; they are not estimates of production risk or proof of production readiness.

### Local verification

**Decision Engine · local run, 4 Oct 2026 · Node 24.19.0 · unpinned checkout:** 16/16 test files for Steps 10–25 passed after TypeScript compilation; 33/33 tests for Steps 26–30 passed. This was a local run, not CI, and its source commit was not recorded. [Reference-engine source and tests](https://github.com/Masterleeaus/decision-engine/tree/main/engines).

## Engineering focus

- **Agent workflows:** keep model interpretation, recommendations, approval, and execution as separate stages.
- **Evaluation:** use fixed scenarios, baselines, failure counts, and explicit test limits.
- **Operational software:** build scoped APIs and offline-capable workflows with reviewable state changes.

## Selected projects

| Project | Work |
| --- | --- |
| [Titan Decision Engine](https://github.com/Masterleeaus/decision-engine) | TypeScript reference engines for evidence, constraints, uncertainty, recommendations, and capability-gated handoff. |
| [Titan Interaction Engine](https://github.com/Masterleeaus/Interaction-engine) | Tenant-scoped interaction workflows and separately evaluated policy decisions. |
| [Titan Trust Engine](https://github.com/Masterleeaus/Trust-Engine) | PHP/Laravel evidence assurance, readiness signals, and human review workflows. |
| [Titan Zero Field Service Workforce](https://github.com/Masterleeaus/Titan-Zero-Field-Service-Workforce) | Company-scoped field operations, offline work, and governed execution. |
| [Climate Crew](https://github.com/Masterleeaus/Climate-crew) | Python research-platform prototype for climate and environmental investigation. |
| [ForgeMesh](https://github.com/Masterleeaus/ForgeMesh) | Repository intelligence for composing task-specific AI engineering teams. |

## Work in progress

- **LLM-in-the-loop evaluation:** [Merged PR #2](https://github.com/Masterleeaus/decision-engine/pull/2) adds a 200-case synthetic proposer-to-gate harness. The [offline CI smoke check](https://github.com/Masterleeaus/decision-engine/actions/runs/37174873332) passed; a live-model evaluation has not run yet.
- **Field Service local checks:** a developer-local record lists 31/31 focused checks on temporary overlays. The tested implementation is unpublished and clean-checkout reproduction is pending, so this is development evidence rather than a public CI result. [Details and limits](https://github.com/Masterleeaus/Titan-Zero-Field-Service-Workforce/blob/main/docs/working/2026-10-04-local-test-evidence.md).
- **Climate Crew:** remains a prototype; I have not published a reproduced scientific result yet.

## Delivery example

[PR #1201](https://github.com/Masterleeaus/Titan-Zero-Field-Service-Workforce/pull/1201) is an agent-assisted merge covering authenticated runtime composition, durable recovery, and company-scoped execution. Its record lists exact-head tests and leaves live-host commissioning unverified.
