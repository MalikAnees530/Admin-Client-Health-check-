# Brainstorming Brief: Client Project Health-Check Portal

> Use with: `superpowers:brainstorming` → then `superpowers:writing-plans` → then `superpowers:subagent-driven-development`
> Project root: `C:\Users\L13\Documents\VS-CODE-Insider\Client_Project_Healthcheck`
> OS: Windows (PowerShell). Assume Docker Desktop is available for local PostgreSQL unless I say otherwise.
> Installed skills directory: `C:\Users\L13\.claude-second\skills`
> GitHub repository (public, `main` branch, currently only `README.md`): https://github.com/MalikAnees530/Admin-Client-Health-check-

---

## 0. How I want you to run this session

1. **Explore first.** Before asking anything, inspect the current project folder (files, `package.json`, git status, any existing config) and tell me in 3–5 lines what already exists. Also check whether this folder is a git repository and whether its `origin` remote points to my GitHub repository (Section 2). If it is not connected, explain the safest way to connect it and ask me before running any git command that changes remotes, history or branches. Do not scaffold or write any code in this session.
2. **Check the installed skills** (Section 1) and tell me in a short list which ones you will use during this brainstorming session and why. Load a skill only when its topic comes up; do not load them all at once.
3. **Use this brief as the source of truth**, but treat it as a starting point, not a final spec. Where my description and my whiteboard/notebook sketches disagree, point it out and ask me which is correct (see Section 11).
4. **Ask me one question at a time**, prefer multiple-choice where possible, and always give me your recommended option with a one-line reason.
5. **For every major decision, propose 2–3 approaches with trade-offs** and a recommendation.
6. **Present the design in sections** (roughly 200–300 words each) and wait for my confirmation before moving on.
7. **Apply YAGNI**: separate what is v1 (MVP) from v2+ explicitly. Do not silently drop anything I listed; move it to a "later" phase and say so.
8. **TDD is non-negotiable** (Section 9). The design must make every feature testable before it is built.
9. At the end, write the validated design document to the location the brainstorming skill specifies, commit it, and tell me it is ready for `superpowers:writing-plans`.

---

## 1. Installed skills: when and how to use them

I have a large library of Claude Code skills installed. Use any of them **whenever they are relevant** to the decision or topic at hand, during this brainstorming session and in the design document you produce.

### 1.1 Rules for using skills
- **Superpowers drives the process.** `superpowers:brainstorming` → `superpowers:writing-plans` → `superpowers:subagent-driven-development` is my workflow. Do **not** invoke other process or planning frameworks that would compete with it, including any `gsd-*`, `gstack-*` (except where listed below), `orch-*`, `sparc-methodology`, `speckit-*`, `make-plan`, `plan-orchestrate`, `blueprint`, `handoffplan`, `ralphinho-rfc-pipeline`, `autonomous-loops`, `continuous-agent-loop`, `swarm-*`, `hive-mind-advanced`, `dev-team`. Use domain/knowledge skills to inform decisions, not to replace the superpowers steps.
- **Verify before you invoke.** Confirm the skill exists and read its description before using it. If two skills overlap (e.g., `shadcn` and `shadcn-ui`), read both descriptions and pick the better fit, or combine them, and tell me which you chose.
- **Skip irrelevant stacks.** Ignore skills for other languages/frameworks (Android, iOS/Swift, Kotlin, Django, Laravel, Rails, Spring, Vue, Angular, Flutter, Go, Rust, etc.).
- **Prefer up-to-date docs over memory.** Use `context7-mcp` / `context7-cli` / `find-docs` / `documentation-lookup` to check current stable versions and APIs (Next.js, Tailwind, shadcn/ui, ORM, auth library, Vitest, Playwright) before recommending them.
- **Record skill usage in the design.** The design document must include a **Skills Map** (Section 12) stating which skill should be used for each phase/task type, so `writing-plans` can reference it in each task and subagents load the right skill during implementation.

### 1.2 Skills relevant to this project (use when the topic comes up)

