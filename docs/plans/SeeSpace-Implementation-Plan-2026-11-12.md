# SeeSpace implementation plan

Version 1.1 • 12 November 2026 • Planning baseline and orchestration map for Aminu

## Direction and how to use this plan

Build SeeSpace entirely in Codex, including visual design, frontend and application logic. Work in the existing `/Users/amisha/www/seeSpace` scaffold, not a replacement starter kit. First approve a visual direction; then complete and approve a working UI prototype; only then implement marketplace business logic. Use the companion `SeeSpace-Codex-Prompts-2026-11-12.md` one milestone at a time. This document does not start implementation or authorize deployment.

The first product is a Nigeria-first public property marketplace. Anyone can browse houses and land for rent or sale without signing in. Publishers maintain inventory, moderators control publication, and seekers send nonbinding enquiries. Property management follows separately. Keep the property asset distinct from its public advertisement so later private records do not contaminate public responses.

### Source of truth and conflicts

1. Aminu's latest direction: Codex-only workflow supersedes the Claude Design → Claude Code → Codex workflow in earlier documents.
2. SeeSpace Business Requirements Specification v1.1, 11 November 2026: business requirements and identifiers used below. It is a draft: most policies remain proposed, not approved.
3. SeeSpace UI/UX prototype design brief v1.1: screen IDs, F01–F07 journeys, fixture definitions and responsive criteria. Its Claude-specific instructions are superseded; its prototype assumptions are not production policy.
4. Current scaffold and AGENTS.md: implementation conventions and existing identity/team functionality must be preserved.

The previous Claude prototype is reference material, not approved production code or evidence of passing tests. Its published visual result was not inspected for this plan. Do not blindly port its HTML or assume its reported 53 screens satisfy requirements. No legacy code or personal data migration is authorized by this plan.

## Verified starting point

Read on the Mac on 12 November: AGENTS.md, composer.json, package.json, resources/js/app.ts, routes/web.php and skill directories.

- Existing Laravel/Inertia/Vue/TypeScript/Tailwind scaffold; Fortify, passkeys, Reka UI and Wayfinder dependencies. Preserve auth, settings and team flows rather than generating parallel versions.
- `app.ts` uses AppLayout by default, AuthLayout for auth, and AppLayout/SettingsLayout for settings and teams. Only Welcome currently has no layout. Public marketplace pages need an explicit public-layout rule; they must not inherit team navigation or an auth requirement.
- The dashboard is under `{current_team}` with authentication, verification and membership middleware. Team Owner/Admin/Member must not silently become landlord/agent/moderator authority.
- composer.json requires PHP `^8.6`; local CLI reports PHP `8.5.12`; AGENTS.md describes PHP 8.5. The current CI workflow now selects PHP 8.6, but local CLI still reports 8.5.12. Verify an explicitly selected compatible executable for local backend commands and PHP 8.6 in cloud setup; do not silently lower requirements or bypass platform checks.
- Refresh for orchestration: this is now a Git repository with origin `https://github.com/hussain4real/SeeSPace.git`; inspected HEAD is `a1e8b8f` (Use PHP 8.6 for CI and refresh platform lock metadata). Working tree was clean before this documentation update. This supersedes the initial no-Git observation. No remote push or CI result was verified during this refresh.
- `.ai/rules` was absent. Recheck it before future edits as required by AGENTS.md.
- These observations are static inspection, not proof the scaffold builds or that authentication works. No application tests, build, migration or UI flow was run for this plan.

### Available skills to use deliberately

- Global `impeccable` v3.9.1: primary shape/craft/critique/audit/polish workflow. Follow its context setup and PRODUCT.md/DESIGN.md discovery; do not assume the skill folder is inside the project. Use its design approval checkpoint.
- Global `frontend-design`: visual direction, typography, composition and critique; complement Impeccable rather than running conflicting design systems.
- Global `modern-web-guidance`, `typescript-best-practices`: implementation quality.
- Project `.agents/skills/inertia-vue-development`, `tailwindcss-development`, `wayfinder-development`, `fortify-development`, `laravel-best-practices`, `testing-best-practices`, `infer-conventions`: activate by area under AGENTS.md.
- Use available Playwright/browser tooling for screenshots and journeys; verify tooling actually runs before promising browser coverage. Skill presence is not proof browser dependencies work. Do not install dependencies without approval.

