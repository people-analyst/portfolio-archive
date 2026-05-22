# Mike West — Software Portfolio

*As of May 2026. Most repositories private; this document is the public-facing summary.*

**Contact**: mike@peopleanalyst.com · 469.406.4699 · Pittsburgh, PA · linkedin.com/in/michaelcwest · peopleanalyst.com

---

## Overview

Since 2022, I have designed and built a portfolio of TypeScript + Python applications, as solo founder of **PeopleAnalyst** (consulting since 2012). What began as a niche consulting practice has evolved into an AI-native product ecosystem applying systematic decision science to progressively broader domains — from enterprise HR analytics to scholarly measurement registries, from intentional baby naming to contemplative materials for being human, from fantasy-football intelligence to an AI-assisted authorship substrate. The common thread is pairing multi-source data with calibrated human inputs to produce better experiences and better decisions. Some of that data is AI-derived from large text and visual corpora; some is drawn from canonical existing sources. AI enables rapid classification of elements found across either, which exposes reality to codification and analysis — enabling new insight, and with that, fresh opportunity.

The ecosystem is architected as a **hub-and-spoke pattern** with a **substrate-first posture**: capabilities live in shared platform packages and reusable cross-portfolio services (substrate), while products (verticals) compose against typed contracts rather than re-implementing primitives. Cross-cutting concerns — PII anonymization, metric calculation engines, survey delivery, adaptive measurement, probabilistic forecasting, microservices and MCP-callable contracts, authored-writing substrates, organizational-measurement registries — live as reusable platform services consumed by multiple verticals. A 2026-05-21 portfolio reconciliation collapsed 12 previously-standalone repos into the People Analytics Toolbox monorepo as `apps/<spoke>` packages, leaving the active portfolio at 13 GitHub repos: 1 hub, 3 tools, and 9 expressions (live or in-flight products).

---

## Product Line 1 — People Analytics Platform

A complete AI-native people analytics infrastructure: measurement, decision science, survey delivery, data engineering, behavioral diagnostics, and a compensation-decision operating system. Built solo, 2022–present. Two live front-doors plus the substrate hub.

### People Analytics Toolbox · `people-analytics-toolbox` · live at peopleanalyticstoolbox.com

**The substrate.** Independently-versioned analytical microservices for people analytics — psychometric diagnostics, preference modeling, privacy primitives, segmentation, statistical enrichment, compensation logic, decision forecasting, metadata-grounded codegen — deployed as a single Next.js application and exposed over two transports: **HTTP for engineers, MCP (Model Context Protocol) for AI agents**. One Vercel project, one Supabase project. Consumer apps vendor only the typed Zod contracts; the algorithms stay in the toolbox.

**Eight live spokes:**

- **`reincarnation`** — Adaptive psychometric diagnostic engine. IRT a-parameter-weighted item selection with Cronbach α tracking. Pool-based item lifecycle. **Outlier:** RID/SID (Respondent-ID / Study-ID) separation lets a single question participate in many studies without confounding — item-response statistics accumulate across studies, and adaptive selection uses the full evidence to choose the next question. Commercial survey platforms either run studies in silos (no cross-study learning) or pool naïvely (lose study-level integrity). This architecture preserves both.
- **`preference-modeler`** — Likert/multi-choice/free-text plus MaxDiff, conjoint, penny-allocation, paired-comparison. BIBD-balanced task generation. MNL utility estimation via Newton-Raphson. Real choice-theory methods implemented as a service API, not bolt-on analytics.
- **`data-anonymizer`** — Cross-cutting privacy. PII detection, deterministic HMAC tokenization (same input → same hashed output across runs), k-anonymity min-N gate, substitution-strategy registry. Privacy as a service, not a setting — every spoke that surfaces team-level rollups calls `min-N-check` before responding.
- **`segmentation-studio`** — HRIS canonical-field normalization with 35-field priority catalog. Multi-membership cohort resolution. OneModel adapter. Recipes. Pack publishing. Handles the reality that every enterprise has inconsistent job codes, titles, and leveling.
- **`calculus`** — Statistical enrichment, anomaly detection, time-series imputation. Metric × segment × period combinatorial factory. **Auto-selects Wilson / t-interval / normal CI by data shape** — the right confidence-interval method by data, not by convention.
- **`anycomp`** — Compensation models, market band math, stateless evaluation, auditable cycle runs. Merit/equity/market-pricing/total-rewards decisions as a coherent product surface.
- **`forecasting`** — Monte Carlo simulation, **EVPI** (Expected Value of Perfect Information), **discrete EVSI** on aligned-chance decision trees. **Outlier:** formal VOI reasoning in HR tooling is essentially absent commercially; this implements the academic framework as production software. Done well, VOI kills more studies than it justifies — its principal virtue.
- **`Conductor`** — **Metadata-grounded SQL/Python codegen.** The model sees schema, field semantics, and canonical metric definitions, so queries it produces are construct-honest by construction. Bridges the gap between an AI writing queries and an AI writing queries that respect what the constructs are supposed to mean.

