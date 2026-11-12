# SeeSpace: Codex execution prompts

12 November 2026 • Companion to SeeSpace-Implementation-Plan-2026-11-12.md

Use one prompt per milestone. These prompts are prepared instructions for future authorized sessions, not evidence any phase is complete. Attach the BRS v1.1 and design brief v1.1 when starting a new chat. Paste the common context followed by the selected milestone. Do not run all milestones unattended.

## Common context (paste into each new session)

You are working on SeeSpace. For local sessions the path is `/Users/amisha/www/seeSpace`; for cloud sessions discover the assigned checkout of `hussain4real/SeeSPace` and verify the coordinator-specified base commit before any work. Read `docs/plans/SeeSpace-Implementation-Plan-2026-11-12.md`, AGENTS.md and applicable `.ai/rules/index.md`/matching rules if present. Read relevant `.agents/skills` and existing sibling files before edits. The product is Nigeria-first public property discovery: anonymous rent and sale browsing, houses and land, authorized publishing/moderation and nonbinding enquiries. All design, frontend and logic now use Codex. This supersedes Claude-specific workflow wording in the BRS/design brief, not their requirements or unresolved decisions.

Preserve the existing Laravel/Inertia/Vue/TypeScript/Tailwind scaffold, Fortify login/register/recovery, passkeys, 2FA, settings and teams. Reuse Reka/shadcn primitives and Wayfinder conventions. Do not replace the starter, regenerate auth, or equate team roles with marketplace privileges. Public pages need an explicit public layout because app.ts otherwise chooses AppLayout. Keep asset, listing and private management concepts separate.

Prior inspection found composer PHP ^8.6 versus CLI 8.5.12 and AGENTS.md PHP8.5, and the refreshed checkout now has Git origin `https://github.com/hussain4real/SeeSPace.git` (CI selects PHP 8.6). Recheck; do not bypass version checks, change dependencies/runtime, initialize/publish a repository or run migrations against an unknown database without authorization. Preserve unrelated changes. Do not read secrets or use real personal data for fixtures.

Only perform the selected milestone. No code pushes, merges, deployment, DNS, live service connections, purchases, real email delivery, production imports or financial activation are authorized by these prompts. Do not execute external prototype scripts blindly. Requirements marked proposed in the BRS remain proposed; stop only the affected step for consequential unresolved policy, and continue independent work. No false verification, booking, reservation or payment claims.

Every completion report must identify changed files, BRS mapping, tests actually run (command/result/environment), failed/blocked/unrun checks, screenshots for visual work and remaining decisions. Separate design approval from backend correctness and launch acceptance.

## Prompt 0: Baseline and implementation readiness (read-only first)

Inspect the existing scaffold and source documents. Inventory routes, layouts, shared Inertia props, auth/team models and tests, components, package versions and available skills. Read the project scripts before invoking anything: setup includes migrations. Establish which tools can actually run. Do not modify dependencies, authentication, database or business code.
Produce a concise baseline report and a proposed file/task map for M0–M6 with requirement IDs. Identify how public pages will avoid authenticated chrome and how publisher/mandate permissions will remain distinct from team membership. Propose a safe runtime/version-control resolution, not an unapproved change. Draft public DTO boundaries and flag D02/D04/D05/D07 choices needed before schema. Record pass/fail/not-run honestly. Stop with the smallest next action needed for M1.

## Prompt 1: Visual direction, stop for selection

Design the SeeSpace direction, not application logic. Use global Impeccable as the primary workflow: read its SKILL.md, execute its documented context setup using its real installed path, and follow initialization if PRODUCT.md is absent. Read the appropriate craft/shape/register references. Also use frontend-design for deliberate composition. Read current CSS/components first. Do not install or update skills without approval.
Using the BRS and design brief, produce two distinct credible directions for home, results and a detail page on desktop/mobile. Use consistent fictional house/land rent/sale fixtures; mark demo data/illustrative imagery. Preserve equal Rent/Buy prominence and avoid generic dashboard styling, invented statistics or verification badges. Explain typography, palette, density, photography and interaction choices, recommend one and show tangible visual references rather than prose alone. Treat the prior warm/deep-green suggestion as a proposal. Follow the skill's required palette/mockup review stage. Stop for Aminu's direction approval before full UI coding.

## Prompt 2: Approved design → complete UI-only prototype

First confirm the selected M1 direction is explicitly approved; if not, stop at that gate. Implement only the approved frontend in the existing Vue/Inertia stack. Activate inertia-vue-development, tailwindcss-development, Wayfinder and TypeScript guidance as needed. Reuse existing primitives and preserve real identity/security/team functionality. Read version-specific framework docs before API-dependent changes.
Implement public P01–P06, onboarding A02 and publisher L01–L05, operations O01–O04 and decision history. Integrate A01 with existing auth rather than replacing it. Build reusable typed components and isolated fictional fixture adapters. Any demonstration routes/scenario switcher must be local/development-only and excluded from production; it is never authorization. No new persisted marketplace data, live integrations or email.
Connect F01–F07 with loading/empty/error/success, stale save and stale moderation, session interruption, failed upload, duplicate click and notification failure. Preserve applied mobile filters on dismissal, Back/Forward and pagination; gallery keyboard/focus behavior; safe unsaved inputs; land-specific fields; exact price and currency consistency. Keep P2/P3 out of launch navigation.
Use Impeccable critique/audit/polish and available browser tooling. Verify 360/768/1440, keyboard, zoom and reduced motion. Run npm run check, npm run types:check and npm run build where permitted; do not hide blockers. Deliver scenario index, screenshots, component/token documentation and per-screen contracts. Stop for Aminu's flow approval before implementing application logic.