## Delivery map

| Milestone | Outcome                                            | Depends on                   | Gate                                    |
| --------- | -------------------------------------------------- | ---------------------------- | --------------------------------------- |
| M0        | Reliable baseline, decisions and contracts         | Source inspection            | Environment and scope recorded          |
| M1        | Approved visual direction and design system        | M0 discovery                 | Aminu selects direction                 |
| M2        | Complete responsive UI prototype                   | M1 approval                  | Aminu approves F01–F07; no logic yet    |
| M3        | Secure marketplace foundation and public discovery | M2; schema/privacy decisions | P0 controls and guest journeys pass     |
| M4        | Publisher, media and moderation vertical slices    | M3                           | Lifecycle and isolation tests pass      |
| M5        | Enquiries, operations and measurement              | M4                           | Durable delivery and privacy tests pass |
| M6        | Hardening and launch-readiness evidence            | M3–M5                        | AT001–AT006, product/ops acceptance     |
| M7        | Private property management                        | Separate approval after P1   | P2 decisions and private-data tests     |

These are dependency milestones, not dates or claims of completion. Avoid a calendar estimate until the baseline runs and design/policy decisions are settled. M3–M6 together deliver BRS P1; BRS P0 is a security prerequisite, not the same as this plan's visual-design stage.

## M0: Establish the baseline and resolve only blocking choices

**Tasks**

- Read AGENTS.md and applicable .ai/rules if present; inventory routes, middleware, shared Inertia props, models, migrations, auth/team tests, components and CSS tokens. Record what exists versus what must be added.
- Record actual installed package versions from lockfiles/package inspection, commands and runtime constraints. Resolve the PHP mismatch through an explicit approved environment decision. Do not run setup against an unknown database: its script includes migrations.
- Preserve a recoverable source baseline. Check unrelated user changes before any edits; establish version control with explicit authorization if needed.
- Create an approved screen-to-requirement map, authorization matrix and draft public page-prop contract. Separate public display identity/location from account records and private authority evidence.
- Record D01–D12 below and assign owners. Nonblocking aesthetic choices can proceed; schema, disclosure and lifecycle choices cannot be silently finalized.
  **Acceptance:** baseline report names actual versions, tests available, what ran/failed/was blocked, existing auth/team behavior to protect, and affected files. No assertion that P0 is complete from inspection alone.

## M1: Design direction before page production

**Tasks**

- Use Impeccable shape/craft and the existing brief. Produce two genuinely distinct but credible directions for home, results and listing detail, including mobile. Recommend one with reasons relevant to property discovery.
- Use fictional Nigeria-first fixtures and representative imagery with rights/provenance. No invented testimonials, verification, scarcity, counts or real contact data.
- Define semantic tokens, type scale, spacing, image ratios, focus and status treatment. Warm surfaces/deep green in the earlier brief are a proposed direction, not immutable branding.
- Agree public, publisher and operations shells; preserve existing security/settings/team pages and identify any purely visual integration required.
  **Acceptance:** Aminu approves a named direction with desktop/mobile references and token decisions. Stop here for approval; do not bulk-build all pages first.

## M2: Complete UI-only prototype in the real stack

**Tasks**

