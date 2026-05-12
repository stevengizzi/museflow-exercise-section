# CLAUDE.md — MuseFlow Exercise Section + Agentic Future

This file orients Claude Code sessions working in this repository.

## What this repo is

Design and (eventually) implementation workspace for two intertwined tracks of MuseFlow work:

1. **The MuseFlow Exercise Section** — one of MuseFlow's core content surfaces (a piano learning app). Currently late design / early implementation phase.
2. **MuseFlow's agentic future** — the AI-mediated "Projects" layer that helps users define goals and build personalized roadmaps. Currently early design phase, with active investor-demo target.

This is a **design-first repo**, not a sprint-cycle implementation repo. The bulk of the content is canonical design documentation. Implementation lives in MuseFlow's main codebase (separate repo); when implementation work happens here, it's mostly authoring and refining specs that engineering (Asif under Staley/Andrew) consumes.

## Repo layout

```
docs/
├── 00-handoff-brief.md            # Pre-A1 handoff; mostly historical
├── 01-project-bible.md             # Vision, content/path mode architecture, foundational frameworks
├── 02-system-architecture.md       # Substrate catalog, training methods, atom schema
├── 03-exercise-taxonomy.md         # Combinatorial exercise matrix, pruning rules
├── 04-glossary.md                  # Vocabulary canon
├── 05-design-decisions-log.md      # Numbered decisions; consult before re-deciding
├── 06-exercise-blueprints.md       # 13 UI/interaction templates
├── 07-ux-navigation-spec.md        # Navigation model, configuration, agentic reframe (§8), open questions (§9)
├── 08-standup-synthesis-apr28-may5.md   # May 2026 team meetings synthesis
├── 09-agentic-museflow-vision.md   # Freestanding agentic-system vision
├── 10-may7-brainstorm-synthesis.md # May 7, 2026 brainstorm synthesis; source of Decisions #42–#47
├── 11-patrick-doc-integration-memo.md  # A2 deliverable; source of Decisions #48–#52
├── 12-open-question-triage.md         # Track B deliverable; 97-entry open-question inventory with disposition and resolutions
└── archive/                        # Prior versions of substantially-revised canon docs (audit trail)
```

The canon evolves through a tracked sequence of conversations on claude.ai (Tracks A1, A2, B done; C/C2/D/E queued). Steven commits to this repo manually after each phase. There is no programmatic write-back from Claude conversations.

## Reading order for orientation

For a fresh session, read in this order:

1. `docs/01-project-bible.md` — vision, content/path modes, foundational frameworks (PTA Loop, FTA Field)
2. `docs/05-design-decisions-log.md` — 55 numbered decisions; this is the operational truth about what's been settled
3. `docs/07-ux-navigation-spec.md` — atom hierarchy, navigation model, open questions register
4. `docs/02-system-architecture.md` — schema definitions, substrate catalog
5. `docs/09-agentic-museflow-vision.md` — agentic system context
6. `docs/10-may7-brainstorm-synthesis.md` — most recent strategic synthesis; source of Decisions #42–#47 and several new open-question clusters
7. `docs/11-patrick-doc-integration-memo.md` — A2 evaluation of Patrick's brainstorm doc; source of committed Decisions #48–#52
8. `docs/12-open-question-triage.md` — Track B deliverable; 97-entry open-question inventory with full disposition. Working backlog for Tracks C2 / C / D / E. Consult §4.5 disposition summary and §8.6 Phase 3 resolutions before starting work in any downstream Track; individual entry status lines (RESOLVED / RETIRED) live with each T-NNN entry in §5.

`docs/04-glossary.md` is reference-on-demand. `docs/03`, `docs/06`, `docs/08`, `docs/00` are read when relevant to the task. `docs/archive/` holds prior versions of substantially-revised canon docs (audit-trail only; not canon).

## Who Steven is

**Steven Gizzi** (founder/CEO) — first-principles systems thinker, comfortable with complexity, treats documentation as handoff artifact. Prefers iterative ideation → blueprinting → spec. Values direct pushback over agreement.

**Current MuseFlow team:**
- **Staley** (CTO) — engineering at the highest level; agentic system / AI/ML infrastructure
- **Andrew Urbanowicz** (VP of Engineering) — repertoire editor, audio recognition, proactive nudging
- **Asif** (contractor) — primary implementer for exercise section work
- **Patrick Boylan** (co-founder) — product, marketing, pitch deck, fundraising

Older canon docs sometimes misattribute Staley's contributions to "Austin Clifton" — these are different people; Austin is a former engineer no longer with the team. Corrections are tracked in Decision #31.

## Working conventions

### Decision Log discipline

- New decisions append to `docs/05-design-decisions-log.md` at the highest number (currently 55)
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

### Edit safety

- **Read before editing.** Canon docs are tightly cross-referenced; an edit in one doc may need a parallel update elsewhere. Use `grep -rn "specific term" docs/` to find references before changing terminology.
- **Match style.** Each doc has internal stylistic conventions (heading levels, list formats, table formats). Match what's there rather than imposing a new style.
- **Cross-references must stay valid.** When citing a Decision, section, or document, verify the reference still exists.

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
| B | Open-question triage | Done — Doc 12 committed (97 entries, 17 clusters); Decisions #53–#55 added; T-022 retired; new cluster C-17 (substrate-architecture refinement) surfaces T-097 (cognitive-vs-motor distinction) pairing with T-026 + T-027 |
| C | Taxonomy reconciliation (Doc 03 ↔ Doc 07) | Queued |
| C2 | Exercise UI shape design pass (resolve T-008 / former Doc 11 §11.10) | Queued — precursor to D and E |
| D | V1 preset atom catalog authoring | Queued — depends on C, C2, and V1-decide-soon backlog from Doc 12. **Foundational sub-task:** C-17 substrate-architecture refinement (T-026 + T-027 + T-097) must resolve before catalog authoring. |
| E | PRD authoring | Queued — depends on D substantially complete |

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

**Don't:**
- Bind V1/V2/V3 phasing without explicit decision
- Add speculative schema fields "just in case"
- Re-derive frameworks from first principles each session — the canon exists for a reason
- Forget the AI-averse user constraint — the design respects users who don't want AI mediation
- Assume "it's been decided" without checking the Decision Log; equally, don't relitigate decisions that *are* in the Log

## Common tasks

### Adding a new Decision

1. Read `docs/05-design-decisions-log.md` to confirm the topic isn't already covered
2. Append a new section at the end, using the highest unused number
3. Follow the existing format: `## Decision N: <Title>`, then `**Source:**`, `**Decision made:**`, `**Reasoning:**` (optional `**Alternative:**`, `**Phasing:**`, `**Cross-references:**`)
4. Cross-reference any related decisions
5. If the new decision contradicts or refines an earlier one, **amend** the earlier one with a dated note rather than replacing its body

### Editing canonical content

1. Identify which docs are affected. Use `grep -rn` for terminology consistency
2. For substantive changes, draft in a working copy first; review before committing
3. For cross-document changes, do them in one commit when possible (so the canon is internally consistent at every commit)
4. Update Decision Log if the edit reflects a new decision

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

Last updated: May 12, 2026 (Track B Phase 3 close).