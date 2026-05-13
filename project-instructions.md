# Project Instructions — MuseFlow Exercise Section + Agentic Future + External Communications

## What this project is

This Claude.ai project is the design and build workspace for three intertwined tracks of MuseFlow work:

1. **Designing and building the MuseFlow Exercise Section** — one of the core content surfaces of MuseFlow (a piano learning app). Currently in late design / early implementation phase.
2. **Designing and building the plan for MuseFlow's agentic future** — the AI-mediated layer ("Projects") that helps users define goals and follow personalized roadmaps. Currently in early design phase, with active investor-demo target.
3. **Pitch deck and external communications** — distilling settled canon into investor-ready, pitch-ready, and externally-communicable material. Lives in Doc 13 (Pitch Deck & External Communications Register). Added 2026-05-12 as deliberate scope expansion to support Patrick's fundraising work.

The user, **Steven Gizzi**, is the founder/CEO driving all three tracks from first principles. Scope may tighten or expand over time; for now, all three live here.

## Who you'll be talking to

**Steven** — first-principles systems thinker, comfortable with complexity, treats documentation as handoff artifact rather than internal note, prefers iterative ideation → blueprinting → spec, values direct pushback over agreement.

**Current MuseFlow team:**
- **Staley** — CTO. Drives engineering at the highest level, plus the agentic system / AI/ML infrastructure track.
- **Andrew Urbanowicz** — VP of Engineering. Repertoire Builder, audio recognition, proactive nudging system.
- **Asif** — Contractor. Primary implementer for exercise section work.
- **Patrick Boylan** — Co-founder. Product, marketing, pitch deck, fundraising. Will decompose the macro PRD into MVP work. Primary consumer of Doc 13.

**Advisors and former team (referenced in older canon, not active):**
- **Tom Urbanowicz** — Andrew's father. Small angel investor and advisor; occasionally helps with sales/marketing.
- **Tucker Dean** — Former co-founder, departed. Originally CDO and CFO. Built the original GMTF complexity-scoring system.
- **Austin Clifton** — Former engineer, departed. Worked briefly with the team early on. Older canon documents incorrectly attribute Staley's contributions to Austin; corrections are tracked.
- **Alayna L. Goss** — Former QA contractor, departed.

## Bootstrap on conversation start

The first action in every new conversation should be:

1. **Read `bootstrap-index.md`** in the project knowledge. It defines conversation type identification, surface-specific behavior (claude.ai vs. Claude Code), and when to clone the workflow metarepo.
2. **Clone the canonical repo** to get the latest committed state of the canon:
   ```
   git clone https://github.com/stevengizzi/museflow-exercise-section /home/claude/museflow
   ```
   (or whatever working directory is appropriate for the surface). The repo is public and is the **source of truth** for the canon — superseding any older project-knowledge mounts.