- Implement reusable Vue components: purpose selector, price display, listing cards, filter controls/sheet, gallery, uploader presentation, stepper, status, enquiry form, alerts and confirmations. Reuse existing primitives.
- Public P01–P06: home, results, house/land rent/sale details, enquiry and report, unavailable/not-found. Preserve filters through pagination, Back and shareable URLs. Sale has no rent suffix; land has no bedrooms.
- A01–A02 and L01–L05: integrate existing auth, onboarding states, listing tabs, five-step editor, draft preview, review feedback, revision/availability and private enquiry inbox.
- O01–O04: review queue/detail, reports/suspension, publisher administration and delivery failures; include decision history. Explicitly model stale decisions.
- Add local fixture adapters and a clearly marked development-only scenario index/reset. Do not introduce production privileges, real email, database writes or live services to simulate flows. Do not replace working auth with pretend auth.
- Cover loading, empty, busy, success, validation, offline/retry, 403/404, revoked delegation, expired session, stale edit, failed photo, duplicate click and notification failure. Safe unsaved input must not enter URLs or inappropriate persistent browser storage.
  **Acceptance:** F01–F07 demonstrable at 360/768/1440 widths; keyboard, focus return, Escape, gallery controls, upload reorder alternatives, reduced motion and 200% zoom reviewed. No unintended overflow. Capture screenshots and record browser/console errors. Run frontend checks/build if runtime permits; report unrun checks. Aminu approves the flows before M3. P2 concepts are optional separate references, never launch navigation.

## M3: Secure domain foundation and public portal

**Requirements:** AC001–AC004, DR001–DR004, SP001–SP004, FR001–FR006.
**Tasks**

- Finalize identity/team/publisher/mandate boundary without reinterpreting existing team roles. Use server policies on each object action and scoped queries; revoked authority must stop subsequent requests.
- Model asset separately from listing, explicit rent/sale purpose, currency/fixed-precision amount, rent period, controlled category and size units. Choose simultaneous rent/sale behavior before schema freeze.
- Design listing revisions and public representation, including publication eligibility and safe media URLs. Public DTO/resource allowlist must not serialize nested accounts, tenants, contacts or authority evidence. Test shared Inertia props and errors too.
- Wire approved public UI to persisted listing summaries/details; implement URL filters, deterministic pagination/sort, compatible price comparisons, safe direct links, canonical/meta and sitemap eligibility.
- Add factories for contrasting records and distinctive private values to detect disclosure. Use isolated test data only. No legacy production import.
  **Acceptance:** AT001 and public parts of AT003 pass. Guests browse without login; guessed private IDs are safe; response-level leakage tests cover HTML/JSON/Inertia/metadata/media. Clean schema setup and applicable upgrade path are tested on disposable data. Existing identity/team tests remain passing. Cache invalidation design supports the 60-second availability requirement.

## M4: Publish safely, moderate exact revisions

**Requirements:** FR007–FR012, BR001–BR003, BR005–BR007, SP002–SP003.
**Tasks**

- Implement publisher onboarding/approval and delegation under approved D04; persist own drafts with field errors and explicit revision/version control.
- Enforce Draft → Pending → Published; rejection → Draft with feedback; Published → Withdrawn/Rented/Sold or moderator Suspended. Restore requires review. Rent/sale completion actions must match purpose.
- Only approve the exact reviewed revision. Concurrent edit/save/moderation must return a conflict, never publish unseen content or overwrite a newer state.
- Implement approved material-edit policy, audit actor/revision/time/reason, public-cache/search/sitemap invalidation, and safe unavailable direct links.
- Media: decoded type/size validation, stable object keys, authorization, EXIF stripping, staging/quarantine until eligible, ordering/captions/cover; deletion by stored key, not current month. Recheck serving and stale cache behavior after withdrawal/suspension.
- Abuse reports private to authorized operators, safe deduplication, reasons for suspension and restoration review.
  **Acceptance:** AT002–AT004; cross-publisher/forged owner/revoked-agent/guest mutation matrix and file spoof/path/oversize cases pass. Previous-month image deletion works. Pending/rejected evidence never becomes publicly retrievable. Stale moderator approval fails without side effects. Removal from all public entry points measured within 60 seconds.

## M5: Enquiries and operational completeness

**Requirements:** FR013–FR017, SP005–SP007.
**Tasks**

