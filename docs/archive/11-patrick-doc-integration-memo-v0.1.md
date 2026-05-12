# Patrick's Theory Library & Exercise Section Doc: Integration Memo

> **Status: A2 deliverable, first draft (May 2026).** This memo evaluates Patrick Boylan's "Theory Library & Exercise Section: Comprehensive Feature Brainstorm & Design Specification" (~1167 lines, written several months prior) against the current MuseFlow Exercise Section canon (post-A1, including Decisions #32–#41 and Doc 09). It identifies alignment, conflict, additive material, and material that is better in our framing. It is a one-pass draft intended for redline.
>
> **Source documents referenced:** Project Bible (Doc 01), System Architecture (Doc 02), Exercise Taxonomy (Doc 03), Glossary (Doc 04), Design Decisions Log (Doc 05), Exercise Blueprints (Doc 06), UX & Navigation Spec (Doc 07), Standup Synthesis (Doc 08), Agentic MuseFlow Vision (Doc 09).
>
> **Methodological note:** Steven explicitly framed Patrick's doc as "important context for what he's thinking" — not a vision to merge in. This memo treats Patrick's content as evaluable input, agrees where his framing is sound, disagrees where ours is better, and absorbs concretely where absorption strengthens the design. Speculative claims are tagged `[Speculative]`. Open questions surfaced are collected in §11.

---

## 1. Executive Summary

1. **Patrick's doc is a "specific UI features and ~50 exercise templates" document.** Our canon is a "first-principles generative architecture" document. The two are working at fundamentally different levels — Patrick proposes named features with passing criteria; our canon defines the framework that *generates* such features. Most apparent conflicts are actually category mismatches between these two levels.

2. **The "Theory" naming collision is the headline structural conflict.** Patrick uses "Theory Library" to mean a video-content surface (YouTube/TikTok embeds); our Bible §2.1.1 has "Theory" as a candidate content mode for theory-practice exercises. **Recommendation: Path (c) — rename Patrick's surface ("Knowledge Library" or "Learn" are leading candidates), and resolve the candidate content mode to "no, theory is just a substrate family within Exercises."** See §7.

3. **Patrick's doc largely predates the agentic Projects pivot** (Decision #32, May 5 standup) and the Content/Path Mode reframe (Decision #41). His "Future Unified Roadmap" (his §3.2) is closer to an expanded Curriculum than to Projects, and our Projects framing has effectively superseded it. The gap is interesting nonetheless — see §4.

4. **Patrick's ~50 exercise templates (Categories A–H) map cleanly to our framework as concrete atom instantiations.** His category boundaries (Sheet Music-Based, Rhythm, Ear Training, etc.) approximate clusters in our hierarchy but are not isomorphic — see §8 for the mapping table. The templates are valuable inputs to V1 catalog authoring; their passing criteria feed `mastery_thresholds` (Decision #40).

5. **Patrick's flat B/I/A difficulty axis conflicts with our 3-axis model** (Decision #7: substrate complexity × training method scaffolding × constraint tightness). **Recommendation: keep the 3-axis model as the engine; defer the question of whether B/I/A appears as a user-facing summary label to UX exploration.** Don't surface B/I/A directly in the schema. See §4.3.