**Requirements, IA and UX (brainstorming phase)**
- `information-architecture`, `navigation-patterns`, `user-flow-diagram`, `wireframe-spec`, `ux-spec`: deciding the tab/navigation model (Section 7) and screen list.
- `dashboard-builder`, `data-visualization`, `metrics-definition`, `analytics-interpretation`: metric sets per channel, chart design, baseline vs. projection views.
- `ad-attribution`, `seo-local-business`: sanity-check Ads, SEO and GBP metric definitions.
- `form-design`, `loading-states`, `error-handling-ux`, `pagination`, `search-ux`: forms, empty/loading/error states, daily ads table.
- `the-fool` or `grill-me`: stress-test the design before finalising (use once, near the end).
- `architecture-decision-records`: record each major decision (ORM, auth, navigation model, data-entry method) as an ADR in the design.

**Architecture**
- `nextjs-developer`, `nextjs-mastery`, `web-frontend-architecture`, `react-best-practices`, `react-patterns`, `typescript-pro`: App Router structure, Server Components vs. Client Components, Server Actions.
- `clean-architecture`, `domain-driven-design`: keeping domain logic (baseline, projections, quarters, health status) pure and testable.
- `api-design`, `backend-patterns`, `error-handling`: server boundary, validation, error model.
- `architecture-diagram`: system and data-flow diagrams in the design doc.

**UI stack**
- `shadcn`, `shadcn-ui`, `tailwind-theme-builder`, `frontend-design`, `ui-ux-pro-max`, `design-system`: component choice, theme tokens, consistent admin UI.
- `accessibility-wcag`, `frontend-a11y`, `responsive-design`: accessibility and responsive rules.

**Database**
- `postgres-patterns`, `postgres-pro`, `sql-pro`: schema design, constraints, indexes, time-series metric storage.
- `database-migrations`: migration strategy.
- `prisma-patterns`: only if Prisma is chosen over Drizzle.
- `postgres-optimization`, `database-optimizer`: indexes for (client_id, date) queries.

**Auth and security**
- `auth-flow`, `authentication-patterns`: admin-only login, sessions, first-admin seeding.
- `security-hardening`, `secure-code-guardian`, `security-review`: headers, rate limiting, authorization on every server action.

**Testing (TDD)**
- `tdd-workflow`, `tdd-feature`, `tdd-mastery`: red → green → refactor discipline per task.
- `testing-strategies`, `test-spec`: overall test pyramid and test-case lists per feature.
- `vitest`, `react-testing`: unit and component tests.
- `integration-test-scaffold`, `test-data-factory`: real-Postgres integration tests and factories.
- `playwright-e2e`, `playwright-expert`, `e2e-testing`: end-to-end flows.
- `coverage-ratchet`: coverage thresholds that only go up.

**Git and GitHub**
- `git-workflow`, `github`, `github-workflow-automation`: branching, PRs, branch protection, GitHub Actions.
- `security-scan`: secret scanning and dependency checks for a public repository.

**DevOps and production**
- `docker-patterns`, `docker-best-practices`: local Postgres via Docker Compose on Windows.
- `ci-cd-pipelines`, `ci-cd-setup`: CI running lint, typecheck, tests, build.
- `deployment-patterns`, `deploy-to-vercel` (if Vercel is chosen): deployment and rollback.
- `logging-setup`, `error-monitoring`, `monitoring-observability`: logs, Sentry, health checks.
- `production-audit`, `release-it`: final production-readiness review.
- `data-export`: later phase (CSV/PDF client reports).

**Reviews during implementation (for the plan, not this session)**
- `code-reviewer`, `security-review`, `verification-loop`: reviews and verification gates between tasks.

---

## 2. Repository, Git and GitHub workflow

- **Remote:** https://github.com/MalikAnees530/Admin-Client-Health-check- (public, default branch `main`, one commit containing only `README.md`).
- **Local folder:** `C:\Users\L13\Documents\VS-CODE-Insider\Client_Project_Healthcheck`. The local folder name and the repo name differ; that is fine, but confirm the local folder tracks this remote.
- **Connecting local to remote:** if the local folder has no git history yet, propose either cloning the repo into it or `git init` + adding the remote + pulling `main`. If the local folder already has its own commits, warn me about unrelated histories and propose the safest option. Ask me before running anything.
- **The repo is public.** Treat this as a hard constraint:
  - `.env*` files (except `.env.example`), database dumps, real client names, real client data, credentials and API keys must never be committed. Set up `.gitignore` in Phase 0, before any other file.
  - Seed data and test fixtures must use fake clients only (e.g., "Acme Dental", "Demo Bakery"), never "iSmash" or "Abdullah.com" or any real client.
  - Propose a secret-scanning safeguard (e.g., GitHub secret scanning / push protection, and optionally a pre-commit check).
  - Ask me whether I want to make the repository private before real work starts.