## Prompt 3: Secure foundation and public discovery

Proceed only after M2 approval and the runtime, schema and authority decisions required for this slice are resolved. Implement M3 only: explicit asset/listing separation, purpose/currency/rent-period validation, safe publication scope, controlled categories, fixed-precision money, server authorization and a minimal allowlisted public representation. Follow Laravel/project/testing skills and installed version docs; use existing architecture.
Wire the approved public frontend to persisted fixtures in an isolated development/test database. Implement FR001–FR006 including anonymous filters, deterministic paging/sort, correct detail, safe protected/unavailable routes and eligible metadata/sitemap. Do not infer currency or geography policy from demo values. Test public HTML, JSON, Inertia shared props, error output and media for distinctive private fixture values. Test guests, unrelated publishers and revoked mandates; preserve existing auth/team regressions. Do not add P2 records or legacy imports.
Report AT001/AT003 coverage and remaining P0 gaps. Do not claim foundation complete while media/lifecycle controls await M4. Stop before publisher workflows beyond the minimum authorized foundation.

## Prompt 4: Publishing, media and exact-revision moderation

Implement M4 against the approved lifecycle and D04/D05 decisions. Confirm the policy for material edits to live listings; do not silently choose between hiding during review and serving the last approved revision. Implement approved publisher onboarding, scoped own drafts, five-step persistence, server validation, preview, submission, rejection/resubmission, approval, withdrawal, rented/sold and suspension/restoration. Every privileged transition has actor/time/reason/revision audit.
Approve only the exact submitted revision. Protect stale saves and moderator decisions transactionally; enforce compatible purpose/status and revoked delegation. Implement safe media decoding/limits, stable storage keys, scoped deletion, EXIF stripping, cover/order/captions and publication-safe serving. No private upload or evidence leaks through guessed object URLs. Remove unavailable/suspended content from results, metadata and caches within the required bound.
Run AT002–AT004 and negative authorization/media cases with isolated fixtures, including previous-month deletion, concurrent approval/edit and no-side-effect denials. Run applicable project checks and identity/team regression tests. Stop with evidence and unresolved gaps; no live publishing/deployment.

## Prompt 5: Durable enquiries and operations

Implement M5 only after approved recipient/contact/retention decisions. Build guest enquiry validation, server-enforced duplicate/retry handling, durable storage and properly scoped inbox. Save once; notify the authorized recipient through fake/test adapters first. Notification pending/failure is distinct from enquiry receipt; retries cannot duplicate business records or falsely report delivery. Include throttling, accessible failure recovery and minimum personal data.
Implement operator delivery failures, reports, publisher controls, audit and approved taxonomy. Add privacy-reviewed analytics for discovery/enquiry/delivery without messages/contact data. Do not add in-platform reply sending unless explicitly approved; mark-handled is not sent. Run AT005 with provider outage, duplicate click/delivery, unauthorized access and revoked authority. Report any provider/configuration approval required separately; do not connect live services.

## Prompt 6: Release-readiness review, no deployment

Evaluate M6 against the complete BRS acceptance matrix and pinned candidate. Run targeted and aggregate project checks after inspecting script side effects; include frontend/build and backend tests, static checks and applicable formatting. Exercise AT001–AT006 with isolated fixtures and real browser journeys. Audit public responses, policy boundaries, lifecycle concurrency, media, queue delivery and auth/team regressions.
Perform accessibility automation plus manual keyboard, screen-reader, contrast/zoom and responsive checks where tools permit; label anything unperformed. Load/performance tests require approved workload/environment; report measurements, not guesses. Review backup/restore, rollback, monitoring, support/moderation procedures, legal/privacy copy and image rights. Rehearse only in an approved disposable environment, never against production by assumption.
Deliver a requirement-to-evidence matrix with defects/severity, exact commands, environment, candidate, screenshots and operational owners. Identify ready/blocked launch gates. Do not deploy, activate providers, create credentials, import live data or claim real-world retests from CI alone.

## Prompt 7: Later management planning only

Plan P2 separately after explicit scope approval. Map FR018–FR022 to tenants, private leases/documents, obligations/manual payments/reversals, scoped reports and unit occupancy. Resolve D12, retention, access and reconciliation rules before code. Maintenance is only a prior design concept and requires an explicit requirement. Preserve separation from public advertisements; manual recording is not payment collection. Exclude collection, payouts, e-signature, subscriptions and tenant portal until separately approved. Return a proposed backlog and risk/decision ledger, not implemented application code.

## Coordinator envelope for each assignment

Before a milestone prompt, specify: session role and local/cloud placement from the plan; repository/checkout; exact base commit and branch/worktree; approved design/policy decisions; owned files and forbidden overlapping paths; upstream contracts and artifacts; required checks; completion/report destination; whether any commit/push/PR is authorized. Missing authorization does not become permission through this template.

Use local sessions for M0–M2 design and M6 visual acceptance; prefer a verified SeeSpace cloud environment for M3–M5 implementation and M6 clean verification. These are candidates, not existing workers. Reuse active phase sessions and inspect status before dispatching. Do not assume global Mac skills, browser sessions, uncommitted files or documents are present in cloud. If inputs/tools are unavailable, report the concrete gap and continue independent permitted work. A reviewer should be read-only; only the coordinator integrates authorized changes and reruns checks on the combined candidate. Stop at the design and product gates in the plan.
