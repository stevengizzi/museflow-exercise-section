# CLAUDE.md — MuseFlow Exercise Section + Agentic Future + External Communications

This file orients Claude Code sessions working in this repository.

## What this repo is

Design and (eventually) implementation workspace for three intertwined tracks of MuseFlow work:

1. **The MuseFlow Exercise Section** — one of MuseFlow's core content surfaces (a piano learning app). Currently late design / early implementation phase.
2. **MuseFlow's agentic future** — the AI-mediated "Projects" layer that helps users define goals and build personalized roadmaps. Currently early design phase, with active investor-demo target.
3. **Pitch deck and external communications** — pitch-ready material distilled from settled canon. Lives in Doc 13. Added 2026-05-12 as deliberate scope expansion supporting Patrick's fundraising work.

This is a **design-first repo**, not a sprint-cycle implementation repo. The bulk of the content is canonical design documentation. Implementation lives in MuseFlow's main codebase (separate repo); when implementation work happens here, it's mostly authoring and refining specs that engineering (Asif under Staley/Andrew) consumes.

## Repo layout

```
docs/
├── 00-handoff-brief.md            # Pre-A1 handoff; mostly historical
├── 01-project-bible.md             # Vision, content/path modes, foundational frameworks (PTA Loop, FTA Field, Novelty-Automaticity Spectrum §2.4, Universal Affordance Symmetry §8.9)
├── 02-system-architecture.md       # Substrate catalog (F/T/A/X/K), training methods, atom schema, semi-lattice engagement §3.2.1
├── 03-exercise-taxonomy.md         # Combinatorial exercise matrix, pruning rules, Technique cluster §11.5
├── 04-glossary.md                  # Vocabulary canon
├── 05-design-decisions-log.md      # 62 numbered decisions; consult before re-deciding
├── 06-exercise-blueprints.md       # 13 UI/interaction templates
├── 07-ux-navigation-spec.md        # Navigation model, configuration, agentic reframe (§8), open questions (§9)
├── 08-standup-synthesis-apr28-may5.md   # April/May 2026 team meetings synthesis
├── 09-agentic-museflow-vision.md   # Freestanding agentic-system vision; Three AI Roles §1.6; Universal Affordance Symmetry §1.7; Spectrum-driven roadmap composition §5.6
├── 10-may7-brainstorm-synthesis.md # May 7, 2026 brainstorm synthesis; source of Decisions #42–#47
├── 11-patrick-doc-integration-memo.md  # A2 deliverable; source of Decisions #48–#52
├── 12-open-question-triage.md         # Track B deliverable; 103-entry open-question inventory across 18 clusters
├── 13-pitch-deck-register-v0.1.md      # Pitch Deck & External Communications Register. Patrick is the primary consumer.
├── 14-standup-synthesis-may12.md       # May 12, 2026 standup synthesis + triage + Funnel cross-project handoff. Source of Decisions #61–#62.
└── archive/                        # Prior versions of substantially-revised canon docs (audit trail)
```

The canon evolves through a tracked sequence of conversations on claude.ai (Tracks A1, A2, B, C-17 done; C/C2/D/E/G queued). Steven commits to this repo manually after each phase. There is no programmatic write-back from Claude conversations.

## Reading order for orientation

For a fresh session, read in this order:

1. `docs/01-project-bible.md` — vision, content/path modes, foundational frameworks (PTA Loop, FTA Field, Novelty-Automaticity Spectrum, Universal Affordance Symmetry §8.9)
2. `docs/05-design-decisions-log.md` — 62 numbered decisions; this is the operational truth about what's been settled
3. `docs/07-ux-navigation-spec.md` — atom hierarchy, navigation model, open questions register
4. `docs/02-system-architecture.md` — schema definitions, substrate catalog (now including K-substrate family §3.1.5)
5. `docs/09-agentic-museflow-vision.md` — agentic system context; Three AI Roles framework §1.6; Universal Affordance Symmetry §1.7
6. `docs/10-may7-brainstorm-synthesis.md` — strategic synthesis; source of Decisions #42–#47 and several open-question clusters
7. `docs/11-patrick-doc-integration-memo.md` — A2 evaluation of Patrick's brainstorm doc; source of committed Decisions #48–#52
8. `docs/12-open-question-triage.md` — Track B deliverable; 103-entry open-question inventory across 18 clusters with full disposition. Working backlog for Tracks C2 / C / D / E / G. Consult §4.5 disposition summary and §8.6 Phase 3 resolutions before starting work in any downstream Track; individual entry status lines (RESOLVED / RETIRED) live with each T-NNN entry in §5. C-17 cluster entries (T-026, T-027, T-097) are Resolved as of 2026-05-12; reopened with T-100 (V2-defer) on 2026-05-13.
9. `docs/13-pitch-deck-register-v0.1.md` — Pitch Deck & External Communications Register. Read when external-comms work surfaces or when assembling pitch-ready content. Sections 1–4 are pitch-ready in v0.1; sections 5–8 are sketch/placeholder.
10. `docs/14-standup-synthesis-may12.md` — May 12, 2026 standup synthesis + triage + Funnel cross-project handoff. Source of Decisions #61 (Universal Affordance Symmetry) + #62 (Adjustable ATA Configuration). Reference document; not active design canon.