**Plus one reserved namespace** (`job-family-agent`, canonical home in meta-factory-prod) and a **VoI capability** lifted into the toolbox 2026-05 at `src/lib/voi/` with a principia-prior adapter.

**Chat-orchestration / MCP-gateway stack** shipped 2026-05: durable conversation history for `/admin`, SSE streaming, chat-turn → runPlan + composite adapter, intent-router catalog grounded to the live MCP registry, MCP gateway as primary dispatch (stateless — kills cross-lambda session-affinity flakes), plan-runner wizard pause-and-resume. **9 new spoke scouts** scaffolded (PAT-D1..D9: workforce-planning, survey-orchestrator, program-evaluation, network-analysis, factor-models, RBAC, ops-console, insight-sprint-studio, org-health-review) — ready for build dispatch when prioritized.

Stack: Next.js 16 + TypeScript + Tailwind 4 + Zod + drizzle-orm + Supabase Postgres + Vercel Fluid Compute + Model Context Protocol.

### Performix · `Performix` · live at performix.app

**Protected feedback and performance intelligence platform** — surfaces what employees can observe but cannot safely say, scores team-level Capability/Alignment/Motivation/Support (CAMS), and renders one binding-constraint card per team. **Precompute-and-playback architecture** — the iTunes of analytics, not a dashboard. **First external MCP consumer** of the People Analytics Toolbox (PFX-30, 2026-05-11) — vendors typed Zod contracts for reincarnation (adaptive measurement), data-anonymizer (suppression gate), segmentation-studio (cohort resolution), and calculus (small-N confidence intervals) rather than re-implementing them.

**Outliers:**
- **Protected feedback as a substrate primitive, not a privacy setting.** Min-N enforcement, small-cell suppression, comment redaction, identity-risk scoring, role-based visibility, and safe aggregation all live in the gate every Insight passes through before it reaches storage. The player never has access to anything that has not been suppression-checked.
- **CAMS as the binding-constraint diagnostic — not a dashboard of metrics.** The output is one card per team naming the dimension that is currently starving the system. Capability/Alignment/Motivation/Support; whichever is lowest is the constraint; that constraint is what to act on. Capability alone never produces realized performance.
- **Safe AI Insight Interpreter** at the interpretation layer, never the headline — summarizes patterns, drafts leadership communications, flags weak evidence, respects min-N and role-based visibility. Hard constraints: never expose raw responses; never infer who said what; never generate individual employee scores from protected feedback.

Stack: Next.js 16 + React 19 + TypeScript + Zod + drizzle-orm + Postgres + Tailwind 4 + Vercel + Model Context Protocol.

### Principia · `principia` · live at peopleprincipia.com

**The continuously-updated, source-graded, citation-verified, Bayesian-prior-bearing registry of organizational science** — a survey-not-original-research curation layer that sits on top of meta-factory's extraction pipelines and feeds canonical priors to the rest of the portfolio over a versioned REST + MCP contract.

**Outliers:**
- **Continuous citation-verified curation, not point-in-time handbook synthesis** — the registry refreshes as the literature does, with provenance preserved end-to-end.
- **Source grading as a first-class field on every claim** — `StudyQualityGrade` lives in the schema, so downstream consumers can weight evidence rather than treat all citations equally.
- **Bayesian-prior bearing** — canonical priors are a first-class output of the registry, not a downstream interpretation; the rest of the portfolio vendors typed priors instead of re-fitting from scratch. **First live CanonicalPrior** is engagement → task performance (k=3, synthesized from Corbeanu 2023 + Neuber 2021); engagement-survey v1.1 promoted 8 FILL markers to live priors.
- **CanonicalTheoreticalModel + instrument-equivalence networks** — explicit modeling that the same construct gets measured by different instruments that should be calibrated against each other, not treated as separate variables.
- **Validity-decay + MethodologyCritique + cultural sub-priors** — the registry doesn't pretend universality where the literature doesn't support it.
- **Book-build orchestrator** — the registry contents compose into "The Principia of Organization Measurement" via directive expansion + appendix auto-builders + XeLaTeX/HTML5/APA-7 templates. The registry is its own primary source.

Stack: TypeScript + Next.js 16 + Node.js + Zod + Model Context Protocol + Vercel + `@people-analyst/measurement-core` (the canonical-vocabulary npm package consumed by the toolbox).

