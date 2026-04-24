# Mike West — Software Portfolio

*As of April 2026. All repositories private; this document is the public-facing summary.*

**Contact**: mike@peopleanalyst.com · 469.406.4699 · Pittsburgh, PA · linkedin.com/in/michaelcwest · peopleanalyst.com

---

## Overview

Since 2022, I have designed and built 20+ TypeScript applications spanning three distinct product lines, as solo founder of **PeopleAnalyst** (consulting since 2012). What began as a niche consulting practice has evolved into an AI-native product ecosystem applying systematic decision science to progressively broader domains — from enterprise HR analytics to scholarly research infrastructure, from intentional baby naming to contemplative visual art, from fantasy football intelligence to memoir composition. The major common thread is pairing multi-source data with human inputs for delivery in better experiences or better decisions. With respect to data I mean some new datasets that are AI derived, and some datasets from standing sources. AI enables rapid classification of elements found large text or visual cannnons, which then exposes reality to codification and analysis, enabling new insight, and with that, fresh opportunity.

The ecosystem is architected as a **hub-and-spoke pattern**: a central registry with spoke applications that integrate via shared data, identity, and UI substrate. Cross-cutting concerns — PII anonymization, metric calculation engines, survey delivery, human-integrated data derived self-improving feedback loops (recursive algoritms), probabilistic programming, microservices, APIs, writer-retrieval for AI-assisted composition — live as reusable platform services consumed by multiple verticals.

---

## Product Line 1 — People Analytics Platform

A complete AI-native people analytics infrastructure: measurement, decision science, survey delivery, data engineering, and a compensation-decision operating system. Built solo, 2022–present.

### Central hub
- **`people-analytics-toolbox`** — Hub-and-spoke registry. Central service-discovery + shared auth + cross-spoke navigation.

### Decision-science applications
- **`voi-calculator`** — Value of Information analysis. Monte Carlo simulation, EVPI/EVSI calculations, AI-assisted decision modeling. Answers *"is this study worth running?"* before resources commit. **Outlier:** formal VOI in HR tooling is essentially absent commercially; this implements the academic framework as production software.
- **`decision-wizard`** — Kepner-Tregoe structured decision-making, instrumented for complex multi-stakeholder HR decisions.
- **`people-analyst` (app)** — Organizational forecasting with probabilistic modeling, Monte Carlo, VOI, and AI-powered research for executive decision-making.

### Measurement + analytics infrastructure
- **`calculus` / `metric-engine-calculus`** — Persistent batch calculation engine for 210+ HR metrics across segments and time periods. **Outlier:** most HR analytics products recompute metrics per-dashboard-render; Calculus precomputes + materializes, so 1,000+ manager-level segmentations are instant rather than minutes-long.
- **`conductor`** — Data intelligence orchestrator. BigQuery metadata, **AI-powered SQL/Python generation** from natural language + schema, One Model imports, tiered metric recipes, field mediation. **Outlier:** AI code generation over metadata rather than over examples — the model sees the schema and documented business logic, not sample SQL.
- **`segmentation-studio`** — HRIS data onboarding, canonical field normalization, multi-membership segmentation. Handles the reality that every enterprise has inconsistent job codes, titles, and leveling.

### Survey + adaptive research delivery
- **`survey-respondent`** — Employee-facing delivery supporting 15 question types including **MaxDiff, Conjoint, Dual-Slider**, NPS, Likert, with full Platform Hub integration. Psychometric rigor, not polls.
- **`reincarnation`** — **Adaptive Diagnostic System with RID/SID architecture** for multi-study item management with adaptive learning. **Major outlier / potentially important achievement:** RID/SID (Respondent-ID / Study-ID) separation allows a single question to participate in many studies without confounding — each question's item-response statistics accumulate across studies, and adaptive selection uses the full accumulated evidence to choose the next question. Commercial survey platforms either (a) run studies in silos with no cross-study learning, or (b) pool naïvely and lose study-level integrity. This architecture preserves both.
- **`preference-modeler`** — MaxDiff / Conjoint analysis engine. Statistical back-end for preference-based compensation and benefits design.

