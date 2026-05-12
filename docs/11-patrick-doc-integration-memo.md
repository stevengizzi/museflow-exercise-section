# Patrick's Theory Library & Exercise Section Doc: Integration Memo

> **Status: A2 deliverable, v0.3 (May 2026).** Supersedes v0.2. Same structural skeleton; targeted edits absorbing Steven's redlines on v0.2.
>
> **v0.3 changes from v0.2:**
> - **§3.1** demoted from clean Alignment to a more nuanced "primitives reusable, session structure undecided" framing, recognizing that the Sight Reading Trainer UI and the Interactive Tutorial exercise UI are distinct shapes and Patrick's wholesale SRT-reuse claim is too broad. Added new §11.10 (exercise UI session structure) and flagged the broader "how exercises look and function" conversation as out of A2 scope. The §8 mapping table is unaffected — it references blueprint IDs without committing to a UI shape per blueprint.
> - **§3.8** softened — carousel-card design is "one possible UI direction among several, not endorsed," not a candidate-for-the-surface endorsement.
> - **§5.1 / Decision #49** rewritten — Game Mode / Free Play is an established MuseFlow Sight Reading pattern (visible in production today), not Patrick's invention; live-toggleability of the completion-policy element during a session preserved as a requirement (matching the existing SRT pattern); the Andrew's-editor mischaracterization removed; the "Free Play" terminological collision flagged with a proposed resolution bundled into Decision #49 (rename the deferred candidate content mode currently called "Free Play original sense" to "Improvisation" or similar, freeing up "Free Play" for the established meaning).
> - **§5.4 / Decision #50** reframed — Patrick's specific thresholds are candidate starting defaults, one configuration in an n-dimensional matrix, easily overridable per atom by AI, preset, or user input. Decision #50 no longer commits the specific numbers; it commits the methodology of having defaults at all.
> - **§7.4** expanded — five additional candidate names for the renamed video surface (Insights, Discover, Reference, Study, Topics) with tradeoff notes; recommendation to keep "Knowledge Library" as the working name and defer the final naming call to when the feature actually enters scope.
> - **§8** framing clarification — the "V1 atom catalog" means the **preset inventory** that ships with MuseFlow at V1 (`authoring_origin = preset`), distinct from the full combinatorial matrix the framework supports. Patrick's templates evaluate as preset-inventory candidates specifically.
> - **§8 mapping table + §11.4** — A4 (Hanon-style) and E1–E5 (technique drills) reframed from unconditional V2 defers to **defer-conditional-on-§11.4** (the technique-drilling architectural placement question). §11.4 priority escalated since it now blocks ~6 V1 preset candidates.
> - **§11.10** added (new open question on exercise UI session structure).
> - **§12** updated absorption summary and added an explicit note on conversations to stage outside A2 scope.
>
> **v0.2 carryover (unchanged):** Renumbering from v0.1's proposed Decisions #42–#46 to #48–#52 (since #42–#47 are now committed canon); post-Phase-2 canon awareness throughout — committed Decisions #42–#47, Bible §2.3 and §6.3 cross-mode reframes, Doc 02 §5.1 cross-mode framing, Doc 09 §1.2 (user-modeling layer pillar), §6A (Agent Control Surfaces per Content Mode), §13.11 (Content Classes Beyond the Core Three), §16 (Cost Considerations), the Glossary's new Interactive Tutorial entry, and Doc 10's 5 demo-relevant goal categories.
>
> **Source documents referenced:** Project Bible (Doc 01), System Architecture (Doc 02), Exercise Taxonomy (Doc 03), Glossary (Doc 04), Design Decisions Log (Doc 05), Exercise Blueprints (Doc 06), UX & Navigation Spec (Doc 07), Standup Synthesis (Doc 08), Agentic MuseFlow Vision (Doc 09), May 7 Brainstorm Synthesis (Doc 10).
>
> **Methodological note.** Steven explicitly framed Patrick's doc as "important context for what he's thinking" — not a vision to merge in. This memo treats Patrick's content as evaluable input, agrees where his framing is sound, disagrees where ours is better, and absorbs concretely where absorption strengthens the design. Speculative claims are tagged `[Speculative]`. Open questions surfaced are collected in §11.
>
> **Scope clarification (carried from v0.2).** This memo evaluates Patrick's "Theory Library & Exercise Section: Comprehensive Feature Brainstorm & Design Specification" (~1167 lines, written several months prior). Patrick's separately-referenced PRD that surfaced in the May 7 brainstorm — the one containing the auto-looping / perfect-practice tree algorithm (Decision #42) — is **not the same artifact** as the brainstorm doc evaluated here. The brainstorm doc does not contain auto-looping. Evaluating Patrick's PRD against canon is a separate piece of work that may be warranted; this memo does not perform it.
>
> **Out-of-A2-scope conversations (new framing in v0.3).** Two conversations surfaced during v0.2 review that are explicitly not absorbed by this memo: (a) the broader "how do different exercises look and function" conversation — exercise UI shape and session structure is currently underspecified in canon (see §11.10), and resolving it requires its own design session, likely with mockups and prototypes; (b) the full V1 atom catalog authoring conversation — this is Track D. The §8 mapping table provides candidate inputs to Track D; it does not constitute Track D.

---

## 1. Executive Summary

1. **Patrick's doc is a "specific UI features and ~50 exercise templates" document.** Our canon is a "first-principles generative architecture" document. The gap has widened since v0.1: post-Phase-2 canon now extends the architecture across modes (Decision #43 promotes performance constraints to a cross-mode primitive; Decision #46 / Doc 09 §6A enumerates per-mode agent control surfaces; Decision #47 / Doc 09 §1.2 elevates the user-modeling layer to a vision pillar). Patrick's enumerated templates sit two architectural levels below this scaffolding. Most apparent conflicts remain category mismatches.

2. **The "Theory" naming collision is the headline structural conflict, and it now sits inside a formally-tracked cluster.** Doc 09 §13.11 (Content Classes Beyond the Core Three) explicitly clusters the Theory mode-status question with the Video Library placement question (#53), the Interactive Tutorial placement question (#52), and Free Play original-sense status (#54). **Recommendation: Path (c) — rename Patrick's surface ("Knowledge Library" or "Learn" are leading candidates), and resolve the candidate Theory content mode to "no, theory is just a substrate family within Exercises."** See §7. The renamed Knowledge Library's architectural placement is the §13.11 #53 sub-question; recommended resolution: agent-surfaced video as roadmap-node primitive (Staley framing), not standalone content mode (Patrick framing).

3. **Patrick's doc predates the agentic Projects pivot (Decision #32) and the Content/Path Mode reframe (Decision #41).** Subsequent commits — Decision #43 (cross-mode performance constraints), Decision #46 (per-mode control surfaces), Decision #47 (user-modeling layer) — extend the gap further. Patrick's "Future Unified Roadmap" (his §3.2) is closer to an expanded Curriculum than to Projects; our Projects framing has effectively superseded it.

4. **Patrick's ~50 exercise templates (Categories A–H) map cleanly to our framework as concrete atom instantiations** (mapping table in §8). The templates are valuable inputs to V1 catalog authoring; their passing criteria feed `mastery_thresholds` (Decision #40), which is now best framed as an exercise-section formulation of the cross-mode performance-constraints primitive (Decision #43, Bible §2.3, Doc 02 §5.1).

5. **Patrick's flat B/I/A difficulty axis conflicts with our 3-axis model (Decision #7) — and the conflict is sharper post-Phase-2.** Decision #43 makes performance-constraint tightness a primitive that travels across content modes. A flat B/I/A label cannot capture cross-mode constraint tightness without losing what makes it useful. **Recommendation: keep the 3-axis model as the engine; defer the question of whether B/I/A appears as a derived user-facing summary label to UX exploration.** See §4.3.

6. **Patrick's "Game Mode vs. Free Play" distinction is an established MuseFlow Sight Reading pattern, not Patrick's invention** (v0.3 correction — the toggle ships in production today; Patrick is echoing it into the exercise context). The pattern is still worth absorbing into the Exercise content mode. Architectural home: a **completion-policy element of the exercise control surface** (Doc 09 §6A.2), live-toggleable during a session (preserving the existing SRT affordance), not a new top-level `session_mode` schema enum. Decision #45 has already formalized the analogous capability ("no completion criteria, just play endlessly") for user-generated sight-reading. **Naming collision flag:** "Free Play" as completion-policy collides with "Free Play" as the deferred candidate content mode for open-ended improvisation (Bible §2.1.1, Decision #45 clarification). Proposed resolution (bundled into Decision #49): rename the deferred candidate to "Improvisation" or similar, freeing "Free Play" for the established meaning. See §5.1.

7. **Patrick's "Proactive Suggestion System" now maps onto three canon scaffoldings, not just one.** The substrate is the user-modeling layer (Decision #47, Doc 09 §1.2); the action vocabulary is the per-mode control surfaces (Decision #46, Doc 09 §6A); the interaction surface is the engagement layer (Decision #19 amendment, Glossary "Engagement Layer"). Patrick's trigger conditions and modal design remain the most concrete instantiation anyone on the team has produced. **Recommendation: absorb as candidate engagement-layer behavior**, scaffolded against all three layers. See §5.2.

8. **Patrick's gamification specifics (named achievements, Practice Points)** should NOT be absorbed at the PRD level. Stay framework-only (the schema supports per-atom tracking; achievements are a derived layer); let Patrick himself decide gamification specifics during MVP decomposition. See §4.7.

9. **Patrick's premium tier proposal is now in tension with the post-Phase-2 cost framework (Doc 09 §16).** Patrick's "50% of exercises gated to premium" treats atoms as scarce/curated content. The §16 framework treats heavy generation (LLM cost) as the variable expense to gate against; atom access — once generated and stored — is not the bottleneck. Patrick's gating intuition is salvageable but applies to AI-generated custom content, not to baseline atom inventory. **Recommendation: preserve as input to the pricing-design conversation; flag the §16 tension explicitly.** See §4.8.

10. **The Theory Library as a video-content surface is conceptually viable but deferred beyond V1.** Doc 09 §13.11 #53 now tracks this as a formal open question with two framings: Patrick's (content-mode-like) and Staley's (node-as-tutorial). **Recommendation: defer per v0.1; lean toward Staley's framing as the resolution** — agent-surfaced video as a roadmap-node type (parallel to how Interactive Tutorial is positioned), not a top-level content mode. See §4.6.

---

## 2. What Patrick's Doc Is

A ~1167-line design specification, written several months prior to the current canon. Three parts:

**Part 1 — Theory Library (lines 9–164):** A separate top-level app surface dedicated to embedded video content from YouTube and TikTok. Compliance-oriented (open-access required by YouTube ToS for embedded content). Three sub-surfaces: **Smart Feed** (personalized landing page, social-feed UI, curated by curriculum progress + performance patterns + repertoire context), **Quick Theory** (TikTok-style short-form vertical video grid, endless scroll), **Deep Dives** (YouTube-style long-form library with search/filter, including premium artist content). Includes a **Proactive Suggestion System** that triggers theory-video modals based on real-time performance pattern detection.

**Part 2 — Exercise Section (lines 166–1125):** A separate top-level sidebar section. Core principles include: fixed/repeatable drills (vs. the never-repeating Sight Reading Trainer), Game Mode vs. Free Play, familiar UI for sheet-music exercises (reuse the Sight Reading Trainer UI), and an intelligent recommendation engine. Then an exercise catalog organized into **eight categories (A–H)**:

- **A** — Sheet Music-Based Technical Exercises (Scales, Arpeggios, Chord Progressions, Hanon-Style, Interval Reading, Sight Reading Challenges, Articulation/Dynamics, Pedaling) — 8 templates
- **B** — Rhythm Exercises (Tapping, Polyrhythm, Dictation, Sight Reading) — 4 templates
- **C** — Ear Training (Interval Recognition Melodic + Harmonic, Chord Quality, Melodic Dictation, Harmonic Progression, Bass Line Dictation, Rhythm Dictation, Scale Degree) — 8 templates
- **D** — Music Theory Quizzes (Note Naming, Key Signature, Chord Spelling, Interval on Staff, Time Signature, Circle of Fifths, Enharmonic) — 7 templates
- **E** — Technique and Coordination Drills (Finger Independence, Hand Coordination, Thumb Crossing, Hand Position Shifts, Wrist Rotation, Velocity Control) — 6 templates
- **F** — Creative and Improvisation (Call and Response, Improvisation over Progressions, Melody Completion, Chord Voicing) — 4 templates
- **G** — Sight Reading Specializations (Clef Reading, Transposition, Score Reading) — 3 templates
- **H** — Genre-Specific (Classical, Jazz, Blues, Pop/Rock, Latin) — 5 templates

Each template has: description, UI template, variations (often as a table), difficulty progression (mostly "unlocks after Level X"), and Game Mode passing criteria (most commonly "four consecutive at 95% accuracy and goal tempo"). Section 2.3 describes the Exercise Section UI (categorized scrollable list, "Recommended for You" carousel, search/filter). Section 2.4 covers progression and gamification (B/I/A difficulty, named achievements, Practice Points, daily streaks).

**Part 3 — Integration and Future Considerations (lines 1127–1167):** Three short subsections — Cross-Feature Integration (curriculum, performance-based recs, data dashboard); the **"Master Roadmap"** vision (one paragraph, §3.2: a unified cross-section roadmap integrating Sight Reading + Repertoire + Theory Library + Exercise Section); and a Premium Content Strategy (Free vs. Premium tier specifics).

**What the brainstorm doc does NOT contain:** the auto-looping / perfect-practice tree algorithm (Decision #42, Doc 09 §6A.1) that surfaced in the May 7 brainstorm as already specified in "Patrick's PRD." Whatever PRD that reference points to, it is a different artifact. The brainstorm doc evaluated here makes no mention of auto-looping, perfect-practice trees, or loop-boundary detection from green-note history.

---

## 3. Alignment Register

Items where Patrick and our canon agree. These are confidence-building data points — independent thinking converging.

### 3.1 Notation rendering primitives reusable; session structure undecided *(substantially revised in v0.3)*

Patrick (§2.1, "Familiar UI for Sheet Music Exercises") proposes that any exercise involving reading/playing notation should use the Sight Reading Trainer UI — the two-line music display, tempo control, chevrons, accuracy %, three-state feedback (green/yellow/red). v0.2 absorbed this as clean Alignment; v0.3 narrows the claim.

**What's clearly alignable.** The notation rendering primitives — staff rendering, note-shape rendering, three-state per-note feedback (green/yellow/red), real-time MIDI-input matching — are reusable across exercise UI shapes. These primitives already exist in the MuseFlow codebase via the SRT and are the right starting point for exercise rendering. No disagreement here.

**What's not yet decided.** The SRT UI is a *specific* session structure: continuous two-line scrolling playback, chevron-based clearance gate (4 chevrons at ≥95% accuracy to clear), automatic tempo adjustment, Game / Free Play toggle, BPM display with adjustment controls. It is designed for *non-stop continuous playing* — top line, bottom line, top line refreshes while bottom plays, etc. The Interactive Tutorial exercise UI (per the Glossary canonical entry, and visible in current MuseFlow tutorials) presents a *different* session structure: a single line of music with a prompt banner above ("Play this line of music in sync with the metronome"), Chapters sidebar for tutorial-flow navigation, progress bar at the bottom, and discrete prompt-and-perform evaluation rather than continuous scroll. Both are valid; neither is the "right" exercise UI a priori.

Patrick's templates plausibly fit different session structures. Some (A1 Scales, A3 Chord Progressions, B4 Rhythm Sight Reading) could go either way — continuous scrolling or discrete prompt-and-perform. Others (B1 Rhythm Tapping, D1 Note Naming flashcards) more obviously fit a discrete prompt-and-perform shape; the SRT's continuous-scroll affordance is awkward for flashcard-style identification. Patrick's wholesale "use SRT UI" framing flattens this distinction.

**What v0.3 commits to.** Reuse the notation rendering primitives and three-state feedback. Defer the session-structure choice per atom (or per blueprint) to a dedicated design conversation. New open question added in §11.10. The broader "how do different exercises look and function" conversation is its own piece of work outside A2 scope.

**Mapping table implications.** The §8 mapping table references blueprint IDs (BP-05, BP-06, BP-07) without committing to a UI shape per blueprint, so the table itself is consistent with this softening. The conflation was concentrated in §3.1's v0.2 framing; correcting §3.1 corrects the broader claim.

### 3.2 Pattern-recognition driven recommendations
Patrick's "performance-based recommendations" (§1.2 Smart Feed, §2.1 Recommendation Engine, §3.1) — surfacing exercises and content based on backend-detected error patterns — aligns with our V2 Recommended Exercises feature (Bible §9.1) and the engagement layer (Decision #19 amendment). **v0.2 strengthening:** what Patrick is sketching here is, in its mature form, the user-modeling layer (Decision #47, Doc 09 §1.2). His "performance-based recommendations" presupposes a per-user accumulating model — the load-bearing capability that Decision #47 has now made a foundational architectural commitment. Patrick's instinct that "the system should know the user well enough to surface relevant content" aligns with canon's most strategic technical claim, and that alignment is non-trivial.

### 3.3 Recommendations at end-of-tier and end-of-level
Patrick's "End of Tier" and "End of Level" recommendation triggers (§2.1) match the natural surface points for cross-section nudging in our model (curriculum completion → exercise/repertoire suggestions). The mechanism survives translation; only the surrounding architecture differs (his is curriculum-tied; ours is more flexible because it can also work via Projects and the engagement layer).

### 3.4 Soft-unlock vs. hard-unlock progressively
Patrick repeatedly uses "soft-unlock" language for difficulty progression (e.g., A1 Scales: "soft-unlock based on curriculum level in end of level modal, but user can decide to play any of them at any time"). This is consistent with our canon's positioning of `prerequisite_atoms` as load-bearing for agent path-building (Decision #40) but not as a hard gate on user navigation. Users in our system can practice anything they want from the Library zone (UX Spec §3.1); recommendations *surface* relevant atoms, they don't *restrict* access.

### 3.5 Streaks
Both treat daily practice streaks as a first-class engagement primitive (Patrick §2.4; Bible §9.1, V1–V2; Glossary "Streak Tracking").

### 3.6 Repeatable drills as a design category
Patrick's framing (§2.1: "Unlike the Sight Reading Trainer, which generates never-repeating music, exercises are designed to be repeated") matches Decision #22's framing: replayability is a product concept, with constraint variation as the multiplier (Bible §6.3). Different vocabulary, same insight. **v0.2 strengthening:** Bible §6.3 now explicitly extends this principle across content modes (per Decision #43): the same replayability dynamic applies in sight reading and repertoire. Patrick's framing applied only to exercises; the canon now generalizes the insight.

### 3.7 Integration with the broader app
Patrick's §3.1 articulates that the Theory Library and Exercise Section are deeply integrated with the rest of MuseFlow (curriculum-driven unlocks, performance-based suggestions, data dashboard rollup). This matches our cross-section complexity language (Architecture Doc §9) and the Project Bible's positioning of Exercises and Repertoire as level-agnostic content modes that compose with paths.

### 3.8 The "Recommended for You" surface
Patrick's "Recommended for You" carousel (§2.3) on the Exercise Section landing page maps to our **Hook zone** in Screen A (UX Spec §3.1). The framing is identical at the surface level. **v0.2 strengthening (retained):** with Decision #47 elevating the user-modeling layer to a vision pillar, the Hook zone is now architecturally significant — it's the most user-visible affordance for the user-model's outputs. **v0.3 tone correction:** Patrick's specific carousel-card design is one possible UI direction for that surface among several, not an endorsed candidate. The architectural significance of the Hook zone stands; the visual treatment is undecided and Patrick's mock isn't load-bearing as a design endorsement.

### 3.9 Genre-as-product-axis intuition (new in v0.2)
Patrick's H category (Genre-Specific Exercises) is rejected as a *cluster* (§4.2 below), but his *intuition* that genre is a real organizing axis for user goals is validated by Doc 10 §5.4's 5 demo-relevant goal categories. Specifically:
- Patrick's H1 ("Classical Technique Drills, including Alberti bass patterns") directly corresponds to Doc 10 §5.4 goal category 3 ("I want to get better at this specific technique" — Alberti bass is the canonical example used).
- Patrick's H category as a whole corresponds to Doc 10 §5.4 goal categories 4 ("play like this specific musician/artist") and 5 ("interested in this specific genre").

This is non-trivial alignment: Patrick's catalog independently surfaced the same goal vocabulary the team converged on during the May 7 brainstorm. The recommendation in §9.4 (genre as filter, not cluster) is unchanged, but its strategic weight rises — genre tagging is now a load-bearing axis for Projects targeting goal categories 4 and 5.

---

## 4. Conflict Register

Items where Patrick and our canon genuinely disagree. Each item includes a recommended resolution.

### 4.1 The "Theory" naming collision *(Headline conflict — see §7 for full treatment)*

Briefly: Patrick uses "Theory" for a video surface; our Bible §2.1.1 uses "Theory" as a candidate content mode for theory-practice exercises. Resolution recommended in §7 below. **v0.2 update:** this conflict now sits inside Doc 09 §13.11's formal "Content Classes Beyond the Core Three" cluster, alongside Video Library placement (#53), Interactive Tutorial placement (#52), and Free Play original-sense status (#54). The proposed resolution (renumbered Decision #48) explicitly resolves the Theory portion of #13.11 #51; the Video Library portion (#53) gets a sub-recommendation; Interactive Tutorial remains in the cluster as a parallel question.

### 4.2 Patrick's Categories A–H vs. our Cluster framework

Patrick's eight categories are skill-domain categories (rhythm, ear training, technique, etc.). Our clusters are organized either by **substrate family** (Pitches, Intervals, Scales, Chords, Chord Progressions, Rhythms) or by **modality grouping** (Ear Training, Note Reading, Keyboard Skills, Music Theory, Sight-Playing, Transcription) — UX Spec §2.4, with both being traversal paths through the same atom graph.

Patrick's categories *partially* line up with our modality-grouped clusters: his "Ear Training Exercises" ≈ our "Ear Training" cluster; his "Music Theory Quizzes" ≈ our "Music Theory" cluster. But several of his categories cut across both groupings or invent dimensions our framework doesn't surface as primary:

- **A. Sheet Music-Based Technical Exercises** — A bundle of "anything that uses the Sight Reading Trainer UI." That's a *blueprint* in our framework, not a cluster. The contents (Scales, Arpeggios, Chord Progressions, Hanon, Interval Reading) span multiple substrate clusters in our model.
- **E. Technique and Coordination Drills** — A pedagogical-focus grouping (motor skill development) that is orthogonal to substrate and modality. Our framework doesn't surface this as primary either; in our model, these are atoms in various substrate clusters with the **Performance** training method and tightened constraints.
- **F. Creative and Improvisation** — Genuinely doesn't map cleanly. Our canon defers fingering and improvisation as exercise types (Decision #13). Patrick's F2 (Improvisation over Chord Progressions) is open-ended/no-passing-criteria territory; our framework currently has no clean atom slot for it.
- **G. Sight Reading Specializations** — Likely belongs with Sight Reading content mode (anticipated, Bible §2.1.1) rather than within Exercises. Multi-staff score reading (G3) is in particular a sight-reading concern, not an exercise drill.
- **H. Genre-Specific Exercises** — Genre is a *content scope* axis in our model, not a category. Pop/Rock patterns aren't a cluster — they're chord-progression atoms with chord-progression-content-scope constrained to common pop progressions, plus rhythm-pattern atoms with content-scope tags. Genre is metadata that can filter atoms across multiple clusters; it isn't a cluster of its own. **v0.2 nuance:** per §3.9, Patrick's intuition about genre as a real user-facing organizing axis is validated by Doc 10 §5.4. The conclusion (genre is tag, not cluster) is unchanged; its strategic importance rises.

**Recommendation:** Reject Categories A, E, G, H as cluster names. Keep Patrick's category groupings as **filter tags** or **secondary navigation views** layered on top of the substrate/modality cluster structure. Specifically:
- **Genre tags** can be a content-scope or metadata filter ("show me Jazz-flavored chord progression atoms"). Now load-bearing for goal-category 5 Projects (Doc 10 §5.4).
- **Pedagogical-focus tags** ("technique drilling," "improvisation," "creative") can similarly be a filter
- **Sight Reading Specializations** (G) should be flagged for the Sight Reading content mode design, not the Exercise content mode

§8 has the full mapping table.

### 4.3 Difficulty: flat B/I/A vs. our 3-axis model

Patrick uses **Beginner / Intermediate / Advanced** as a flat difficulty axis applied to most templates (e.g., his interval table, his chord table, his polyrhythm table). Our canon (Decision #7) treats difficulty as three orthogonal axes:

1. Substrate complexity (atomic → molecular → compound → cross-domain)
2. Training method scaffolding (VER → REC → SEL → ASM → ALT → RCL → PRF)
3. Performance constraint tightness (loose → tight)

Plus content scope ladders within strands (UX Spec §6.3).

**v0.2 strengthening.** Decision #43 (Performance Constraints Generalize Across Content Modes) makes constraint tightness a *cross-mode* primitive, not just an exercise-section-internal axis. A flat B/I/A label would now have to simultaneously summarize:
- Exercise-section substrate complexity + method + constraints,
- Sight-reading parameter difficulty + accuracy thresholds + time pressure,
- Repertoire success threshold + tempo target + hand-isolation settings.

These are not commensurable on a single B/I/A scale without losing what makes the scale useful for any one mode. Storing B/I/A as a schema field would compound this; deriving B/I/A at filter time, per mode, is the only coherent option if a summary label is wanted at all.

**Recommendation:** **Keep the 3-axis model as the engine. Defer the question of whether B/I/A appears as a user-facing summary label to UX exploration** (Open Question #5 in UX Spec §9 — "Named presets vs. individual sliders"). Don't add a B/I/A field to the atom schema; don't allow users to pick "Beginner" as a primary axis. If we later want a B/I/A summary label as a quick-filter convenience, derive it from the 3-axis state at filter time. Per-mode derivation rules are likely required.

`[Speculative]` Patrick's flat B/I/A may be artifact of the doc being written at a level where exposing the 3-axis model would have been too much detail. Once Patrick sees the 3-axis model and the cross-mode generalization (Decision #43), he may agree the underlying engine is more powerful — the question is just what we expose to users, and how that exposure varies per content mode.

### 4.4 "Master Roadmap" vs. Projects

Patrick's §3.2 (one paragraph) describes a **"Future Unified Roadmap" / "Master Roadmap"** — singular, comprehensive, integrating Sight Reading + Repertoire + Theory Library + Exercise Section into one cohesive learning journey.

Our canon has **Projects** (Doc 09; Decision #32; Bible §2.1.2) — plural, per-user, goal-bound, AI-generated, sitting alongside Curriculum and User Paths.

These are different shapes:
- Patrick's Master Roadmap is closer to a **single, expanded, cross-section Curriculum** — preset, multi-section, MuseFlow-authored, used by many.
- Our Projects are **per-user, AI-generated, goal-bound** — distinct per user.

**Recommendation:** Reject Patrick's Master Roadmap as a separate architectural concept. The functional intent (a unified cross-section progression) is already served, in our framework, by:
- **Curriculum expanded across sections** — when Curriculum stops being just-sight-reading and broadens into a multi-content-mode preset path (Bible §2.2 anticipates this evolution)
- **Projects** — when the user wants per-user goal-bound personalization

Patrick's "Master Roadmap" intent reveals **team appetite for cross-section preset paths** (i.e., the Curriculum-broadening evolution), which is worth tracking. It does not reveal a third path-mode primitive we're missing.

**v0.2 strengthening.** Decision #46 (per-mode agent control surfaces) makes Projects' supersession of Master Roadmap even more decisive. The agent's job in a Project is now defined as a *policy over enumerable per-mode control surfaces*, not a static authored sequence — which is a different shape from any preset Master Roadmap. Patrick's Master Roadmap is a content-mode-spanning *plan*; a Project's roadmap is a content-mode-spanning *plan plus live policy over the modes' control surfaces during execution*. The second is strictly more powerful.

`[Speculative]` Patrick's framing predates the May 5 Projects pivot and the May 7 control-surface enumeration. If asked today, Patrick likely sees Projects as the more powerful realization of his Master Roadmap intent. The May 7 brainstorm — where Patrick was an active participant in elaborating the Projects vision — supports this read.

### 4.5 The Exercise Section as "a separate top-level sidebar section" vs. the content/path mode architecture

Patrick frames the Exercise Section as one of several top-level surfaces (sidebar siblings: Sight Reading Trainer, Repertoire, Theory Library, Exercise Section). Our canon (Decision #41) frames everything as content modes (Exercises, Repertoire, anticipated Sight Reading) and path modes (Curriculum, User Paths, Projects), with a unified three-flow pattern (Browse / Generate / Project) within each content mode.

Patrick's framing isn't *wrong* — content modes will likely each have a top-level entry point. But his framing flattens the architecture (everything is a sibling tab) where ours layers it (content modes hold content; path modes traverse them; Projects is its own first-class entry point alongside the content-mode entries).

**Recommendation:** Our framing supersedes. The Exercise Section is a content mode entry point; Projects is a separate path-mode entry point; the Theory Library (if it ships) is *not* a content mode in our taxonomy and needs another home (see §7 and §13.11 #53 cluster).

### 4.6 The Theory Library video surface itself — top-level mode at V1?

Independent of the naming question (§4.1, §7), evaluating the Theory Library as a *concept*: Patrick proposes a separate top-level app surface for embedded YouTube/TikTok video content, with three sub-surfaces and curation logic.

The concept is well-developed and the YouTube-ToS argument for open access is real. But several factors weigh against shipping it as a top-level mode at V1:

- **It's not in our V1 scope.** Bible §9.1 lists V1 as: Exercise Section (filter/browse), Core Exercise Blueprints, Repertoire User Uploads. Adding a video-curation surface dramatically expands V1 build effort.
- **The curation logic depends on infrastructure we don't have at V1.** Patrick's Smart Feed prioritization requires backend pattern recognition on Sight Reading Trainer + Repertoire + Exercise data — what Decision #47 / Doc 09 §1.2 now names the **user-modeling layer**. That layer is recognized as a foundational architectural commitment, but team ownership is currently open (Doc 09 §13.7 #33). Building it for video curation alone is high-cost-low-value relative to building it once and pointing it at all content surfaces.
- **The proactive suggestion system is more usefully built once than twice.** Patrick's modal triggers are well-designed but they apply equally to *non-video* nudges (suggested exercises, suggested repertoire, prescribed practice tools via the agent control surfaces, Decision #46). Building the engagement layer once and pointing it at all content types is better than building a dedicated Theory Library suggestion system.
- **Video content as an in-Project resource is a more natural agentic-era home.** When Projects exist (Doc 09), the agent surfacing a relevant video as part of a Project node (Doc 09 §5.2 candidate node types) is a more powerful interaction than browsing a separate library. The Theory Library as a top-level browsable surface is a 2018-2022 era design pattern; video-as-agent-resource is the 2024+ pattern. This framing now formally tracks as Doc 09 §13.11 #53 (Video Library architectural placement), with Staley framing it as "node-as-tutorial" and Patrick framing it as content-mode-like.

**Recommendation:** **Defer the Theory Library video surface beyond V1**, and lean toward the Staley framing (node-as-tutorial / roadmap-node primitive) as the resolution direction for §13.11 #53. Keep Patrick's design (Smart Feed / Quick Theory / Deep Dives architecture) as input for the deferred feature; the engineering and curation work it describes is largely preserved as roadmap-node behavior under Projects. **Absorb the proactive suggestion system as candidate engagement-layer behavior** (see §5.2). Don't add "Theory Library" as a top-level navigation tab in V1.

### 4.7 Gamification: named achievements, Practice Points, leaderboards

Patrick proposes specific named achievements ("Scale Master," "Rhythm Guru," "Perfect Pitch," "Theory Wizard"), Practice Points as accumulating currency, and "future leaderboards or rewards" (§2.4). Our canon has streak tracking but no designed achievement system.

This is below the level the macro PRD should commit to. **Recommendation:** Stay framework-only at the PRD level. The schema (per-atom completion, Exercise Result, mastery thresholds) supports any achievement system that gets layered on top. Patrick himself is the natural owner of the gamification design — it's exactly the kind of MVP-decomposition work Patrick volunteered for (Standup Synthesis §2). Don't bake Patrick's specific achievement names into the canon.

### 4.8 Premium tier specifics

Patrick's §3.3 specifies tiers in detail:
- **Free**: Unlimited Sight Reading + Curriculum, unlimited community theory videos, ~50% of exercises
- **Premium**: All exercises + exclusive artist content + advanced analytics + priority access

Our canon (Decision #37) explicitly defers `tier_gating` from the schema until pricing is designed. Doc 09 §16 (new in v0.2 canon) establishes the team's working framework for cost considerations — six principles including "MAGE is a cost reducer relative to LLM-only architectures," "heavy generation periods amortize over engagement," and "per-month curriculum-generation limits with token-purchase upsell."

**v0.2 tension surfaced.** Patrick's "free tier gets ~50% of exercises" treats atoms as scarce/curated content gated by tier. The §16 framework treats *generation cost* (LLM tokens for custom content, custom roadmaps, AI-extracted summaries) as the variable expense to gate against. In our model — where exercises are framework-generated and the marginal cost of "another atom" is near zero once authored — atom-by-atom gating is a strange place to put a paywall. The natural gating points under §16 are:
- Heavy generation (custom AI-generated exercises beyond a monthly budget)
- Custom Projects (per-Project compute amortization)
- Premium artist/instructor content (which is genuinely scarce — recording/licensing costs)

Patrick's "exclusive artist content in the Theory Library" matches the §16 framework. Patrick's "50% of atoms" doesn't.

**Recommendation:** Patrick's proposal is **input to a future pricing-design conversation**. Decision #37 stands. The §16-vs-Patrick tension should be surfaced explicitly when the pricing conversation begins — the pricing model that aligns with our cost framework is materially different from Patrick's framing, and the team should converge on which framing wins before pitch deck commitments are made. UX Spec §9 Open Questions 21–23 already track this; v0.2 strengthens the framing.

`[Speculative]` Patrick's "50% atom gating" may be an artifact of treating exercises as scarce/curated rather than combinatorially generated. Once the combinatorial framework is shared with him, the §16 framework's natural gating points should land more naturally. This is partly a team-alignment question, not just a pricing one.

---

## 5. Additive Register

Items in Patrick's doc that our canon doesn't have, where absorbing them would strengthen the design.

### 5.1 Free Play within exercises — absorbing the established SRT pattern *(substantially revised in v0.3)*

**Provenance correction.** v0.2 framed Patrick's "Game Mode vs. Free Play" as Patrick's contribution. v0.3 corrects: the Game / Free Play toggle is an **established MuseFlow Sight Reading pattern**, visible in production today as a top-of-screen tab in the SRT (Game | Free Play). Patrick is echoing this existing pattern into the exercise context, not inventing it. The absorption is still valuable; the framing is "extend an established pattern across content modes," not "introduce a new distinction."

**What Free Play means in the existing pattern.** Per the production SRT: practice the same content indefinitely with real-time feedback on accuracy/tempo, but without the chevron clearance gate or completion-policy that drives mastery progression. Useful for warm-up, experimentation, or extended practice without pass/fail pressure. The toggle is **live-switchable during a session** — the user can flip between Game and Free Play mid-exercise without backing out and reconfiguring.

**Architectural home (carryover from v0.2 with v0.3 refinement).** Per v0.2: a more economical placement than a `session_mode` schema enum is the **exercise control surface** (Doc 09 §6A.2), explicitly listing "performance constraints" and "configurable assistance" as enumerable surface elements. Adding a **completion-policy** element to that surface — with values `practice` (default; session contributes to mastery) and `free_play` (non-assessable; no mastery contribution; stats still tracked) — handles the pattern without introducing a parallel schema axis. **v0.3 addition:** the completion-policy element must be **live-toggleable during a session**, matching the existing SRT affordance. Pre-session configuration alone is not sufficient; live toggle is a design requirement carried over from the existing pattern. Whether the agent can also flip the toggle mid-session is a separate question (per Decision #46, the agent's policy operates over the surface elements; live-toggle by user and by agent are not mutually exclusive).

**The naming collision (new in v0.3).** "Free Play" carries two different meanings in our current canon and team vocabulary, and the collision is a real problem:

- **Free Play (completion-policy)** — the established SRT meaning, now proposed for the exercise control surface: practice without pass/fail, no mastery contribution, stats still tracked. Production-current. This is what Patrick is echoing.
- **Free Play (original sense)** — the deferred candidate content mode per Bible §2.1.1 and Decision #45's clarification: open-ended musical improvisation without notation guidance. Deferred indefinitely.

Sharing the name is unworkable. Two options for resolution:
- *(a) Rename the completion-policy element* — but this fights the established SRT terminology, which is bad. Users see "Free Play" in production today.
- *(b) Rename the deferred candidate content mode* — the candidate is uncommitted and not yet user-visible, so renaming it costs nothing in production-vocabulary terms.

**Recommended resolution (bundled into Decision #49):** rename the deferred candidate content mode currently called "Free Play (original sense)" to **"Improvisation"**, freeing "Free Play" for the established SRT/exercise completion-policy meaning. Alternates worth considering: "Open Play," "Jam." "Improvisation" reads as the most accurate to the original-sense intent. Bible §2.1.1's candidate-content-mode list, Decision #45's scope clarification, and Doc 09 §13.11 #54 would update accordingly.

**Cross-references and connections.**
- **Established SRT precedent** — production today, screenshots-of-record.
- **Staley's "free-play interlude as part of the path"** comment (Standup Synthesis §1) — likely refers to the completion-policy meaning, invocable as part of a Project's roadmap.
- **Decision #45** — the user-generated-sight-reading resolution already established the analogous capability ("no completion criteria, just play endlessly") within that content mode. Decision #49 is the exercise-side parallel.
- The repertoire-side parallel (playing a piece endlessly without it logging as practice or completion) is its own thing, separate from Andrew's repertoire editor (which is an authoring/audition tool, not a Free Play mode). The repertoire parallel falls under the repertoire control surface (Doc 09 §6A.1) and likely already exists in some form; not a target of this memo.

**Recommendation:** Absorb the established Game / Free Play pattern into the Exercise content mode as a **completion-policy element of the exercise control surface (Doc 09 §6A.2), live-toggleable during a session**. Bundle the naming-collision resolution (rename the deferred candidate to "Improvisation" or similar) into the same Decision (#49). See §10.

### 5.2 The Proactive Suggestion System as concrete engagement-layer specification *(strengthened in v0.2)*

Patrick's §1.5 (Proactive Suggestion System) is the most concrete engagement-layer proposal anyone on the team has produced. Specific trigger conditions:
- Accuracy drops below 75% for four consecutive phrases, errors cluster around a specific concept → modal at session end suggesting relevant content
- Four consecutive failed tier attempts → modal suggesting tier-concept content
- Repeated repertoire struggles → modal on back-out with applicable help

Specific modal design:
- "Based on your patterns…" headline
- Concept-named explanation
- Three-button choice: [Watch Now] [Maybe Later] [Don't Show Again for This Topic]
- Suggested content also lands in user's feed under "Recommended for You"

This is well-considered and applies generically — not just to videos. The same modal can suggest exercises, repertoire, or curriculum review when those are the more useful interventions.

**v0.2 architectural mapping.** Patrick's system now grounds against three layers:
1. **User-modeling layer (Decision #47, Doc 09 §1.2)** — the substrate. Patrick's trigger conditions ("accuracy drops below threshold," "errors cluster around a specific concept," "repeated repertoire struggles") presuppose a per-user accumulating model that can detect these patterns. That model is the user-modeling layer.
2. **Per-mode agent control surfaces (Decision #46, Doc 09 §6A)** — the action vocabulary. Patrick's "Watch Now" is one possible action; the surface enumeration adds others: "prescribe an exercise atom at specific parameters," "start a repertoire session with auto-looping engaged," "open the Sight Reading Generate flow with parameters pre-filled." Once enumerated, the engagement layer's modal can offer the right surface action per trigger, not just video content.
3. **Engagement layer (Decision #19 amendment, Glossary "Engagement Layer")** — the interaction surface. Patrick's modal pattern, button choices, and "Don't Show Again" affordance live here.

This layered grounding strengthens the absorption. v0.1 absorbed Patrick's system as candidate engagement-layer behavior; v0.2 specifies that the absorption is into three layers, with the trigger logic in the user-modeling layer, the action vocabulary in the control surfaces, and the modal pattern in the engagement layer.

**Recommendation:** Absorb as **candidate engagement-layer behavior with explicit dependencies on the user-modeling layer (Decision #47) and the per-mode control surfaces (Decision #46 / Doc 09 §6A)**. The trigger conditions and modal pattern survive as-is; the *content surfaced by the modal* generalizes from "video" to "any helpful intervention available on the relevant control surface." Tag this in UX Spec §9 open-questions as input to the engagement layer's design, with cross-references to Decisions #46 and #47.

### 5.3 Adaptive note-by-note expansion (Patrick's "Suggested Flow Gameplay Option") *(reframed in v0.2)*

In A1 (Scales) and A2 (Arpeggios), Patrick describes a specific adaptive mechanic:
> "Start with two notes moving up and down. Add one note at a time, expanding upward and downward, until two full octaves are complete. Progress adapts to performance: if the player achieves 95% accuracy or higher, a new note is added… If the player stays on the same number of notes for too long, the tempo decreases. As performance improves, the tempo increases back to the goal tempo."

This is a concrete instantiation of Optimal Grip™ (V2; Bible §9.1; Architecture Doc §5.4). Patrick names a specific algorithm: **expand sequence length when accuracy is high; reduce tempo when stuck; expand tempo back to goal when improving; gate on 95% at goal tempo before expanding length.**

**v0.2 framing.** Patrick's scale-expansion algorithm is now best understood as a **meta-policy over the exercise control surface (Doc 09 §6A.2)**, parallel in shape to the auto-looping algorithm (Decision #42) as a meta-policy over the repertoire control surface (Doc 09 §6A.1). Both bundle several surface elements (tempo, accuracy threshold, content-scope progression) into a coherent practice mode. Recognizing this parallel is useful for V2 design: the same architectural pattern (meta-policy over enumerated control surface) yields specific algorithms per content mode.

**Recommendation:** Don't absorb at the V1 PRD level (it's V2 territory). But **flag this as a candidate Optimal Grip™ algorithm and the exercise-side parallel of auto-looping** in V2 design conversations. It's the most concrete spec we have for adaptive difficulty on the exercise side. Worth surfacing alongside Decision #42 when V2 design begins.

### 5.4 Concrete mastery thresholds *(framing loosened in v0.3)*

Patrick's templates uniformly include passing criteria — and they're consistent enough to extract a recurring pattern:
- Most performance/sight-reading exercises: **"Four consecutive phrases at 95% accuracy and goal tempo"**
- Most ear-training quizzes: **"Four consecutive correct identifications"**
- Most theory quizzes: **"Four consecutive correct identifications"**
- D1 Note Naming (flashcard): **"Name 20 notes correctly with average response time under 3 seconds"**
- Score Reading (G3, harder content): **"Four consecutive at 90% accuracy"** (relaxed for difficulty)

These are useful inputs to the `mastery_thresholds` field (Decision #40), but the framing matters.

**v0.2 framing (kept).** Per Decision #43 (cross-mode performance constraints), these patterns are best understood as the **exercise-section formulations of cross-mode performance-constraints primitives**. The same shape (N consecutive at X% accuracy, with optional tempo or time targets) is the canonical form across exercises, sight reading (per Decision #45's "completion criteria"), and repertoire (per Doc 09 §6A.1's "takes-required" and "success threshold"). The exercise-section instantiation Patrick's templates give us is the most developed; the sight-reading and repertoire instantiations will follow.

**v0.3 loosening.** Patrick's specific numbers are **one possible configuration** in the n-dimensional matrix of performance-constraint settings the framework supports. They are not "the right defaults" — they are *a* defensible starting point that a Track D author could begin from, then override per atom as pedagogical reasoning dictates. Per-atom values can be set by:
- **Catalog author** (during Track D) — typically using Patrick's patterns as a starting baseline, overriding where the substrate or method warrants different thresholds
- **AI generation** (per Decision #33, Decision #44 — generation on demand) — the agent may compute thresholds per atom based on user state, goal, or pedagogical inference, not just look up a default
- **Preset** — specific atoms may carry hand-tuned thresholds reflecting expert judgment that diverges from the pattern
- **User input** — users can adjust performance-constraint settings during session configuration (the exercise control surface, Doc 09 §6A.2)

Patrick's contribution is the pattern shape, not the specific numbers. Decision #50 (renumbered) reflects this: it commits the *methodology* of having defaults at all, and treats Patrick's patterns as candidate starting baselines that Track D ratifies or revises.

**Recommendation:** Treat Patrick's patterns as **candidate starting baselines for V1 catalog authoring**, easily overridable per atom. Decision #50 (renumbered) is reframed accordingly — see §10. Specific numbers held loosely.

### 5.5 Specific UI elements for Screen A

Patrick's §2.3 (Exercise Section UI and Navigation) gives concrete UI elements for the equivalent of our Screen A. Several are useful inputs to UX exploration:
- "Recommended for You" carousel at the top → maps to Hook zone (now load-bearing for the user-modeling layer's outputs, per §3.8)
- Collapsible category sections → one possible answer to Open Question #2 (Zoom vs. flat) and #3 (toggle UI)
- Filter icon (top-right) for difficulty / category / sort by recommended/recent/A-Z
- Search bar at top
- Exercise card design (name, category icon, difficulty level, completion status, best score)

None of these is binding, but they're candidate UI elements for the Screen A design exploration.

### 5.6 Tagging vocabulary *(strengthened in v0.2)*

Patrick's §1.3 (Quick Theory tagging) defines tags for video content:
- **Concept Tags**: circle of fifths, major scales, minor scales, chord inversions, syncopation, pedaling, dynamics, articulation
- **Skill Level Tags**: beginner, intermediate, advanced
- **Instrument Focus Tags**: right hand, left hand, both hands, pedal technique
- **Genre Tags**: classical, jazz, pop, blues, ragtime

The vocabulary is reasonable. "Skill Level Tags" conflict with our 3-axis difficulty (§4.3 — now sharpened by Decision #43); the **Concept**, **Instrument Focus**, and **Genre** tag categories are useful as candidate atom-metadata extensions or as engagement-layer filter axes. **v0.2 strengthening:** Genre tags are now strategically more important per Doc 10 §5.4 (goal categories 4 and 5 are genre/artist-defined). Concept tags are candidate metadata for cross-content-mode linkage — when a Project's roadmap surfaces a video (per §13.11 #53) and an exercise atom that share the concept tag "circle of fifths," that's the linkage.

**Recommendation:** Don't add to the atom schema at V1, but **flag as a candidate metadata-extension conversation** for catalog authoring. Genre tags warrant priority given the Doc 10 §5.4 alignment. Open question for §11.

### 5.7 Patrick's H category as a "genre-tagged content scope" framing *(strengthened in v0.2)*

Patrick's H (Genre-Specific Exercises) — Classical, Jazz, Blues, Pop/Rock, Latin — is rejected as a cluster (§4.2) but its *content* points to a real gap, now strategically important: how does a user filter for "exercises that prepare me for jazz"? Or "exercises in the style of classical period pieces"? Our canon doesn't surface this as a primary axis. **v0.2 weight:** Doc 10 §5.4 goal categories 4 ("play like this specific musician/artist") and 5 ("interested in this specific genre") *depend* on this filtering capability working well. A Project targeting "I want to play like Bill Evans" needs to assemble atoms across multiple substrate clusters tagged with jazz-relevant content scope. Without genre/style tagging, the agent has no way to do this.

**Recommendation:** Add **genre-tag (and stylistic-content-scope-tag more broadly) as a high-priority candidate atom-metadata extension** for catalog authoring. Don't surface as a primary nav axis; surface as a filter ("show me chord-progression atoms tagged Jazz") and as agent-queryable metadata. Doesn't need a schema change at the atom level if implemented as a tag set, but the tag set is now load-bearing for goal-category-4/5 Projects.

---

## 6. "Ours Does Better" Register

Items where our canon has more rigor or better framing, where Patrick's content should NOT be adopted. Recorded so the team knows the choice was deliberate.

### 6.1 First-principles framework vs. enumerated catalog

The single most important "ours does better" point. Patrick's doc enumerates ~50 templates with no underlying generative principle. Our canon (Bible §3, §6; Architecture Doc §1, §7) generates exercises from substrate × modality × training method × constraint composition. The 50 templates are emergent from a much smaller set of primitives, and the framework can produce thousands of atoms our 50-template enumeration would miss. **v0.2 strengthening:** Decision #33 (Exercise Generation on Demand) plus Decision #44 (MAGE augmentation framing) plus Doc 09 §6A.2 (exercise control surface with generation_mode as a queryable field) now make on-demand atom generation a first-class capability. Patrick's "catalog" is, in our framework, one origin (`authoring_origin = preset`) feeding what is actually a generative system.

Patrick's catalog is useful as a sanity check — does our framework produce all his templates? (Answer: yes, plus many more.) But the framework itself should not be replaced or supplemented with hand-curated lists at the architecture level.

### 6.2 Atom identity model vs. flat exercise list

Patrick's templates flatten dimensions that our canon explicitly separates. For example, his "C1. Interval Recognition (Melodic)" bundles together:
- Substrate (melodic interval recognition)
- Input modality (Aural)
- Output modality (Semantic)
- Target variables ([interval size + quality])
- Pitch reference mode (Relative)
- Content scope (varying by interval type table)
- Training method (multiple-choice = Recognition)

— into a single named template. Our atom model (Decision #25) treats those as orthogonal dimensions, which means the *real* count of distinct interval-recognition atoms is much higher than Patrick's "C1." His framing collapses meaningfully different exercises (e.g., harmonic vs. melodic; relative vs. absolute) into surface variants of "the same exercise."

### 6.3 Training method spectrum

Patrick's framework only really uses two methods: multiple-choice (Recognition) and direct-play (Performance). His templates occasionally hint at others (rhythm dictation as Assembly; chord spelling as Recall) but don't formalize the spectrum. Our 7-level training method spectrum (Verification → Recognition → Selection → Assembly → Alteration → Recall → Performance, Decision #2) provides a richer space. Patrick's missing methods are real exercise types — our canon enables them; his doesn't.

### 6.4 Performance constraints as replayability multipliers *(strengthened in v0.2)*

Bible §6.3 frames performance constraints as replayability multipliers (Decision #22). Patrick's framework treats difficulty as a static property of the exercise (B/I/A) rather than a configurable space the user navigates. Our framing produces dramatically more practice mileage from the same atom catalog. **v0.2 strengthening:** Bible §6.3 now explicitly extends the replayability principle across content modes per Decision #43, with worked examples for sight reading and repertoire. Patrick's framing applied only to exercises and treated constraints as static; our framing applies constraints across modes as a configurable space. The advantage compounds.

### 6.5 Cross-Section Complexity Language and GMTF integration

Architecture Doc §9 articulates the cross-section problem and connects it to MuseFlow's existing GMTF system (Decision #23). Patrick's doc has no equivalent — his cross-section integration (§3.1) is described qualitatively, not architecturally. Our framing supports the systems-level coherence Patrick gestures at but doesn't operationalize. **v0.2 strengthening:** Decision #47 (user-modeling layer) is now the canonical home for per-user cross-section signals to consolidate. Cross-section complexity is the *content-level* language; the user-modeling layer is the *user-level* aggregation. Patrick's doc has neither.

### 6.6 Mode architecture (Decision #41)

Patrick's "everything is a top-level sidebar tab" framing is flatter and more brittle than our content-modes / path-modes architecture. Our model handles AI-averse users explicitly (Bible §2.1.2), explains where custom-authored content lives (Decision #34, Decision #41), and provides a single architectural primitive that absorbs Projects, custom authoring, sight-reading evolution, and atom `authoring_origin` into one pattern. Patrick's framing has none of this leverage.

### 6.7 Agentic Projects vs. Master Roadmap *(strengthened in v0.2)*

See §4.4. Our Projects framing is more flexible, more personalized, more demoable, and more aligned with the team's commercial pitch. Patrick's Master Roadmap (one paragraph) is a sketch; our Doc 09 is ~1000 lines including the user-modeling-layer vision pillar (§1.2), the per-mode control surfaces (§6A), and the cost framework (§16). The architectural depth on our side is several orders of magnitude greater.

### 6.8 Theory practice as substrate, not dedicated mode

Our framework recognizes that "music theory" isn't a coherent skill domain — it's a collection of substrates (chord quality, interval recognition, key signature recognition, etc.) that already live within Frequency-Domain and Time-Domain substrates. Patrick's "Music Theory Quizzes" (Category D) is correctly treated, in our framework, as Semantic-output exercises across multiple existing substrate clusters. We don't need a separate "theory" mode.

### 6.9 Configuration model *(strengthened in v0.2)*

Our distinction between **atom identity** (chosen by navigation, fixed) and **practice mode configuration** (training method, constraints, session shape — chosen on Screen B; UX Spec §4.1) is structurally cleaner than Patrick's "every template has variations" framing. Our model supports user customization while keeping the catalog enumerable; Patrick's model multiplies the catalog by every variation, making it harder to reason about. **v0.2 strengthening:** Doc 09 §6A.2 (exercise control surface) now provides an architectural home for the configuration layer Patrick gestures at. Patrick's "variations tables" map cleanly onto the exercise control surface's enumeration — they're not catalog multipliers, they're configurations the agent or user makes over a fixed atom identity.

### 6.10 The user-modeling layer as a positional commitment *(new in v0.2)*

Decision #47 / Doc 09 §1.2 frames the per-user accumulating user-model as a foundational architectural commitment that distinguishes MuseFlow structurally from competitors. Patrick's "performance-based recommendations" implies the existence of this layer but doesn't articulate it as a load-bearing architectural commitment. Our framing makes the layer explicit, named, and elevated to vision-pillar status — which is investor-defensible in a way Patrick's framing is not. This is a clear "ours does better" point that didn't exist in v0.1's canon state.

---

## 7. The Theory Naming Question

This is the headline structural conflict. It deserves its own section.

### 7.1 The collision

- **Patrick's "Theory Library"** = a separate top-level surface for embedded YouTube/TikTok video content, with three sub-surfaces (Smart Feed, Quick Theory, Deep Dives). Theory exercises in Patrick's framing live in the Exercise Section as Category D ("Music Theory Quizzes").
- **Our Bible §2.1.1 "Theory" candidate content mode** = a possible future content mode for theory-practice exercises. Status TBD pending exactly this doc review.

These are two different things using the same word.

### 7.2 The three resolution paths (from the handoff brief)

**(a) Adopt Patrick's framing.** Theory = video-content surface; theory exercises stay in Exercise Section as a substrate family. Bible §2.1.1 Theory candidate-content-mode entry gets removed; a new "Knowledge Library" or similar gets added.

**(b) Reject Patrick's framing.** Theory remains as our candidate content mode for theory practice; Patrick's video-library concept becomes a separately-named thing.

**(c) Both, renamed.** Neither uses "Theory" alone. Patrick's video surface gets a name like "Learn" or "Concepts" or "Knowledge Library"; theory practice exercises live within the Exercise content mode (so the Theory candidate-content-mode entry resolves to "no, theory is just a substrate family within Exercises").

### 7.3 Recommendation: Path (c)

Path (c) is correct because:

1. **Patrick's "Theory Library" is misnamed in his own doc.** His Smart Feed and Deep Dives explicitly include videos about technique (pedaling, finger placement), genre (jazz history, ragtime), performance psychology (anxiety, flow state), sight-reading tips, ear-training tips, and song-specific repertoire context (Debussy biography for Clair de Lune). Most of that content isn't theory in the music-theory sense — it's *anything an instructional video might cover.* Calling the surface "Theory Library" was already a mismatch with its own scope. The right name for what Patrick is describing is closer to "Learn," "Knowledge Library," "Concepts," or "Lessons."

2. **Theory practice exercises don't warrant a dedicated content mode.** Our framework already handles them as Semantic-output exercises across multiple existing substrate clusters (chord quality recognition, interval-on-staff identification, key signature recognition, etc.). Adding a "Theory" content mode would either duplicate atoms (also-present-in-Exercises) or fragment the cluster (some chord exercises in Theory, some in Exercises). Both options are worse than just keeping these atoms in the Exercises content mode.

3. **The "Theory" content mode candidate (Bible §2.1.1) was always conditional on this doc review.** That's exactly the resolution this memo is supposed to produce. Resolving to "no, theory is just a substrate family within Exercises" is the right call.

4. **(New in v0.2) The cluster framing makes Path (c) more coherent.** Doc 09 §13.11 now formally clusters the Theory mode-status question with Video Library placement (#53), Interactive Tutorial placement (#52), and Free Play original-sense status (#54). Resolving Theory specifically is one piece of resolving the cluster; resolving it in the Path (c) direction (Theory dissolves; the video surface gets renamed and its architectural placement becomes the §13.11 #53 sub-question) leaves the cluster's other questions cleanly addressable.

### 7.4 Specific changes recommended

1. **Bible §2.1.1**: Remove "Theory" from the Candidate future content modes list. Add a footnote or §2.4 entry explaining that theory practice was evaluated as a candidate content mode and rejected — theory practice exercises live within the Exercises content mode as Semantic-output atoms across existing substrate clusters.

2. **Glossary "Content Mode"**: Update to remove Theory from the candidate list (currently reads "Theory and Free Play are candidate future content modes (status TBD)"). Theory resolves. The "Free Play" candidate is renamed to "Improvisation" per Decision #49 Part 2 (the naming-collision resolution), so the updated entry reads "Improvisation is a candidate future content mode (status TBD, deferred indefinitely per Decision #45's clarification)."

3. **Patrick's video-library concept** gets a new name. Eight candidates worth Steven's selection, with tradeoffs (expanded in v0.3):
    - **"Knowledge Library"** — generic, accurate to the actual scope. Safe. Slightly clinical.
    - **"Learn"** — short, brand-y. Possibly confusable with Curriculum.
    - **"Concepts"** — accurate but cold.
    - **"Insights"** — modern, no collision, slight business-app risk. `[Speculative]` Could land either premium or buzzword-y depending on visual treatment.
    - **"Discover"** — verb-as-noun, emphasizes the Smart Feed feed-nature. Reads product-y / Spotify-y. Fits if the Smart Feed sub-surface dominates; weaker if Deep Dives (library/archive) is primary.
    - **"Reference"** — accurate, no collision. Cold; textbook-y; probably wrong for a video-feed surface.
    - **"Study"** — accurate to purpose, academic. Could land well for adult learners; might feel like homework for casual users.
    - **"Topics"** — descriptive, flat. Probably too neutral to carry brand.

   `[Speculative]` Of the eight, **Knowledge Library** and **Insights** are the two most defensible. Knowledge Library is safest; Insights has more brand life but slightly less precision. Discover is third-place — strong if the Smart Feed dominates, weaker otherwise.

   **v0.3 recommendation: defer the final naming call to when the feature actually enters scope.** Since this names a deferred-beyond-V1 feature (proposed Decision #51), the working name is a reservation, not a commitment. Keep "Knowledge Library" as the working name in canon. Revisit when the feature enters scope, at which point user testing or brand work can inform the decision with less speculation.

4. **The video-library feature itself** is deferred beyond V1 (see §4.6) — but with its new name reserved, so it's clear what space it would occupy when it's revisited. Doc 09 §13.11 #53 (Video Library architectural placement) is the formal cluster home for the deferred-resolution; recommended lean is toward Staley's framing (roadmap-node primitive) over Patrick's (content-mode-like).

5. **Doc 09 §13.11**: Update #51 (Content Classes Inventory) to mark Theory as resolved (per Decision #48 below). #52 (Interactive Tutorial) and #53 (Video Library) remain open within the cluster. #54 (Free Play original-sense) remains deferred indefinitely per Decision #45.

### 7.5 Resolution proposed as Decision #48 (renumbered from v0.1's #42)

See §10 below for the candidate Decision Log entry.

---

## 8. Specific Exercise Template Absorption

**Scope clarification (v0.3).** When this memo refers to "the V1 atom catalog," it means the **preset inventory** that ships with MuseFlow at V1 with `authoring_origin = preset` (per Decision #41's four authorship origins). This is distinct from the full combinatorial matrix of atoms our framework supports — that universe also includes user-generated atoms (Decision #34, Decision #41), AI-generated atoms (Decision #33, Decision #44), and (future) community-generated atoms. Patrick's ~50 templates evaluate as candidates for the **preset inventory specifically**, not for the universe of what's possible. An atom marked "Defer-V2" in this table means "not in the V1 preset inventory" — it does not mean "the framework cannot produce this atom," and it does not preclude AI-generated or user-generated atoms of the same shape in V1.

Patrick has ~50 named exercise templates with passing criteria. This section evaluates each for absorption into the V1 preset inventory. The recommendation per template is one of:

- **Adopt** — Strong V1 candidate. Add to atom catalog as concrete instantiation.
- **Adopt-modified** — V1 candidate but reshape to fit our atom-identity model.
- **Defer-V2** — Pedagogically valid but better suited to V2 or later.
- **Defer-Sight-Reading** — Belongs in the Sight Reading content mode, not Exercises.
- **Pedagogically-restate** — Patrick's template aggregates across multiple atoms in our framework; pick one or more to surface as featured atoms; the others fall out from the framework.
- **Reject** — Not a strong V1 fit; framework supports it but not worth featuring.

### 8.1 Mapping table

| Patrick's ID | Title | Primary Substrate (ours) | Our Cluster | Recommendation | Notes |
|---|---|---|---|---|---|
| **A1** | Scales | F-C2 (Scale construction) | Scales | **Adopt** | Multiple atoms: by hand × by scale type × by content scope. Tempos and 95% threshold feed `mastery_thresholds`. Patrick's adaptive scale-expansion mechanic (§5.3) is V2 Optimal Grip material — meta-policy over exercise control surface. |
| **A2** | Arpeggios | F-C6 (Chord construction)  | Chords  (or new Arpeggios cluster) | **Adopt** | Arpeggios are chord constructions; could be a sub-strand within Chords or its own cluster. Open Q (§11.2). |
| **A3** | Chord Progressions | F-C12 (Progression recognition) + F-C8 (Voicing) | Chord Progressions | **Adopt** | Multiple atoms by progression × key × rhythm. Patrick's progression list is good V1 content scope. |
| **A4** | Hanon-Style Finger Exercises | X-4 (Fingering) + technique | (Cross-domain) | **Defer-conditional on §11.4** | Pedagogically valid; user-value clear (foundational technique drilling). Currently defers because our framework lacks a clean home for "motor pattern" as a substrate or "technique drilling" as a category. If §11.4 resolves toward accommodating these (e.g., adding a motor-pattern substrate to Architecture Doc §3.1, or treating these as Performance-method atoms with content-scope specifying the technique pattern), A4 becomes a V1 preset candidate. If §11.4 resolves the other way (technique drilling as a V2+ feature or distinct content mode), A4 stays deferred. Currently the defer reflects framework-fit ambiguity, not a user-value assessment. Decision #13 also flags fingering as needing dedicated design. |
| **A5** | Interval Reading Drills | F-M3 (Interval construction) | Intervals | **Adopt** | Visual-input + Performance-output; concrete instantiation of an existing strand. |
| **A6** | Sight Reading Challenges | X-2 (Sight reading) | (Cross-domain / Sight Reading) | **Defer-Sight-Reading** | Belongs in Sight Reading content mode, not Exercises. Decision #45 confirms Sight Reading's content-mode trajectory. |
| **A7** | Articulation and Dynamics Drills | A-A2, A-M2 (Amplitude) | (Amplitude — deferred) | **Defer-V2** | Decision #3 defers amplitude exercises beyond V1. |
| **A8** | Pedaling Exercises | (Pedal substrate not in catalog) | — | **Defer-V2** | Pedal handling is its own substrate not yet in our catalog. Defer with a note (§11.3). |
| **B1** | Rhythm Tapping (Single Line) | T-C2 (Rhythm sequence recognition) | Rhythms | **Adopt** | Strong V1 candidate. BP-06 (Listen → Rhythm Tap) is the blueprint. |
| **B2** | Polyrhythm Trainer (Two Lines) | T-C3 (Polyrhythm recognition) | Rhythms | **Adopt** | Same blueprint, different content. |
| **B3** | Rhythm Dictation | T-A2 (Rhythm value notation) + T-C2 | Rhythms | **Adopt** | Visual output (Assembly method); BP-07 candidate. |
| **B4** | Rhythm Sight Reading | T-C2 + sight-reading constraints | Rhythms (or Sight Reading) | **Adopt** | Could be in Exercises *or* Sight Reading content mode. Likely both — same atoms, different framing surfaces. |
| **C1** | Interval Recognition (Melodic) | F-M1 (Melodic interval recognition) | Intervals | **Adopt** | Aural→Semantic, REC method. Direct atom. |
| **C2** | Interval Recognition (Harmonic) | F-M2 (Harmonic interval recognition) | Intervals | **Adopt** | Sister atom to C1, different substrate. |
| **C3** | Chord Quality Identification | F-C5 (Chord quality recognition) | Chords | **Adopt** | Aural→Semantic. Multiple atoms across content scope (triads only → all qualities → 7ths → extended). |
| **C4** | Melodic Dictation | F-A4 + T-A3 (notation/playback) | (Cross-domain) | **Adopt-modified** | Aural→Kinesthetic (play back) is a clear atom; Aural→Visual (notate) is a different atom. Patrick's template collapses both. |
| **C5** | Harmonic Progression Identification | F-C12 (Chord progression recognition) | Chord Progressions | **Adopt** | Direct atom. |
| **C6** | Bass Line Dictation | F-A4 + T-A3 (specialized to bass) | (Cross-domain) | **Adopt-modified** | Same as C4 but content-scoped to bass-line material. |
| **C7** | Rhythm Dictation (Ear Training) | T-A3 → T-A2 | Rhythms | **Adopt** | Sister to B3 but Aural input. |
| **C8** | Scale Degree Identification | F-C3 (Scale degree mapping) | Scales (or Pitches in scale context) | **Adopt** | Aural→Semantic with key reference. |
| **D1** | Note Naming (Flash Cards) | F-A1 + F-A2 (Pitch-name + notation) | Pitches | **Adopt** | Visual→Semantic, REC. Patrick's specific threshold (20 in a row, <3s avg) is a useful default for flashcard-style atoms. |
| **D2** | Key Signature Identification | F-C4 (Key signature recognition) | (Music Theory cluster) | **Adopt** | Visual→Semantic, REC. |
| **D3** | Chord Spelling | F-C6 (Chord construction) | Chords | **Adopt** | Semantic→Kinesthetic, PRF or REC. |
| **D4** | Interval Identification on Staff | F-M1/M2 + F-A2 | Intervals | **Adopt** | Visual→Semantic, REC. |
| **D5** | Time Signature Identification | T-C1 (Meter recognition) | Rhythms | **Adopt** | Visual→Semantic, REC. |
| **D6** | Circle of Fifths Quiz | (Multi-substrate: F-C4 + F-A5 + relations) | Music Theory | **Adopt-modified** | Patrick's framing is multi-question Q&A. Our framework handles each question type as a distinct atom. |
| **D7** | Enharmonic Equivalents Quiz | F-A5 (Enharmonic equivalence) | Pitches | **Adopt** | Already in our taxonomy as P-018. |
| **E1** | Finger Independence Drills | (Technique substrate) | — | **Defer-conditional on §11.4** | Pedagogically valid; user-value clear. Defers on the same framework-fit basis as A4 — see A4 notes. If §11.4 resolves toward accommodating technique drilling in the Exercise content mode, E1 becomes V1 preset candidate. |
| **E2** | Hand Coordination Drills | (Cross-substrate, mostly motor) | — | **Defer-conditional on §11.4** | Same. |
| **E3** | Thumb Crossing Exercises | (Technique substrate) | — | **Defer-conditional on §11.4** | Same. |
| **E4** | Hand Position Shifts | (Technique + spatial) | — | **Defer-conditional on §11.4** | Same. |
| **E5** | Wrist Rotation Exercises | (Technique substrate) | — | **Defer-conditional on §11.4** | Same. |
| **E6** | Velocity Control Exercises | A-* (Amplitude) | (Amplitude — deferred) | **Defer-V2** | Decision #3. |
| **F1** | Call and Response | Improvisation territory | — | **Defer** | Decision #13 defers improvisation. |
| **F2** | Improvisation over Chord Progressions | Improvisation territory | — | **Defer** | Same. |
| **F3** | Melody Completion | Improvisation territory | — | **Defer** | Same. |
| **F4** | Chord Voicing Exploration | F-C8 (Chord voicing) — exploratory | Chords | **Pedagogically-restate** | Patrick's Free Play completion-policy setting (§5.1, exercise control surface §6A.2) on a Chords atom approximates this. |
| **G1** | Clef Reading (Alto/Tenor) | F-A2 specialized | Pitches/Note Reading | **Defer-V2** | Niche; advanced users. Defer until catalog has critical mass for typical users. |
| **G2** | Transposition Exercises | F-A6 / X-* | (Cross-domain) | **Defer-V2** | Transposition is a substrate-spanning operation; needs dedicated design (Decision #13 territory). |
| **G3** | Score Reading (Multiple Staves) | X-2 specialized | (Sight Reading) | **Defer-Sight-Reading** | Belongs in Sight Reading content mode. |
| **H1** | Classical Technique Drills (incl. Alberti bass) | Genre-tagged content scope | various | **Reject as cluster, adopt as tag — high priority** | Alberti bass is the canonical example for Doc 10 §5.4 goal category 3 ("specific technique"). Patrick's H1 is a direct demo-input. Genre/style tagging now load-bearing for Projects per §5.7. |
| **H2** | Jazz Voicings and Comping | F-C8 + jazz content scope | Chords | **Reject as cluster, adopt as tag — high priority** | Load-bearing for Doc 10 §5.4 goal categories 4 ("play like Bill Evans") and 5 ("interested in jazz"). |
| **H3** | Blues Patterns and Licks | Genre-tagged content scope | various | **Reject as cluster, adopt as tag** | Same. |
| **H4** | Pop/Rock Patterns | F-C12 + pop content scope | Chord Progressions | **Reject as cluster, adopt as tag** | Same. |
| **H5** | Latin Rhythms | T-C2 + Latin content scope | Rhythms | **Reject as cluster, adopt as tag** | Same. |

### 8.2 Summary by category

- **Category A (8 templates)**: 4 adopt (A1, A2, A3, A5); 1 defer-conditional on §11.4 (A4); 3 defer (A6 sight-reading, A7 amplitude, A8 pedal-substrate)
- **Category B (4)**: All 4 adopt (B1, B2, B3, B4)
- **Category C (8)**: 6 adopt clean (C1, C2, C3, C5, C7, C8); 2 adopt-modified (C4, C6 split into multiple atoms)
- **Category D (7)**: 5 adopt clean (D1, D2, D3, D4, D5, D7); 2 adopt-modified (D6 splits into multiple atoms)
- **Category E (6)**: 5 defer-conditional on §11.4 (E1–E5); 1 defer V2 (E6 amplitude per Decision #3)
- **Category F (4)**: All defer (improvisation territory; one — F4 — covered by Free Play completion-policy setting in exercise control surface)
- **Category G (3)**: All defer (V2 or Sight Reading content mode)
- **Category H (5)**: All reject as clusters; their content lives as genre-tagged atoms across other clusters — **strategic priority elevated in v0.2** because Doc 10 §5.4 goal categories 3/4/5 depend on the tagging working

**Net for V1 preset inventory**: ~22 templates from Patrick survive direct or modified absorption (Categories A, B, C, D). An additional **6 templates (A4, E1–E5) are defer-conditional on §11.4's resolution** — if §11.4 resolves toward accommodating technique drilling in the Exercise content mode, the V1 preset inventory grows by these 6. Most adopted templates map to atoms our framework would generate anyway; what Patrick adds is concrete content scope examples, passing criteria, and (newly important) the demo-aligned genre/style content scope.

**§11.4 priority signal (new in v0.3).** §11.4's resolution is now blocking ~6 V1 preset candidates, not just abstract framework completeness. Worth elevating in B-track triage when that work begins.

### 8.3 Passing criteria absorption *(framing loosened in v0.3 to match §5.4)*

Patrick's passing criteria are consistent across templates. Per Decision #43, these patterns are the exercise-section instantiation of the cross-mode performance-constraints primitive. **Candidate starting baselines** (not committed defaults — see §5.4 framing):

| Atom shape | Candidate starting threshold |
|---|---|
| PRF method on note-reading exercises (A1, A2, A3, A5, B4, etc.) | 4 consecutive phrases at 95% accuracy + goal tempo |
| REC method on identification (C1–C5, D2–D7) | 4 consecutive correct |
| REC method on flashcards (D1) | 20 correct in a row, avg response < 3 seconds |
| PRF on cross-domain at high difficulty (G3) | 4 consecutive at 90% (relaxed) |
| PRF on rhythm-only (B1, B2) | 4 consecutive patterns at 95% accuracy |

These become *starting points* for V1 catalog authors (Track D) to build from, not committed canon defaults. Per-atom values during catalog authoring can override based on substrate, method, pedagogical reasoning, or expert judgment. AI generation (Decision #33) may compute thresholds dynamically based on user state. User input via the exercise control surface may adjust per-session. The pattern shape is Patrick's contribution; the specific numbers are held loosely. Decision #50 (renumbered) reflects this — see §10.

---

## 9. Implications for V1 Scope

What does this evaluation suggest about V1 catalog scoping?

### 9.1 V1 catalog primarily comes from Categories B, C, D
The cleanest direct absorption is Categories B (Rhythm), C (Ear Training), D (Music Theory Quizzes). These are 19 of Patrick's 50 templates, and they map most directly to our atom-identity model. **Recommendation:** V1 catalog should prioritize comprehensive coverage of these three skill domains, derived from our substrate × modality × method framework, with content scope progressions that match Patrick's variation tables (his interval table, his chord table, his polyrhythm table, etc., are useful inputs).

### 9.2 Sight Reading exercises move out of the V1 Exercise Section
Patrick's A6, B4 (in some framings), and G1–G3 are sight-reading-focused exercises. Per our Bible §2.1.1, Sight Reading is anticipated to evolve into its own content mode; Decision #45 has now confirmed user-generated sight-reading lives there. **Recommendation:** Don't ship sight-reading-specific atoms in the V1 Exercise content mode — they belong in the (anticipated) Sight Reading content mode. This keeps the Exercise content mode focused on isolated substrate drilling, which is its functional definition (Bible §2.2).

### 9.3 Technique drilling (Category E) is V2+
Patrick's E1–E6 are pure-Performance, motor-skill-focused drilling. Decision #13 already defers technique drilling; this evaluation confirms. **Recommendation:** V1 ships Performance method only on existing substrate atoms (where the substrate provides the cognitive content). Pure-motor drills (Hanon-style, finger independence, wrist rotation) wait for V2.

### 9.4 Genre is a filter, not a cluster — *and it's strategically load-bearing for demo (v0.2)*
Patrick's H category should not produce a "Genre" cluster in our nav. **Recommendation:** Add genre tags to atom metadata as a candidate during catalog authoring, with priority elevated because Doc 10 §5.4 goal categories 3 (technique-specific, Alberti bass), 4 (artist-specific, Bill Evans), and 5 (genre-specific, bluegrass/jazz) depend on this tagging for Projects to assemble coherent goal-bound roadmaps. The user can filter "show me jazz-flavored chord progression atoms" without genre being a primary nav axis; the agent can query the same metadata when building goal-category-4/5 Projects.

### 9.5 Free Play absorbs the existing SRT pattern into the exercise control surface *(revised in v0.3)*
§5.1 Free Play absorption is small and worth doing in V1. The pattern already ships in production (SRT Game / Free Play toggle), so absorbing it into the exercise context is extending an established pattern, not introducing a new one. Placement: a completion-policy element of the exercise control surface (Doc 09 §6A.2), live-toggleable during a session per the existing SRT affordance. The naming-collision resolution (rename the deferred candidate content mode to "Improvisation" or similar, freeing "Free Play" for the established meaning) is bundled into Decision #49.

### 9.6 Theory practice doesn't need its own surface
Patrick's Category D (Music Theory Quizzes) confirms the §7 recommendation: theory practice exercises are Semantic-output atoms across multiple existing substrate clusters. They live in Exercises. No "Theory" content mode is needed.

### 9.7 The Exercise Section landing page (Screen A) absorbs Patrick's UI elements as design candidates
Patrick's §2.3 (Recommended for You carousel, collapsible category sections, filter icon, search bar, exercise card design) is direct input to UX exploration of Screen A. These should feed the design conversation, not be committed at the PRD level. **v0.2 note:** the "Recommended for You" carousel is now load-bearing for the user-modeling layer's outputs (Decision #47, §3.8).

### 9.8 Net impact on V1 build effort
Lower than it might first appear. Patrick's doc looks like ~50 features to build, but the framework collapses most of them into shared blueprints + content-scope variation. **Most of Patrick's templates reduce to 4–6 blueprints we already have planned (BP-01, BP-02, BP-05, BP-06, BP-07, BP-10) plus content variation.** The V1 build effort is dominated by content scope authoring and blueprint polish, not by adding new exercise types.

---

## 10. Decision Log Entries Proposed *(renumbered in v0.2)*

Candidate Decision Log entries this evaluation produces, written for Steven's review. Renumbered from v0.1's #42–#46 to #48–#52, since #42–#47 are now committed canon. Cross-references updated for the post-Phase-2 canon.

### Proposed Decision #48: Theory Naming Resolution (Path c) *(renumbered from v0.1's #42)*

**Source:** A2 evaluation of Patrick's Theory Library & Exercise Section doc.

**Decision proposed:** Resolve the "Theory" naming collision via Path (c):
1. Remove "Theory" from the Bible §2.1.1 candidate content modes list. Theory practice exercises are correctly handled as Semantic-output atoms across existing substrate clusters (Frequency-Domain, Time-Domain) within the Exercises content mode.
2. Patrick's video-library concept gets renamed (working candidate: "Knowledge Library"; alternatives "Learn," "Concepts").
3. The renamed video-library feature is **deferred beyond V1** (see Decision #51 below) but its name is reserved.
4. Glossary "Content Mode" entry updates to remove Theory from the candidate list. The "Free Play (original sense)" candidate is renamed to "Improvisation" per Decision #49 Part 2 (this Decision and #49 are paired updates to the candidate list).
5. Doc 09 §13.11 #51 (Content Classes Inventory) marks Theory as resolved by this Decision. #52 (Interactive Tutorial placement) and #53 (Video Library placement) remain open within the cluster. #54 (originally "Free Play original-sense status") refers to the renamed "Improvisation" candidate per Decision #49 Part 2.

**Reasoning:** Patrick's "Theory Library" is misnamed in his own doc — its scope is broader than music theory and includes technique, genre, performance psychology, and song-context videos. Theory-practice exercises don't warrant a separate content mode because they decompose cleanly into Semantic-output atoms across existing substrate clusters. Adding a "Theory" content mode would either duplicate atoms or fragment clusters; both are worse than absorbing the pattern into Exercises.

**Cross-references:** Bible §2.1.1, Glossary "Content Mode," Decision #41, Decision #45 (clarified for the renamed candidate per Decision #49 Part 2), Decision #49 Part 2 (paired update — Improvisation rename), Doc 09 §13.11 (cluster home).

---

### Proposed Decision #49: Free Play as Completion-Policy Element of the Exercise Control Surface (with Naming-Collision Resolution) *(renumbered from v0.1's #43, substantially rewritten in v0.3)*

**Source:** A2 evaluation of Patrick's Game Mode vs. Free Play framing (his §2.1), corrected in v0.3 to recognize the pattern's existing MuseFlow Sight Reading precedent.

**Decision proposed (two parts):**

**Part 1 — Absorb Free Play into the Exercise content mode.** Extend the existing Sight Reading Game / Free Play pattern (production-current today) into the Exercise content mode by adding a **completion-policy element to the exercise control surface (Doc 09 §6A.2)** with two values:
- **`practice`** (default) — assessable, contributes to mastery thresholds, produces ExerciseResult with completion status
- **`free_play`** — non-assessable, no completion contribution, but stats (accuracy, tempo, errors) are still tracked and displayed

The completion-policy element is **live-toggleable during a session**, preserving the existing SRT affordance where the user flips between Game and Free Play mid-exercise without backing out and reconfiguring. Whether the agent can also flip the toggle mid-session is a separate question per Decision #46 (the agent's policy operates over the surface elements; live-toggle by user and by agent are not mutually exclusive).

Free Play is available on any atom that supports a continuous-practice interaction (most PRF atoms; some REC/RCL atoms). Specific applicability per blueprint is open.

This placement parallels Decision #45's "no completion criteria, just play endlessly" option for user-generated sight-reading; both are completion-policy settings within their respective mode's control surface, not new content modes.

**Part 2 — Rename the deferred candidate content mode currently called "Free Play (original sense)" to "Improvisation."** "Free Play" as completion-policy collides with "Free Play" as the deferred candidate content mode for open-ended improvisation. Sharing the name is unworkable. Since the deferred candidate is uncommitted and not yet user-visible, renaming it costs nothing in production-vocabulary terms; renaming the completion-policy would fight established SRT terminology. Specific changes:

- **Bible §2.1.1**: rename "Free Play" candidate content mode entry to "Improvisation"
- **Glossary "Content Mode"** entry: update to read "Improvisation is a candidate future content mode (status TBD, deferred indefinitely per Decision #45's clarification)"
- **Decision #45's scope clarification** is amended to refer to the renamed candidate
- **Doc 09 §13.11 #54** updates to refer to "Improvisation original-sense status (deferred indefinitely)"

Alternate names considered: "Open Play," "Jam." "Improvisation" lands as most accurate to the original-sense intent (open-ended musical improvisation without notation guidance) and is the recommended primary candidate.

**Reasoning.** Free Play is a real practice need (warm-up, experimentation, indefinite practice without pass/fail pressure), and a pattern already ships in production via the SRT. Placing it in the exercise control surface (an architecture that already exists per Decision #46 and Doc 09 §6A.2) is the smallest change with the most reusability. The live-toggle requirement preserves what users expect from the existing SRT pattern. The naming-collision resolution removes a real ambiguity that would otherwise confuse users, the team, and downstream design work.

**Phasing.** V1 for Part 1 — the control surface element addition is non-breaking; the UI surface for Free Play in exercises mirrors the existing SRT toggle UI. V1 for Part 2 — a documentation/naming change with no implementation cost.

**Cross-references:** Doc 09 §6A.2 (exercise control surface), Decision #46 (control surface enumeration), Decision #45 (parallel for sight-reading; Decision #45's scope clarification amended by Part 2 of this Decision), Bible §2.1.1 (candidate content mode list — updated by Part 2), Glossary "Content Mode" (updated by Part 2), Doc 09 §13.11 #54 (Improvisation original-sense status — refers to renamed candidate), Standup Synthesis §1 (Staley's "free-play interlude as part of the path"), Architecture Doc §8.

---

### Proposed Decision #50: Patrick's Mastery-Threshold Patterns as Candidate Starting Baselines *(renumbered from v0.1's #44, reframed in v0.3)*

**Source:** A2 evaluation of Patrick's passing criteria across ~50 exercise templates.

**Decision proposed:** Adopt Patrick's recurring passing-criteria patterns as **candidate starting baselines for `mastery_thresholds` during V1 catalog authoring**. These are starting points, not committed defaults — easily overridable per atom, AI-generated, preset, or user-input configuration.

Candidate starting baselines by atom shape:

| Atom shape | Candidate starting threshold |
|---|---|
| PRF on note-reading exercises (most BP-05 atoms) | 4 consecutive phrases at 95% accuracy + goal tempo |
| REC on identification tasks (BP-01, BP-02 atoms) | 4 consecutive correct |
| REC on flashcard-style atoms (BP-10 candidate) | 20 correct in a row, avg response time < 3 seconds |
| PRF on cross-domain / sight-reading atoms (X-*) | 4 consecutive phrases at 90% accuracy |
| PRF on rhythm-only atoms (BP-06) | 4 consecutive patterns at 95% accuracy |

**What this Decision commits.** The *methodology* of having defaults at all — atoms in the V1 preset inventory carry `mastery_thresholds` populated during catalog authoring, with Patrick's patterns as one defensible starting baseline. Catalog authors (Track D) can override per atom based on substrate, method, or pedagogical reasoning. AI-generated atoms (per Decision #33) may compute thresholds dynamically based on user state, goal, or pedagogical inference. User input via the exercise control surface (Doc 09 §6A.2) may adjust per-session.

**What this Decision does not commit.** The specific numbers above as the *right* numbers. The n-dimensional matrix of cross-mode performance-constraint settings (per Decision #43) supports many valid configurations; Patrick's patterns are *a* defensible region of that space, not *the* region. Track D may converge on different patterns once authoring begins in earnest.

Per Decision #43 (Performance Constraints Generalize Across Content Modes), these patterns are the **exercise-section instantiation of the cross-mode performance-constraints primitive**. The same shape (N consecutive at X% accuracy, optional tempo or time targets) will inform sight-reading and repertoire performance-constraint defaults as those modes' design progresses.

**Reasoning.** Patrick's templates are consistent enough to suggest a recurring pattern, and that pattern gives Track D a defensible starting point. Treating the specific numbers as committed defaults would over-constrain Track D and pre-empt judgment that's better made during atom-level authoring. Treating the methodology as committed (defaults exist; Patrick's patterns are the baseline) gives Track D a working scaffold without prematurely closing decisions.

**Phasing:** V1, applied during catalog authoring (Track D).

**Cross-references:** Decision #40 (`mastery_thresholds` field), Decision #43 (cross-mode performance constraints), Decision #33 (generation on demand — agent may compute thresholds dynamically), Bible §2.3 (cross-mode primitive framing), Doc 02 §5.1 (cross-mode tech spec scope), Architecture Doc §8.1.

---

### Proposed Decision #51: Knowledge Library / Video Resource Surface — Deferred Beyond V1 *(renumbered from v0.1's #45)*

**Source:** A2 evaluation of Patrick's Theory Library proposal (his Part 1).

**Decision proposed:** The renamed video-resource surface (working name: "Knowledge Library") is **deferred beyond V1**. Patrick's design (Smart Feed / Quick Theory / Deep Dives, with curation logic and proactive suggestion modal) is preserved as design input for the deferred feature. The surface's architectural placement is the Doc 09 §13.11 #53 sub-question (Video Library architectural placement); recommended resolution lean is toward **Staley's framing (roadmap-node primitive / agent-surfaced video)** over Patrick's (content-mode-like).

Two specific elements are absorbed earlier:
- Patrick's **Proactive Suggestion System** (his §1.5) is absorbed as candidate engagement-layer behavior, scaffolded against the user-modeling layer (Decision #47) for trigger logic and the per-mode control surfaces (Decision #46) for action vocabulary. Trigger conditions and modal pattern apply generically — content surfaced is whatever the engagement layer determines is most useful (exercises, repertoire, video, prescribed control-surface settings), not just video.
- Patrick's **content tagging vocabulary** (concept, instrument focus, genre — his §1.3) is flagged as candidate metadata extension for catalog authoring conversations. Genre tags are high-priority given Doc 10 §5.4 goal-category alignment.

The Knowledge Library as a top-level content surface waits until: (a) the engagement layer ships, (b) Projects ships and the "agent surfaces a relevant video as part of a Project node" pattern is testable, (c) compliance / licensing for embedded video is cleared, and (d) the §13.11 #53 placement question resolves.

**Reasoning:** Patrick's Theory Library is well-designed but its V1 implementation cost is high relative to its V1 value. The proactive suggestion system, which is the interaction-layer innovation in his design, is generically valuable and absorbed early; the surface itself (browsable video library) is more naturally a 2024+ pattern of "agent surfaces relevant content" than a 2018-2022 pattern of "user browses curated library." Doc 09 §13.11 #53 now formally tracks this placement question with the two candidate framings.

**Cross-references:** Decision #19 amendment (engagement layer), Decision #41 (content/path mode architecture), Decision #46 (per-mode control surfaces — the agent's action vocabulary for suggested interventions), Decision #47 (user-modeling layer — the substrate the suggestion system depends on), Doc 09 §13.11 #53 (formal cluster home for Video Library placement), Doc 09 (Projects as the natural home for agent-surfaced video).

---

### Proposed Decision #52: B/I/A as a Candidate Derived Label (Not a Schema Axis) *(renumbered from v0.1's #46)*

**Source:** A2 evaluation of Patrick's flat Beginner/Intermediate/Advanced difficulty axis.

**Decision proposed:** **B/I/A is not added to the atom schema as a primary difficulty field.** The 3-axis difficulty model (Decision #7: substrate complexity × training method scaffolding × constraint tightness) is the engine. If the UX exploration determines a user-facing summary label is needed (Open Question #5: "Named presets vs. individual sliders"), B/I/A or a similar label can be **derived** from atom configuration at filter time — it does not exist as a stored field. Per Decision #43 (cross-mode performance constraints), if a B/I/A-style summary label is wanted across content modes, the derivation rules are likely per-mode rather than shared — the same B/I/A bucket means materially different things for an exercise atom vs. a sight-reading level vs. a repertoire practice session.

**Reasoning:** Flat B/I/A is a brittle simplification of our richer 3-axis model, and the brittleness compounds across content modes per Decision #43. Storing it as a schema field would require ongoing maintenance to keep B/I/A in sync with the underlying axes, and the mapping isn't deterministic anyway (a Compound substrate at REC method with loose constraints is "easier" than an Atomic substrate at PRF method with tight constraints, but in different ways). Derive-on-filter is the right level of commitment.

**Phasing:** V1 — at the schema level, this is a non-decision (don't add the field). UX exploration may surface B/I/A or alternatives later.

**Cross-references:** Decision #7, Decision #43 (cross-mode performance constraints — sharpens the case against a flat schema label), UX Spec §9 Open Question #5.

---

## 11. Open Questions Surfaced

Items Patrick's doc raises that our canon hasn't addressed and should track. Each gets a brief framing for B-track (open-question triage) intake. Several have updated framing in v0.2 reflecting post-Phase-2 canon.

### 11.1 Where do videos live in MuseFlow when they exist?
**v0.2 update:** This question now sits inside Doc 09 §13.11 #53 (Video Library architectural placement) as a formally-tracked cluster sub-question. Patrick's framing (content-mode-like) vs. Staley's framing (node-as-tutorial / roadmap-node primitive) are the two candidate resolutions. Recommended lean per §4.6 and proposed Decision #51: Staley's framing wins. Resolution timing post-V1.

### 11.2 What does an Arpeggio cluster look like? (Or is it a sub-strand of Chords?)
Patrick's A2 (Arpeggios) raises a real classification question. Arpeggios are chord constructions performed sequentially. In our framework, are they:
- A separate cluster (parallel to Chords)?
- A sub-strand within Chords?
- Atoms with a "performance mode = arpeggiated" content-scope configuration?

Open. Worth resolving during catalog authoring (Track D).

### 11.3 Where do pedaling exercises live?
Pedal substrate isn't in our current substrate catalog (Architecture Doc §3.1). Patrick's A8 highlights this gap. Open: do we add pedal as a distinct substrate (likely under a new "Articulation/Pedal" cluster), or treat it as a constraint/configuration on existing atoms? Probably distinct substrate; worth a catalog-authoring conversation. **v0.2 cross-ref:** pedaling-as-substrate is also a candidate roadmap-node concept under Doc 09 §6A.1's repertoire control surface (pedal handling can be a per-session enabled assistance).

**Resolution status (2026-05-12, Track B Phase 3):** A pedal-as-distinct-substrate Decision was initially proposed during Phase 3 but withdrawn after review surfaced architectural pairing with T-027 (Technique drills, Doc 11 §11.4) and a newly-surfaced question T-097 (Cognitive-vs-motor substrate distinction and dual-training representation). The substrate catalog currently treats substrates as cognitive transformations and does not model motor/execution skills as distinct substrates; deciding pedal's placement unilaterally would prejudge T-027 and ignore the broader cognitive-vs-motor architectural question. T-026 (this question) is now re-bucketed as V1-decide-soon and paired with T-027 and T-097 in a new C-17 cluster ("Substrate-architecture refinement") in the open-question triage. Resolution venue: Track D substrate-architecture refinement work, where the cognitive/motor framing for the catalog gets decided alongside Technique-drill placement and pedaling placement.

### 11.4 Are technique drills exercises or something else? *(priority elevated in v0.3)*
Patrick's E category (Technique and Coordination Drills) is pedagogically valid but doesn't fit the substrate-driven model — these are motor-skill drills with no specific substrate content. Open: are technique drills:
- A V2 expansion of the Exercise content mode with a new "Technique" cluster?
- A distinct content mode (alongside Improvisation candidate)?
- A blueprint variant where the substrate is "motor pattern" and the content scope describes the pattern?
- Performance-method atoms in existing substrate clusters with content-scope specifying the technique pattern (Patrick's framing, retrofitted)?

Decision #13 defers; this question survives the deferral. **v0.3 priority elevation:** §11.4's resolution now blocks **~6 V1 preset inventory candidates** — A4 (Hanon-style) and E1–E5 (finger independence, hand coordination, thumb crossing, hand position shifts, wrist rotation) per the §8 mapping table's defer-conditional reframe. The defer reflects framework-fit ambiguity, not a user-value assessment — these are foundational exercises for many users. Worth elevating in B-track triage when that work begins. **v0.2 cross-ref retained:** this question is adjacent to Doc 09 §13.11's "Content Classes Beyond the Core Three" cluster, though it's not yet listed there explicitly. If Technique becomes a candidate distinct content class, it would join the cluster.

### 11.5 What's the right granularity for genre tagging?
Patrick's H category implies 5 genre buckets (Classical, Jazz, Blues, Pop/Rock, Latin); his Quick Theory tagging implies more (classical, jazz, pop, blues, ragtime). Open: when genre tags are added as filter metadata, what's the canonical list, and at what granularity? (E.g., does "Latin" decompose into bossa nova / samba / salsa / tango per Patrick's H5?) **v0.2 elevation:** priority raised given Doc 10 §5.4 goal-category alignment — genre tags are now load-bearing for Projects targeting "I'm interested in [genre]" goals (category 5) and "play like [artist]" goals (category 4). The granularity choice affects what kind of Projects the agent can build.

### 11.6 Improvisation and creative exercises — is there a path for these in our framework?
Patrick's F category (Creative and Improvisation) exposes a real gap. Decision #13 defers improvisation, but the gap remains. Open: as Projects mature and the exercise control surface (§6A.2) stabilizes, does creative exercise design re-enter scope? Or does it stay deferred indefinitely? **v0.2 cross-ref (updated in v0.3):** related to the renamed candidate content mode "Improvisation" (formerly "Free Play original sense") — per Decision #45 (clarified) and Decision #49 (Part 2), this remains deferred indefinitely as a content mode. The renamed Improvisation content mode and Patrick's F category cluster together — both are open-ended, non-completable music-making territory.

### 11.7 The Cross-Section "Master Roadmap" appetite
Patrick's §3.2 reveals team appetite for **cross-section preset paths** (Curriculum that spans Sight Reading + Repertoire + Theory/Knowledge + Exercises). Our canon (Bible §2.2) anticipates Curriculum either dissolving in favor of Projects or broadening into a multi-content-mode preset path. Open: which evolution wins, and on what timeline? **v0.2 cross-ref:** Doc 09 §3.1 (Where Projects Sit in MuseFlow's Architecture) addresses some of this; the question becomes "does the team also want a non-AI-mediated, MuseFlow-authored, cross-content-mode Curriculum, in addition to Projects?" If yes, that's a Curriculum-broadening commitment. If no, Projects subsumes the intent.

### 11.8 Five-exercises-cover-90% question (from Standup Synthesis)
Staley asked Steven, "what maybe five exercises do you think could probably apply to like 90% of pieces?" — Steven didn't answer in the standup. Patrick's catalog provides a partial answer (his A1 Scales + A2 Arpeggios + A3 Chord Progressions + B1 Rhythm Tapping + C1 Interval Recognition is a reasonable five-pack). Open: is this question worth answering deliberately as part of the PRD, both as curriculum primitive and investor-demo framing? **v0.2 cross-ref:** connects to Doc 10 §10 Track D recommendation (user-story-driven prioritization) and the reverse-engineering methodology (Doc 10 §4.5) — the "feed the AI the universe" approach is essentially the inverse of this question.

### 11.9 *(New in v0.2)* Patrick's premium-tier framing vs. Doc 09 §16 cost framework
Patrick's "50% atom gating" treats exercises as scarce/curated; Doc 09 §16 treats generation cost (LLM tokens) as the variable expense. Resolution: pick a gating framing for the pricing conversation. Two candidate resolutions: (a) Patrick's atom-gating wins and §16's framework gets refined; (b) §16's generation-gating wins and Patrick's atom-gating becomes a teaching example of pre-§16 thinking that we superseded. Recommended lean: (b), but this is a team-alignment question, not just a memo recommendation. Cross-ref: Decision #37 (pricing deferred), Doc 09 §16, UX Spec §9 Open Questions 21–23.

**Resolution (2026-05-12, per Decision #55):** Confirmed (b) — generation-cost-gating is canonical pricing framing. Patrick's atom-gating proposal is preserved as a discussion artifact / pre-§16 thinking that the team superseded; not the forward-design direction. The Decision resolves only the *framing*; the actual pricing structure remains deferred per Decision #37.

### 11.10 *(New in v0.3)* Exercise UI session structure
Patrick's framing collapses all reading/playing exercises onto the Sight Reading Trainer UI — continuous two-line scroll, chevron clearance gate, automatic tempo adjustment, Game/Free Play toggle. The Interactive Tutorial exercise UI (per Glossary canonical entry; production-current) presents a different shape — single-line prompt, prompt banner above, Chapters sidebar, discrete prompt-and-perform evaluation. Which session structure applies to which Patrick-template-derived atom is currently undecided in canon. Some templates (A1 Scales, A3 Chord Progressions, B4 Rhythm Sight Reading) could plausibly fit either; others (B1 Rhythm Tapping, D1 Note Naming flashcards) fit the discrete prompt-and-perform shape more obviously — the SRT's continuous-scroll affordance is awkward for flashcard-style identification.

The notation rendering primitives and three-state note feedback are clearly reusable across UIs; the session structure choice is not. Resolving this is a Track D / Track E precursor and warrants **its own design conversation outside A2 scope**, likely with mockups and prototypes (the conversation may need to surface things screenshots alone can't communicate, like the difference between non-stop continuous play and discrete prompt-and-perform pacing).

Connected to: Patrick's §2.1 SRT-reuse claim (§3.1 of this memo); the Interactive Tutorial Glossary entry; the open question of how blueprints map to UI shapes (Doc 06).

---

## 12. Closing Assessment

Patrick's brainstorm doc is competent, comprehensive, and largely consistent with itself. It is also substantially superseded by the canon's evolution — the agentic Projects pivot (Decision #32), the content/path mode architecture (Decision #41), the atom-identity model (Decision #25), the first-principles framework (Bible §3, §6), and now (post-Phase-2) the cross-mode performance-constraints primitive (Decision #43), the per-mode agent control surfaces (Decision #46, Doc 09 §6A), and the user-modeling layer as foundational architectural commitment (Decision #47, Doc 09 §1.2). The brainstorm doc operates at the feature/UI level; the canon operates at the architecture/primitive level.

**Net absorption from the brainstorm doc (updated in v0.3):**
- **~22 of 50 exercise templates** survive direct or modified absorption as concrete V1 preset inventory candidates
- **~6 additional templates (A4, E1–E5) are defer-conditional on §11.4's resolution** — if §11.4 resolves toward accommodating technique drilling in the Exercise content mode, the V1 preset inventory grows by these. §11.4 is now blocker-class for this subset.
- **5 candidate mastery-threshold patterns** extracted from Patrick's passing criteria, framed (per v0.3) as candidate starting baselines for Track D, not committed defaults
- **Free Play (within atoms)** absorbed as a completion-policy element of the exercise control surface, **live-toggleable during a session** (preserving the existing SRT affordance), with the naming-collision resolution (rename the deferred candidate content mode currently called "Free Play (original sense)" to "Improvisation") bundled into the same Decision (#49)
- **Recognition that Free Play / Game Mode is an established MuseFlow Sight Reading pattern** — Patrick is echoing production-current behavior, not inventing it. The absorption extends an established pattern across content modes.
- **Proactive Suggestion System** absorbed as engagement-layer design input, scaffolded against the user-modeling layer (Decision #47) and per-mode control surfaces (Decision #46)
- **Tagging vocabulary** (concept, genre, instrument focus) flagged as candidate metadata extension, with genre tags elevated to high-priority given Doc 10 §5.4 goal-category alignment
- **Theory naming question** resolved Path (c) (proposed Decision #48, resolving Doc 09 §13.11 #51 for Theory specifically)
- **Knowledge Library** (renamed Theory Library) deferred beyond V1 (proposed Decision #51, formal tracking under Doc 09 §13.11 #53). Eight candidate names surfaced; final naming call deferred to when the feature enters scope.
- **Patrick's H1 Alberti bass example** confirmed as direct demo-relevant content per Doc 10 §5.4 goal category 3
- **9 open questions** in the queue for B-track triage (one new in v0.3: §11.10 exercise UI session structure)

**Net rejection from the brainstorm doc:**
- Patrick's flat B/I/A difficulty model (proposed Decision #52) — rejection sharpened by Decision #43
- Patrick's "Master Roadmap" as a separate architectural primitive — rejection sharpened by Decisions #46, #47
- Patrick's specific named achievements / Practice Points gamification (stays Patrick's MVP-decomposition work)
- Patrick's premium tier specifics as schema-level commitment, with §16 tension explicitly flagged
- Patrick's Categories A, E, G, H as cluster names (kept as filter tags; H tags elevated in priority per Doc 10 §5.4)
- Patrick's Theory Library as a V1 top-level content surface; deferred to post-V1 with recommended placement-resolution direction (Staley's roadmap-node framing over Patrick's content-mode framing)
- Patrick's wholesale "use the SRT UI for all reading/playing exercises" claim (v0.3 softening) — primitives reusable; session structure undecided per atom/blueprint
- Patrick's specific carousel-card design as endorsed Hook-zone UI (v0.3 tone correction) — Hook zone architecturally significant; visual treatment undecided

**On the user-modeling layer alignment:** Patrick's instincts about "the system should know the user well enough to surface relevant content" align with what is now MuseFlow's most strategic architectural commitment (Decision #47). This is non-trivial. Patrick's brainstorm doc precedes the explicit articulation of the user-modeling layer as a vision pillar, but the intuition was already there — the system Patrick describes presupposes the layer. That alignment is confidence-building.

**On the auto-looping clarification:** Patrick's separately-referenced PRD (the one cited in May 7 brainstorm as containing the auto-looping algorithm) is **not** the brainstorm doc evaluated here. The brainstorm doc contains no auto-looping content. Evaluating the PRD itself against canon is a separate piece of work that may be warranted; this memo does not perform it.

**Headline action items:**
- The five proposed decisions (#48–#52) for Steven's review, with Decision #49 now carrying two parts (completion-policy absorption + naming-collision resolution)
- The open-question additions for B-track triage (nine items: §§11.1–11.10, with §11.4 priority elevated and §11.10 new in v0.3)
- The §13.11 #51 cluster update (mark Theory as resolved by Decision #48); §13.11 #54 update (refer to "Improvisation" rather than "Free Play original-sense" per Decision #49 Part 2)
- The pricing-framework tension surfaced as input to future pricing conversation

**Conversations to stage outside A2 scope (explicit in v0.3):**
- **The broader "how do different exercises look and function" conversation** — exercise UI shape and session structure is currently underspecified in canon (§11.10). Its own design session, likely with mockups and prototypes. Track D / Track E precursor.
- **The full V1 atom catalog authoring conversation** — Track D. This memo provides candidate inputs (§8 mapping table, §8.3 candidate starting baselines) to that work; it does not constitute Track D.
- **Evaluation of Patrick's separately-referenced PRD** (the auto-looping source) — its own piece of work; not performed here.

Once the headline action items resolve, Patrick's brainstorm doc has been fully integrated to the extent integration is warranted. Subsequent design tracks (C — taxonomy reconciliation; D — V1 atom catalog authoring; E — PRD) can proceed without further reference to the brainstorm. The separately-referenced PRD remains a candidate target for a future evaluation pass.

---

*End of A2 Integration Memo v0.3.*
