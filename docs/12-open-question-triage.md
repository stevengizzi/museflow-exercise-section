# Open-Question Triage — Inventory

**Track:** B (open-question triage)
**Phase:** 1 — Inventory + dedupe + stale check
**Status:** Draft for Steven's review (not yet committed)
**Date:** 2026-05-12

---

## 1. What this document is

This document is the Phase 1 deliverable of Track B. It is the **unified deduplicated inventory** of all open questions accumulated across the four primary registers plus the Decision Log, with provenance for each entry and stale-by-canon-evolution flags where Decisions #42–#52 (or earlier resolutions not formally retired) have answered or partially answered an entry.

It is **not yet a disposition**. Bucket assignment (decide-now / V1-decide-soon / V2-defer / explicit-punt / formally-retired) is Phase 2 work.

---

## 2. Methodology

**Sources scanned:**
- Doc 07 (UX & Navigation Spec) §8.6 *(treated as cross-reference provenance, not separate IDs — per Q2 confirmation)*
- Doc 07 §9 — primary register, 40 numbered entries
- Doc 09 (Agentic Vision) §13 — 55 numbered entries across §13.1–§13.11
- Doc 10 (May 7 Synthesis) §6.1 + §6.2 — 19 entries
- Doc 11 (Patrick Integration Memo v0.3) §11.1–§11.10 — 10 entries
- Decision Log — scanned for genuine architectural open items (not Phasing-TBD entries, per Q1 confirmation)

**Sources deferred to Phase 2 / later** *(per Q5 confirmation)*:
- Bible §2.1.1 candidate-content-modes list
- Individual decision amendments noting open sub-questions
- Doc 06 blueprint-level UX shape mentions
- Glossary entries with terms-pending-decision

Any additional registers encountered during reading are noted in §6.

**Dedup rule:** Two source entries are the same unified question if a single decision (architectural call, UX spec, or schema change) would close both. Sub-questions of a parent question get their own unified entry only when they could plausibly be resolved independently of the parent. Otherwise they fold in as cross-references.

**Stale flag rule:**
- `STALE` — the question is fully resolved by a Decision or canon evolution; the entry exists only because no register has formally retired it. Recommend retirement in Phase 2.
- `PARTIALLY STALE` — the architectural direction is resolved, but a specific sub-question (often UX or implementation) remains genuinely open. Entry stays in inventory; framing notes which part is resolved.

**ID scheme:** `T-NNN` numbered globally, cluster-ordered. Cluster tag noted at each entry.

---

## 3. Source register summary

| Source | Raw entries | Unique entries contributed |
|---|---|---|
| Doc 07 §8.6 | 9 | 0 (all subsumed) |
| Doc 07 §9 | 40 | ~28 (after dedup vs. Doc 09 §13) |
| Doc 09 §13 | 55 | ~50 (a few merge with §9 or Doc 10) |
| Doc 10 §6 | 19 | ~5 (most are duplicates of Doc 09 §13) |
| Doc 11 §11 | 10 | 10 (mostly substrate-fit edge cases; little overlap) |
| Decision Log | ~6 | 3 unique architectural items |
| **Raw total** | **139** | |
| **Unified total** | | **96** |

---

## 4. Cluster index

| ID | Cluster | Count | Likely Track |
|---|---|---|---|
| C-01 | Exercise Section UX (hierarchy, nav, card design, naming) | 7 | C2 / C |
| C-02 | Exercise UI session structure | 1 | **C2 (priority)** |
| C-03 | Configuration & performance-constraints UI | 3 | C2 / D |
| C-04 | Progress, completion, mastery (user-facing) | 4 | C2 / D |
| C-05 | Catalog authoring & enumeration | 9 | D |
| C-06 | Substrate-fit edge cases | 5 | C / D, partly B |
| C-07 | Per-blueprint catalog-time defaults | 3 | D |
| C-08 | Cross-section / Master Roadmap appetite | 1 | B / strategic |
| C-09 | Agentic — Project / Goal / Roadmap structure | 14 | Agentic track |
| C-10 | Agentic — AI Surface & Dashboard UX | 14 | Agentic track |
| C-11 | Agentic — Custom Content Generation & Authoring | 5 | Agentic track |
| C-12 | Agentic — MAGE, LLM Infra, User-Modeling, Cost | 8 | Agentic / Staley |
| C-13 | Engagement / Notifications | 4 | Andrew's track |
| C-14 | Pricing / Tiering / Gating | 7 | Patrick / strategic |
| C-15 | Teacher / Institutional | 6 | Patrick + Staley |
| C-16 | Content classes beyond core three | 5 | B / strategic |
| | **Total** | **96** | |

---

## 5. Unified inventory

### C-01 — Exercise Section UX (hierarchy, navigation, card design, naming)

**T-001 — *Universe visual metaphor.*** What does the cluster/strand/molecule/atom hierarchy look like visually? Planetary orbits, constellation map, skill tree, folder structure, or something else? Needs design exploration.
  Sources: UX §9 #1

**T-002 — *Zoom vs. flat library view.*** Should the Library zone always start at the cluster level and require progressive zoom-in, or should users be able to toggle between hierarchical and flat/filtered list views?
  Sources: UX §9 #2

**T-003 — *Substrate-grouped vs. modality-grouped toggle UX.*** How does the toggle between these two organizations work in the UI — tabs, dropdown, page restructure, or re-sort?
  Sources: UX §9 #3

**T-004 — *Exercise card design.*** What information does each card show at each level of the hierarchy? How much progress detail is visible before tapping in?
  Sources: UX §9 #4