### Compensation + composable visualization
- **`anycomp`** — Compensation Decision Operating System. Merit, equity, market-pricing, and total-rewards decisions as a coherent product surface.
- **`metric-market`** — Card-based workbench with interactive data-visualization, compensation-range simulation, and cross-application integration. **Outlier:** composable-cards pattern (each visualization is a self-contained card composable into client-specific dashboards) rather than the dashboard-as-monolith pattern most tools use.

### Cross-cutting infrastructure
- **`data-anonymizer`** — Cross-cutting data-privacy layer. Automatic PII detection, **deterministic anonymization** (same input → same hashed output across runs, allowing reversible analysis without compromising sharing), HRIS-specific field handling, Hub integration for safe client data sharing. Runs ahead of any data-leaving-the-client boundary.

---

## Product Line 2 — Adjacent consumer + cultural products

Applications of the same systems-thinking + AI-integration approach to domains outside enterprise HR. Proof the patterns generalize.

### Vela · `vela` · live at vela.study

A contemplative visual-art platform. 385 active curated works sourced from Art Institute of Chicago, Metropolitan Museum, BnF, Smithsonian, Europeana, Rijksmuseum. An editorial magazine (16 published articles, 4 fiction series). An adaptive-intelligence sequenced player with desire scoring and pool management. The Reveal (aperture-based image discovery). AI curation with learning feedback loop. Stripe membership. A Transformation Studio revenue loop for partner photographers, wired end-to-end.

**Outliers:**
- **Dual-grade corpus ingestion.** Same database holds curator-grade editorial picks (high-charge, hand-labeled, small N per source) AND research-bulk chunks (neutral, paragraph-respecting, large N per source), distinguished by a theme tag. Both grades coexist in one table; the curator UI filters out research-bulk chunks while research retrieval uses everything. Solves the documented problem that the same corpus needs to serve two categorically different use cases.
- **$0.13-per-research-run cost at 30,000+ passage scale.** Sonnet synthesis of a research question across seven sub-questions, with primary-source citations, costs ~13 cents. Most "AI-powered research" tools run 10-100× more expensive because they retrieve without pattern-extraction, forcing the LLM to consume more context.
- **Cryptographic provenance contract.** SHA-256 hashes tracked for every source file in Supabase Storage. Safe-delete invariant: a laptop-local file can be deleted only when verified present on external backup AND on Supabase Storage AND content hashes match.

Stack: Next.js 16 + React 19 + Tailwind 4 + Supabase + Vercel + Modal + Anthropic API.

### Namesake · `baby-namer` · live at namesake.baby

An intentional baby-naming platform. 47,000+ names with 145+ years of SSA popularity data. A Name Wizard walking parents through a structured 20-minute selection process keyed to stated values + inspirations. Name-intelligence profiles (origin, meaning, pronunciation, 10-year popularity charts, feasibility scores). Parallel partner brainstorming, tournament-bracket voting with family and friends, themed collections, and a live baby-shower participation mode.

**Outlier / potentially important achievement:** Built-in research pipeline at **PhD-cultural-diffusion rigor**: five theoretical frameworks, 13 research questions, 15 external data sources (SSA, OMDB, TMDB, US Census, Social Security Numident, etc.), 11 phases, 843 cultural events analyzed to model how names go viral. Publication-grade methodology inside a consumer product. Rare.

Stack: Next.js 16 + Supabase + Vercel + Tailwind, Anthropic API for naming intelligence + spike attribution, FAL for illustration generation, OMDB/TMDB for cultural-event correlation, WhoisFreaks for domain feasibility.

### Fourth & 2 · Gridiron Platform · `MFL-GM-Consol` · in development