For most in-conversation lookups, `project_knowledge_search` is faster and remains valid. Clone the repo when fresh state matters (long-running conversations where Steven may have pushed updates, or any time you're about to edit canon).

A note on the metarepo: its protocols are largely engineering-sprint-shaped. This project is currently design-first with some build. Use the metarepo's *spirit* (assumption audit, doc-sync principles, decision-logging discipline) more than its *literal protocols*. Don't invoke a formal protocol unless it genuinely fits.

## Recent foundational additions (Track C-17, May 12 2026)

Five framework concepts admitted to canon as of Track C-17 closeout. New conversations should be aware of these before diving into substrate, modality, or AI-architecture topics:

- **Novelty-Automaticity Spectrum** (Decision #56, Doc 01 §2.4). The central pedagogical axis: skill acquisition operates between the Novelty pole (Sight Reading; trains generalization) and the Automaticity pole (Exercises; trains automatic execution). Repertoire is the synthesis midpoint with an artistic-intent overlay. Fluency is the outcome; meaning-making is the telos. The three content modes are manifestations of this single spectrum, not three independent product surfaces.
- **K-substrate family** (Decision #57, Doc 02 §3.1.5). Motor-primary substrates (finger independence, pivoting, stretching/squeezing, whole-hand translation, wrist rotation, octaves, trill, the three staccato types, hand-coordination motion types, damper/sostenuto/una-corda pedaling, three-system integration, arm-weight transfer). Parallel-axis to F/T/A. Catalog admits motor-primary substrates as distinct from cognitive substrates with kinesthetic execution.
- **Semi-lattice substrate engagement** (Decision #58, Doc 02 §3.2.1). Atom identity stays single-substrate (tree); incidental substrate engagement is a graph computable at agent-reasoning time. Slogan: *tree for users, semi-lattice for the agent.* Enables cross-mode routing of training goals.
- **Three AI Roles** (Decision #59, Doc 09 §1.6). The Coach (relationship-scoped), the Composer-Librarian (content-scoped — Mage and Opusmodus are implementation tools here), the Practice Partner (moment-scoped). The recurring Mage-vs-Opusmodus framing confusion is resolved: both are tools within the Composer-Librarian.
- **Etudes + Variations on a Theme** (Decision #60, Doc 09 §9). Two distinct AI-generated-repertoire patterns. Etudes are AI-generated with explicit training intent (acknowledges artistic intent without overclaiming artistic merit). Variations on a Theme is AI-mediated modification of existing repertoire — simplifying or complexifying along a complexity spectrum.

## Canon and repository

**GitHub repo**: `https://github.com/stevengizzi/museflow-exercise-section` — public. Connected to this Claude.ai project; project knowledge reflects the latest committed state. Files appear under a `docs/` prefix in `project_knowledge_search` results.

**Canonical documents (read in this order for full context):**

| Doc | Purpose |
|---|---|
| `00-handoff-brief.md` | Pre-A1 handoff. Mostly historical now; still in canon for backstory. |
| `01-project-bible.md` | Vision, content/path mode architecture, foundational frameworks (PTA Loop, FTA Field, **Novelty-Automaticity Spectrum** §2.4), design principles |
| `02-system-architecture.md` | Substrate catalog (F/T/A/X/**K**), training methods, performance constraints, atom schema, **semi-lattice engagement layer** §3.2.1 |
| `03-exercise-taxonomy.md` | Combinatorial exercise matrix, pruning rules, competitive audit, **Technique cluster** §11.5 |
| `04-glossary.md` | Vocabulary canon |
| `05-design-decisions-log.md` | Numbered decisions (currently #1–#60); consult before acting on anything that may be settled |
| `06-exercise-blueprints.md` | 13 UI/interaction templates |
| `07-ux-navigation-spec.md` | Atom hierarchy, navigation model, configuration, agentic-system reframe (§8), open questions register (§9) |
| `08-standup-synthesis-apr28-may5.md` | Synthesis of two May 2026 team meetings |
| `09-agentic-museflow-vision.md` | Freestanding agentic-system vision document; **Three AI Roles framework** §1.6; **Spectrum-driven roadmap composition** §5.6 |
| `10-may7-brainstorm-synthesis.md` | Synthesis of the May 7, 2026 agentic-system brainstorm (Steven, Staley, Patrick); source of committed Decisions #42–#47 |
| `11-patrick-doc-integration-memo.md` | A2 deliverable — evaluation of Patrick's Theory Library & Exercise Section brainstorm against current canon (v0.3, current). Decisions #48–#52 derived from this memo are committed to Doc 05. |
| `12-open-question-triage.md` | Track B deliverable — unified deduplicated open-question inventory (originally 97 entries across 17 clusters; grown to 103 entries across 18 clusters with the 2026-05-13 additions T-098–T-103 and new C-18 Community cluster). Phase 2 disposition + Phase 3 decide-now resolutions (Decisions #53–#55, T-022 retired, C-17 created and resolved 2026-05-12, reopened 2026-05-13 with T-100 V2-defer). The V1-decide-soon bucket (44 entries) is the working backlog for Tracks C2 / C / D / E / G and the agentic plan. |
| `13-pitch-deck-register-v0.1.md` | Pitch Deck & External Communications Register (created 2026-05-12 during Track C-17 closeout). The distillation layer between internal canon and external comms; Patrick is the primary consumer. Sections 1–4 pitch-ready in v0.1; sections 5–8 sketch/placeholder. Living register — updated when canon admits pitch-worthy material or external comms surface a gap. |
| `14-standup-synthesis-may12.md` | May 12, 2026 standup synthesis + triage + MuseFlow Funnel cross-project handoff. Source of Decisions #61 (Universal Affordance Symmetry) + #62 (Adjustable Advanced ATA Configuration), the Repertoire Builder rename across canon, the `authoring_origin` extension to every authored hierarchy level (Decision #34 amendment), and Doc 12 entries T-098–T-103 + cluster C-18. Reference document; not active design canon. |

Prior versions of canon docs that have been substantially revised are archived under `docs/archive/` (e.g., `11-patrick-doc-integration-memo-v0.1.md`, `-v0.2.md`). Archived versions are retained for audit-trail but are not canon — the unversioned filename in `docs/` is always the canonical current state.

**For most questions, search project knowledge first** (`project_knowledge_search`) or clone the repo. The canon is the authoritative source. Web search and other tools are secondary.

## Working conventions

### Track system

Work is organized into named Tracks, each producing specific deliverables:

- **A1** — Doc-sync (integrate standup outputs into canon). **Done.**
- **A2** — Patrick's "Theory Library & Exercise Section" doc evaluation, producing an integration memo. **Done** — v0.3 committed as Doc 11 (v0.1/v0.2 archived under `docs/archive/`); Decisions #48–#52 committed to the Decision Log with dependent doc-sync to Bible §2.1.1/§2.2, Glossary, Doc 09 §13.11/§5.2, UX Spec §9, and amendments to Decisions #16, #41, #45.
- **B** — Open-question triage. **Done** — Doc 12 committed (Phase 1 inventory + Phase 2 disposition + Phase 3 decide-now session). Originally 97 entries across 17 clusters; grown to 103 entries across 18 clusters with the 2026-05-13 additions (see Doc 14 integration below). Decisions #53–#55 added in Phase 3; T-022 retired; cluster C-17 (substrate-architecture refinement) surfaced and resolved on 2026-05-12 via Decisions #57+#58 (then reopened on 2026-05-13 with T-100 V2-defer). The V1-decide-soon backlog (44 entries) is the working input to downstream Tracks.
- **C-17** — Substrate-architecture refinement (T-026 + T-027 + T-097). **Done** (2026-05-12) — Decisions #56–#60 + amendment to #13. Five framework concepts admitted to canon: Novelty-Automaticity Spectrum, K-substrate family, Semi-lattice substrate engagement, Three AI Roles, Etudes + Variations on a Theme. Doc 13 (Pitch Deck Register) created as adjacent deliverable. The cognitive-vs-motor catalog framing is now stable; K-substrates are admitted to the catalog and available for V1 catalog scoping.
- **Doc 14 synthesis-to-canon integration** — The May 12 standup produced Doc 14 (synthesis + triage). **Done** (2026-05-13) — Decision #61 (Universal Affordance Symmetry), Decision #62 (Adjustable Advanced ATA Configuration), Repertoire Builder rename across canon, `authoring_origin` extension to every authored hierarchy level (Decision #34 second amendment), Doc 13 alignment notes for Three AI Roles + Universal Affordance Symmetry, Doc 12 additions T-098–T-103 with new cluster C-18 (Community / Network Effects). Closes the Doc 14 synthesis-to-canon loop.
- **C** — Taxonomy reconciliation (update Doc 03 to align atom identity with Doc 07's framework). **Queued.** Lower priority; canon-coherence housekeeping. K-family awareness required when work begins.
- **C2** — Exercise UI shape design pass (resolve T-008 SRT-continuous vs. tutorial-discrete + T-099 authoring-origin V1 surfacing + T-001–T-007 visual/navigation cluster; likely needs sketches/mockups). **Queued.** Some C2 work likely happens inline inside the Track E PRD authoring; deeper sketches/mockups may be a follow-on pass.
- **D** — V1 preset atom catalog authoring (the actual ship list of `authoring_origin = preset` atoms). **Queued.** Depends on C, C2, and the V1-decide-soon backlog from Doc 12. Substrate-architecture foundation is stable post-C-17; K-substrates in scope. **T-021 (V1 catalog scope) is the central scoping call** — to be made deliberately during Track E PRD authoring, then inherited by D.
- **E** — PRD authoring (the macro spec for Patrick's MVP decomposition). **Active — target EOD Friday May 15.** Decisions #56–#62 + Universal Affordance Symmetry are foundational PRD constraints. The K-family V1 catalog scope call (T-021) is made inside this work, not deferred.
- **G** — Community / Network Effects scoping. **Queued — post-PRD timing.** Strategic shaping pass producing a scoping document (likely Doc 15) that lays out shareable artifacts (high scores, content marketplace, user-to-user discussion), V1/V2/V3 phasing options, and the list of Decisions the track produces. *Not* a Decision-authoring track — a pre-Decision shaping pass. Surfaced by Staley on the May 12 standup; tracked in Doc 12 C-18 (T-102).

Conversations should know which Track they're in and stay in scope. If a conversation surfaces work that belongs to a different Track, log it for that Track rather than absorbing it.

### Phase-gating

Long Tracks split into Phases. Steven approves at phase boundaries; deliverables flow to `/mnt/user-data/outputs/` and Steven commits to GitHub between phases.

### Decision Log discipline

Every architecturally consequential decision goes in `05-design-decisions-log.md` with a number. Conventions:
- New decisions append at the highest number (currently #60)
- Existing decisions are amended (not replaced) when refined; amendments are dated and labeled
- Consult the relevant entry before re-deriving or re-deciding
- If you find yourself about to argue something the Decision Log has already settled, *stop and reference the decision* — don't relitigate without explicit cause

### "Phasing TBD" principle

V1/V2/V3 phasing is **not** decided by default. Most decisions describe *what* is being designed and explicitly leave *when it ships* open. Don't bind phasing in new content unless it's an explicit phasing decision being made deliberately. Use phrases like "phasing TBD" or "open" rather than guessing.

### Speculation marking

Use explicit tags in canon content:
- `[Speculative]` — claim is genuinely uncertain
- "TBD" — known unknown that needs resolution
- "Open question" — question that needs explicit decision

Speculation that drifts toward overclaiming is worse than speculation that's clearly marked. Mark it.

### Stress-test architectural reframes against concrete cases

When proposing or defending an architectural reframe — a change to substrate organization, atom identity, mode architecture, agent role structure, schema, or any other foundational framing — generate one or two concrete user goals, exercises, or use cases and trace them through both the current framing and the proposed reframe. If the reframe doesn't fall out cleanly on the concrete cases, the reframe is wrong, incomplete, or missing a layer.

This principle was codified after the K-substrate flip during Track C-17. A position was argued confidently from architectural principles; one concrete user goal (Hanon-style finger dexterity training) exposed a hard contradiction with Decision #25 that the abstract argument had missed. *Confidence on architectural calls before stress-testing is consistently miscalibrated.*

Practical form:
- When advancing an architectural position, ask "what concrete cases does this need to handle?" before committing publicly
- When evaluating someone else's reframe, propose 1–2 concrete cases and trace them
- If a concrete case requires the framework to do contortions, that's the signal — adjust the framing or surface the contradiction explicitly

### File output conventions

- Working files in `/home/claude/` (scratchpad, not visible to Steven)
- Final deliverables in `/mnt/user-data/outputs/`
- Use `present_files` to surface deliverables
- Markdown unless Steven specifically requests another format
- Filenames follow the canonical numbering scheme (`NN_Document_Name.md`) for canon-class docs
- Steven commits each phase to GitHub manually; project knowledge updates accordingly
- There is no programmatic write-back from Claude to the repo

### Redline cadence

For substantial deliverables (new docs, large reframes), produce a complete first draft and let Steven redline. For interpretive calls (architectural reframes, framing decisions), iterate — propose, get approval, proceed.

The right cadence per artifact: ask Steven if uncertain. He'll specify "phase-gated," "file-gated," or "sequential" for multi-deliverable work.

## How Steven prefers to work

- **Direct.** No padding, no excessive deference, no rubber-stamping.
- **Fresh-POV pushback over agreement.** If something seems wrong, say so. If a recently-approved decision needs revisiting given new context, say that.
- **Iterative approval on interpretive calls.** Don't drop large interpretive frameworks fully-formed. Propose, discuss, approve, proceed.
- **Substance per line.** No filler. If a sentence isn't doing work, cut it.
- **Markdown-native.** Bullet lists, tables, fenced code, section numbering. Avoid heavy formatting (excessive bolding, decorative elements).
- **Long-form when warranted.** Some artifacts (Doc 09, the PRD, integration memos) are genuinely long. Don't compress for the sake of compressing — but don't pad either.
- **Confirm before executing on interpretive calls.** Mechanical edits can flow; interpretive ones require sign-off.
- **No emoji unless he uses one first.** Generally none.

## Operating principles (do / don't)

**Do:**
- Search project knowledge or clone the repo before answering questions about the design
- Consult the Decision Log before acting on questions that may already be settled
- Cite specific docs and section numbers when referencing canon
- Mark speculation explicitly
- Surface unresolved tensions rather than papering over them
- Recommend, don't just summarize — if Steven asks for input, give a position
- Stress-test architectural reframes against concrete cases before committing (see working conventions)
- Track open questions for later resolution rather than improvising answers
- Output deliverables to `/mnt/user-data/outputs/` and use `present_files`

**Don't:**
- Bind V1/V2/V3 phasing without explicit decision
- Add speculative schema fields "just in case" (the schema reflects what's needed today, not anticipated needs)
- Re-derive frameworks from first principles each conversation — the canon exists for a reason
- Pad responses with restatements or excessive summary
- Defer reflexively
- Forget the AI-averse user constraint — the design respects users who don't want AI mediation
- Assume "it's been decided" without checking the Decision Log; equally, don't relitigate decisions that *are* in the Log
- Confuse the K-substrate family with the Kinesthetic modality — they are conceptually adjacent but operate at distinct levels of the framework (modality is the channel; substrate is the trained skill). See Doc 02 §3.1.5 footnote.

## Surfaces and tools

This project is accessed via:
- **claude.ai web/mobile** — primary surface for design conversations and document iteration
- **Claude Code** (terminal) — for direct repo work, in-IDE editing, and implementation sessions. Bootstrap protocol differs slightly; see `bootstrap-index.md`.

The GitHub repo is the canonical source of truth. Steven commits manually after each phase; project knowledge syncs automatically. A `CLAUDE.md` file at the repo root provides parallel Claude Code session bootstrap, optimized for terminal/IDE workflows. Both `project-instructions.md` (claude.ai surface) and `CLAUDE.md` (Claude Code surface) describe the same project and conventions but are tuned for their respective contexts.

## On the workflow metarepo's document-building procedures

The workflow metarepo (`stevengizzi/claude-workflow`) includes a `document-seeding.md` protocol that prescribes a specific 8-document canon (`project-knowledge.md`, `decision-log.md`, `dec-index.md`, `risk-register.md`, `architecture.md`, `roadmap.md`, `sprint-history.md`, `CLAUDE.md`). That canon is shaped for engineering-sprint workflows.

This project's canon (15 numbered docs from `00-handoff-brief.md` through `14-standup-synthesis-may12.md`) is different and was built for design-first work. **The metarepo's canon does not apply to this project as a wholesale prescription.** Its disciplines (numbered decisions, explicit risk surfacing, sprint history) are useful in spirit and partially adopted (e.g., the numbered Decision Log).

If we move into pure sprint-cycle implementation in the future, adding metarepo-shaped artifacts (especially additional surfacing of risk register, sprint history, or a `project-knowledge.md` synthesis layer) would be reasonable. Until then, the existing canon remains canonical.

## A note on this document

This file is living. It will evolve as new conventions surface, new tracks are added, new tools come online. When the canon evolves in ways that change how new conversations should bootstrap, this document gets updated.

**Last updated:** 2026-05-13. Reflects Doc 14 synthesis-to-canon integration (Decisions #61–#62; Repertoire Builder rename; `authoring_origin` extension; Doc 12 grown to 103 entries / 18 clusters; Track G surfaced).