- Save an enquiry once using a server-enforced retry/idempotency strategy; snapshot the authorized recipient scope safely. Collect only approved reply information and disclose recipient/purpose.
- Queue minimal notifications with retries and terminal-failure visibility. Notification retries must not recreate enquiries. Receipt means saved, not delivered, reserved or agreed.
- Private inbox authorization, report handling, publisher status, taxonomy and operational audit. Disable/revocation must affect access immediately under policy.
- Validation/throttling and accessible retry; synthetic provider-outage and duplicate-delivery tests. Only use fake mail/provider adapters until live integration is separately authorized.
- Privacy-reviewed analytics for search/result/detail/enquiry/delivery, excluding raw messages/contacts and separating test traffic. Record retention and incident procedures.
  **Acceptance:** AT005 passes including outage, duplicate click and unauthorized recipient cases. Operator sees delivery failure distinct from missing enquiry. Analytics contain no private sentinel values. Product decides whether publisher replies happen outside platform; no fabricated send-reply capability.

## M6: Hardening and release readiness, not automatic deployment

**Tasks**

- Re-run AT001–AT006 against a pinned candidate and clean environment; test identity/team regressions, policies, migrations, media, queues and lifecycle end-to-end.
- Run project checks: `npm run check`, `npm run types:check`, `npm run build`; PHP checks/test scripts after runtime resolution, including applicable `composer ci:check`. Read script side effects first; PHP edits require AGENTS.md Pint workflow. Report targeted and aggregate results separately.
- Automated accessibility plus manual keyboard, screen-reader, contrast and zoom on core journeys. Audit public data in all delivery surfaces, not just pixels.
- Validate approved NFR targets on declared hardware/workload: proposed 10,000 listings/50 concurrent browsers, p95 <1s/errors <1%, LCP ≤2.5s/CLS ≤0.1. Treat targets as proposed until D11 approval.
- Prepare backup/restore, rollback, health/queue/storage alerts, moderation/support runbooks, inventory/image-rights review and privacy/legal copy. Rehearse destructive operations only in an authorized disposable environment.
  **Acceptance:** acceptance matrix links each requirement to evidence, commit, test/environment and residual defect. Product and operations sign off. No unresolved launch-blocking security/privacy/data-integrity issues. Deployment, DNS, real credentials, external providers and live-data operations need their own authorization; launch readiness is not a deployed service.

## M7 and later: Explicitly out of marketplace delivery

P2 requires separate scope: FR018 tenant records; FR019 leases/documents; FR020 manual rent obligations/payments/reversals; FR021 reconciled scoped reports/exports; FR022 units/occupancy. Decide D12 before implementation. Preserve private portfolio boundaries and public-data leakage tests. Manual tracking does not move money. Maintenance appears in the design brief but has no standalone BRS FR018–FR022 requirement: scope it explicitly rather than treating the mockup as approval.
P3 FR023: maps, favorites, saved searches, viewing scheduling, verification, collection/payout, e-signature, subscriptions and commercial integrations. No placeholder teasers, dormant paid buttons or provider selection in P1. Each needs business case, policies, data-sharing and separate authorization.

## Decision ledger: recommendations are not approvals

| Decision     | Proposed approach / unresolved detail                                                                                                                                                               | Must resolve before       |
| ------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------- |
| D01          | Nigeria confirmed; cities, operator, language and legal disclosures open                                                                                                                            | Real content/launch       |
| D02          | Houses and land confirmed; apartments/commercial/units and dual rent/sale asset rule open                                                                                                           | Schema freeze             |
| D03          | Explicit configurable currency/period/fees; NGN monthly is demo only                                                                                                                                | Production validation     |
| D04          | Approved landlord/agent with revocable scoped mandate; team mapping open                                                                                                                            | Publisher policies        |
| D05          | Review first publication/material edits; define material fields, operators and SLAs                                                                                                                 | Lifecycle implementation  |
| D05 revision | Earlier brief hides listing during material review. Alternative: keep last approved immutable revision live unless withdrawn/suspended. Recommend evaluating latter; do not silently override brief | Revision schema and tests |
| D06          | No property-verification badge in P1                                                                                                                                                                | Public copy               |
| D07          | Private enquiry, approximate area; decide exact public precision and reply channel                                                                                                                  | Public DTO/enquiries      |
| D08–D09      | No checkout/collection/contracts; commercial policy remains open                                                                                                                                    | Any financial feature     |
| D10          | Retention, erasure, support ownership and reporter/enquiry access                                                                                                                                   | Production data           |
| D11          | Photo limits 20/10MB and NFR targets proposed; staffing/budget/provider choices open                                                                                                                | Upload rules/launch       |
| D12          | Private management, units, ledger and occupancy rules                                                                                                                                               | P2                        |