`docs/04-glossary.md` is reference-on-demand. `docs/03`, `docs/06`, `docs/08`, `docs/00` are read when relevant to the task. `docs/archive/` holds prior versions of substantially-revised canon docs (audit-trail only; not canon).

## Recent foundational additions (May 12–13 2026)

Seven framework concepts and product calls admitted to canon across the Track C-17 closeout (May 12) and the Doc 14 standup synthesis integration (May 13). Quick orientation for sessions that don't have time to read the full Doc 01 / 02 / 09 / 13 updates:

- **Novelty-Automaticity Spectrum** (Decision #56, Doc 01 §2.4) — central pedagogical axis: Novelty pole (Sight Reading; generalization) ↔ Automaticity pole (Exercises; automatic execution); Repertoire as synthesis midpoint with artistic-intent overlay. Fluency is the outcome.
- **K-substrate family** (Decision #57, Doc 02 §3.1.5) — motor-primary substrates, parallel-axis to F/T/A. Catalogs finger-independence, pivoting, stretching/squeezing, whole-hand translation, wrist rotation, octaves, trill, three staccato types, hand-coordination motion types, pedaling, three-system integration, etc.
- **Semi-lattice substrate engagement** (Decision #58, Doc 02 §3.2.1) — atom identity stays single-substrate; incidental substrate engagement is a graph computable at agent-reasoning time. *Tree for users, semi-lattice for the agent.*
- **Three AI Roles** (Decision #59, Doc 09 §1.6) — Coach (relationship-scoped), Composer-Librarian (content-scoped; Mage and Opusmodus are implementation tools here), Practice Partner (moment-scoped). Resolves the recurring Mage-vs-Opusmodus framing confusion.
- **Etudes + Variations on a Theme** (Decision #60, Doc 09 §9) — two distinct AI-generated-repertoire patterns. Etudes: AI-generated with explicit training intent. Variations: AI-mediated modification of existing repertoire along a complexity spectrum.
- **Universal Affordance Symmetry** (Decision #61, Doc 09 §1.7, Doc 01 §8.9) — every AI capability has a manual user-driven equivalent. AI mediation is a layer over user-accessible primitives, not a replacement. Load-bearing constraint on all subsequent design work; *test every feature design against "what's the user-driven equivalent?"*
- **Adjustable Advanced ATA Configuration** (Decision #62, Doc 04 Glossary "ATA") — Automatic Tempo Adjustment gets a configurable threshold panel + adjusted defaults; queued for Asif post the data-fixes freeze. Sight Reading mode primary; Exercise-mode interaction TBD.

Additionally, **Repertoire Builder** is the canonical name for the surface previously called "Repertoire Editor" (per Decision #34's May 12 amendment, sourced from Doc 14 §2.5). Use Repertoire Builder in all new writing.

## Who Steven is

**Steven Gizzi** (founder/CEO) — first-principles systems thinker, comfortable with complexity, treats documentation as handoff artifact. Prefers iterative ideation → blueprinting → spec. Values direct pushback over agreement.

**Current MuseFlow team:**
- **Staley** (CTO) — engineering at the highest level; agentic system / AI/ML infrastructure
- **Andrew Urbanowicz** (VP of Engineering) — Repertoire Builder, audio recognition, proactive nudging
- **Asif** (contractor) — primary implementer for exercise section work
- **Patrick Boylan** (co-founder) — product, marketing, pitch deck, fundraising. Primary consumer of Doc 13.

Older canon docs sometimes misattribute Staley's contributions to "Austin Clifton" — these are different people; Austin is a former engineer no longer with the team. Corrections are tracked in Decision #31.

## Working conventions

### Decision Log discipline

- New decisions append to `docs/05-design-decisions-log.md` at the highest number (currently 62)
- Existing decisions are amended (not replaced) when refined; amendments are dated and labeled
- Consult the relevant entry before re-deriving or re-deciding
- If you find yourself about to argue something the Log already settled, **stop and reference the decision** — don't relitigate without explicit cause

### "Phasing TBD" principle

V1/V2/V3 phasing is **not** decided by default. Most decisions describe *what* is being designed and explicitly leave *when it ships* open. Don't bind phasing in new content unless it's an explicit phasing decision being made deliberately.

### Speculation marking

Use explicit tags in canon content:
- `[Speculative]` — claim is genuinely uncertain
- `TBD` — known unknown that needs resolution
- `Open question` — question that needs explicit decision

Speculation that drifts toward overclaiming is worse than speculation that's clearly marked. Mark it.

### Stress-test architectural reframes against concrete cases

When proposing or defending an architectural reframe — substrate organization, atom identity, mode architecture, agent role structure, schema, or any other foundational framing — generate 1–2 concrete user goals or exercises and trace them through both the current framing and the proposed reframe. If the reframe doesn't fall out cleanly on concrete cases, the reframe is wrong, incomplete, or missing a layer.

This principle was codified after the K-substrate flip during Track C-17. A position was argued confidently from architectural principles; one concrete user goal (Hanon-style finger dexterity training) exposed a hard contradiction with Decision #25 that the abstract argument had missed. *Confidence on architectural calls before stress-testing is consistently miscalibrated.*

Practical form:
- When advancing an architectural position, ask "what concrete cases does this need to handle?" before committing publicly
- When evaluating someone else's reframe, propose 1–2 concrete cases and trace them
- If a concrete case requires the framework to do contortions, that's the signal — adjust the framing or surface the contradiction explicitly

### Edit safety

- **Read before editing.** Canon docs are tightly cross-referenced; an edit in one doc may need a parallel update elsewhere. Use `grep -rn "specific term" docs/` to find references before changing terminology.
- **Match style.** Each doc has internal stylistic conventions (heading levels, list formats, table formats). Match what's there rather than imposing a new style.
- **Cross-references must stay valid.** When citing a Decision, section, or document, verify the reference still exists.
- **K-substrate family vs. Kinesthetic modality** — these are conceptually adjacent but distinct framework elements. Don't conflate them in writing. K-substrate family is the trained-skill catalog; Kinesthetic modality is the perception/action channel. See Doc 02 §3.1.5 footnote for the canonical distinction.

### Git conventions

- Branch off `main` for any non-trivial work
- Commit messages: `docs: <short description>` for canonical doc updates; other prefixes (`feat:`, `fix:`, etc.) when implementation arrives
- Steven approves before pushing back to `origin/main` — even on the design canon
- Don't force-push or rewrite history on `main`

## Track system

Work is organized into named Tracks:

| Track | Purpose | Status |
|---|---|---|
| A1 | Doc-sync (integrate standup outputs) | Done |
| A2 | Patrick's "Theory Library & Exercise Section" doc evaluation | Done — Doc 11 v0.3; Decisions #48–#52 committed |
| B | Open-question triage | Done — Doc 12 committed (originally 97 entries across 17 clusters; grown to 103 across 18 with the May 13 additions); Decisions #53–#55 added; T-022 retired; cluster C-17 created |
| C-17 | Substrate-architecture refinement (T-026, T-027, T-097) | Done (2026-05-12) — Decisions #56–#60 + amendment to #13. Five frameworks admitted (Spectrum, K-family, Semi-lattice engagement, Three AI Roles, Etudes/Variations). Doc 13 created. Cluster reopened 2026-05-13 with T-100 (V2-defer). |
| (Doc 14 synthesis-to-canon integration) | Decision #61 (Universal Affordance Symmetry), Decision #62 (Adjustable ATA Configuration), Repertoire Builder rename, `authoring_origin` extension, Doc 12 additions T-098–T-103, C-18 cluster (Community) | Done (2026-05-13) — closes the Doc 14 synthesis-to-canon loop |
| C | Taxonomy reconciliation (Doc 03 ↔ Doc 07) | Queued — K-family awareness required; lower priority |
| C2 | Exercise UI shape design pass (resolve T-008 + T-099) | Queued — precursor to D; may interleave with E |
| D | V1 preset atom catalog authoring | Queued — depends on C, C2, and the V1-decide-soon backlog from Doc 12. Substrate-architecture foundation stable; K-substrates in scope. T-021 V1 catalog scope call is central. |
| E | PRD authoring | **Active — target EOD Friday May 15.** Macro spec for Patrick's MVP decomposition. Decisions #56–#62 + Universal Affordance Symmetry are foundational PRD constraints. |
| G | Community / Network Effects scoping | Queued — post-PRD timing. Strategic shaping pass producing scoping document (likely Doc 15) that lays out shareable artifacts, content/roadmap/exercise marketplace, V1/V2/V3 phasing options, and the list of Decisions the track produces. *Not* a Decision-authoring track — a pre-Decision shaping pass. Surfaced by Staley on May 12 standup; tracked in Doc 12 C-18 (T-102). |

A session should know which Track it's in. If a session surfaces work belonging to a different Track, log it for that Track rather than absorbing it.

## How Steven prefers to work

- **Direct.** No padding, no excessive deference, no rubber-stamping.
- **Fresh-POV pushback over agreement.** If something seems wrong, say so.
- **Iterative approval on interpretive calls.** Propose, discuss, approve, proceed.
- **Substance per line.** No filler.
- **Markdown-native.** Bullets, tables, fenced code, section numbering. Avoid heavy formatting.
- **Confirm before executing on interpretive calls.** Mechanical edits can flow; interpretive ones require sign-off.
- **No emoji** unless he uses one first.

## Operating principles (do / don't)

**Do:**
- Search the canon before answering questions about the design (`grep`, `rg`, etc. work fine on `docs/`)
- Consult the Decision Log before acting on questions that may already be settled
- Cite specific docs and section numbers when referencing canon
- Mark speculation explicitly
- Surface unresolved tensions rather than papering over them
- Recommend, don't just summarize — give a position
- Stress-test architectural reframes against concrete cases before committing (see working conventions)

**Don't:**
- Bind V1/V2/V3 phasing without explicit decision
- Add speculative schema fields "just in case"
- Re-derive frameworks from first principles each session — the canon exists for a reason
- Forget the AI-averse user constraint — the design respects users who don't want AI mediation
- Assume "it's been decided" without checking the Decision Log; equally, don't relitigate decisions that *are* in the Log
- Confuse the K-substrate family with the Kinesthetic modality (see Edit safety above)

## Common tasks

### Adding a new Decision

1. Read `docs/05-design-decisions-log.md` to confirm the topic isn't already covered
2. Append a new section at the end, using the highest unused number (currently next is #63)
3. Follow the existing format: `## Decision N: <Title>`, then `**Source:**`, `**Decision made:**`, `**Reasoning:**` (optional `**Alternative:**`, `**Phasing:**`, `**Cross-references:**`)
4. Cross-reference any related decisions
5. If the new decision contradicts or refines an earlier one, **amend** the earlier one with a dated note rather than replacing its body

### Editing canonical content

1. Identify which docs are affected. Use `grep -rn` for terminology consistency
2. For substantive changes, draft in a working copy first; review before committing
3. For cross-document changes, do them in one commit when possible (so the canon is internally consistent at every commit)
4. Update Decision Log if the edit reflects a new decision

### Updating Doc 13 (pitch deck register)

Doc 13 is a living register, not a bounded deliverable. Update when:
- The design canon adds material that is pitch-worthy (new Decisions, new framework concepts, new positioning)
- External communication surfaces a need the register doesn't yet cover
- Patrick's fundraising work surfaces investor-asked questions that need pitch-ready answers
- Sections 5–8 (Roadmap, KPIs, Investor Asks) firm up via Track D / Track E / fundraising work

Treat Doc 13 as the distillation layer between internal canon and external comms. Internal precision lives in Docs 01–12; pitch-friendliness lives in Doc 13.

### Searching the canon

```
grep -rn "term" docs/                         # find all references
rg --type md "term" docs/                     # ripgrep version (faster)
grep -nE "^## |^### " docs/01-project-bible.md  # section structure of a doc
```

## What this file is NOT

- **Not a substitute for the canon.** Read the actual docs for design content. This file orients you to *where* to look.
- **Not a substitute for the project instructions in claude.ai.** Those are the parallel orientation file for chat-interface conversations. Both files describe the same project but are optimized for their respective surfaces.
- **Not a sprint plan.** Work in this repo is currently design-first, not sprint-cycle implementation. If/when sprints arrive, additional artifacts (sprint history, risk register) may be added per the patterns in `stevengizzi/claude-workflow`.

## Workflow metarepo relationship

Steven maintains a separate repo `stevengizzi/claude-workflow` with general-purpose conversation protocols (Strategic Check-In, Sprint Planning, Mid-Sprint Doc-Sync, etc.). Those protocols are **engineering-sprint-shaped**. This project is currently design-first, so the metarepo's protocols apply in spirit (assumption audit, doc-sync principles) more than literally. Don't invoke a formal metarepo protocol unless it genuinely fits the current task.

## A note on this file

This file is living. Update it when conventions change, new tracks arrive, or new tools come online. Keep it terse — every line gets read at session start.

Last updated: 2026-05-13 (Doc 14 synthesis-to-canon integration — Decisions #61 + #62 admitted, Repertoire Builder rename across canon, `authoring_origin` extension to all hierarchy levels, Doc 12 grown to 103 entries across 18 clusters, Track G surfaced).