A fantasy-football intelligence platform applying systematic decision-support to a high-volume-decision consumer domain. Monorepo: Next.js web app (Team Command Center, Waiver Command Center, League Intelligence Dashboard, Weekly Strategy Engine, Draft Day, Rankings) + Python/FastAPI analytics API (**PRISM, CAMS, rankings, decisions engines**) + gm-console FastAPI proxy + shared TypeScript packages (engine, adapters, 16 analytics card types, typed HTTP client). Side games (The Pick, The Matchup, Survivor) shipped as playable with per-device localStorage.

---

## Product Line 3 — Research + memoir infrastructure (in flight)

Shared intellectual infrastructure letting a single writer conduct research at institutional-scale depth.

### Commonplace (platform-level)

Scholarly corpus infrastructure. Ingests public-domain primary-source archives (Patrologia Latina via Corpus Corporum — 217 volumes; CCEL's Ante-Nicene and Nicene–Post-Nicene Fathers — 38 volumes; Sefaria's full Jewish primary corpus; Perseus Digital Library) alongside contemporary academic works. Per-vertical extraction manifests pull relevant passages into downstream editorial products. Retrieval-based evidence aggregation, diachronic semantic drift tracking, claim-level corpus coverage analysis, all built-in.

**Outlier:** one scholar's research capacity amplified by approximately 1000×. Demonstrated: a research question that would require a scholar weeks of library work returns a cited synthesis in under 2 minutes at ~$0.13 in API cost.

### Loom (in flight)

AI-assisted long-form composition workshop. Pattern-first compositional scaffolding: retrieves structural rhetorical moves from a curated memoir corpus **without exposing source sentences** (plagiarism-distance enforcement at two layers — bigram overlap + Sonnet critic pass for invented-content detection). Experience × emotion taxonomy lets the writer query for "scene-setting under shame" or "internal monologue under tenderness" — not semantic similarity, pattern similarity.

**Outlier / potentially important achievement:** **voice-match with explicit anti-invention constraint.** The Sonnet voice-match pass is instructed to *never* invent biographical content the user hasn't written, enforced via a per-rendering `invented_content[]` array returned from the model and surfaced as warnings. When a structural move requires material the user hasn't supplied, the tool **refuses to render** rather than confabulating. This is unusual for AI-writing tools, which default to producing something over flagging a limitation.

### Supporting infrastructure
- **`devplane`** — Kanban/workflow tool. Assignment coordination across multi-agent engineering (Claude Code + Cursor + human curator). Completion-block protocol, session-report integration, DevPlane kanban cards with commit-SHA lineage. **Outlier:** the completion-block protocol cryptographically links every kanban movement to a specific git commit, preventing the "card says DONE, code not actually shipped" failure mode.
- **`meta-factory` / `meta-factory-prod`** — **Universal Information Factory**: transforms unstructured knowledge into structured, queryable intelligence. Cross-project transformation pipeline; takes any document corpus and produces schema-conformant typed records ready for downstream product use. **Outlier / potentially important achievement:** a single pipeline producing production-grade structured data from any unstructured source (PDF, HTML, audio, video) with provenance and confidence scores preserved.
- **`Kanbai`** — Kanban-related personal workflow tool (earlier iteration; devplane is the production descendant).

---

## Advanced software engineering patterns applied

Every pattern below is implemented in production across at least one of the applications above.