Also resolve pending-submission withdrawal, retention of unavailable prices, staff MFA policy and notification/rate limits. Record owner, decision, date and affected requirement/test. Continue independent design work while blocking only affected implementation.

## Progress tracking and completion template

For every milestone keep: task ID; BRS IDs; files changed; dependency; acceptance evidence; status (not started/in progress/blocked/accepted); blocker/owner. Use small reviewable vertical slices rather than one giant generation request.
At handoff report: what changed; exact candidate/baseline; checks actually run and results; checks not run and why; screenshots where relevant; unresolved decisions; next permitted milestone. Never label a mock, screenshot, CI report or source-only inspection as production validation.

## Orchestrated sessions: local design, cloud engineering, one integration owner

Aminu owns product/design decisions. The dot coordinates assignments, dependencies, evidence and handoffs. Session names below are candidates, not sessions already created. Start with one implementation worker and one independent read-only reviewer; add parallel writers only when file ownership and data contracts are stable.

### Recommended session placement

| Milestone       | Lead session candidate                                                      | Supporting session and boundary                                                                                             | Required handoff/gate                                                          |
| --------------- | --------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| M0 baseline     | **Local: SeeSpace foundation coordinator**                                  | Cloud environment preparation only after setup authorization; read-only contract review may run independently               | Verified baseline, runtime, source commit, skill availability, decisions       |
| M1 direction    | **Local: SeeSpace design studio**                                           | Cloud read-only UX/requirements critique using supplied screenshots/specs, not assumed access to the Mac browser            | Aminu chooses direction before page production                                 |
| M2 UI prototype | **Local: SeeSpace frontend studio**, continuing M1                          | Independent reviewer can audit contracts/copy; browser validation stays local unless cloud browser tooling is verified      | Approved F01–F07, tokens/components, screenshots, safe DTO contracts           |
| M3 foundation   | **Cloud: SeeSpace domain and public portal**                                | Local coordinator integrates UI against agreed contracts; no simultaneous edits to shared routes/types/layouts              | M2 approval and D02/D04/D07; P0 negative tests and public discovery evidence   |
| M4 lifecycle    | **Cloud: SeeSpace publishing and moderation**                               | Separate cloud read-only security/concurrency reviewer; local visual validation of editor/operations                        | M3 integrated baseline, D05 revision policy, immutable reviewed-revision tests |
| M5 enquiries    | **Cloud: SeeSpace enquiries and operations**                                | Local coordinator handles final UI integration after contracts; cloud independent delivery/privacy review                   | M4 baseline, recipient/retention decisions, durable retry evidence             |
| M6 acceptance   | **Cloud: SeeSpace verification** plus **Local: SeeSpace acceptance studio** | Cloud clean setup/backend/aggregate checks; local real-browser/accessibility/visual acceptance; independent security review | Same candidate commit, AT001–AT006, no unresolved launch blockers              |
| M7 later        | **Cloud: SeeSpace management planning**, only after separate scope approval | Local design exploration after product decisions                                                                            | D12 and separate implementation authorization                                  |

Cloud is recommended for reproducible backend/tests and work while the Mac is asleep, not because it automatically has better tools. Local is preferred for the installed design skills, current scaffold and visual feedback. If cloud setup is not ready, continue permitted local planning/design; do not block everything or claim cloud execution occurred. If the Mac is offline, cloud review can continue on its verified snapshot; local visual acceptance waits.

### Coordination contract