6. **Patrick's "Game Mode vs. Free Play" distinction is genuinely additive.** Free Play (no pass/fail, indefinite practice with stats tracking) isn't currently a first-class concept in our canon, even though it shows up adjacent to it (the candidate content mode "Free Play," Staley's "free-play interlude" comment). Worth absorbing as a session-mode extension. See §5.1.

7. **Patrick's "Proactive Suggestion System" maps directly onto our engagement layer** (Decision #19 amendment, Glossary "Engagement Layer"). His specific trigger conditions and modal design are the most concrete instantiation of that layer anyone on the team has produced. **Recommendation: absorb as candidate engagement-layer behavior**, scoped to the future engagement layer's design. See §5.2.

8. **Patrick's gamification specifics (named achievements, Practice Points)** should NOT be absorbed at the PRD level. Stay framework-only (the schema supports per-atom tracking; achievements are a derived layer); let Patrick himself decide gamification specifics during MVP decomposition. See §4.7.

9. **Patrick's premium tier proposal is input to a future pricing-design conversation, not an update to schema.** Decision #37 (defer `tier_gating`) stands. See §4.8.

10. **The Theory Library as a video-content surface is conceptually viable but not at V1.** Its design (Smart Feed / Quick Theory / Deep Dives) is well-considered but premature relative to current V1 scope. Better positioning: defer to post-V1 as a candidate adjacent feature, possibly absorbed into Projects (agent-surfaced contextual videos) rather than as a top-level mode. See §4.6.

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

---

## 3. Alignment Register

Items where Patrick and our canon agree. These are confidence-building data points — independent thinking converging.

### 3.1 Exercise UI reuse from Sight Reading Trainer
Patrick (§2.1, "Familiar UI for Sheet Music Exercises") proposes that any exercise involving reading/playing notation should use the Sight Reading Trainer UI — the two-line music display, tempo control, chevrons, accuracy %, three-state feedback (green/yellow/red). This aligns with our blueprint architecture (Doc 06 §1.1): Blueprints are reusable interaction templates, and BP-05 (Prompt → Physical Key Performance) effectively *is* the Sight Reading Trainer UI. Multiple of Patrick's templates (A1–A8, E1–E6, G1–G3, much of H) reduce to BP-05 with different content.

### 3.2 Pattern-recognition driven recommendations
Patrick's "performance-based recommendations" (§1.2 Smart Feed, §2.1 Recommendation Engine, §3.1) — surfacing exercises and content based on backend-detected error patterns — aligns with our V2 Recommended Exercises feature (Bible §9.1) and the engagement layer (Decision #19 amendment).

### 3.3 Recommendations at end-of-tier and end-of-level
Patrick's "End of Tier" and "End of Level" recommendation triggers (§2.1) match the natural surface points for cross-section nudging in our model (curriculum completion → exercise/repertoire suggestions). The mechanism survives translation; only the surrounding architecture differs (his is curriculum-tied; ours is more flexible because it can also work via Projects and the engagement layer).

### 3.4 Soft-unlock vs. hard-unlock progressively
Patrick repeatedly uses "soft-unlock" language for difficulty progression (e.g., A1 Scales: "soft-unlock based on curriculum level in end of level modal, but user can decide to play any of them at any time"). This is consistent with our canon's positioning of `prerequisite_atoms` as load-bearing for agent path-building (Decision #40) but not as a hard gate on user navigation. Users in our system can practice anything they want from the Library zone (UX Spec §3.1); recommendations *surface* relevant atoms, they don't *restrict* access.

### 3.5 Streaks
Both treat daily practice streaks as a first-class engagement primitive (Patrick §2.4; Bible §9.1, V1–V2; Glossary "Streak Tracking").

### 3.6 Repeatable drills as a design category
Patrick's framing (§2.1: "Unlike the Sight Reading Trainer, which generates never-repeating music, exercises are designed to be repeated") matches Decision #22's framing: replayability is a product concept, with constraint variation as the multiplier (Bible §6.3). Different vocabulary, same insight.

### 3.7 Integration with the broader app
Patrick's §3.1 articulates that the Theory Library and Exercise Section are deeply integrated with the rest of MuseFlow (curriculum-driven unlocks, performance-based suggestions, data dashboard rollup). This matches our cross-section complexity language (Architecture Doc §9) and the Project Bible's positioning of Exercises and Repertoire as level-agnostic content modes that compose with paths.

### 3.8 The "Recommended for You" surface
Patrick's "Recommended for You" carousel (§2.3) on the Exercise Section landing page maps to our **Hook zone** in Screen A (UX Spec §3.1). The framing is identical at the surface level, even if our canon lacks Patrick's specific carousel-card design.

---

## 4. Conflict Register

Items where Patrick and our canon genuinely disagree. Each item includes a recommended resolution.

### 4.1 The "Theory" naming collision *(Headline conflict — see §7 for full treatment)*

Briefly: Patrick uses "Theory" for a video surface; our Bible §2.1.1 uses "Theory" as a candidate content mode for theory-practice exercises. Resolution recommended in §7 below.

### 4.2 Patrick's Categories A–H vs. our Cluster framework

Patrick's eight categories are skill-domain categories (rhythm, ear training, technique, etc.). Our clusters are organized either by **substrate family** (Pitches, Intervals, Scales, Chords, Chord Progressions, Rhythms) or by **modality grouping** (Ear Training, Note Reading, Keyboard Skills, Music Theory, Sight-Playing, Transcription) — UX Spec §2.4, with both being traversal paths through the same atom graph.

Patrick's categories *partially* line up with our modality-grouped clusters: his "Ear Training Exercises" ≈ our "Ear Training" cluster; his "Music Theory Quizzes" ≈ our "Music Theory" cluster. But several of his categories cut across both groupings or invent dimensions our framework doesn't surface as primary:

- **A. Sheet Music-Based Technical Exercises** — A bundle of "anything that uses the Sight Reading Trainer UI." That's a *blueprint* in our framework, not a cluster. The contents (Scales, Arpeggios, Chord Progressions, Hanon, Interval Reading) span multiple substrate clusters in our model.
- **E. Technique and Coordination Drills** — A pedagogical-focus grouping (motor skill development) that is orthogonal to substrate and modality. Our framework doesn't surface this as primary either; in our model, these are atoms in various substrate clusters with the **Performance** training method and tightened constraints.
- **F. Creative and Improvisation** — Genuinely doesn't map cleanly. Our canon defers fingering and improvisation as exercise types (Decision #13). Patrick's F2 (Improvisation over Chord Progressions) is open-ended/no-passing-criteria territory; our framework currently has no clean atom slot for it.
- **G. Sight Reading Specializations** — Likely belongs with Sight Reading content mode (anticipated, Bible §2.1.1) rather than within Exercises. Multi-staff score reading (G3) is in particular a sight-reading concern, not an exercise drill.
- **H. Genre-Specific Exercises** — Genre is a *content scope* axis in our model, not a category. Pop/Rock patterns aren't a cluster — they're chord-progression atoms with chord-progression-content-scope constrained to common pop progressions, plus rhythm-pattern atoms with content-scope tags. Genre is metadata that can filter atoms across multiple clusters; it isn't a cluster of its own.

**Recommendation:** Reject Category A, E, G, H as cluster names. Keep Patrick's category groupings as **filter tags** or **secondary navigation views** layered on top of the substrate/modality cluster structure. Specifically:
- **Genre tags** can be a content-scope or metadata filter ("show me Jazz-flavored chord progression atoms")
- **Pedagogical-focus tags** ("technique drilling," "improvisation," "creative") can similarly be a filter
- **Sight Reading Specializations** (G) should be flagged for the Sight Reading content mode design, not the Exercise content mode

§8 has the full mapping table.

### 4.3 Difficulty: flat B/I/A vs. our 3-axis model

Patrick uses **Beginner / Intermediate / Advanced** as a flat difficulty axis applied to most templates (e.g., his interval table, his chord table, his polyrhythm table). Our canon (Decision #7) treats difficulty as three orthogonal axes:

1. Substrate complexity (atomic → molecular → compound → cross-domain)
2. Training method scaffolding (VER → REC → SEL → ASM → ALT → RCL → PRF)
3. Performance constraint tightness (loose → tight)

Plus content scope ladders within strands (UX Spec §6.3).

These models aren't compatible at face value. B/I/A *can* be derived from the 3-axis model (a "Beginner" exercise might be: atomic substrate + REC method + loose constraints + early content scope), but the derivation isn't deterministic — different combinations of the three axes can produce experiences that feel "Beginner" or "Advanced" in different ways. Patrick's flat B/I/A erases that.

**Recommendation:** **Keep the 3-axis model as the engine. Defer the question of whether B/I/A appears as a user-facing summary label to UX exploration** (this is currently Open Question #5 in UX Spec §9 — "Named presets vs. individual sliders"). Don't add a B/I/A field to the atom schema; don't allow users to pick "Beginner" as a primary axis. If we later want a B/I/A summary label as a quick-filter convenience, derive it from the 3-axis state at filter time.

`[Speculative]` Patrick's flat B/I/A may also be artifact of the doc being written at a level where exposing the 3-axis model would have been too much detail. Once Patrick sees the 3-axis model, he may agree the underlying engine is more powerful — the question is just what we expose to users.

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

`[Speculative]` Patrick's framing predates the May 5 Projects pivot. If asked today, Patrick likely sees Projects as the more powerful realization of his Master Roadmap intent.

### 4.5 The Exercise Section as "a separate top-level sidebar section" vs. the content/path mode architecture

Patrick frames the Exercise Section as one of several top-level surfaces (sidebar siblings: Sight Reading Trainer, Repertoire, Theory Library, Exercise Section). Our canon (Decision #41) frames everything as content modes (Exercises, Repertoire, anticipated Sight Reading) and path modes (Curriculum, User Paths, Projects), with a unified three-flow pattern (Browse / Generate / Project) within each content mode.

Patrick's framing isn't *wrong* — content modes will likely each have a top-level entry point. But his framing flattens the architecture (everything is a sibling tab) where ours layers it (content modes hold content; path modes traverse them; Projects is its own first-class entry point alongside the content-mode entries).

**Recommendation:** Our framing supersedes. The Exercise Section is a content mode entry point; Projects is a separate path-mode entry point; the Theory Library (if it ships) is *not* a content mode in our taxonomy and needs another home (see §7).

### 4.6 The Theory Library video surface itself — top-level mode at V1?

Independent of the naming question (§4.1, §7), evaluating the Theory Library as a *concept*: Patrick proposes a separate top-level app surface for embedded YouTube/TikTok video content, with three sub-surfaces and curation logic.

The concept is well-developed and the YouTube-ToS argument for open access is real. But several factors weigh against shipping it as a top-level mode at V1:

- **It's not in our V1 scope.** Bible §9.1 lists V1 as: Exercise Section (filter/browse), Core Exercise Blueprints, Repertoire User Uploads. Adding a video-curation surface dramatically expands V1 build effort.
- **The curation logic depends on infrastructure we don't have at V1.** Patrick's Smart Feed prioritization requires backend pattern recognition on Sight Reading Trainer + Repertoire + Exercise data. That pipeline doesn't yet exist; building it for video curation alone is high-cost-low-value relative to building it for exercise/repertoire recommendation (which is V2 work).
- **The proactive suggestion system is more usefully built once than twice.** Patrick's modal triggers are well-designed but they apply equally to *non-video* nudges (suggested exercises, suggested repertoire). Building the engagement layer once and pointing it at all content types (exercises, repertoire, video-when-available) is better than building a dedicated Theory Library suggestion system that we'd later refactor.
- **Video content as an in-Project resource is a more natural agentic-era home.** When Projects exist (Doc 09), the agent surfacing a relevant video as part of a Project node is a more powerful interaction than browsing a separate library. The Theory Library as a top-level browsable surface is a 2018-2022 era design pattern; video-as-agent-resource is the 2024+ pattern.

**Recommendation:** **Defer the Theory Library video surface beyond V1.** Keep the design (Patrick's doc is preserved; the Smart Feed / Quick Theory / Deep Dives architecture is good thinking) as input for a future "Knowledge Library" or in-Project video-resource feature. **Absorb the proactive suggestion system as candidate engagement-layer behavior** (see §5.2). Don't add "Theory Library" as a top-level navigation tab in V1.

### 4.7 Gamification: named achievements, Practice Points, leaderboards

Patrick proposes specific named achievements ("Scale Master," "Rhythm Guru," "Perfect Pitch," "Theory Wizard"), Practice Points as accumulating currency, and "future leaderboards or rewards" (§2.4). Our canon has streak tracking but no designed achievement system.

This is below the level the macro PRD should commit to. **Recommendation:** Stay framework-only at the PRD level. The schema (per-atom completion, Exercise Result, mastery thresholds) supports any achievement system that gets layered on top. Patrick himself is the natural owner of the gamification design — it's exactly the kind of MVP-decomposition work Patrick volunteered for (Standup Synthesis §2). Don't bake Patrick's specific achievement names into the canon.

### 4.8 Premium tier specifics

Patrick's §3.3 specifies tiers in detail:
- **Free**: Unlimited Sight Reading + Curriculum, unlimited community theory videos, ~50% of exercises
- **Premium**: All exercises + exclusive artist content + advanced analytics + priority access

Our canon (Decision #37) explicitly defers `tier_gating` from the schema until pricing is designed.

**Recommendation:** Patrick's proposal is **input to a future pricing-design conversation, not an update to Decision #37.** No schema change. The proposal is preserved as a starting point for that conversation. Open Question 21–23 in UX Spec §9 already track this.

One specific point worth flagging: Patrick's "free tier gets ~50% of exercises" is at odds with his own framing that Free Tier should get unlimited Sight Reading and Curriculum. Why would exercises be 50%-gated when they're cheaper to ship than Sight Reading content? `[Speculative]` This may be an artifact of the doc treating exercises as scarce/curated rather than combinatorially generated. Once exercises are framework-generated (which is our model), the marginal cost of "another exercise atom" is near zero, so atom-by-atom gating is a strange place to put a paywall. The pricing conversation should pressure-test this.

---

## 5. Additive Register

Items in Patrick's doc that our canon doesn't have, where absorbing them would strengthen the design.

### 5.1 Free Play mode within exercises

Patrick's "Game Mode vs. Free Play" distinction (§2.1) is genuinely additive. **Free Play** in his framing means: practice an exercise indefinitely with no pass/fail, no advancement, just real-time feedback on accuracy/tempo. Useful for warm-up, experimentation, or extended practice.

Our canon doesn't have this. Session shape options in UX Spec §4.2 are "Quick / Standard / Deep Practice / Endless" — but "Endless" still implies an exercise-attempt with a result; it isn't quite the same thing as "this is just sustained free-form practice with stats tracked but nothing being assessed for completion."

This connects to:
- **Candidate content mode "Free Play"** (Bible §2.1.1) — which is currently a placeholder
- **Staley's "free-play interlude as part of the path"** comment (Standup Synthesis §1)
- **Andrew's Free Play mode** in the repertoire editor demo

**Recommendation:** Absorb Free Play as a session-mode extension within atoms (not a session-shape option, but a separate axis). An atom session can be invoked in:
- **Practice mode** (the current default; assessable, contributes to mastery)
- **Free Play mode** (no assessment, no completion contribution, but stats still tracked)

This is a small schema addition (`session_mode` enum on Exercise Instance / Result) and it generalizes across atoms, repertoire, and possibly sight-reading. Worth a candidate Decision (see §10, proposed Decision #43).

### 5.2 The Proactive Suggestion System as concrete engagement-layer specification

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

**Recommendation:** Absorb as **candidate engagement-layer behavior** for the engagement-layer design (Decision #19 amendment, Glossary "Engagement Layer"). The trigger conditions and modal pattern survive as-is; the *content surfaced by the modal* generalizes from "video" to "any helpful resource." Tag this in UX Spec §9 open-questions as input to the engagement layer's design.

### 5.3 Adaptive note-by-note expansion (Patrick's "Suggested Flow Gameplay Option")

In A1 (Scales) and A2 (Arpeggios), Patrick describes a specific adaptive mechanic:
> "Start with two notes moving up and down. Add one note at a time, expanding upward and downward, until two full octaves are complete. Progress adapts to performance: if the player achieves 95% accuracy or higher, a new note is added… If the player stays on the same number of notes for too long, the tempo decreases. As performance improves, the tempo increases back to the goal tempo."

This is a concrete instantiation of Optimal Grip™ (V2; Bible §9.1; Architecture Doc §5.4). Patrick names a specific algorithm: **expand sequence length when accuracy is high; reduce tempo when stuck; expand tempo back to goal when improving; gate on 95% at goal tempo before expanding length.**

**Recommendation:** Don't absorb at the V1 PRD level (it's V2 territory). But **flag this as a candidate Optimal Grip™ algorithm** in the V2 design conversation. It's the most concrete spec we have for adaptive difficulty.

### 5.4 Concrete mastery thresholds

Patrick's templates uniformly include passing criteria — and they're consistent enough to extract a default pattern:
- Most performance/sight-reading exercises: **"Four consecutive phrases at 95% accuracy and goal tempo"**
- Most ear-training quizzes: **"Four consecutive correct identifications"**
- Most theory quizzes: **"Four consecutive correct identifications"**
- D1 Note Naming (flashcard): **"Name 20 notes correctly with average response time under 3 seconds"**
- Score Reading (G3, harder content): **"Four consecutive at 90% accuracy"** (relaxed for difficulty)

These are valuable inputs to the `mastery_thresholds` field (Decision #40, atom schema). They give us defensible defaults rather than guessing.

**Recommendation:** Absorb as **default mastery threshold patterns by training method**. Specifically:
- PRF (Performance) on note-reading exercises → "4 consecutive phrases at 95% accuracy + goal tempo"
- REC (Recognition) on identification tasks → "4 consecutive correct"
- REC on flashcard-style → "20 correct in a row, avg response < 3 seconds"
- PRF on cross-domain (X-2 sight-reading) → "4 consecutive phrases at 90%"

These are starting defaults; per-atom values can override during catalog authoring. Worth a candidate Decision (see §10, proposed Decision #44).

### 5.5 Specific UI elements for Screen A

Patrick's §2.3 (Exercise Section UI and Navigation) gives concrete UI elements for the equivalent of our Screen A. Several are useful inputs to UX exploration:
- "Recommended for You" carousel at the top → maps to Hook zone
- Collapsible category sections → one possible answer to Open Question #2 (Zoom vs. flat) and #3 (toggle UI)
- Filter icon (top-right) for difficulty / category / sort by recommended/recent/A-Z
- Search bar at top
- Exercise card design (name, category icon, difficulty level, completion status, best score)

None of these is binding, but they're candidate UI elements for the Screen A design exploration.

### 5.6 Tagging vocabulary

Patrick's §1.3 (Quick Theory tagging) defines tags for video content:
- **Concept Tags**: circle of fifths, major scales, minor scales, chord inversions, syncopation, pedaling, dynamics, articulation
- **Skill Level Tags**: beginner, intermediate, advanced
- **Instrument Focus Tags**: right hand, left hand, both hands, pedal technique
- **Genre Tags**: classical, jazz, pop, blues, ragtime

The vocabulary is reasonable. While "Skill Level Tags" conflict with our 3-axis difficulty (§4.3), the **Concept**, **Instrument Focus**, and **Genre** tag categories are useful as candidate atom-metadata extensions or as engagement-layer filter axes. `[Speculative]` Especially relevant if/when video resources get attached to atoms or curriculum levels — the tag overlap creates the linkage.

**Recommendation:** Don't add to the atom schema at V1, but **flag as a candidate metadata-extension conversation** for catalog authoring. Open question for §11.

### 5.7 Patrick's H category as a "genre-tagged content scope" framing

Patrick's H (Genre-Specific Exercises) — Classical, Jazz, Blues, Pop/Rock, Latin — is rejected as a cluster (§4.2) but its *content* points to a real gap: how does a user filter for "exercises that prepare me for jazz"? Or "exercises in the style of classical period pieces"? Our canon doesn't surface this as a primary axis.

**Recommendation:** Add **genre-tag as a candidate content-scope or metadata filter** for the catalog authoring conversation. Don't surface as a primary nav axis; surface as a filter ("show me chord-progression atoms tagged Jazz"). Doesn't need a schema change at the atom level if implemented as a tag set.

---

## 6. "Ours Does Better" Register

Items where our canon has more rigor or better framing, where Patrick's content should NOT be adopted. Recorded so the team knows the choice was deliberate.

### 6.1 First-principles framework vs. enumerated catalog

The single most important "ours does better" point. Patrick's doc enumerates ~50 templates with no underlying generative principle. Our canon (Bible §3, §6; Architecture Doc §1, §7) generates exercises from substrate × modality × training method × constraint composition. The 50 templates are emergent from a much smaller set of primitives, and the framework can produce thousands of atoms our 50-template enumeration would miss.

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

Patrick's framework only really uses two methods: multiple-choice (Recognition) and direct-play (Performance). His templates occasionally hint at others (rhythm dictation as Assembly; chord spelling as Recall) but doesn't formalize the spectrum. Our 7-level training method spectrum (Verification → Recognition → Selection → Assembly → Alteration → Recall → Performance, Decision #2) provides a richer space. Patrick's missing methods are real exercise types — our canon enables them; his doesn't.

### 6.4 Performance constraints as replayability multipliers

Bible §6.3 frames performance constraints as replayability multipliers (Decision #22). Patrick's framework treats difficulty as a static property of the exercise (B/I/A) rather than a configurable space the user navigates. Our framing produces dramatically more practice mileage from the same atom catalog.

### 6.5 Cross-Section Complexity Language and GMTF integration

Architecture Doc §9 articulates the cross-section problem and connects it to MuseFlow's existing GMTF system (Decision #23). Patrick's doc has no equivalent — his cross-section integration (§3.1) is described qualitatively, not architecturally. Our framing supports the systems-level coherence Patrick gestures at but doesn't operationalize.

### 6.6 Mode architecture (Decision #41)

Patrick's "everything is a top-level sidebar tab" framing is flatter and more brittle than our content-modes / path-modes architecture. Our model handles AI-averse users explicitly (Bible §2.1.2), explains where custom-authored content lives (Decision #34, Decision #41), and provides a single architectural primitive that absorbs Projects, custom authoring, sight-reading evolution, and atom `authoring_origin` into one pattern. Patrick's framing has none of this leverage.

### 6.7 Agentic Projects vs. Master Roadmap

See §4.4. Our Projects framing is more flexible, more personalized, more demoable, and more aligned with the team's commercial pitch. Patrick's Master Roadmap (one paragraph) is a sketch; our Doc 09 is a 764-line vision artifact.

### 6.8 Theory practice as substrate, not dedicated mode

Our framework recognizes that "music theory" isn't a coherent skill domain — it's a collection of substrates (chord quality, interval recognition, key signature recognition, etc.) that already live within Frequency-Domain and Time-Domain substrates. Patrick's "Music Theory Quizzes" (Category D) is correctly treated, in our framework, as Semantic-output exercises across multiple existing substrate clusters. We don't need a separate "theory" mode.

### 6.9 Configuration model

Our distinction between **atom identity** (chosen by navigation, fixed) and **practice mode configuration** (training method, constraints, session shape — chosen on Screen B; UX Spec §4.1) is structurally cleaner than Patrick's "every template has variations" framing. Our model supports user customization while keeping the catalog enumerable; Patrick's model multiplies the catalog by every variation, making it harder to reason about.

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

### 7.4 Specific changes recommended

1. **Bible §2.1.1**: Remove "Theory" from the Candidate future content modes list. Add a footnote or §2.4 entry explaining that theory practice was evaluated as a candidate content mode and rejected — theory practice exercises live within the Exercises content mode as Semantic-output atoms across existing substrate clusters.

2. **Glossary "Content Mode"**: Update to remove Theory from the candidate list (currently reads "Theory and Free Play are candidate future content modes (status TBD)"). Free Play stays as candidate; Theory resolves.

3. **Patrick's video-library concept** gets a new name. Three candidates worth Steven's selection:
    - **"Knowledge Library"** — generic, accurate to the actual scope
    - **"Learn"** — short, more brand-y, but possibly confusable with Curriculum
    - **"Concepts"** — accurate but cold

   `[Speculative]` "Knowledge Library" is the safest.

4. **The video-library feature itself** is deferred beyond V1 (see §4.6) — but with its new name reserved, so it's clear what space it would occupy when it's revisited.

### 7.5 Resolution proposed as Decision #42

See §10 below for the candidate Decision Log entry.

---

## 8. Specific Exercise Template Absorption

Patrick has ~50 named exercise templates with passing criteria. This section evaluates each for absorption into the V1 atom catalog. The recommendation per template is one of:

- **Adopt** — Strong V1 candidate. Add to atom catalog as concrete instantiation.
- **Adopt-modified** — V1 candidate but reshape to fit our atom-identity model.
- **Defer-V2** — Pedagogically valid but better suited to V2 or later.
- **Defer-Sight-Reading** — Belongs in the Sight Reading content mode, not Exercises.
- **Pedagogically-restate** — Patrick's template aggregates across multiple atoms in our framework; pick one or more to surface as featured atoms; the others fall out from the framework.
- **Reject** — Not a strong V1 fit; framework supports it but not worth featuring.

### 8.1 Mapping table

| Patrick's ID | Title | Primary Substrate (ours) | Our Cluster | Recommendation | Notes |
|---|---|---|---|---|---|
| **A1** | Scales | F-C2 (Scale construction) | Scales | **Adopt** | Multiple atoms: by hand × by scale type × by content scope. Tempos and 95% threshold feed `mastery_thresholds`. |
| **A2** | Arpeggios | F-C6 (Chord construction)  | Chords  (or new Arpeggios cluster) | **Adopt** | Arpeggios are chord constructions; could be a sub-strand within Chords or its own cluster. Open Q. |
| **A3** | Chord Progressions | F-C12 (Progression recognition) + F-C8 (Voicing) | Chord Progressions | **Adopt** | Multiple atoms by progression × key × rhythm. Patrick's progression list is good V1 content scope. |
| **A4** | Hanon-Style Finger Exercises | X-4 (Fingering) + technique | (Cross-domain) | **Defer-V2** | Pure technique drilling; pedagogically valid but our canon defers Performance-method-only motor drilling to V2+. Decision #13 already flags fingering as needing dedicated design. |
| **A5** | Interval Reading Drills | F-M3 (Interval construction) | Intervals | **Adopt** | Visual-input + Performance-output; concrete instantiation of an existing strand. |
| **A6** | Sight Reading Challenges | X-2 (Sight reading) | (Cross-domain / Sight Reading) | **Defer-Sight-Reading** | Belongs in Sight Reading content mode, not Exercises. |
| **A7** | Articulation and Dynamics Drills | A-A2, A-M2 (Amplitude) | (Amplitude — deferred) | **Defer-V2** | Decision #3 defers amplitude exercises beyond V1. |
| **A8** | Pedaling Exercises | (Pedal substrate not in catalog) | — | **Defer-V2** | Pedal handling is its own substrate not yet in our catalog. Defer with a note. |
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
| **E1** | Finger Independence Drills | (Technique substrate) | — | **Defer-V2** | Pure technique; per Decision #13 / V2. |
| **E2** | Hand Coordination Drills | (Cross-substrate, mostly motor) | — | **Defer-V2** | Same. |
| **E3** | Thumb Crossing Exercises | (Technique substrate) | — | **Defer-V2** | Same. |
| **E4** | Hand Position Shifts | (Technique + spatial) | — | **Defer-V2** | Same. |
| **E5** | Wrist Rotation Exercises | (Technique substrate) | — | **Defer-V2** | Same. |
| **E6** | Velocity Control Exercises | A-* (Amplitude) | (Amplitude — deferred) | **Defer-V2** | Decision #3. |
| **F1** | Call and Response | Improvisation territory | — | **Defer** | Decision #13 defers improvisation. |
| **F2** | Improvisation over Chord Progressions | Improvisation territory | — | **Defer** | Same. |
| **F3** | Melody Completion | Improvisation territory | — | **Defer** | Same. |
| **F4** | Chord Voicing Exploration | F-C8 (Chord voicing) — exploratory | Chords | **Pedagogically-restate** | Free Play mode (§5.1) on a Chords atom approximates this. |
| **G1** | Clef Reading (Alto/Tenor) | F-A2 specialized | Pitches/Note Reading | **Defer-V2** | Niche; advanced users. Defer until catalog has critical mass for typical users. |
| **G2** | Transposition Exercises | F-A6 / X-* | (Cross-domain) | **Defer-V2** | Transposition is a substrate-spanning operation; needs dedicated design (Decision #13 territory). |
| **G3** | Score Reading (Multiple Staves) | X-2 specialized | (Sight Reading) | **Defer-Sight-Reading** | Belongs in Sight Reading content mode. |
| **H1** | Classical Technique Drills | Genre-tagged content scope | various | **Reject as cluster, adopt as tag** | See §5.7 — genre is a tag, not a cluster. |
| **H2** | Jazz Voicings and Comping | F-C8 + jazz content scope | Chords | **Reject as cluster, adopt as tag** | Same. |
| **H3** | Blues Patterns and Licks | Genre-tagged content scope | various | **Reject as cluster, adopt as tag** | Same. |
| **H4** | Pop/Rock Patterns | F-C12 + pop content scope | Chord Progressions | **Reject as cluster, adopt as tag** | Same. |
| **H5** | Latin Rhythms | T-C2 + Latin content scope | Rhythms | **Reject as cluster, adopt as tag** | Same. |

### 8.2 Summary by category

- **Category A (8 templates)**: 4 adopt (A1, A2, A3, A5); 4 defer (A4 V2, A6 sight-reading, A7 amplitude, A8 pedal-substrate)
- **Category B (4)**: All 4 adopt (B1, B2, B3, B4)
- **Category C (8)**: 6 adopt clean (C1, C2, C3, C5, C7, C8); 2 adopt-modified (C4, C6 split into multiple atoms)
- **Category D (7)**: 5 adopt clean (D1, D2, D3, D4, D5, D7); 2 adopt-modified (D6 splits into multiple atoms)
- **Category E (6)**: All defer V2 (technique drilling)
- **Category F (4)**: All defer (improvisation territory; one — F4 — covered by Free Play mode)
- **Category G (3)**: All defer (V2 or Sight Reading content mode)
- **Category H (5)**: All reject as clusters; their content lives as genre-tagged atoms across other clusters

**Net for V1 catalog**: ~22 templates from Patrick survive direct or modified absorption. Most map to atoms we'd generate from the framework anyway; what Patrick adds is concrete content scope examples and passing criteria.

### 8.3 Passing criteria absorption

Patrick's passing criteria are remarkably consistent across templates. Extract these as default `mastery_thresholds` patterns:

| Atom shape | Default mastery threshold |
|---|---|
| PRF method on note-reading exercises (A1, A2, A3, A5, B4, etc.) | 4 consecutive phrases at 95% accuracy + goal tempo |
| REC method on identification (C1–C5, D2–D7) | 4 consecutive correct |
| REC method on flashcards (D1) | 20 correct in a row, avg response < 3 seconds |
| PRF on cross-domain at high difficulty (G3) | 4 consecutive at 90% (relaxed) |
| PRF on rhythm-only (B1, B2) | 4 consecutive patterns at 95% accuracy |

These become the `mastery_thresholds` defaults for V1 catalog atoms; per-atom values can override during catalog authoring. Worth flagging as candidate Decision #44 (see §10).

---

## 9. Implications for V1 Scope

What does this evaluation suggest about V1 catalog scoping?

### 9.1 V1 catalog primarily comes from Categories B, C, D
The cleanest direct absorption is Categories B (Rhythm), C (Ear Training), D (Music Theory Quizzes). These are 19 of Patrick's 50 templates, and they map most directly to our atom-identity model. **Recommendation:** V1 catalog should prioritize comprehensive coverage of these three skill domains, derived from our substrate × modality × method framework, with content scope progressions that match Patrick's variation tables (his interval table, his chord table, his polyrhythm table, etc., are useful inputs).

### 9.2 Sight Reading exercises move out of the V1 Exercise Section
Patrick's A6, B4 (in some framings), and G1–G3 are sight-reading-focused exercises. Per our Bible §2.1.1, Sight Reading is anticipated to evolve into its own content mode. **Recommendation:** Don't ship sight-reading-specific atoms in the V1 Exercise content mode — they belong in the (anticipated) Sight Reading content mode. This keeps the Exercise content mode focused on isolated substrate drilling, which is its functional definition (Bible §2.2).

### 9.3 Technique drilling (Category E) is V2+
Patrick's E1–E6 are pure-Performance, motor-skill-focused drilling. Decision #13 already defers technique drilling; this evaluation confirms. **Recommendation:** V1 ships Performance method only on existing substrate atoms (where the substrate provides the cognitive content). Pure-motor drills (Hanon-style, finger independence, wrist rotation) wait for V2.

### 9.4 Genre is a filter, not a cluster
Patrick's H category should not produce a "Genre" cluster in our nav. **Recommendation:** Add genre tags to atom metadata as a candidate during catalog authoring. The user can filter "show me jazz-flavored chord progression atoms" without genre being a primary nav axis.

### 9.5 Free Play mode is a small but real V1 addition
§5.1 Free Play absorption is a small schema and UX addition (`session_mode` enum on Exercise Instance / Result). Worth doing in V1 because it pairs well with the user's natural desire to "just play around with this exercise" and it generalizes to repertoire later. Low cost, generic value.

### 9.6 Theory practice doesn't need its own surface
Patrick's Category D (Music Theory Quizzes) confirms the §7 recommendation: theory practice exercises are Semantic-output atoms across multiple existing substrate clusters. They live in Exercises. No "Theory" content mode is needed.

### 9.7 The Exercise Section landing page (Screen A) absorbs Patrick's UI elements as design candidates
Patrick's §2.3 (Recommended for You carousel, collapsible category sections, filter icon, search bar, exercise card design) is direct input to UX exploration of Screen A. These should feed the design conversation, not be committed at the PRD level.

### 9.8 Net impact on V1 build effort
Lower than it might first appear. Patrick's doc looks like ~50 features to build, but the framework collapses most of them into shared blueprints + content-scope variation. **Most of Patrick's templates reduce to 4–6 blueprints we already have planned (BP-01, BP-02, BP-05, BP-06, BP-07, BP-10) plus content variation.** The V1 build effort is dominated by content scope authoring and blueprint polish, not by adding new exercise types.

---

## 10. Decision Log Entries Proposed

Candidate Decision Log entries this evaluation produces, written for Steven's review.

### Proposed Decision #42: Theory Naming Resolution (Path c)

**Source:** A2 evaluation of Patrick's Theory Library & Exercise Section doc.

**Decision proposed:** Resolve the "Theory" naming collision via Path (c):
1. Remove "Theory" from the Bible §2.1.1 candidate content modes list. Theory practice exercises are correctly handled as Semantic-output atoms across existing substrate clusters (Frequency-Domain, Time-Domain) within the Exercises content mode.
2. Patrick's video-library concept gets renamed (working candidate: "Knowledge Library"; alternatives "Learn," "Concepts").
3. The renamed video-library feature is **deferred beyond V1** (see Decision #45 below) but its name is reserved.
4. Glossary "Content Mode" entry updates to remove Theory from the candidate list.

**Reasoning:** Patrick's "Theory Library" is misnamed in his own doc — its scope is broader than music theory and includes technique, genre, performance psychology, and song-context videos. Theory-practice exercises don't warrant a separate content mode because they decompose cleanly into Semantic-output atoms across existing substrate clusters. Adding a "Theory" content mode would either duplicate atoms or fragment clusters; both are worse than absorbing the pattern into Exercises.

**Cross-references:** Bible §2.1.1, Glossary "Content Mode," Decision #41.

---

### Proposed Decision #43: Free Play Mode as Session-Mode Extension

**Source:** A2 evaluation of Patrick's Game Mode vs. Free Play distinction (his §2.1).

**Decision proposed:** Add a `session_mode` enum to the Exercise Instance and Exercise Result schemas (Architecture Doc §8.2, §8.3) with two values:
- **`practice`** (default) — assessable, contributes to mastery thresholds, produces ExerciseResult with completion status
- **`free_play`** — non-assessable, no completion contribution, but stats (accuracy, tempo, errors) are still tracked and displayed

Free Play mode is available on any atom that supports a continuous-practice interaction (most PRF atoms; some REC/RCL atoms). Specific applicability per blueprint is open.

**Reasoning:** Free Play is a real practice need (warm-up, experimentation, indefinite practice without pass/fail pressure) that the current schema doesn't support. It's small to add. It generalizes to repertoire (where Free Play is even more natural) and to the candidate "Free Play" content mode (Bible §2.1.1) without committing to that mode now.

**Phasing:** V1. The schema addition is non-breaking; the UI surface for Free Play is a small Screen B / Screen C addition.

**Cross-references:** Bible §2.1.1 (Free Play candidate content mode), Standup Synthesis §1 (Staley's "free-play interlude as part of the path"), Architecture Doc §8.

---

### Proposed Decision #44: Default Mastery Thresholds From Patrick's Patterns

**Source:** A2 evaluation of Patrick's passing criteria across ~50 exercise templates.

**Decision proposed:** Adopt the following as **default `mastery_thresholds` per training method**, applied to atoms during catalog authoring unless per-atom overrides apply:

| Atom shape | Default threshold |
|---|---|
| PRF on note-reading exercises (most BP-05 atoms) | 4 consecutive phrases at 95% accuracy + goal tempo |
| REC on identification tasks (BP-01, BP-02 atoms) | 4 consecutive correct |
| REC on flashcard-style atoms (BP-10 candidate) | 20 correct in a row, avg response time < 3 seconds |
| PRF on cross-domain / sight-reading atoms (X-*) | 4 consecutive phrases at 90% accuracy |
| PRF on rhythm-only atoms (BP-06) | 4 consecutive patterns at 95% accuracy |

**Reasoning:** Patrick's templates are remarkably consistent; the patterns are defensible defaults rather than guessing. They satisfy the "explicit clearance criteria" requirement of Decision #40 with a starting point. Per-atom values during catalog authoring can override.

**Phasing:** V1, applied during catalog authoring (Track D in the A1→PRD plan).

**Cross-references:** Decision #40 (`mastery_thresholds` field), Architecture Doc §8.1.

---

### Proposed Decision #45: Knowledge Library / Video Resource Surface — Deferred Beyond V1

**Source:** A2 evaluation of Patrick's Theory Library proposal (his Part 1).

**Decision proposed:** The renamed video-resource surface (working name: "Knowledge Library") is **deferred beyond V1**. Patrick's design (Smart Feed / Quick Theory / Deep Dives, with curation logic and proactive suggestion modal) is preserved as design input for the deferred feature. Two specific elements are absorbed earlier:
- Patrick's **Proactive Suggestion System** (his §1.5) is absorbed as candidate engagement-layer behavior (Decision #19 amendment territory). Trigger conditions and modal pattern apply generically — content surfaced is whatever the engagement layer determines is most useful (exercises, repertoire, video, etc.), not just video.
- Patrick's **content tagging vocabulary** (concept, instrument focus, genre — his §1.3) is flagged as candidate metadata extension for catalog authoring conversations.

The Knowledge Library as a top-level content surface waits until: (a) the engagement layer ships, (b) Projects ships and the "agent surfaces a relevant video as part of a Project node" pattern is testable, and (c) compliance / licensing for embedded video is cleared.

**Reasoning:** Patrick's Theory Library is well-designed but its V1 implementation cost is high relative to its V1 value. The proactive suggestion system, which is the interaction-layer innovation in his design, is generically valuable and absorbed early; the surface itself (browsable video library) is more naturally a 2024+ pattern of "agent surfaces relevant content" than a 2018-2022 pattern of "user browses curated library."

**Cross-references:** Decision #19 amendment (engagement layer), Decision #41 (content/path mode architecture), Doc 09 (Projects as the natural home for agent-surfaced video).

---

### Proposed Decision #46: B/I/A as a Candidate Derived Label (Not a Schema Axis)

**Source:** A2 evaluation of Patrick's flat Beginner/Intermediate/Advanced difficulty axis.

**Decision proposed:** **B/I/A is not added to the atom schema as a primary difficulty field.** The 3-axis difficulty model (Decision #7: substrate complexity × training method scaffolding × constraint tightness) is the engine. If the UX exploration determines a user-facing summary label is needed (Open Question #5: "Named presets vs. individual sliders"), B/I/A or a similar label can be **derived** from atom configuration at filter time — it does not exist as a stored field.

**Reasoning:** Flat B/I/A is a brittle simplification of our richer 3-axis model. Storing it as a schema field would require ongoing maintenance to keep B/I/A in sync with the underlying axes, and the mapping isn't deterministic anyway (a Compound substrate at REC method with loose constraints is "easier" than an Atomic substrate at PRF method with tight constraints, but in different ways). Derive-on-filter is the right level of commitment.

**Phasing:** V1 — at the schema level, this is a non-decision (don't add the field). UX exploration may surface B/I/A or alternatives later.

**Cross-references:** Decision #7, UX Spec §9 Open Question #5.

---

## 11. Open Questions Surfaced

Items Patrick's doc raises that our canon hasn't addressed and should track. Each gets a brief framing for B-track (open-question triage) intake.

### 11.1 Where do videos live in MuseFlow when they exist?
[Speculative] When the deferred Knowledge Library ships (proposed Decision #45), where do videos attach? Three plausible homes: (a) standalone browsable surface (Patrick's framing); (b) attached to atoms / curriculum levels / repertoire pieces as "see also" resources; (c) surfaced by the agent inside Projects as roadmap nodes or supplementary content. **Lean: (b) + (c) over (a)** — but the design conversation for this is post-V1.

### 11.2 What does an Arpeggio cluster look like? (Or is it a sub-strand of Chords?)
Patrick's A2 (Arpeggios) raises a real classification question. Arpeggios are chord constructions performed sequentially. In our framework, are they:
- A separate cluster (parallel to Chords)?
- A sub-strand within Chords?
- Atoms with a "performance mode = arpeggiated" content-scope configuration?

Open. Worth resolving during catalog authoring.

### 11.3 Where do pedaling exercises live?
Pedal substrate isn't in our current substrate catalog (Architecture Doc §3.1). Patrick's A8 highlights this gap. Open: do we add pedal as a distinct substrate (likely under a new "Articulation/Pedal" cluster), or treat it as a constraint/configuration on existing atoms? Probably distinct substrate; worth a catalog-authoring conversation.

### 11.4 Are technique drills exercises or something else?
Patrick's E category (Technique and Coordination Drills) is pedagogically valid but doesn't fit the substrate-driven model — these are motor-skill drills with no specific substrate content. Open: are technique drills:
- A V2 expansion of the Exercise content mode with a new "Technique" cluster?
- A distinct content mode (alongside Free Play candidate)?
- A blueprint variant where the substrate is "motor pattern" and the content scope describes the pattern?

Decision #13 defers; this question survives the deferral.

### 11.5 What's the right granularity for genre tagging?
Patrick's H category implies 5 genre buckets (Classical, Jazz, Blues, Pop/Rock, Latin); his Quick Theory tagging implies more (classical, jazz, pop, blues, ragtime). Open: when genre tags are added as filter metadata, what's the canonical list, and at what granularity? (E.g., does "Latin" decompose into bossa nova / samba / salsa / tango per Patrick's H5?)

### 11.6 Improvisation and creative exercises — is there a path for these in our framework?
Patrick's F category (Creative and Improvisation) exposes a real gap. Decision #13 defers improvisation, but the gap remains. Open: as Projects mature and Free Play mode (proposed Decision #43) ships, does creative exercise design re-enter scope? Or does it stay deferred indefinitely?

### 11.7 The Cross-Section "Master Roadmap" appetite
Patrick's §3.2 reveals team appetite for **cross-section preset paths** (Curriculum that spans Sight Reading + Repertoire + Theory/Knowledge + Exercises). Our canon (Bible §2.2) anticipates Curriculum either dissolving in favor of Projects or broadening into a multi-content-mode preset path. Open: which evolution wins, and on what timeline?

### 11.8 Five-exercises-cover-90% question (from Standup Synthesis)
Staley asked Steven, "what maybe five exercises do you think could probably apply to like 90% of pieces?" — Steven didn't answer in the standup. Patrick's catalog provides a partial answer (his A1 Scales + A2 Arpeggios + A3 Chord Progressions + B1 Rhythm Tapping + C1 Interval Recognition is a reasonable five-pack). Open: is this question worth answering deliberately as part of the PRD, both as curriculum primitive and investor-demo framing?

---

## 12. Closing Assessment

Patrick's doc is competent, comprehensive, and largely consistent with itself. It is also largely superseded by the canon's evolution — the agentic Projects pivot, the content/path mode architecture (Decision #41), the atom-identity model (Decision #25), and the first-principles framework (Bible §3, §6) all postdate it and operate at a higher level of abstraction.

Net absorption from the doc:
- **~22 of 50 exercise templates** survive direct or modified absorption as concrete V1 catalog instantiations
- **5 default mastery thresholds** patterns extracted from Patrick's passing criteria
- **Free Play mode** absorbed as a session-mode extension (proposed Decision #43)
- **Proactive Suggestion System** absorbed as engagement-layer design input
- **Tagging vocabulary** (concept, genre, instrument focus) flagged as candidate metadata extension
- **Theory naming question** resolved Path (c) (proposed Decision #42)
- **Knowledge Library** (renamed Theory Library) deferred beyond V1 (proposed Decision #45)
- **6 open questions** added to the queue for B-track triage

Net rejection:
- Patrick's flat B/I/A difficulty model (proposed Decision #46)
- Patrick's "Master Roadmap" as a separate architectural primitive
- Patrick's specific named achievements / Practice Points gamification
- Patrick's premium tier specifics as schema-level commitment
- Patrick's Categories A, E, G, H as cluster names (kept as filter tags)
- Patrick's Theory Library as a V1 top-level content surface

The headline action items are the five proposed decisions (#42–#46) plus the open-question additions for B-track. Once those resolve, Patrick's doc has been fully integrated to the extent integration is warranted, and subsequent design tracks (C — taxonomy reconciliation; D — V1 atom catalog authoring; E — PRD) can proceed without further reference to it.

---

*End of A2 Integration Memo.*