- **Hub-and-spoke registry architecture** — Central service catalog; spokes ship independently, discover each other through the hub. (`people-analytics-toolbox` hubbing 14+ spokes.)
- **Platform/vertical separation with lint-enforced boundary** — `lib/platform/` may not import any vertical-specific module; enforced by CI lint guard. Platform primitives are consumed by multiple verticals without coupling.
- **Dual-grade ingestion with tag-based filtering** — Same table, two use cases, tag-distinguished. (`mosaic_passages` holding curator-grade + research-bulk-grade passages.)
- **Runtime-registered loader pattern** — Platform defines the interface; vertical registers concrete loaders at boot. (`registerVoiceSampleLoader(id, loader)` in writer-retrieval.) Keeps the platform Vela-free while allowing BIBLE-backed voice samples.
- **Cryptographic content provenance** — SHA-256 for every file ingested; safe-delete invariant requires hash verification on both backup + durable storage before local delete.
- **Idempotent migrations + content-hash-based incremental embedding** — Re-running any ingestion script is safe; embeddings recompute only when content actually changed.
- **Dual-write fanout** — Writes land in both primary table and event-log / audit table atomically for downstream consumption.
- **Append-only signal streams** — Preferences, reactions, curator decisions recorded append-only; derived state materialized separately so history is recoverable.
- **Pattern abstraction in retrieval** — Retrieval returns abstracted *templates* (structural skeletons with placeholders) rather than source sentences, enabling pattern reuse without plagiarism risk.
- **Hard-capped AI budgets** — Per-session rate limits and per-request Sonnet-call caps enforced at API route level; oversized requests fail early with clear errors rather than silently truncating.
- **Semantic-boundary-preserving chunking** — Paragraph-respecting at ~500-word target with ±25% flex; hard-splits giant paragraphs by sentence boundary; merges too-small stragglers into adjacent chunks.
- **Two-phase critic architecture** — AI output passed through a second AI critic pass that specifically checks for invented biographical content (not grammar, not style — provenance of claims).
- **Row-Level Security with service-role bypass** — Default RLS locks everything; service-role client used only for explicit admin-authorized operations; application-role clients always run under the current user's RLS scope.

---

## DevOps + engineering discipline

- **CI-applied migrations.** Agents commit migration files to main; CI auto-applies on merge. No human SQL paste, no "did I apply that locally" drift.
- **Commit-SHA deployment verification.** Every deployed instance exposes `/api/health` returning the running commit SHA; Definition-of-Done includes verifying deployed SHA matches pushed SHA before declaring work complete.
- **Assignment-driven multi-agent engineering.** `docs/AGENT-ASSIGNMENTS.md` is the canonical work queue. Every non-trivial unit has a self-contained prompt, explicit files-you-will-touch, acceptance criteria, and dependencies. Claude Code and Cursor agents pick up work cold without conversational context — the assignment IS the context.
- **Lane-based parallelism.** Independent work organized into lanes that execute concurrently; shared-file work explicitly serialized via dependency declarations to avoid merge conflicts.
- **Session-report discipline.** Every meaningful work unit produces a dated session report at `docs/session-reports/YYYYMMDDTHHMMSS-<slug>.md` with commit SHAs referenced. Report is immutable after write — the record is the record.
- **Multi-environment deploy.** Vercel preview + production; separate Supabase environments; environment variables typed in `.env.example` and diffed against deployed state via `vercel env`.
- **Cost observability.** Every AI call logged to `writer_retrieval_usage` (or equivalent) with tokens + model + operation type for admin-dashboard aggregation.
- **Modal for GPU workloads.** Python serverless with A10G GPUs for Whisper large-v3 audiobook transcription and FAL-equivalent image generation workloads.
- **AI Gateway routing.** Multi-provider LLM access through Vercel AI Gateway with unified billing, provider failover, zero-data-retention enforcement.
- **Playwright E2E + QA bot infrastructure.** Automated link-auditing, SEO checks, persona simulation, screenshot regression.

---

## Productivity + code quality (Vela alone, last ~50 days)

These are objectively measurable claims, verifiable by anyone with repo access. Not averages over career — just one project's ~50-day period from initial commit through the date of this document.