1. The coordinator records the current accepted commit, milestone, active session, owned files, dependencies, tests and blockers. Reuse the phase session rather than starting overlapping work.
2. Each worker receives the BRS/design brief, approved decisions, exact base commit/branch, scope and acceptance criteria. Cloud paths are discovered in that environment; never assume the Mac path exists there. Local-only uncommitted files, global skills and browser sessions do not transfer automatically.
3. Give each writer an isolated branch/worktree/workspace. One writer owns shared schema/migrations, policies, route definitions, global types and design tokens at a time. Freeze/review public DTO contracts before parallel work. Independent reviewers do not edit the author's workspace.
4. Default sequence is M0 → M1 approval → M2 approval → M3 → M4 → M5 → M6. Read-only reviews, test-plan drafting and copy audits may overlap; competing implementation of the same feature may not. M5 can be split only after stable lifecycle and recipient contracts exist.
5. Worker handoff includes diff/commit, changed files, requirement coverage, executed checks, unrun limits and screenshots where relevant. Coordinator reviews the delta, integrates only under authorization, then reruns affected and aggregate checks against the combined candidate. Passing isolated branches does not prove the integrated app passes.
6. Never switch/rebase a working checkout another session is using. Preserve user edits; stop conflicting writes and reconcile them. Use authorized Git commits/patch artifacts to move work, not credential copying. Push/PR creation, merging and deployment remain separately scoped actions; this document update authorizes none.
7. Product gates remain human decisions: visual direction, full UI flow acceptance, consequential policy and production release. Ordinary coding choices inside an authorized milestone are delegated; do not ask Aminu to manage every worker.

### What setup is needed, and what is optional?

- **GitHub repository:** versioned source, already configured as `hussain4real/SeeSPace`. This is not a Codex project or a runnable cloud environment. Recheck cloud GitHub access and selected branch/commit before starting a worker; a local remote URL alone proves neither.
- **Codex desktop project:** an app entry organizing chats around the local folder. The current project catalog has no SeeSpace entry. Adding the existing folder is recommended for organization, not required to create the repository or for the dot to inspect that folder. Do not create a duplicate repository.
- **Cloud environment:** reusable runtime/repository/tool setup. The catalog has a runnable default environment and other named environments, but no SeeSpace-specific environment. A cloud task can start with the default and access a permitted repository; a dedicated SeeSpace environment is recommended for repeatable PHP/frontend checks, not a prerequisite to local design.
- **Session/task:** one work conversation using a selected environment. Aminu does not need to start one manually for every phase; the dot can coordinate authorized tasks once access/setup is ready. Creating an app project alone does not install dependencies or transfer source.

Recommended one-time user setup: optionally add `/Users/amisha/www/seeSpace` as a local Codex project; before cloud implementation, use **Settings → Codex Cloud → Environments → Create environment**, select the existing SeeSpace repository, request compatible PHP 8.6 and the lockfile-compatible Node/toolchain, isolated test database, fake mail/queue/storage and frontend/browser test tools where supported. Review the setup report and publish only when checks work. The dot can prepare and guide this setup when authorized; there is no need for the user to hand-start a cloud coding session now. Supply GitHub access only if the picker actually requests it. Do not add production credentials or data.

Carry repository skills into cloud through the checked-out source if tracked; verify them there. Global Mac Impeccable/frontend-design/modern-web-guidance/TypeScript skills were found locally, not in a verified cloud installation. Keep M1/M2 local or explicitly authorize a supported skill installation/transfer; never promise automatic inheritance. The updated plan/prompts remain local edits until an authorized commit/push or file handoff makes them available to cloud workers.

Verification at this update: Mac and dot cloud computer listed connected; project and saved-cloud catalogs read; SeeSpace Git origin/HEAD/status, PHP CLI/requirement/CI workflow and relevant skill paths inspected. No cloud workspace was launched, no dependency/runtime changed, no project created, no implementation/tests/build run and no push performed. Product setup guidance checked against [official Cloud environments documentation](https://learn.chatgpt.com/docs/environments/cloud-environments) on 12 November 2026.