- **Branching:** propose a strategy that fits superpowers (it may use git worktrees and feature branches during `subagent-driven-development`). Recommend: protected `main`, one feature branch per phase or task group, pull requests with CI required to pass before merge. Ask me whether I want PRs or direct merges, since I am a solo developer.
- **Commits:** small commits per TDD cycle (test → implementation → refactor), with a consistent message convention (propose Conventional Commits).
- **GitHub Actions CI:** lint, typecheck, unit, integration (Postgres service container), e2e (Playwright), and build on every push and pull request.
- **Repo hygiene:** replace the placeholder `README.md` with real setup instructions for Windows, add a repository description, and consider Dependabot for dependency updates.
- Relevant skills: `git-workflow`, `github`, `github-workflow-automation`, `ci-cd-setup`, `ci-cd-pipelines`, `security-scan`.

---

## 3. What I am building

An **admin-only web portal** for my agency to track the health of every client project: what the client's performance was before we started (baseline), what we promised (projections), what is actually happening now (actuals, including a daily ads report), and the commercial and relationship details of each engagement (onboarding date, POC, billing, contract value, services, quarterly milestones).

The core question the portal must answer at a glance: **"For client X, are we on track against baseline and projection, and what have we committed to this quarter?"**

---

## 4. Source material (transcribed from my whiteboard and notebook)

