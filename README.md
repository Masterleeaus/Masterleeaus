<h1 align="center">Jason Lee</h1>
<p align="center"><strong>AI Systems Developer · Qualified Environmental Chemist · Creator of Titan Zero</strong></p>
<p align="center">Building evidence-led AI workflows where recommendations and authority stay separate.</p>

I design and build AI-enabled software for decisions, research, and business operations. My environmental chemistry background shapes how I handle evidence, provenance, uncertainty, and reproducibility.

I’m interested in AI developer and AI systems engineering roles involving agentic workflows, applied AI, evaluation, and reliable software.

## Engineering focus

- **AI workflows:** Connect model-assisted interpretation to structured tasks, scoped tools, explicit approvals, and reviewable outcomes.
- **Decision and evaluation systems:** Represent evidence, constraints, uncertainty, alternatives, and abstention explicitly; test behaviour with fixed scenarios and baselines.
- **Operational software:** Build tenant-aware workflows, offline-capable field tools, and governed integrations.

A model can interpret and recommend. The application still needs to verify evidence, resolve company scope, check policy, and record what an approved action changed.

| Stage | Engineering question |
| --- | --- |
| **Evidence and context** | What is known, where did it come from, how current is it, and what conflicts? |
| **Decision** | Which options meet hard requirements, and what remains uncertain? |
| **Authority** | Who may act, for which company, within what scope and time? |
| **Execution** | What changed, how is the result checked, and what can be recovered? |

## Measured test evidence

### CI-backed evaluations

- **[Titan Decision Engine · 20-case evaluation](https://github.com/Masterleeaus/decision-engine/actions/runs/37170763045)** · 4 October 2026. Step 27 produced **0/17 ready handoffs** for blocked or unresolved cases, wrongly blocked **0/3 valid cases**, generated **0/2 requests** for wrong-company attempts, and had **0/20 undispatched-request contract violations**. A recommendation-only baseline treated 15/17 blocked or unresolved cases as actionable. This tests request preparation, not host persistence, approval, or execution. [Method and full report](https://github.com/Masterleeaus/decision-engine#reproducible-authority-handoff-evaluation).
- **[Titan Interaction Engine · 31-case policy evaluation](https://github.com/Masterleeaus/Interaction-engine/actions/runs/37171514412)** · 4 October 2026. **0/24 blocked requests** were allowed, **0/7 valid requests** were wrongly denied, and **0/1 cross-tenant approval attempts** passed. This evaluates policy decisions, not host adapters, persistence, or downstream execution. [Method and full report](https://github.com/Masterleeaus/Interaction-engine#reproducible-authority-policy-evaluation).
- **[Titan Trust Engine · 32-case GPS-signal evaluation](https://github.com/Masterleeaus/Trust-Engine/actions/runs/37172099402)** · 4 October 2026. **0/32 trust-level mismatches**, **0/32 quality-flag mismatches**, and **0/32 scenario failures**. The evaluation also surfaced a design diagnostic: all 3 GPS-present cases with missing accuracy still receive a high signal, while carrying a no-accuracy flag. GPS signals do not prove attendance or truth. [Method and full report](https://github.com/Masterleeaus/Trust-Engine#reproducible-trust-signal-evaluation).

All three evaluation workflows completed successfully in GitHub Actions. These results measure bounded reference behavior and policy; they do not establish production readiness.

### Local suite runs

- **Titan Decision Engine:** In the 4 October deep-scan run, all **16 test files for Steps 10–25 passed after TypeScript compilation**, and **33 tests for Steps 26–30 passed**. These are local results, not a CI run. [Reference-engine source and tests](https://github.com/Masterleeaus/decision-engine/tree/main/engines).
- **Titan Zero Field Service Workforce:** Focused checks recorded **31/31 passes**: session lifecycle 14/14, DirectAdmin owner boundaries 12/12, and Communications reader 5/5. The tests used temporary execution overlays; the tested implementation is unpublished, and clean-checkout reproduction and live-host verification remain pending. [Commands, revisions, coverage, and limits](https://github.com/Masterleeaus/Titan-Zero-Field-Service-Workforce/blob/main/docs/working/2026-10-04-local-test-evidence.md).

## Selected projects

| Project | Engineering work |
| --- | --- |
| [Titan Decision Engine](https://github.com/Masterleeaus/decision-engine) | TypeScript decision-support reference engines for evidence, hard constraints, ranking, uncertainty, abstention, history, and capability-gated handoff. The host retains approval and execution. |
| [Titan Interaction Engine](https://github.com/Masterleeaus/Interaction-engine) | Governed interaction workflows across conversation and offline surfaces, with tenant-scoped context and a separately evaluated policy engine. |
| [Titan Trust Engine](https://github.com/Masterleeaus/Trust-Engine) | PHP/Laravel evidence-assurance extension for job evidence, configurable requirements, readiness, and human review. Trust signals inform review; they do not establish truth or authority. |
| [Titan Zero Field Service Workforce](https://github.com/Masterleeaus/Titan-Zero-Field-Service-Workforce) | TypeScript operating platform for field-service workflows, offline work, company boundaries, and authority-gated execution. |
| [Climate Crew](https://github.com/Masterleeaus/Climate-crew) | Python research-platform prototype for multi-agent climate and environmental investigation, evidence provenance, competing hypotheses, and human validation. |
| [ForgeMesh](https://github.com/Masterleeaus/ForgeMesh) | Repository-intelligence project that composes task-specific AI engineering teams from detected architecture, risks, and required capabilities. |

These repositories span **TypeScript/Node.js, Python, and PHP/Laravel**, with work on structured APIs, workflow orchestration, reproducible evaluations, and evidence-aware systems.

## Delivery example

[Titan Zero PR #1201](https://github.com/Masterleeaus/Titan-Zero-Field-Service-Workforce/pull/1201) is a bounded, issue-scoped runtime change. Review surfaced authority-revocation, identity-boundary, hung-operation, and storage-lock risks; follow-up changes and exact-head checks informed the merge. The linked record keeps the merge scope separate from the wider mission and live-host commissioning.

## Contact

For AI development, engineering, research, or collaboration enquiries: [jason@titanzero.io](mailto:jason@titanzero.io).

[Explore all repositories](https://github.com/Masterleeaus?tab=repositories)