- **2,263 commits** on `main` — working sessions produce multiple commits per hour, each typecheck-clean before push
- **365,199 lines** of TypeScript across application + library + scripts + components
- **278 database migrations** (all CI-applied; zero manual SQL paste)
- **204 admin pages** implementing operational surfaces for curation, review, ingestion, QA, adaptive-intelligence tuning, research synthesis, LoRA training, derivative pipelines, fragment management, corpus density, writer retrieval, partner portals, magazine editing, audit, and more
- **362 API routes** spanning public product surfaces, admin operations, webhook handlers, and platform primitives
- **Zero TypeScript errors on `main`** maintained as a merge gate; `npm run typecheck` is part of the Definition-of-Done
- **Parallel multi-agent development** — Claude Code + Cursor agents frequently ship coordinated work simultaneously, with dependency coordination via `docs/AGENT-ASSIGNMENTS.md` lane declarations
- **Every PR** (functional equivalent — most work is direct-to-main under pair-with-Mike discipline) carries its own commit message detailing what shipped, why, and any follow-ups captured as new ASN entries

**Relative perspective.** Solo-founder software shipping at this rate is unusual. Most solo founders ship one or two production applications in a career; this portfolio represents 20+ applications in four years, with Vela alone producing more production code in 50 days than many single-person startups ship in their first year.

---

## Technology range

**Languages (production use)**:

| Language | Role | Applications |
|---|---|---|
| TypeScript | Primary | All 20+ applications |
| Python | Analytics APIs, ML, audio, image | Gridiron analytics-api, Modal workloads (Whisper, FAL), data-extraction scripts |
| SQL | Postgres DDL, migrations, admin queries | Every application |
| Shell | Build scripts, tooling, CI | Every application |
| Markdown | Documentation, prompts, templates, BIBLEs | Vela, AGENT-ASSIGNMENTS, session reports |
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

Anthropic, OpenAI, FAL, Stripe, Supabase, Radford / WTW / Mercer / CompAnalyst (compensation data), Lightcast / EMSI / Burning Glass (labor market), LinkedIn Talent Insights, WhoisFreaks (domain feasibility), OMDB / TMDB (cultural metadata), Modal, Vercel, Sentry (error tracking), Playwright (E2E testing), Posthog-class analytics, Resend (transactional email), GitHub + gh CLI (automation), Cloudflare (where applicable), Internet Archive, Project Gutenberg, Perseus Digital Library, CCEL, Corpus Corporum, Sefaria, Wikimedia Commons, Europeana, Rijksmuseum API, Metropolitan Museum API, Art Institute of Chicago API, BnF, Smithsonian, Workday, Oracle HR, PeopleSoft, Greenhouse, Syndio, Payscale, MarketPay, Visier, One Model, ZeroedIn, MicroStrategy, Cognos, Tableau, Power BI, Culture Amp, Glint, SurveyMonkey, Qualtrics, and more.

---

## Standing

**Published author** — *People Analytics for Dummies* (Wiley, March 2019), the first mainstream book on people analytics.

**22,000+ LinkedIn followers**. 97+ published articles on analytics methodology, management, compensation science, AI-product intersection, and organizational decision-making.

**First practitioner** to have worked on all three leading workforce-analytics platforms (Visier, One Model, ZeroedIn).

**Pioneer roles** at Merck (65K employees, $4B HR investment), PetSmart (20K employees, $40M+ investment), Google (7K→21K growth era, designed Google's first attrition prediction model + Googlegeist precursor survey), Children's Medical Dallas, Pure Storage.

**Consultancy** — 25+ enterprise clients including The New York Times, Pfizer, Nike, Mars, Juniper Networks, Zoom, Reddit, Pure Storage, Datavant, Cityblock Health, 10X Genomics, Atlassian, Udemy, Otsuka, AstraZeneca, and others.

**Currently pivoting toward product-leadership roles** and applying to PhD programs at Carnegie Mellon and the University of Pittsburgh to deepen the research foundation for the next phase.

**Notable methodologies originated**: Rapid Collaborative Insight (RCI) · Net Activated Value · Three A's Framework (Attraction/Activation/Attrition) · Lean People Analytics · Full-Stack People Analytics Systems · Quantitative Model of Human Resources.