**Whiteboard:**
- Heading "Clients" → "Client Names" → example client "iSmash" → a box representing that client's project details.
- A "Selection" dropdown with a checkmark at the top (I read this as a client selector).
- Left side: "Avg. 3 months" → example client "Abdullah.com" → "Meta" with two toggles **BP** (Baseline Performance) and **PN** (Projected Numbers), and a line chart with a solid rising line (actuals) and dashed horizontal lines (baseline / projected).
- From the project box: "Baseline Performance Numbers" and "Projected Numbers", connected to channels **Ads, Social, SEO**, where SEO branches to **Org, Paid** and **GBP** (Google Business Profile).
- Right side, linked to the project box: **Onboarding Date** (with a box labelled "Zero" pointing at it), **POC Details** (Contact #, Email, Name, with a "+" add button), **Billing cycle**, **Contract value**, **Services agreed** (marked with `*` and visually connected to the channel list), **Milestone** (with "+") → Q1, Q2, Q3, Q4.

**Notebook:**
- "For each client we have: Baseline performance, Projected number, Date — for past 3M."
- Same tree: Clients → Client names → iSmash → project details → onboarding date, POC details (contact, email, name, +), billing cycle, contract value, services agreed, milestones (+) → "Quarter Base" Q1–Q4.

**My interpretations (please confirm or challenge each):**
- **Baseline = the average of the 3 months before onboarding**, per channel/metric.
- **"Zero" = onboarding date is Day 0**; everything (quarters, projections, progress) is measured relative to it.
- **Quarters are relative to onboarding, not calendar quarters**, which is why I mentioned Q5 (months 13–15 of the engagement). The number of quarters should be open-ended, not fixed at 4.
- **Services agreed controls which channels appear** in Baseline/Projected for that client (if a client only bought SEO-Org and GBP, Ads/Social tabs are hidden or disabled).
- **BP / PN are toggles on the chart** so the admin can overlay baseline and/or projection against actuals.

---

## 5. Users and access

- Only admins can access anything. No public pages except login.
- No client logins in v1.
- Ask me: single admin or multiple admins? Do we need roles (e.g., Super Admin vs Admin/Viewer) now or later?
- Admin can add, edit, archive and delete clients (recommend soft-delete/archive with confirmation; ask me).

---

## 6. Functional scope

### 6.1 Clients (main tab)
- List of all clients (search, filter by status/service, sort), with a quick health indicator per client.
- Client selector (the whiteboard "Selection" dropdown) to jump between clients.
- Add / edit / archive / remove client.
- Each client opens a **Client Project Details** view.

### 6.2 Baseline Performance Numbers (per client)
- Channels and sub-channels:
  - **Ads** (ask me which platforms: Meta, Google Ads, others)
  - **Social** (ask me which platforms: Instagram, Facebook, LinkedIn, TikTok, etc.)
  - **SEO** → **Organic**, **Paid**, **GBP**
- Every channel and sub-channel must be fully working: its own metric set, data entry, display and chart. No placeholder tabs.
- Propose a default metric set per channel for me to approve, for example:
  - Ads: spend, impressions, reach, clicks, CTR, CPC, conversions, CPA, ROAS
  - Social: followers, reach, impressions, engagement, engagement rate, posts published
  - SEO Organic: organic sessions, Search Console clicks, impressions, avg. position, ranking keywords, backlinks
  - SEO Paid: (clarify with me how this differs from Ads; it may mean paid search)
  - GBP: profile views, searches, calls, direction requests, website clicks, reviews count, avg. rating
- Design question: fixed metric definitions in code vs. admin-configurable metric definitions per channel. Recommend one.

### 6.3 Projected Numbers (per client)
- Targets per channel/metric over the engagement.
- Ask me how projections are produced: manually entered by admin, formula-based (baseline × growth %), or both.
- Ask me the projection granularity: monthly targets, quarterly targets, or a single end target with interpolation.

### 6.4 Charts and time ranges
- Range selector: **Past 3 months, 6 months, 1 year** (ask if I also want custom range and "since onboarding").
- Chart shows actuals as a line, with **Baseline** and **Projected** as toggleable overlays (BP / PN toggles from the whiteboard).
- Per channel and sub-channel, with a metric picker.
- Summary cards above the chart: current value, vs. baseline (% change), vs. projection (% of target), trend.
- Use shadcn/ui charts (Recharts) unless you have a strong reason otherwise.

### 6.5 Daily Ads Report (inside Client Project Details)
- Daily rows per platform (and optionally per campaign): date, spend, impressions, clicks, conversions, etc.
- Table view with date filter, totals, and a chart.
- Ask me how data gets in: manual entry, CSV upload, or API integration (Meta Marketing API / Google Ads API). Recommend manual + CSV in v1 and API sync in a later phase, but let me decide.
- Daily ads data should feed the "actuals" for the Ads channel charts so data is not entered twice.

### 6.6 Onboarding Date
- Per client; acts as Day 0 for baseline window, quarters and projections.
- Changing it must recalculate dependent views; ask whether that should require confirmation.

### 6.7 POC Details
- Multiple contacts per client (the "+" button): name, contact number, email (ask about role/designation and "primary contact" flag).
- Add, edit, remove. Validate email and phone formats.

### 6.8 Billing Cycle
- Cycle type (monthly / quarterly / yearly / custom), start date, billing day, next billing date (computed).
- Ask if v1 needs invoice/payment tracking or only the cycle information.

### 6.9 Contract Value
- Amount, currency (ask which currencies; ask about PKR/USD), contract start/end dates, monthly retainer vs. one-off.
- Store money safely (integer minor units or `numeric`, never float).

### 6.10 Services Agreed
- Selection from the channel/sub-channel catalogue (Ads, Social, SEO-Org, SEO-Paid, GBP), plus optional notes/scope per service.
- Drives which channels are shown in Baseline/Projected (confirm with me).

### 6.11 Milestones
- Grouped by **engagement quarter** (Q1, Q2, Q3, Q4, Q5, … open-ended, relative to onboarding date).
- Add milestone via "+": title, description, related service/channel, target metric (optional), due date, status (planned / in progress / done / missed).
- Quarter progress summary (x of y milestones done).

### 6.12 Health indicator (my project is called "health check")
- Propose a simple, explainable rule for On Track / At Risk / Off Track per client, based on actuals vs. projection and overdue milestones. Ask me to approve the thresholds. Keep it rule-based, not magic.

---

## 7. Navigation / information architecture — IMPORTANT DECISION

My written description lists Onboarding Date, POC, Billing Cycle, Contract Value, Services Agreed and Milestones as **separate top-level tabs (tab 2 to tab 7)**. My whiteboard and notebook show them as **fields inside each client's project details**.

Present 2–3 options, for example:
- **A:** Top-level sidebar with only "Clients" (+ Dashboard, Settings); each client page has inner tabs: Overview, Performance (Baseline/Projected), Daily Ads Report, Onboarding & Contract, POC, Billing, Services, Milestones.
- **B:** Top-level tabs for each area (Clients, Onboarding, POC, Billing, Contract, Services, Milestones), each showing a cross-client table filtered by the client selector.
- **C:** Hybrid: per-client inner tabs (A) plus portfolio-level views (e.g., "all upcoming billing dates", "all milestones due this quarter").

Give me your recommendation and ask me to choose before designing screens. (Use `information-architecture` and `navigation-patterns` here.)

---

## 8. Tech stack (fixed) and decisions to propose

**Fixed:**
- Next.js (latest stable, App Router, TypeScript strict mode). Verify the current stable version with the docs skills instead of assuming.
- Tailwind CSS (latest; check v4 setup compatibility with shadcn/ui).
- shadcn/ui components (including data table, forms, dialogs, tabs, charts).
- PostgreSQL.

**Decide with me (propose options + recommendation):**
- ORM / query layer: Drizzle vs. Prisma.
- Auth for admin-only access: Auth.js vs. Better Auth vs. simple credentials + session. Include password hashing, session expiry, login rate limiting, and how the first admin is created (seed script, not a public sign-up page).
- Data mutations: Server Actions vs. Route Handlers (or both), and where validation lives (Zod schemas shared between form and server).
- Forms: react-hook-form + Zod.
- Date handling and timezone strategy (store UTC, display in my timezone; ask me which).
- Local Postgres on Windows: Docker Compose (recommended) vs. native install.
- Hosting for production: e.g., Vercel + managed Postgres (Neon/Supabase) vs. VPS with Docker. Ask me.

**Architecture expectations:**
- Clear folder structure (feature-based modules recommended), shown as a tree in the design.
- Domain logic (baseline averaging, projection calculations, quarter derivation from onboarding date, health status) in **pure, framework-independent functions** so it is unit-testable.
- Database access behind a thin data layer; UI never queries the DB directly.
- Full database schema in the design: tables, columns, types, relations, indexes, constraints, cascade/soft-delete behaviour. At minimum consider: admins/users, sessions, clients, contacts (POC), contracts, billing_cycles, services catalogue, client_services, channels/sub-channels, metric definitions, baseline values, projections, actual metric values (time series), daily_ads_reports, milestones, audit_log.

---

## 9. Test-first development (mandatory)

Every feature in the plan must follow **red → green → refactor**:
1. Write the failing test first.
2. Run it and confirm it fails for the expected reason.
3. Write the minimum code to make it pass.
4. Run all tests and confirm green.
5. Refactor, keep green, commit.

The design must define the testing strategy and tooling, for example:
- **Unit:** Vitest for domain logic (baseline averages, projection math, quarter calculation incl. Q5+, health status rules, money formatting, date ranges 3M/6M/1Y).
- **Component:** Vitest + React Testing Library for forms, tabs, tables, chart toggles.
- **Integration:** data layer and server actions against a **real test PostgreSQL database** (Docker / Testcontainers), with migrations applied and data reset between tests. No mocking of the database for integration tests.
- **End-to-end:** Playwright for critical flows: admin login, unauthenticated redirect, create client, add POC, set onboarding date, enter baseline and projections, view chart with BP/PN toggles and range switch, add daily ads rows (and CSV import if in scope), add milestone in Q1 and Q5, archive client.
- **Auth/security tests:** every protected route and server action rejects unauthenticated requests.
- Test data factories / seed fixtures.
- Coverage target (propose one, e.g., ≥ 80% on domain and data layers), enforced in CI.
- Tests must run with one command locally and in CI.

---

## 10. Production-readiness (beginning to production)

The design must cover the full path, broken into phases, for example:
- **Phase 0 – Foundation:** connect local folder to the GitHub repo, `.gitignore` first, scaffolding, TypeScript strict, ESLint/Prettier, test tooling, Docker Postgres, env validation, GitHub Actions CI green on an empty app, real README.
- **Phase 1 – Auth & shell:** admin login, protected layout, sidebar/navigation, client selector.
- **Phase 2 – Clients & project details:** CRUD, onboarding date, POC, billing, contract, services.
- **Phase 3 – Performance:** metric definitions, baseline entry, projections, charts with ranges and BP/PN toggles.
- **Phase 4 – Daily ads report:** entry, table, totals, (CSV import), feeding actuals.
- **Phase 5 – Milestones & health status.**
- **Phase 6 – Hardening & deploy.**
- **Later:** API integrations (Meta, Google Ads, GA4/Search Console, GBP), exports (PDF/CSV client report), notifications, client-facing read-only view.

Production concerns to address in the design:
- Environment variables validated at startup; `.env.example` committed, secrets never committed.
- Database migrations (versioned), seed script, backup/restore approach.
- Input validation on every server boundary; authorization check on every server action.
- Security headers, CSRF considerations, login rate limiting, secure cookies.
- Audit log of who changed what (create/update/delete on client data).
- Error handling: error boundaries, user-friendly messages, server-side logging; consider Sentry.
- Loading/empty/error states for every screen.
- Accessibility (keyboard navigation, labels, contrast) and responsive layout (desktop-first, usable on tablet).
- Performance: pagination for daily ads data, DB indexes on (client_id, date) style queries.
- CI on GitHub Actions: lint, typecheck, unit, integration, e2e, build on every push/PR; `main` protected so failing checks cannot merge.
- Public-repo safety: no secrets or real client data in git history; secret scanning enabled.
- Deployment and rollback procedure, plus a README for setup on Windows.

---

## 11. Open questions to resolve with me (ask one at a time, highest impact first)

1. Navigation model: A, B or C from Section 7?
2. Are my interpretations in Section 4 correct (baseline = 3-month pre-onboarding average; onboarding = Day 0; quarters relative to onboarding; services drive visible channels)?
3. How does performance data get in for v1: manual entry, CSV import, API, or a mix?
4. Which platforms exist under Ads and under Social? What exactly is "SEO → Paid" vs. "Ads"?
5. Approve or edit the default metric set per channel; fixed vs. configurable metrics?
6. How are projections created and at what granularity?
7. Health status thresholds.
8. Single vs. multiple admins; roles needed?
9. Currencies and timezone.
10. Billing: cycle info only, or invoice/payment tracking too?
11. Delete behaviour: archive (soft delete) vs. hard delete.
12. Hosting target for production.
13. Keep the GitHub repository public, or make it private?
14. Pull requests with required CI checks, or direct merges to `main`?

---

## 12. Expected output of this brainstorming session

A validated design document that contains:
- Goal, scope, and explicit v1 vs. later list.
- Confirmed answers to all open questions.
- ADRs for major decisions (ORM, auth, navigation model, data-entry method, hosting).
- Information architecture and screen list with what each screen shows.
- Full database schema and relations.
- Folder structure.
- Git/GitHub workflow: how the local folder connects to the repo, branching, commit convention, CI workflow jobs, branch protection, and public-repo safety rules.
- Domain logic definitions with worked examples (e.g., baseline calculation, quarter for a given date, health status).
- Testing strategy per layer, with the list of test cases for each feature.
- Phased delivery from foundation to production, each phase ending in a working, tested, deployable state.
- **Skills Map**: a table of phase / task type → installed skill(s) to load (e.g., schema tasks → `postgres-patterns` + `database-migrations`; UI tasks → `shadcn` + `frontend-design`; every task → `tdd-workflow`; e2e tasks → `playwright-e2e`; deploy → `deployment-patterns`). Only list skills you confirmed exist.
- Risks and assumptions.

Then commit it (and push to the GitHub repository only after asking me) and tell me to run `superpowers:writing-plans`. The implementation plan should break each phase into small TDD tasks (test first, then code) suitable for `superpowers:subagent-driven-development`, and each task should name the skill(s) from the Skills Map that the subagent must use.