**T-005 — *Atom/Molecule/Strand/Cluster naming for users.*** Internal vocabulary is set; user-facing equivalents are not. Users should never see "atom" or "molecule."
  Sources: UX §9 #13

**T-006 — *Default Browse view: preset-default vs. all-mixed.*** When a user enters a content mode's Browse flow, do they see all content together (with origin tags) or only MuseFlow presets, with custom/AI/community opt-in? AI-averse vs. full-power user tension.
  Sources: UX §9 #18

**T-007 — *User Paths naming.*** "User Paths" is a placeholder. Alternatives: "Playlists," "Plans." User-facing name TBD.
  Sources: UX §9 #19

---

### C-02 — Exercise UI session structure

**T-008 — *Exercise UI session structure: SRT-style continuous vs. tutorial-style discrete vs. other.*** Patrick's framing collapses all reading/playing exercises onto the SRT UI (continuous scroll, chevron gate, Game/Free Play toggle). The Interactive Tutorial UI presents a different shape (single-line prompt, prompt banner, discrete prompt-and-perform). Which session structure applies to which atom is undecided. Likely needs sketches/mockups; warrants its own design conversation. **This is the Track C2 anchor question.**
  Sources: Doc 11 §11.10
  Cross-refs: T-001 / T-002 / T-004 (general UX); T-024–T-026 (catalog scope, since session structure may constrain which atoms ship)

---

### C-03 — Configuration & performance-constraints UI

**T-009 — *Named presets vs. individual sliders for performance constraints.*** Presets simpler; sliders give more control. Default + "Advanced" toggle revealing sliders is a candidate pattern. Connects to Decision #52 (B/I/A as candidate derived label, not schema axis) — the user-facing summary label, if needed, can be derived from atom configuration at filter time.
  Sources: UX §9 #5
  Cross-refs: Decision #52 (the schema side is resolved; this is the UI side)

**T-010 — *Configuration persistence per atom.*** When a user adjusts settings for an atom, do those settings persist for next time, or reset to defaults? Per-atom persistence adds data storage complexity.
  Sources: UX §9 #6

**T-011 — *Cross-mode performance-constraints UI pattern.*** Per Decision #43, performance constraints are a cross-content-mode primitive. Shared-vs-mode-specific UI vocabulary is open: consistent enough for recognition across modes, specific enough that affordances make sense locally.
  Sources: UX §9 #33
  Cross-refs: Decision #43 (principle resolved; UI pattern still open)
  Status: **PARTIALLY STALE** — principle resolved by Decision #43; cross-mode UI pattern itself remains open.

---

### C-04 — Progress, completion, mastery (user-facing)

**T-012 — *Mastery tier system within atoms.*** Simple cleared/not-cleared per training method, or sub-tiers within each method (e.g., "cleared Multiple Choice at Easy" vs. "cleared Multiple Choice at Hard")? More tiers = more granularity, more visual complexity.
  Sources: UX §9 #7

**T-013 — *Completion incentive visual system.*** Stars, badges, checkmarks, fill colors, numeric scores? Needs design exploration aligned with MuseFlow's brand.
  Sources: UX §9 #8

**T-014 — *Streak and gamification interaction with atom system.*** Daily streak across any exercise? Per-strand streaks? Per-atom consistency tracking?
  Sources: UX §9 #9

**T-015 — *Completion handicap behavior with non-default assistance.*** When the user invokes any non-default assistance, the session is flagged as assisted. Display treatment (asterisk, visual flag, separate "assisted-clear" state) and downstream computation (does an assisted clear count toward molecule completion?) are open. Per Decision #38.
  Sources: UX §9 #32
  Cross-refs: Decision #38 (assistance-flagging principle set; per-atom/per-blueprint specifics open)

---

### C-05 — Catalog authoring & enumeration

**T-016 — *Content scope progression authoring.*** Difficulty ladders per substrate family need authoring and pedagogical review. Who authors — Steven, partially automated, mixed?
  Sources: UX §9 #10

**T-017 — *Distractor selection quality.*** Generation rules give structure; specific distractor selection within rules affects exercise quality. Random within valid options vs. curated to target common confusions?
  Sources: UX §9 #11

**T-018 — *V1 atom enumeration / total count.*** How many atoms does V1 contain across substrate families × modality combinations × content scope levels × target variable sets? Enumeration exercise needed. (Track D directly.)
  Sources: UX §9 #12, UX §9 #16 *(these are effectively the same question — total count emerges from the V1 catalog decisions)*
  Cross-refs: T-024 (V1 catalog scope question proper); T-022 (Five-exercises question)

**T-019 — *GMTF integration with exercise atom framework.*** GMTF complexity scoring needs mapping to atoms. Score derived from content scope? Target variables? Both? How does it attach?
  Sources: UX §9 #14
  Cross-refs: Decision #23 (use existing GMTF; don't reinvent — sets the principle; integration mechanic still open)

**T-020 — *Atom-creation validation rules.*** For the agentic future, the system needs to support creating new atoms outside the standard catalog. Can any valid combination of identity dimensions produce an atom, or are additional validation rules needed? *(Distinct from authoring-UI question T-046 — this is the schema-level constraint question.)*
  Sources: UX §9 #15

**T-021 — *V1 exercise catalog scope.*** Which substrate families, modality combinations, and content scope levels ship in V1? Single most important scoping question; determines build effort. (Track D direct deliverable.)
  Sources: UX §9 #16
  Cross-refs: T-018, T-022, T-024–T-029 (substrate-fit edge cases all feed this)