---

## Product Line 2 — Adjacent consumer + cultural products

Applications of the same systems-thinking + AI-integration approach to domains outside enterprise HR. Proof the patterns generalize across audience shape and product register.

### Vela · `vela` · live at vela.study

**A platform about what it is to be human** — built to help people surface and replace the belief-rooted thoughts and emotional patterns that work against their lives and communities with ones that work for them. Vela began as a contemplative figurative-art platform and has broadened into a substrate that brings together the materials that have always taught us what it is to be human: figurative art, longform writing, the religious and contemplative traditions, emotional engagement, association with others, the act of making something rather than only consuming it. Underneath all of it: the bet that a single adaptive substrate can compose those materials into a sustained practice.

**Live surfaces:**
- **385 active curated works** sourced from museum APIs (Art Institute of Chicago, Metropolitan Museum, BnF, Smithsonian, Europeana, Rijksmuseum) under full attribution and license discipline.
- **Reincarnation engine** — per-user desire scoring with RID/SID adaptive measurement and visual-rhyme sequencing; first production batch shipped.
- **Five-layer Written System** — analytical essays, **Mosaic** (1,353-passage testimony corpus), fiction, audio readings, submissions — paced per-user (each reader's magazine begins when they arrive, not on a calendar).
- **Narrative Intelligence Platform** — generalizes the Mosaic engine into a three-domain spine (lived / fiction / research); five admin surfaces deployed.
- **Artist Studies** as the flagship editorial arc pattern — Warhol shipped (10 ASNs, Virtual Docent, Pittsburgh walking tour); Schiele/Klimt/Sargent staged.
- **Penwright Pennebaker Exercise Studio** + **FRAME-REFRAME triage instrument** — sub-surfaces inside Vela's authorship substrate.
- **Bible-translation Phase 1** — one of the contemplative-text translation projects; treats translation as an editorial-authorship problem inside Vela.
- **Literature source adapters** (OpenAlex / CrossRef / Scholar) feeding the Narrative Intelligence Platform.
- **Editorial Office** — Writer's Desk + multi-writer convening with round-2 react.
- **Preregistered research program at `/study`** — consent-gated session, instrument-validation cohort, dissertation-track scaffolds.
- **Stripe membership in live mode.**

**Outliers:**
- **Dual-grade corpus ingestion.** Same database holds curator-grade editorial picks (high-charge, hand-labeled, small N per source) AND research-bulk chunks (neutral, paragraph-respecting, large N per source), distinguished by a theme tag. Both grades coexist; the curator UI filters out research-bulk chunks while research retrieval uses everything.
- **$0.13-per-research-run cost at 30,000+ passage scale.** Sonnet synthesis across seven sub-questions with primary-source citations costs ~13 cents. Most "AI-powered research" tools run 10-100× more expensive because they retrieve without pattern-extraction.
- **Cryptographic provenance contract.** SHA-256 tracked for every source file. Safe-delete invariant: a laptop-local file can be deleted only when verified present on external backup AND on Supabase Storage AND content hashes match.
- **Per-user magazine pacing** — each reader's editorial schedule begins when they arrive; the positioning wedge is *"your magazine begins when you do."*

Stack: Next.js 16 + React 19 + Tailwind 4 + Supabase + pgvector + Vercel + Modal + Anthropic API + Stripe.

### Namesake · `baby-namer` · live at namesake.baby

A name chosen, not stumbled upon. Every baby-naming product helps parents find names; Namesake is the only one that helps them choose one. Built on twenty years of weekly search data, a per-name composite score (SSA stats × LLM-enriched meaning × cultural-event attribution), a tournament-bracket decision UX with village voting, and a cultural-diffusion research apparatus underneath.

**Live at $24 one-time tournament unlock** (Stripe live, no subscription). A wizard flow walks parents through their story, taste, and constraints; the system produces a scored, swipable list. The **Namesake score** is a deterministic composite (uniqueness × 0.30 + trend × 0.25 + meaning × 0.20 + feasibility × 0.13 + search × 0.12, percentile-normalized into a 5–95 display range against the dataset).

**Outliers:**
- **Twenty years of weekly search data plus systematic cultural-event attribution.** Most naming products show annual SSA rankings; Namesake shows weekly trend velocity with named causal events (the film that landed, the character who became iconic, the royal birth) attached. No competitor has the dataset.
- **Cultural-diffusion research apparatus** — Bass diffusion, Hawkes self-exciting processes, Moran's I, Granger causality, Lieberson null model, phonetic-spillover graphs, variance decomposition. The research surface is mirrored to `peopleanalyst.com/research/namesake` and is structural substrate for the network-mediated-adoption book project: same mechanism on a cultural-name corpus that the book argues for on organizational adoption.
- **Deterministic, percentile-normalized scoring** — no LLM-on-render. The Namesake score is computed in a batch rescore script; the LLM enrichment runs once per name, not per request. Every name's display score is reproducible and bounded; the substrate stays interpretable.

Stack: Next.js 16 + TypeScript + Supabase + Stripe + Anthropic API + FLUX (via FAL) + Playwright + Vercel.

### Fourth & Two · Gridiron Platform · `MFL-GM-Consol` · in development

A fantasy-football intelligence platform built around **four converging efforts**: a **GM Command Center** (lineup, waivers, trades, draft, rankings); a **Gridiron Analytics API** (Python/FastAPI service with PRISM and CAMS frameworks ported from people analytics to football); an **Insight Card system** (PRISM-trend / CAMS-alignment / market-signal cards composed across surfaces); and **Strategy League / Football IQ** (a coaching-strategy game with simulation engine layered on fantasy leagues).

**Outliers:**
- **Four converging efforts on one substrate.** Each ships standalone value; together they compose into a cohesive product narrative.
- **CAMS ported from people analytics to football** — the same Capability/Alignment/Motivation/Support framework that drives Performix's diagnostic instrument, adapted to roles, matchups, and weekly performance. Cross-portfolio framework reuse without re-implementation.
- **PRISM** — analytics-grade ranking + decision support built into the Python/FastAPI service; not a generic projection engine. Same statistical-rigor posture the rest of the portfolio inherits.
- **Insight Card system as the legibility surface** — composable cards browse-able at `/insights` and embeddable in context. Cards are first-class products; meta-tagging + context filtering govern when each one appears.
- **MFL adapter pattern** — formal adapter contract for fantasy provider swaps; provider-agnostic by design.

Stack: Next.js + TypeScript + Python + FastAPI + Postgres + Alembic + Clerk + Vercel.

---

## Product Line 3 — Editorial, authorship, and book-length work

The substrate-first posture extends to long-form writing. Shared infrastructure lets a single writer conduct research at institutional-scale depth and produce book-length work with anti-fabrication discipline.

### Penwright · in flight inside `vela/app/labs/penwright/`

**An AI-augmented authorship system** — corpus control, packet-shaped composition, and a measurement framework that asks whether the writer is *better with it, than without it, in six months*. Memoirists, essayists, and editorial writers who would rather become more capable than write faster.

Most AI writing tools optimize for output fluency. They make it easier to produce something faster — and that something is often shaped by the model rather than the writer. The longer-term cost (capability erosion, voice flattening, sycophancy spirals, source-attribution buried) is barely measured. Penwright is the bet on the other side.

**Outliers:**
- **Authorship Packet Model** — writers assemble *intent · structure · key ideas · relevant passages · counterpositions* before the AI is invoked. The structure itself is data; the prompt-then-edit pattern is inverted.
- **Corpus Control Layer** — the writer selects which sources influence the work rather than inheriting the LLM's training distribution.
- **Adaptive Authorship Control Kernel (F-19)** — central registry of skill measurement, intervention, and **genre-aware behavior** (memoir / nonfiction / fiction never collapsed; copy + schema enums + prompts + metrics fork rather than collapse).
- **Penwright Measurement Framework** — six skill dimensions, six derived indices, three measurement layers, five-step learning loop, four non-negotiable failure modes (output-only optimization · over-automation · weak measurement · ignoring genre differences) acting as veto.
- **Accumulating named writing-method primitives** — Borrowed Architecture (v1.0, 2026-05-12), *They Say / I Say* (third primitive, v1.1, 2026-05-13). Each is a registered method with structural anatomy + worked examples + anti-patterns, callable as a move inside the kernel rather than advice in a style guide.
- **Anti-invention constraint** — when a structural rhetorical move requires biographical material the user has not supplied, the tool refuses to render rather than confabulating.

Has its own published research program at `peopleanalyst.com/research/ai-human-interaction` (12-paper Penwright Research Program across three tiers).

### Backburn · book in progress · `peopleanalyst-site/content/research/adoption/sample-chapters/`

**Book-length argument on AI/people-analytics adoption rendered through a wildfire-management metaphor.** 14 chapters at v1 fidelity (~40,000 words). The wildfire register is load-bearing: the book argues that AI-adoption failure is *ecological*, not *tactical* — pilots burn out, rollouts drift, dashboards manufacture noise where signal should sit, and the structural correctives (prescribed burns, holding the line, mapping the forest via ONA) require the operator to read a fire pattern they do not yet have the literacy to read.

The four-S synthesis (Strategy, Science, Statistics, Systems) sits underneath the book as the framework the chapters compose against. The first three Ss have shipped as magazine pieces at `peopleanalyst.com/magazine/4s-{science,statistics,systems,strategy}` and feed back into Backburn's Chapter 12 (The Discipline for the AI Era).

### People-analyst.com · `peopleanalyst-site` · live at peopleanalyst.com

**Portfolio + research aggregator + editorial magazine + consulting hub.** The site is the *aggregator* for everything in the portfolio: each sister repo's research surface mirrors here at `/research/<product>/` for build-time rendering; the home page shows portfolio cards from a synced sister-repo brief feed; the *principal-issues* magazine renders editorial pieces; the consulting page is the lead-gen surface; the CV page renders from markdown.

**Live surfaces:**
- **Portfolio detail pages** at `/portfolio/[slug]` — each active product has a per-page deep-dive with synced sister-repo briefs, staleness badges, and (now) animated workflow diagrams.
- **`principal-issues` magazine** — voice-locked editorial publication. ~11 articles live including the 4S synthesis arc, the **Twelve Conditions for the Crown Fire** field guide, the **Why CAMS** + **Net Activated Value** + **Before the Ratings** methodology pieces, the **The Failure Record** (seven enterprise-AI deployments citation-anchored to primary sources), and the cross-portfolio-architecture meta-piece.
- **AI Human Interaction Guide** at `/ai` — seven-part guide + three appendices on AI in customer experience / product+operations / decision support / governance / network-mediated adoption.
- **`/research/`** — research surfaces mirrored from sister repos (vela, devplane, principia, namesake) for build-time rendering.

**Outliers:**
- **Portfolio Brief Protocol** — sister repos emit StoryBrand-shaped `docs/portfolio-brief.json` files; PA-site syncs them on demand; per-project detail pages render the synced data with staleness badges. Cross-portfolio narrative state is now machine-readable and continuously refreshed.
- **Detail-page diagram pattern** — animated CSS-keyframe SVG workflow diagrams (paper-palette, `prefers-reduced-motion` honored, accessible) for each portfolio product. The MetaFactory diagram is mirrored to sister repos as the canonical upstream-architecture reference.
- **Voice spec** at `docs/magazine/VOICE.md` — the **principal-issues-register** v1.0 LOCKED, governing all Mike-voice writing across the portfolio. Sibling repos inherit via a one-line reference.

Stack: Next.js 16 + React 19 + Tailwind 4 + TypeScript + Resend (newsletter).

### DevPlane · `devplane` · live locally + hosted at devplane.dev

**Two products in one project.** A local cockpit for multi-tool software development (assignment registry, two-phase actor handoff, coordination-event log, MCP server, CLI, Chrome extension) AND the portfolio's shared engineering brain (pattern library, architecture maps, session handoffs, cross-project assignment registry, API registry, decision log, capabilities catalog).

**Outliers:**
- **Two-phase actor handoff** (builder → reviewer) where the second transition requires an artifact only the reviewer can produce — enforces review without trusting it.
- **Coordination-event log as a research instrument**, not just an audit trail — the apparatus for the **C1 risk-compensation field study**, a pre-registered test of Bainbridge 1983 (Ironies of Automation) in real coding work with hypotheses, analysis plan, and falsification criteria specified before data accumulates.
- **Completion blocks as a protocol** — every assignment ends with structured machine-readable completion, not free-text close-out.
- **Cross-project documentation hub** — patterns, maps, handoffs, assignments, APIs, decisions, and capabilities legible across every repo. Reduces the rebuild-it-five-times tax that solo-cadence multi-product work would otherwise pay.
- **Coordination-pill extraction (DP-165)** — the first substrate-first pill the repo is building toward: `src/coordination/` boundary enforced (no outside imports, no `DevPlaneConfig` references; accepts a `CoordinationStorage` adapter). End state: `@devplane/coordination-core` v0.1.0 published to npm.
- **Pattern-propagation stack** — `dp patterns` CLI + `devplane_patterns_search` / `devplane_patterns_get` MCP tools + reconciled `MASTER-PATTERNS.md`. Patterns discoverable from any agent over MCP, from the operator over CLI, and actively reconciled rather than write-only.
- **Portfolio reconciliation 2026-05-21**: `~/.devplane/portfolio.json` now tracks 19 entries (1 hub, 3 tools, 6 expressions, 9 archives).

Stack: Node.js + TypeScript + Hono + SQLite + libsodium + Clerk + Stripe + MCP + Server-Sent Events.

### MetaFactory · `meta-factory` + `meta-factory-prod`

**Two-shell production-factory substrate** for the portfolio. An engine (OLD, AI-controlled, local-only, no human UI) that ingests books and research at chapter-respecting fidelity and runs a roster of named factories (Persona, Survey, Competency, Models, Requirements, Prompt, Publishing, Business Ideas, Application Designs) producing canonical outputs; and an API host (PROD, Vercel) that exposes a v1.2.0 REST + MCP contract plus a cross-portfolio library layer (Stream 7, ~944 records) the rest of the portfolio reads from.

**Outliers:**
- **Split engine + API host architecture** — OLD does the work; PROD makes it accessible. The seam is a snapshot + cloud-storage refresh, run manually on a manual cadence. The two repos evolve independently without coupling consumer integration to engine internals.
- **Named factories as units of production** — Persona / Survey / Competency / Models / Requirements / Prompt / Publishing / Business Ideas / Application Designs. Each is a package that outputs a structured behavioral artifact; analytics offerings explicitly excluded. The roster grows; the substrate doesn't.
- **Cross-portfolio library layer (Stream 7)** — a single read surface for ~944 corpus records that every product consumes, with a shared lifecycle and spec.
- **Dual-grade corpus ingestion** — same database holds editorially-selected curator passages and bulk research chunks, distinguished by tag. Vela's pipeline lifted into the substrate.
- **Cryptographic provenance contract** — SHA-256 tracked for every source file; safe-delete invariants require hash verification on backup and durable storage before any local delete.
- **MF-150 chat-capture pipeline** (Chrome extension → `/books`) shipped 2026-05; **MetaFactory Console v2 Phase 1** (DP-161/163) admin write surface shipped same window.
- **Schema-extracted measurement vocabulary** (`@measurement/core`, recently renamed `@people-analyst/measurement-core`) shared across consumers — constructs, items, instruments, effect-sizes defined once in canonical form, so behavioral measurement compares cleanly across Performix / Principia / PA Toolbox.

Stack: TypeScript + Next.js + Supabase + pgvector + OpenAI embeddings + Anthropic API + Model Context Protocol + Vercel.

---

## Advanced software engineering patterns applied

Every pattern below is implemented in production across at least one of the applications above.

- **Hub-and-spoke registry architecture** — Central service catalog; spokes ship independently, discover each other through the hub. People Analytics Toolbox hubs eight live spokes plus nine scouted future spokes.
- **Substrate-first capability extraction** — Capabilities live in shared platform packages (`@people-analyst/measurement-core` for the measurement vocabulary; the in-flight `@devplane/coordination-core` for coordination primitives) consumed by multiple products. Verticals compose against typed contracts, never re-implement primitives.
- **Platform/vertical separation with lint-enforced boundary** — `lib/platform/` (or its analogs) may not import any vertical-specific module; enforced by CI lint guard. Platform primitives are consumed without coupling.
- **Dual-grade ingestion with tag-based filtering** — Same table, two use cases, tag-distinguished (curator-grade + research-bulk-grade passages on one substrate).
- **Runtime-registered loader pattern** — Platform defines the interface; vertical registers concrete loaders at boot. Keeps the platform vertical-free while allowing vertical-specific behavior.
- **Cryptographic content provenance** — SHA-256 for every file ingested; safe-delete invariant requires hash verification on both backup + durable storage before local delete.
- **Idempotent migrations + content-hash-based incremental embedding** — Re-running any ingestion script is safe; embeddings recompute only when content actually changed.
- **Dual-write fanout** — Writes land in both primary table and event-log / audit table atomically for downstream consumption.
- **Append-only signal streams** — Preferences, reactions, curator decisions recorded append-only; derived state materialized separately so history is recoverable.
- **Pattern abstraction in retrieval** — Retrieval returns abstracted templates (structural skeletons with placeholders) rather than source sentences, enabling pattern reuse without plagiarism risk.
- **Two-phase critic architecture** — AI output passed through a second AI critic pass that specifically checks for invented biographical content (not grammar, not style — provenance of claims).
- **Anti-invention veto on AI rendering** — When a structural move requires material the user hasn't supplied, the tool refuses to render rather than confabulating.
- **Precompute-and-playback** — Insights / InsightCharts / Smart Lists computed upstream + stored; the consumer surface retrieves rather than recomputes at render. The user's home is the player; the library is the secondary discovery surface.
- **Auto-CI method selection** — Confidence interval method chosen by data shape (Wilson for small-N proportions; t-interval for continuous data with small samples; normal CI where asymptotic conditions hold) rather than by convention.
- **Two-phase actor handoff** — Builder → reviewer; second transition requires reviewer-only artifact. Enforces review without trusting it.
- **Completion-block protocol** — Every assignment ends with structured machine-readable close-out, not free-text.
- **MCP-native distribution** — Every analytical spoke is callable from AI agents over Model Context Protocol without bespoke integration. Per-consumer auth, scope-restricted keys, fire-and-forget audit log.
- **Hard-capped AI budgets** — Per-session rate limits and per-request Sonnet-call caps enforced at API route level; oversized requests fail early with clear errors rather than silently truncating.
- **Semantic-boundary-preserving chunking** — Paragraph-respecting at ~500-word target with ±25% flex; hard-splits giant paragraphs by sentence boundary; merges too-small stragglers into adjacent chunks.
- **Row-Level Security with service-role bypass** — Default RLS locks everything; service-role client used only for explicit admin-authorized operations.
- **Portfolio Brief Protocol** — Sister repos emit StoryBrand-shaped briefs; the hub syncs them; PA-site renders them as per-project detail pages with staleness badges. Cross-portfolio narrative state is machine-readable and continuously refreshed.
- **Detail-page diagram pattern** — Animated paper-palette CSS-keyframe SVG workflow diagrams with `prefers-reduced-motion` honored, accessible, mobile-friendly. When a workflow is too large for a single 4:1 diagram, series treatment (multiple 16:10 diagrams with prose interstitials between) per a pattern spec.

---

## DevOps + engineering discipline

- **CI-applied migrations.** Agents commit migration files to main; CI auto-applies on merge. No human SQL paste, no "did I apply that locally" drift.
- **Commit-SHA deployment verification.** Every deployed instance exposes `/api/health` returning the running commit SHA; Definition-of-Done includes verifying deployed SHA matches pushed SHA before declaring work complete.
- **Assignment-driven multi-agent engineering.** `docs/AGENT-ASSIGNMENTS.md` (with per-repo prefixes — PA, ASN, DP, PRN, PAT, A, F2) is the canonical work queue. Every non-trivial unit has a self-contained prompt, explicit files-touched, acceptance criteria, and dependencies. Claude Code, Cursor, and Codex agents pick up work cold without conversational context — the assignment IS the context.
- **Lane-based parallelism with blitz-mode discipline.** Up to three concurrent tracks (this session / Cursor cloud / Claude Code subagent). Shared-file work explicitly serialized via dependency declarations to avoid merge conflicts.
- **Session-report discipline.** Every meaningful work unit produces a dated session report at `docs/handoff/YYYY-MM-DD-<slug>.md` (or per-repo equivalent) with commit SHAs referenced.
- **Multi-environment deploy.** Vercel preview + production; separate Supabase environments; environment variables typed in `.env.example` and diffed against deployed state via `vercel env`.
- **Cost observability.** Every AI call logged with tokens + model + operation type for admin-dashboard aggregation. Vercel build cost ~$0.75 per push; cloud-agent PRs ≈ $1.50 each — discipline bundles related work into one push per wave.
- **Modal for GPU workloads.** Python serverless with A10G GPUs for Whisper large-v3 audiobook transcription and FAL-equivalent image generation workloads.
- **AI Gateway routing.** Multi-provider LLM access through Vercel AI Gateway with unified billing, provider failover, zero-data-retention enforcement.
- **Playwright E2E + QA bot infrastructure.** Automated link-auditing, SEO checks, persona simulation, screenshot regression.

---

## Productivity baseline (Vela alone, ~50-day window)

Objectively measurable claims, verifiable by anyone with repo access. Not averages over career — just one project's window of intense initial build-out.

- **2,263+ commits** on `main` — working sessions produce multiple commits per hour, each typecheck-clean before push.
- **365,000+ lines** of TypeScript across application + library + scripts + components.
- **278+ database migrations** (all CI-applied; zero manual SQL paste).
- **204+ admin pages** implementing operational surfaces for curation, review, ingestion, QA, adaptive-intelligence tuning, research synthesis, LoRA training, derivative pipelines, fragment management, corpus density, writer retrieval, partner portals, magazine editing, audit.
- **362+ API routes** spanning public product surfaces, admin operations, webhook handlers, and platform primitives.
- **Zero TypeScript errors on `main`** maintained as a merge gate.
- **Parallel multi-agent development** — Claude Code + Cursor agents frequently ship coordinated work simultaneously.

Solo-founder software shipping at this rate is unusual. Most solo founders ship one or two production applications in a career; this portfolio represents 20+ applications in four years, with Vela alone producing more production code in 50 days than many single-person startups ship in their first year.

---

## Technology range

**Languages (production use)**:

| Language | Role | Applications |
|---|---|---|
| TypeScript | Primary | All web applications |
| Python | Analytics APIs, ML, audio, image | Gridiron analytics-api, Modal workloads (Whisper, FAL), data-extraction scripts |
| SQL | Postgres DDL, migrations, admin queries | Every application |
| Shell | Build scripts, tooling, CI | Every application |
| Markdown | Documentation, prompts, voice specs, session reports | Every application |
| YAML, JSON | Configuration, data, webhooks | Every application |
| HTML/CSS (via Tailwind) | UI layer | Every web application |

**Frameworks & runtimes**:

| Layer | Technology |
|---|---|
| Web framework | Next.js 16 App Router, React 19 |
| Styling | Tailwind CSS 4, shadcn/ui primitives |
| Python web | FastAPI |
| Serverless (Node) | Vercel Functions (Fluid Compute) |
| Serverless (Python + GPU) | Modal |
| Deployment | Vercel (web + edge + functions) |
| Database | PostgreSQL 16+ with pgvector extension |
| Database-as-service | Supabase (Postgres + Storage + RLS + Auth + Edge Functions) |
| Object storage | Supabase Storage (private buckets + RLS + signed URLs) |
| Data warehouse | BigQuery |
| Search + vectors | pgvector (1536-dim for text-embedding-3-small) |
| Inter-agent protocol | Model Context Protocol (MCP) |

**AI + ML stack**:

| Use case | Technology |
|---|---|
| Reasoning + synthesis | Anthropic Claude (Opus / Sonnet / Haiku) via SDK + via Vercel AI Gateway |
| Embeddings | OpenAI text-embedding-3-small (1536-dim) + Voyage (fallback) |
| Audio transcription | Whisper large-v3 on Modal A10G GPUs |
| Image generation | FAL (FLUX + SDXL variants) |
| Statistical analysis | R, SPSS, Python (scikit-learn adjacent) |
| ETL | Alteryx, custom Python pipelines, Modal batch jobs |

**External services consumed in production**:

Anthropic, OpenAI, FAL, Stripe, Supabase, Radford / WTW / Mercer / CompAnalyst (compensation data), Lightcast / EMSI / Burning Glass (labor market), LinkedIn Talent Insights, WhoisFreaks (domain feasibility), OMDB / TMDB (cultural metadata), Modal, Vercel, Sentry (error tracking), Playwright (E2E testing), Resend (transactional email), GitHub + gh CLI (automation), Internet Archive, Project Gutenberg, Perseus Digital Library, CCEL, Corpus Corporum, Sefaria, Wikimedia Commons, Europeana, Rijksmuseum API, Metropolitan Museum API, Art Institute of Chicago API, BnF, Smithsonian, Workday, Oracle HR, PeopleSoft, Greenhouse, Syndio, Payscale, MarketPay, Visier, One Model, ZeroedIn, MicroStrategy, Cognos, Tableau, Power BI, Culture Amp, Glint, SurveyMonkey, Qualtrics, OpenAlex, CrossRef, Google Scholar, US Census, Social Security Numident, Census TIGER (county + CBSA polygons via PostGIS), and more.

---

## Standing

**Published author** — *People Analytics for Dummies* (Wiley, March 2019), the first mainstream book on people analytics.

**22,000+ LinkedIn followers**. 97+ published articles on analytics methodology, management, compensation science, AI-product intersection, and organizational decision-making.

**First practitioner** to have worked on all three leading workforce-analytics platforms (Visier, One Model, ZeroedIn).

**Pioneer roles** at Merck (65K employees, $4B HR investment), PetSmart (20K employees, $40M+ investment), Google (7K→21K growth era, designed Google's first attrition prediction model + Googlegeist precursor survey), Children's Medical Dallas, Pure Storage.

**Consultancy** — 25+ enterprise clients including The New York Times, Pfizer, Nike, Mars, Juniper Networks, Zoom, Reddit, Pure Storage, Datavant, Cityblock Health, 10X Genomics, Atlassian, Udemy, Otsuka, AstraZeneca, and others.

**Notable methodologies originated**: **Rapid Collaborative Insight (RCI)** · **Net Activated Value (NAV)** · **Three A's Framework** (Attraction / Activation / Attrition) · **CAMS** (Capability / Alignment / Motivation / Support — the binding-constraint diagnostic) · **Four-S synthesis** (Strategy / Science / Statistics / Systems as the load-bearing set) · **Lean People Analytics** · **Full-Stack People Analytics Systems** · **Quantitative Model of Human Resources** · **the principal-issues-register** (voice spec) · **the Portfolio Capability Platform Playbook** (cross-portfolio architecture doctrine).

**Currently pivoting toward product-leadership roles** and applying to PhD programs at Carnegie Mellon and the University of Pittsburgh to deepen the research foundation for the next phase.