**T-022 — *Micro-PTA exercises in V1 scope.*** Should exercises explicitly training the endogenous micro-PTA loop (play with eyes closed, error recovery drills) be V1 or deferred? Current lean: deferred (per Decision #24).
  Sources: UX §9 #17
  Cross-refs: Decision #24 (deferred — directional resolution; V1 inclusion remains open as the deferred-by-default position)
  Status: **PARTIALLY STALE** — Decision #24 deferred beyond V1; entry stays in inventory in case V1 scope reopens this.

**T-023 — *Reverse-engineered catalog merger with bottom-up enumeration methodology.*** Track D will have two methodologies — top-down agent-demand and bottom-up substrate enumeration. What's the merge/triage process?
  Sources: Doc 10 §6 #4

**T-024 — *Five-exercises-cover-90% question.*** Staley asked Steven what five exercises could apply to ~90% of pieces. Patrick's catalog provides a partial answer. Worth answering deliberately as curriculum primitive and investor-demo framing?
  Sources: Doc 11 §11.8
  Cross-refs: T-021 (V1 catalog), T-023 (reverse-engineering methodology)

---

### C-06 — Substrate-fit edge cases

**T-025 — *Arpeggio cluster shape.*** Separate cluster parallel to Chords, sub-strand within Chords, or atoms with a "performance mode = arpeggiated" content-scope configuration? Real classification question per Patrick's A2.
  Sources: Doc 11 §11.2

**T-026 — *Pedaling exercises placement.*** Pedal substrate isn't in the current substrate catalog. Add as distinct substrate (likely under new "Articulation/Pedal" cluster), or treat as constraint/configuration on existing atoms? Probably distinct substrate; worth catalog-authoring conversation.
  Sources: Doc 11 §11.3

**T-027 — *Technique drills: exercises or distinct content class.*** Patrick's E category is pedagogically valid but doesn't fit the substrate-driven model. Candidates: V2 Exercise cluster, distinct content mode, blueprint variant with substrate="motor pattern", or performance-method atoms. **Priority elevated in Doc 11 v0.3** — blocks ~6 V1 preset candidates (A4 Hanon-style and E1–E5 finger independence / hand coordination / thumb crossing / hand position shifts / wrist rotation).
  Sources: Doc 11 §11.4
  Cross-refs: Decision #13 (improvisation+fingering placeholder — adjacent territory); T-094 (Content classes inventory)

**T-028 — *Genre tag granularity.*** Patrick's H category implies 5 genre buckets; his Quick Theory tagging implies more. Canonical list and granularity? Priority raised given Doc 10 §5.4 goal-category alignment — genre tags are load-bearing for Projects targeting "I'm interested in [genre]" or "play like [artist]" goals.
  Sources: Doc 11 §11.5

**T-029 — *Improvisation and creative exercises path.*** Patrick's F category exposes a real gap. As Projects mature and the exercise control surface stabilizes, does creative exercise design re-enter scope, or stay deferred indefinitely? Adjacent to renamed "Open Play" candidate content mode (deferred per Decision #41 + Decision #49 Part 2).
  Sources: Doc 11 §11.6
  Cross-refs: Decision #13 (defer); Decision #41 (Open Play candidate); Decision #49 Part 2 (renaming); T-094 (content classes)

---

### C-07 — Per-blueprint catalog-time defaults

**T-030 — *Mobile parity per blueprint defaults.*** Each of the 13 blueprints needs a `mobile_supported` value (`full` / `partial` / `none`). Default values per blueprint unspecified; will be set during catalog authoring.
  Sources: UX §9 #20
  Cross-refs: Decision #36, Decision #40

**T-031 — *Lit-Keys Mode applicability per blueprint defaults.*** Which atoms and blueprints support Lit-Keys assistance? Default values per blueprint unspecified.
  Sources: UX §9 #31
  Cross-refs: Decision #38

**T-032 — *Free Play (completion-policy) per-blueprint applicability defaults.*** Free Play is available on any atom that supports continuous-practice interaction (most PRF atoms; some REC/RCL atoms). Specific applicability per blueprint is open; Track D scoping concern.
  Sources: Decision #49 Part 1 (sub-question explicitly flagged open)

---

### C-08 — Cross-section / Master Roadmap appetite

**T-033 — *Cross-section Master Roadmap appetite.*** Patrick's §3.2 reveals team appetite for cross-section preset paths (Curriculum spanning Sight Reading + Repertoire + Exercises + Knowledge). Bible §2.2 anticipates Curriculum either dissolving into Projects or broadening into a multi-content-mode preset path. Open: which evolution wins, on what timeline? Does the team also want a non-AI-mediated, MuseFlow-authored, cross-content-mode Curriculum in addition to Projects?
  Sources: Doc 11 §11.7
  Cross-refs: Doc 09 §3.1 (architectural placement)

---

### C-09 — Agentic — Project / Goal / Roadmap structure & adaptation

**T-034 — *Multi-goal Projects.*** One Project per goal, or can a Project encompass multiple related goals?
  Sources: Doc 09 §13.1 #1
  Cross-refs: Doc 09 §4.5

**T-035 — *Project termination.*** When does a Project end? On goal completion, user dismissal, agent declaration, or timeout? Does it persist as "completed" archive?
  Sources: Doc 09 §13.1 #2

**T-036 — *Project sharing.*** Can a user share a Project (goal + roadmap) with another user? With a teacher? Its own object, or a snapshot?
  Sources: Doc 09 §13.1 #3

**T-037 — *Project pause/resume semantics.*** How are Projects paused and resumed? Does the agent reassess on resume?
  Sources: Doc 09 §13.1 #4

**T-038 — *Goal type taxonomy.*** Discrete categories the system reasons over, or everything free-form natural-language input?
  Sources: Doc 09 §13.2 #5

**T-039 — *Goal decomposition logic.*** How does the agent get from a goal to a roadmap? What's the model of musical skill composition?
  Sources: Doc 09 §13.2 #6

**T-040 — *Skill assessment for goal-relevant capabilities.*** How does the agent measure current state on the skills a goal requires? Direct atom mastery? Inferred from repertoire? Asked of the user?
  Sources: Doc 09 §13.2 #7

**T-041 — *Time-to-goal estimation.*** How does the agent project completion time? What does it base this on?
  Sources: Doc 09 §13.2 #8

**T-042 — *Roadmap node types completeness.*** Are the node types listed in Doc 09 §5.2 sufficient, or are others needed? Tutorial-node and Video-node placement is open. *(Clusters with C-16 content classes — but it's also a roadmap-structure question, hence here.)*
  Sources: Doc 09 §13.3 #9
  Cross-refs: T-095, T-096 (content-class placements); T-098 (tutorial-as-roadmap-node phasing)

**T-043 — *Roadmap topology.*** Is a roadmap always linear, or can it have branches, parallel tracks, optional sections?
  Sources: Doc 09 §13.3 #10

**T-044 — *Roadmap adaptation cadence.*** How often does the agent re-evaluate and update the roadmap?
  Sources: Doc 09 §13.3 #11

**T-045 — *User vs. agent edit authority on conflicts.*** When the user edits the roadmap and the agent adapts, who has authority on conflicts?
  Sources: Doc 09 §13.3 #12

**T-046 — *Auto-looping AI-judgment override.*** Steven flagged the algorithmic perfect-practice tree may need AI judgment to "break the rules" (e.g., actual issue is the previous measure, not the errored one). When does AI override the algorithm? How does the user perceive the override?
  Sources: Doc 09 §13.3 #13, Doc 10 §6 #2
  Cross-refs: Decision #42 (algorithm itself); Decision #44 (augmentation framing supports this pattern)

**T-047 — *Auto-looping ⟷ Optimal Grip relationship.*** Both are adaptive difficulty at different levels (Optimal Grip session-level; auto-looping practice-section-level). Are there situations where Optimal Grip's logic should drive auto-looping's parameters? Not pressing; worth defining when both are V1+.
  Sources: Doc 09 §13.3 #14, Doc 10 §6 #17

---

### C-10 — Agentic — AI Surface & Dashboard UX

**T-048 — *Levels-of-agency default for V1.*** Suggest-only, approve-by-default, or mixed?
  Sources: Doc 09 §13.4 #15

**T-049 — *AI surface UI location.*** Dedicated panel, in-Project, both, persistent vs. summoned?
  Sources: Doc 09 §13.4 #16

**T-050 — *Conversation persistence and searchability.*** Are AI conversations preserved across sessions? Searchable? Can the user reference past conversations?
  Sources: Doc 09 §13.4 #17

**T-051 — *Multi-session agent memory.*** Does the agent remember what it said before? How implemented? Sub-question of user-modeling-layer (T-064).
  Sources: Doc 09 §13.4 #18
  Cross-refs: T-064 (user-modeling implementation)

**T-052 — *Voice/text default modality for AI feedback.*** Voice vs. text vs. both; configurable per user; configurable per content mode? Steven OK with text-first per Doc 09 §6.5. Default behavior in V1 of voice-feedback capability is undefined.
  Sources: Doc 09 §13.4 #19, UX §9 #34, Doc 10 §6 #1

**T-053 — *End-of-round AI feedback timing.*** Steven's "in between plays" feedback per Doc 09 §6.1 — specific UX for the pause / feedback / setup-loop flow needs design. When does the agent fire? User's affordance to dismiss or accept?
  Sources: Doc 09 §13.4 #20, Doc 10 §6 #9

**T-054 — *Exercise and Sight Reading control surfaces enumeration.*** Per Doc 09 §6A, repertoire surface is enumerated (Decision #46). Exercise and sight-reading surfaces are sketched but not enumerated to the same depth.
  Sources: Doc 09 §13.4 #21, Doc 10 §6 #18

**T-055 — *AI-analogy implementation choices.*** Per Doc 09 §10.7. Diagnostic-agent / auto-engaged-plan-mode is prompt-level or application-level? Per-user "MD file" memory — single growing markdown vs. structured RAG store with retrieval logic? Decide deliberately rather than letting the analogy specify the implementation by default.
  Sources: Doc 09 §13.4 #22, Doc 10 §6 #14

**T-056 — *Onboarding path-split logic.*** How does the system decide which onboarding path (Projects-first vs. exploration-first vs. others) to surface to which user? Chooser, default rule, declared user type at signup, combination?
  Sources: Doc 09 §13.4 #23, UX §9 #36, Doc 10 §6 #19

**T-057 — *Dashboard rendering structure.*** How are Projects rendered on the dashboard? List, grid, tree, other?
  Sources: Doc 09 §13.6 #28

**T-058 — *Vertical roadmap visualization details.*** Working direction is vertical tree with branching. Specific rendering: pan/zoom across long roadmaps, mobile rendering, progress indicators, node-state visualization.
  Sources: Doc 09 §13.6 #29, UX §9 #35, Doc 10 §6 #8

**T-059 — *Cross-project "what to do today" view.*** Unified view that draws across Projects?
  Sources: Doc 09 §13.6 #30

**T-060 — *Project flow entry from content modes.*** What does the in-content-mode entry point look like? Button, command, AI summon? *(The "where does Project flow live in nav" lean is "both top-level dashboard + per-content-mode entry" per UX §8.6 #1 — this entry is about the per-content-mode entry point UX.)*
  Sources: Doc 09 §13.6 #31, UX §9 #24, UX §8.6 #1

**T-061 — *Agent live-toggle scope for Free Play completion-policy.*** Whether the agent can flip the Free Play toggle mid-session is open per Decision #46 (user live-toggle is established; agent live-toggle is separate). Sub-question of agent-policy capability design.
  Sources: Decision #49 Part 1 (sub-question explicitly flagged open), Decision #46
  Cross-refs: T-054 (exercise control surface enumeration)

---

### C-11 — Agentic — Custom Content Generation & Authoring

**T-062 — *Generation-on-demand UX flows.*** User-triggered, teacher-triggered, and agent-triggered generation are likely distinct flows. Specific UX unspecified for any of them.
  Sources: UX §9 #25, UX §8.6 #3
  Cross-refs: Decision #33 (capability committed; UX open)

**T-063 — *Custom atom authoring UI.*** How does the editor → atom flow work? Where do custom atoms live (private library, shareable, gradeable)? How are user-authored atoms validated for pedagogical coherence?
  Sources: UX §9 #26, UX §8.6 #4, Doc 09 §13.5 #27
  Cross-refs: Decision #34 (custom authoring path committed); T-020 (validation rules — schema-level)

**T-064 — *Generation cost limits.*** Is on-demand generation unlimited, rate-limited, or premium-gated? *(Architectural mechanism — distinct from the pricing-tier-design question in C-14.)*
  Sources: Doc 09 §13.5 #24
  Cross-refs: T-082 (Generation volume tiers — pricing side); Decision #37

**T-065 — *Generation provenance preservation.*** When generated content is shared (e.g., via marketplace), how is provenance preserved?
  Sources: Doc 09 §13.5 #25

**T-066 — *Pedagogical safety guardrails for AI-generated exercises.*** What guardrails or review layers prevent the agent from generating pedagogically unsound combinations?
  Sources: Doc 09 §13.5 #26, UX §8.6 #8

---

### C-12 — Agentic — MAGE, LLM Infrastructure, User-Modeling, Cost

**T-067 — *MAGE long-term role.*** Resolving toward augmentation per Decision #44 (MAGE persists as permanent algorithmic generation engine; AI adjusts MAGE's music-XML output). Full closure of Decision #39's open status awaits Staley's explicit retirement of the training-data-then-replacement framing.
  Sources: Doc 09 §13.7 #32, UX §9 #27, UX §8.6 #5
  Cross-refs: Decision #39 (logged open), Decision #44 (direction confirmed)
  Status: **PARTIALLY STALE** — direction resolved by Decision #44; full closure pending Staley framing-retirement.

**T-068 — *LLM-layer vs. user-modeling-layer ownership.*** Two interpretations of "we're an AI company" — LLM-layer expertise (Staley's current direction) and user-modeling-layer expertise (data structures, retrieval logic, AI-driven user-context store). Both defensible; both need explicit ownership. The implicit assumption that they're the same job will create gaps.
  Sources: Doc 09 §13.7 #33, Doc 10 §6 #13
  Cross-refs: Decision #47 (user-modeling layer recognized as foundational; ownership explicitly noted as separate question still open)

**T-069 — *User-modeling-layer implementation architecture.*** The user-model's actual shape — RAG over which data, with what retrieval logic, what summarization cadence, what user-correction affordances — needs concrete design.
  Sources: Doc 09 §13.7 #34
  Cross-refs: Decision #47 (architectural commitment made; implementation architecture explicitly out of scope of that Decision)

**T-070 — *Fine-tuning quality threshold.*** Can Bedrock-hosted models (or external API fallbacks) hit the quality bar at acceptable cost?
  Sources: Doc 09 §13.7 #35

**T-071 — *Frontier-model fallback commitment level.*** The line between "external-API fallback while we figure out the architecture" and "commit to frontier APIs as the architecture" needs to be drawn deliberately if cost forces it.
  Sources: Doc 09 §13.7 #36

**T-072 — *Cache strategy.*** What gets cached, for how long, with what invalidation rules?
  Sources: Doc 09 §13.7 #37

**T-073 — *Cost amortization model granularity.*** The team's "heavy generation periods amortize" framing needs a concrete mental model — at what generation rate do unit economics break? Per-Project, per-month, per-account?
  Sources: Doc 09 §13.7 #38, Doc 10 §6 #5

**T-074 — *"Large Music Model" framing for external use.*** As positioning, powerful. As implementation, it could imply training a single foundation model on music — not the team's direction. Whether this language enters customer- or investor-facing material warrants deliberate decision.
  Sources: Doc 09 §13.7 #39, Doc 10 §6 #10

---

### C-13 — Engagement / Notifications

**T-075 — *Notification policy.*** Frequency, opt-in/opt-out granularity, message variation logic.
  Sources: Doc 09 §13.8 #40

**T-076 — *Project-driven vs. activity-driven nudges balance.*** How does the engagement layer balance these?
  Sources: Doc 09 §13.8 #41

**T-077 — *Re-engagement targeting per user state.*** Which user states trigger which messages? (Trial-conversion vs. churn-prevention, e.g.)
  Sources: Doc 09 §13.8 #42

**T-078 — *Engagement layer × Project goals integration.*** How do Project goals and roadmap progress interact with the engagement/nudging layer? Re-engagement triggered by Project deadlines vs. by Project-agnostic activity patterns?
  Sources: UX §8.6 #7
  Cross-refs: Decision #19 amendment (the engagement layer itself); T-076

---

### C-14 — Pricing / Tiering / Gating

**T-079 — *Pricing model design.*** Not yet designed (Decision #37). Implications for which Project capabilities are free vs. paid?
  Sources: Doc 09 §13.9 #43, UX §9 #21, UX §8.6 #9
  Cross-refs: Decision #37 (deferred)

**T-080 — *Are exercises gated by tier?*** If so, by atom, by blueprint, by training method, by feature category, combination? Open until pricing structure exists.
  Sources: UX §9 #22

**T-081 — *Generation volume tiers per pricing tier.*** How many AI-generated exercises does a free user get?
  Sources: Doc 09 §13.9 #44, UX §9 #23
  Cross-refs: T-064 (architectural mechanism for limits)

**T-082 — *Project count limits per tier.*** Is there a limit on active Projects per user? Per tier?
  Sources: Doc 09 §13.9 #45

**T-083 — *Token-based pricing surfacing UX.*** Do users see token meters directly (Staley: "we could even surface tokens directly")? Or opaque "AI generations remaining"? Different UX implications.
  Sources: Doc 09 §13.9 #46, UX §9 #37, Doc 10 §6 #6

**T-084 — *MAGE pricing under augmentation framing.*** Under the augmentation framing, even MAGE-only generation could be charged for "tokens" since the AI adjusts MAGE's output. This conflates LLM compute with MAGE compute for billing. Right or wrong?
  Sources: Doc 09 §13.9 #47, Doc 10 §6 #7

**T-085 — *Patrick's atom-gating framing vs. Doc 09 §16 generation-cost framing.*** Patrick's "50% atom gating" treats exercises as scarce/curated; Doc 09 §16 treats generation cost (LLM tokens) as the variable expense. Resolution: pick a gating framing for the pricing conversation. Two candidate resolutions: (a) atom-gating wins; (b) generation-gating wins. Recommended lean from Doc 11: (b). Team-alignment question, not just a memo recommendation.
  Sources: Doc 11 §11.9
  Cross-refs: Decision #37; Doc 09 §16

---

### C-15 — Teacher / Institutional

**T-086 — *Teacher-assigned Projects.*** Can a teacher assign a Project to a student? Student then in a "managed Project" with different controls?
  Sources: Doc 09 §13.10 #48

**T-087 — *Curriculum-as-Project.*** Could a teacher's structured curriculum be expressed as a Project the system manages? Or is that a separate path mode (User Path with assigned attribution)?
  Sources: Doc 09 §13.10 #49

**T-088 — *Institutional / multi-user Projects.*** Could a school assign Projects across cohorts? How does multi-user Project authorship work?
  Sources: Doc 09 §13.10 #50

**T-089 — *Teacher → student data visibility UX.*** Teachers should see student progress per atom / molecule / strand / cluster. Specific UX (per-student dashboard, class roster view) unspecified.
  Sources: UX §9 #28

**T-090 — *Assignment flow first-class-ness.*** Teachers should assign atoms / molecules / strands / paths to specific students. Whether assignment is first-class (deadlines, completion tracking, feedback) or lighter-weight ("recommended" tag) is open.
  Sources: UX §9 #29

**T-091 — *Teacher-authored exercise sharing scope.*** Can teacher-authored exercises be shared with all of a teacher's students? All teachers? Public marketplace? Per-student only?
  Sources: UX §9 #30

---

### C-16 — Content classes beyond core three

**T-092 — *Content classes inventory beyond core three.*** What content classes exist beyond Exercise / Repertoire / Sight Reading? Candidates: ~~Theory~~ (resolved by Decision #48 as substrate family within Exercises), Open Play (deferred indefinitely per Decision #41 + #49 Part 2), Video / Knowledge Library (placement open per T-094), Interactive Tutorial (existing canonical content; placement open per T-093). Some may collapse/overlap.
  Sources: Doc 09 §13.11 #51, Doc 10 §6 #15
  Cross-refs: T-027 (Technique drills as candidate class); Decision #48 (Theory resolved); Decision #41 (Open Play deferred)
  Status: **PARTIALLY STALE** — Theory resolved by Decision #48; rest of cluster genuinely open.

**T-093 — *Interactive Tutorial architectural placement.*** Existing canonical content class (animated video + live-action hand clips + Phaser-JS exercises gated mid-flow) with no clean home in current architecture. Candidates: own content mode, path-mode primitive in Curriculum (matches current state), roadmap-node type prescribable by the agent, hybrid.
  Sources: Doc 09 §13.11 #52, Doc 10 §6 #16, UX §9 #39
  Cross-refs: T-042 (roadmap node types), T-098 (tutorial-as-roadmap-node phasing)

**T-094 — *Video Library / Knowledge Library architectural placement.*** Patrick's framing ("video library") leans content-mode-like; Staley's framing ("node-as-tutorial") leans roadmap-primitive. Decision #51 resolved deferral beyond V1 but not placement; current team-lean is Staley's framing, but placement remains formally open.
  Sources: Doc 09 §13.11 #53, Doc 10 §6 #11, Doc 11 §11.1
  Cross-refs: Decision #51 (deferral resolved; placement open)
  Status: **PARTIALLY STALE** — deferral-status resolved by Decision #51; architectural placement formally still open.

**T-095 — *Game Mode / Free Play toggle collapse pattern across modes.*** Current Sight Reading curriculum levels have Game Mode and Free Play toggles. As the content/path mode architecture is implemented, these may subsume into other functionality. Decision #49 Part 1 specifically extends Free Play into Exercise content mode; UX consolidation pattern across modes remains open. Distinct from Open Play (renamed; deferred indefinitely per Decision #49 Part 2).
  Sources: Doc 09 §13.11 #54, Doc 10 §6 #12, UX §9 #38
  Cross-refs: Decision #49 Part 1 (Free Play in Exercise mode resolved); Decision #49 Part 2 (Open Play renaming)

**T-096 — *Tutorial-as-roadmap-node phasing.*** If Interactive Tutorials become a roadmap-node type, near-term schema accommodation question: does the architecture allow human-authored tutorials as roadmap nodes in the meantime, even if AI-generated tutorials are deferred? This sub-question doesn't depend on resolving T-093 fully.
  Sources: Doc 09 §13.11 #55, Doc 10 §6 #3, UX §9 #40
  Cross-refs: T-093 (placement parent); T-042 (roadmap node types)

---

## 6. Stale / Resolved summary

### 6.1 Recommended for formal retirement in Phase 2 (no remaining open sub-question)

None found in this pass. Every register entry I reviewed either has a genuinely-open sub-question (treated as `PARTIALLY STALE` and kept in inventory) or a non-retired direction that may still want explicit retirement language even if substantively answered.

### 6.2 `PARTIALLY STALE` entries (kept in inventory; resolution status noted)

| T-ID | Topic | Resolved by | What remains open |
|---|---|---|---|
| T-011 | Cross-mode performance-constraints UI pattern | Decision #43 (principle) | UI pattern specifics |
| T-022 | Micro-PTA exercises in V1 scope | Decision #24 (deferred) | Whether V1 scope reopens this |
| T-067 | MAGE long-term role | Decision #44 (direction) | Full closure pending Staley framing-retirement |
| T-092 | Content classes inventory | Decision #48 (Theory) | Rest of the cluster |
| T-094 | Video Library architectural placement | Decision #51 (deferral) | Architectural placement formally open |

### 6.3 Decision Log items absorbed into inventory as new entries

| Decision | Sub-question | New T-ID |
|---|---|---|
| Decision #49 Part 1 | Per-blueprint Free Play applicability | T-032 |
| Decision #46 + #49 Part 1 | Agent live-toggle scope | T-061 |

### 6.4 Decision Log items I considered but did not generate entries for

- **Decision #25 open question** about navigating 500–2000-atom combinatorial space — the framework (atom/molecule/strand/cluster hierarchy with progressive zoom) has held up through subsequent work (Decisions #26, #40, #41 build on it without re-opening). Treating as silently resolved by canon evolution. Worth a Phase-2 explicit retirement note in Decision #25 if Steven wants the audit trail clean.
- **Phasing-TBD entries across Decisions #32–#52** — per Q1 confirmation, treated as committed decisions with intentionally-open sequencing, not as triagable open questions.

---

## 7. Notes for Phase 2 disposition

The following observations may matter when bucket assignment begins:

1. **C-02 (T-008)** is the single most blocking entry per Doc 11 v0.3's elevation, and the natural Track C2 anchor. Strong candidate for the V1-decide-soon bucket with C2 as the resolution venue.
2. **C-06 (substrate-fit edge cases)** — five entries that all gate Track D V1 catalog work. T-027 (Technique drills) is explicitly priority-elevated and blocks ~6 V1 preset candidates. Likely V1-decide-soon with B-track partial resolution where feasible, D-track for the rest.
3. **C-09 / C-10 / C-11 / C-12 (agentic clusters, 41 entries combined)** are mostly post-V1 work tied to the agentic track's roadmap. Most candidates for V2-defer or explicit-punt depending on investor-demo scope.
4. **C-14 (pricing, 7 entries)** is blocked by Decision #37 deferral; almost all entries are explicit-punt until pricing design begins. Exception: T-085 (gating-framing alignment) is a team-alignment question that can be resolved in advance of pricing design.
5. **C-15 (teacher, 6 entries)** is half tied to Patrick + Staley's instructor-portal track, half to schema/capability hooks owned by the exercise section. Bucket assignment needs to split between "exercise-section schema obligation" and "instructor-portal track concern."
6. **`PARTIALLY STALE` entries** all merit a Phase 2 decision: either close fully by extending the resolving Decision, or formally split into a resolved part + a new open question with a clearer scope.

---

## 8. Cross-reference index — source → unified ID

For traceability when Phase 2 redlines reference original registers.

### Doc 07 UX Spec §9

| Source # | Title (truncated) | Unified ID |
|---|---|---|
| 1 | Universe visual metaphor | T-001 |
| 2 | Zoom vs. flat | T-002 |
| 3 | Substrate-grouped/modality-grouped toggle | T-003 |
| 4 | Exercise card design | T-004 |
| 5 | Named presets vs. sliders | T-009 |
| 6 | Configuration persistence | T-010 |
| 7 | Mastery tier system | T-012 |
| 8 | Completion incentives | T-013 |
| 9 | Streak and gamification | T-014 |
| 10 | Content scope progressions | T-016 |
| 11 | Distractor quality | T-017 |
| 12 | Total atom count | T-018 |
| 13 | Atom/Molecule/Strand/Cluster naming | T-005 |
| 14 | GMTF integration | T-019 |
| 15 | Custom atom creation validation | T-020 |
| 16 | V1 exercise catalog | T-021 |
| 17 | Micro-PTA in V1 | T-022 |
| 18 | Default Browse view | T-006 |
| 19 | User Paths naming | T-007 |
| 20 | Mobile parity per blueprint | T-030 |
| 21 | Pricing structure | T-079 |
| 22 | Exercises gated by tier | T-080 |
| 23 | Generation volume limits | T-081 |
| 24 | Project flow entry points | T-060 |
| 25 | Generation-on-demand UX | T-062 |
| 26 | Custom atom authoring UI | T-063 |
| 27 | MAGE long-term role | T-067 |
| 28 | Teacher → student data visibility | T-089 |
| 29 | Assignment flows | T-090 |
| 30 | Custom exercise sharing | T-091 |
| 31 | Lit-Keys per blueprint | T-031 |
| 32 | Completion handicap behavior | T-015 |
| 33 | Cross-mode performance-constraints UI | T-011 |
| 34 | Voice/text default modality | T-052 |
| 35 | Vertical roadmap visualization | T-058 |
| 36 | Onboarding path-split logic | T-056 |
| 37 | Token-based pricing surfacing | T-083 |
| 38 | Game Mode / Free Play toggle collapse | T-095 |
| 39 | Interactive Tutorial UX placement | T-093 |
| 40 | Tutorial-as-roadmap-node UX | T-096 |

### Doc 07 §8.6 (cross-reference provenance only — no new IDs)

All 9 §8.6 entries absorbed: #1→T-060, #3→T-062, #4→T-063, #5→T-067, #7→T-078, #8→T-066, #9→T-079; #2 and #6 fold into agentic cluster entries.

### Doc 09 §13

| Source # | Cluster | Unified ID |
|---|---|---|
| #1–#4 | §13.1 | T-034–T-037 |
| #5–#8 | §13.2 | T-038–T-041 |
| #9–#14 | §13.3 | T-042–T-047 |
| #15–#23 | §13.4 | T-048–T-056 |
| #24–#27 | §13.5 | T-064, T-065, T-066, T-063 |
| #28–#31 | §13.6 | T-057, T-058, T-059, T-060 |
| #32–#39 | §13.7 | T-067–T-074 |
| #40–#42 | §13.8 | T-075–T-077 |
| #43–#47 | §13.9 | T-079, T-081, T-082, T-083, T-084 |
| #48–#50 | §13.10 | T-086–T-088 |
| #51–#55 | §13.11 | T-092–T-096 |

### Doc 10 §6

| Source # | Title (truncated) | Unified ID |
|---|---|---|
| #1 | Voice-LLM default | T-052 |
| #2 | Auto-looping AI override | T-046 |
| #3 | Tutorial-as-roadmap-node phasing | T-096 |
| #4 | Catalog merger methodology | T-023 |
| #5 | Cost amortization | T-073 |
| #6 | Token-based pricing | T-083 |
| #7 | MAGE pricing under augmentation | T-084 |
| #8 | Vertical roadmap visualization | T-058 |
| #9 | End-of-round AI feedback timing | T-053 |
| #10 | Large Music Model framing | T-074 |
| #11 | Video Library placement | T-094 |
| #12 | Game Mode / Free Play toggle collapse | T-095 |
| #13 | LLM-layer vs. user-modeling ownership | T-068 |
| #14 | AI-analogy implementation | T-055 |
| #15 | Content classes inventory | T-092 |
| #16 | Interactive Tutorial placement | T-093 |
| #17 | Auto-looping ⟷ Optimal Grip | T-047 |
| #18 | Exercise/SR control surfaces | T-054 |
| #19 | Onboarding path-split | T-056 |

### Doc 11 §11

| Source # | Title (truncated) | Unified ID |
|---|---|---|
| §11.1 | Where do videos live | T-094 |
| §11.2 | Arpeggio cluster shape | T-025 |
| §11.3 | Pedaling exercises | T-026 |
| §11.4 | Technique drills (priority elevated) | T-027 |
| §11.5 | Genre tag granularity | T-028 |
| §11.6 | Improvisation/creative | T-029 |
| §11.7 | Cross-Section Master Roadmap appetite | T-033 |
| §11.8 | Five-exercises-cover-90% | T-024 |
| §11.9 | Premium-tier framing vs. §16 cost | T-085 |
| §11.10 | Exercise UI session structure | T-008 |

### Decision Log items absorbed as new entries

| Source | Unified ID |
|---|---|
| Decision #49 Part 1 (per-blueprint Free Play applicability) | T-032 |
| Decision #46 + #49 Part 1 (agent live-toggle scope) | T-061 |

---

## 9. Approval gate

This is the Phase 1 deliverable. Phase 2 begins on approval.

If approved as-is, the suggested file commit name is `12-open-question-triage.md` per the kickoff. Phase 2 disposition will add bucket assignments (decide-now / V1-decide-soon / V2-defer / explicit-punt / formally-retired) per unified entry, and Phase 3 will work through the decide-now bucket inline.

Items I'd want input on if you'd like to redirect:

- **Cluster shape**: any clusters that should merge, split, or rename. C-07 (3 entries, "Per-blueprint catalog-time defaults") and C-08 (1 entry, "Cross-section Master Roadmap appetite") are the thinnest; flagging in case you'd rather fold them into C-05 and the strategic/agentic clusters respectively.
- **Stale handling**: §6.1 has zero formally-retire candidates. If you'd like a more aggressive stale interpretation (e.g., calling fully-resolved-by-direction items STALE rather than PARTIALLY STALE), I can re-pass.
- **Decision Log scope confirmation**: I added two Decision-Log-only entries (T-032, T-061). If those should not get their own T-IDs and should instead be tracked only as Decision sub-question notes, easy to remove.
- **Sub-question splitting**: T-018 collapses UX §9 #12 and §9 #16 (atom count and V1 catalog) since one resolves the other. If you prefer keeping them split, the count grows by 1.
