# MuseFlow Exercise System: Design Decisions Log

This document tracks every significant decision made autonomously while drafting the project documents, where the source notes were ambiguous, incomplete, or left an open loop. Each entry includes the decision made, the reasoning behind it, and notes on alternative approaches you may prefer.

---

## Decision 1: Semantic Modality — First-Class Status

**The gap:** Your notes evolved from three modalities (visual, aural, kinesthetic) to four (adding semantic), but you expressed some uncertainty about whether "semantic" was truly a separate modality or just the transformation stage surfacing as output.

**Decision made:** I treated Semantic as a fully independent, first-class modality on equal footing with Visual, Aural, and Kinesthetic — both for input and output. I added explicit language in the Architecture Doc (Section 2.2) defending this: "Reading the text 'C♯' is a categorically different perceptual act from seeing a note on a staff or hearing a pitch."

**Reasoning:** The CSV matrix already depends on this distinction to generate exercises (many exercises have Semantic input or Semantic output), and collapsing it back into Transformation would break the patching model. The four-modality system is cleaner and more generative.

**Alternative:** You could instead treat Semantic as a sub-type of Visual (since it's always text-based), which would reduce the modality matrix from 4×4 to 3×3 but lose some combinatorial resolution. If you want to go this route, the CSV and Architecture Doc would need restructuring.

---

## Decision 2: Training Method Spectrum — Consolidated and Ordered

**The gap:** Your notes mentioned two main training methods (multiple choice and tabula rasa), the CSV used "Identify - multiple choice" and "Reproduce - free generation," and scattered notes at the bottom of the CSV listed additional methods (Assembly, Verification, Find-and-select, Alteration, Continuous playback) without organizing them into a coherent spectrum.

**Decision made:** I consolidated all mentioned methods into a seven-level spectrum ordered from most-scaffolded to least-scaffolded: Verification → Recognition → Selection → Assembly → Alteration → Recall → Performance. I assigned three-letter codes (VER, REC, SEL, ASM, ALT, RCL, PRF) for use in specifications.

**Reasoning:** Your instinct that these exist on a spectrum from limited-choice to tabula-rasa was correct; the seven levels formalize that spectrum. The ordering follows the cognitive demand trajectory from "judge something presented to you" to "produce something from nothing in real time."

**Alternatives:**
- You could collapse Recall and Performance into a single "Tabula Rasa" method if the distinction between cognitive free-generation and real-time motor execution isn't important for your system.
- You could add "Continuous Playback" as an eighth method (you mentioned it in the CSV notes). I didn't include it because it seemed more like a performance constraint (tempo/endurance setting) applied to the Performance method rather than a distinct method. But if it represents a meaningfully different interaction pattern (nonstop execution without discrete prompts), it could be its own level.
- "Static playback" was mentioned in the CSV notes but left undefined. I omitted it. If you have a definition in mind, it could be added.

---

## Decision 3: Amplitude Exercises — Defined but Deferred

**The gap:** Your notes acknowledged amplitude as the third FTA dimension but noted that it was underrepresented. The CSV had no amplitude-specific exercises.

**Original decision:** I created a full AMP-### exercise family (8 exercises) covering dynamic level recognition, relative dynamic comparison, dynamic contour recognition, accent pattern recognition, articulation execution, and phrase-level dynamic shaping.

**Steven's direction (post-review):** Amplitude exercises are **deferred beyond V1**, but should remain in the schema and architecture. The AMP-### family stays defined in the taxonomy and the amplitude substrates stay in the catalog, so that engineering builds a data model that accommodates them and they can be activated later without structural changes.

**Current status:** AMP-### exercises are marked as deferred in the Exercise Taxonomy (Section 10) and the amplitude substrates carry a deferral note in the Architecture Doc (Section 3.1.3). The schema supports them; they are not in V1 build scope.

---

## Decision 4: Substrate Catalog — Created Formal ID System

**The gap:** Your notes described substrates narratively (atomic, molecular, compound) with examples but didn't assign formal identifiers or create a complete catalog.

**Decision made:** I created a formal substrate catalog with IDs using the convention `[Domain]-[Level][Number]`: F-A1 for Frequency-Atomic-1, T-M3 for Time-Molecular-3, A-C1 for Amplitude-Compound-1, X-1 for Cross-domain-1. I populated it with every substrate I could identify or infer from your notes and CSV.

**Reasoning:** A formal catalog with IDs is necessary for the exercise generation pipeline to reference substrates unambiguously. The naming convention encodes both the FTA domain and the complexity level, which makes the system self-documenting.

**Alternatives:**
- You might prefer a different naming convention (e.g., numeric-only, or grouped by pedagogical sequence rather than structural complexity).
- I may have missed substrates or included ones you'd prune. The catalog should be reviewed for completeness and accuracy by someone with deep music pedagogy expertise.

---

## Decision 5: Kinesthetic Input — Defined as Spatial/Positional

**The gap:** You were uncertain about whether kinesthetic perception should be included as a macro-perception modality or only exists as the micro-PTA loop inside the action stage. Your notes said "kinesthetic perception is a tighter, smaller PTA loop that happens *inside* of the Action stage" but the CSV then used "Kinesthetic" as a top-level input modality for exercises like "Highlighted key → Named pitch."

**Decision made:** I resolved this by defining kinesthetic input at the macro level as **spatial/positional** information (seeing a highlighted key on an onscreen keyboard, or being aware of a key position), while reserving the micro-PTA loop model for **proprioceptive/tactile** feedback during performance. This means kinesthetic works as both a macro-input modality (for keyboard-based exercises) and a micro-PTA feedback channel (during playing).

**Reasoning:** The CSV requires kinesthetic as a macro-input modality for exercises like keyboard identification. Your micro-PTA loop insight is correct for the performance context but doesn't eliminate the need for kinesthetic as an input modality in non-performance exercises.

**Alternative:** You could rename the macro-level kinesthetic input to something like "Spatial" or "Topographic" to distinguish it more clearly from the proprioceptive micro-loop. This would make the terminological distinction sharper.

---

## Decision 6: Pruning Rules — Formalized Five Rules

**The gap:** Your CSV had many rows marked with dashes and "N/A" notes, and your long-form notes discussed why certain combinations are trivial, but you didn't formalize the pruning logic into explicit rules.

**Decision made:** I extracted five pruning rules from your implicit reasoning: (1) Identity pass-through, (2) Substrate irrelevance, (3) Redundancy with simpler exercise, (4) Technical infeasibility, (5) Pedagogical emptiness. These are documented in the Architecture Doc, Section 2.4.

**Reasoning:** Explicit pruning rules are necessary for the exercise generation pipeline to be reproducible. Without them, every new substrate family would require ad hoc judgment calls about which combinations to keep.

**Alternative:** You might identify additional pruning rules or disagree with how I've categorized specific pruned exercises. The rules should be validated against the full CSV to ensure they correctly predict every dash/N/A you already marked.

---

## Decision 7: Difficulty Scaling — Three Orthogonal Axes

**The gap:** Your notes discussed difficulty in terms of the limited-choice-to-tabula-rasa spectrum and the tech specs, but didn't explicitly define how difficulty scaling works as a system.

**Decision made:** I defined difficulty as a function of three independent, orthogonal axes: (1) Substrate complexity (atomic → molecular → compound → cross-domain), (2) Training method scaffolding (verification → performance), (3) Performance constraint tightness (loose → tight). I stated these can be adjusted independently.

**Reasoning:** This three-axis model maps directly onto your existing framework components and gives Optimal Grip™ three independent "knobs" to turn. It also explains why a simple exercise can still be hard (an atomic substrate at high tempo with no scaffolding) and a complex exercise can be approachable (a compound substrate with multiple-choice scaffolding and no time pressure).

**Alternative:** You might want to add FTA dimensional scope as a fourth axis (single-dimension → dual → triple). I considered this but decided it's partially captured by substrate complexity (cross-domain substrates inherently engage multiple FTA dimensions). If you disagree, it can be split out.

---

## Decision 8: Exercise Numbering — Family-Prefix System

**The gap:** Your CSV used sequential numbers (1–44) for the matrix and no numbers for the audit section.

**Decision made:** I replaced the sequential numbering with a family-prefix system (P-001, R-001, INT-001, SC-001, CH-001, CP-001, RS-001, AMP-001, X-001) to make exercise IDs self-documenting and to allow each family to grow independently.

**Reasoning:** Sequential numbering breaks down when you add new exercise families or insert exercises into existing families. Prefixed numbering is extensible and immediately communicates what substrate family an exercise belongs to.

**Alternative:** You might prefer a different organizational scheme, such as numbering by difficulty tier, by FTA dimension, or by training method. Or you might want a flat sequential number with metadata tags instead of prefixes.

---

## Decision 9: Cross-Domain Exercises — Created Dedicated Section

**The gap:** Your notes discussed sight-reading and other multi-dimensional tasks but didn't formally categorize them. The CSV had these implicitly (the Tenuto section has keyboard and ear training exercises that span domains) but no dedicated section.

**Decision made:** I created an X-### section for cross-domain exercises that explicitly combine substrates from multiple FTA dimensions: sight-reading (F+T), expressive performance (F+T+A), fingering selection (F+T+K), chord chart reading, and improvisation.

**Reasoning:** These are among the most important exercises in the system (sight-reading is the core use case for many piano students), and they need to be explicitly represented rather than left implicit. They also demonstrate the framework's power — they're generated by composing simpler substrates, not invented ad hoc.

**Alternative:** You could instead treat cross-domain exercises as configurations of single-family exercises (e.g., sight-reading is just P-006 with sequence length > 1 and tempo constraints). This would be more parsimonious but might obscure the pedagogical significance of multi-domain integration.

---

## Decision 10: Competitive Audit — Mapped to MuseFlow IDs

**The gap:** Your CSV had a detailed list of exercises from Beato, musictheory.net/Tenuto, and 4four, but they weren't mapped back to the generated exercise catalog.

**Decision made:** I created a mapping table showing which MuseFlow exercise IDs correspond to each competitor's exercises. This demonstrates that the framework subsumes all competitor exercises while also producing exercises they don't offer.

**Reasoning:** This mapping serves two purposes: (1) it validates that the framework is complete enough to cover the competitive landscape, and (2) it identifies where MuseFlow's combinatorial approach produces exercise types that no competitor offers (construction exercises, alteration exercises, amplitude exercises, multi-modal exercises, and the full training method spectrum).

**Alternative:** The mapping is at a summary level. You may want a more granular mapping that shows exactly which configuration parameters reproduce each specific Beato or Tenuto exercise.

---

## Decision 11: Enharmonic Equivalence — Added as Substrate

**The gap:** Your notes didn't explicitly mention enharmonic equivalence (C♯ = D♭) as a substrate, but your note manipulation category ("assigning accidentals, transposing, etc.") implies it.

**Decision made:** I added F-A5 (Enharmonic Equivalence) as an atomic frequency substrate, and P-018 as the one Semantic→Semantic pitch exercise that survives pruning (because the transformation is non-trivial: given "D♭," respond "C♯").

**Reasoning:** Enharmonic equivalence is a genuine cognitive skill that needs training, and it's one of the few cases where an S→S patch is meaningful. It also underpins many compound substrates (understanding chord spellings, key relationships, etc.).

**Alternative:** You could subsume this under "Note Manipulation" (F-A6) rather than giving it its own substrate ID. If enharmonic equivalence is always trained in the context of accidentals and transposition rather than in isolation, a dedicated substrate may be unnecessary.

---

## Decision 12: Micro-PTA Training — Added Explicit Exercises

**The gap:** Your notes described the endogenous micro-PTA loop in detail but didn't specify exercises that train it.

**Decision made:** I added a section in the Architecture Doc (Section 6.2) proposing four categories of micro-PTA training exercises: kinesthetic awareness drills (play with eyes closed), aural monitoring drills (self-correct against a reference), error recovery speed drills, and motor automaticity drills (high-tempo forcing cached patterns).

**Reasoning:** Your notes explicitly state that "the micro-loop is trainable," and one of your design principles is that error detection and course correction should be trained explicitly. These exercise types follow directly from the micro-PTA architecture.

**Alternative:** These could be treated as performance constraint configurations (e.g., "eyes closed" is just a constraint applied to any Performance-method exercise) rather than distinct exercise categories. The question is whether they need their own section or just their own constraint parameters.

---

## Decision 13: Fingering and Improvisation — Left as Placeholders

**The gap:** You mentioned fingering assembly exercises and improvisation/free-play templates in the CSV notes but didn't develop them.

**Decision made:** I included X-004 (fingering selection) and X-007 (improvisation) as named exercises in the cross-domain section, flagged them as gaps in Section 13.2 of the Taxonomy, and did not attempt to fully specify them.

**Reasoning:** These are complex enough to deserve their own design process. Fingering involves biomechanical optimization that goes beyond the PTA framework's cognitive model. Improvisation is inherently open-ended and challenges the exercise template (what is the "correct" output?). Both need dedicated design attention rather than being force-fit into the current framework.

**Alternative:** You could ask me to attempt a first-pass specification for either or both. I can, but I wanted to flag them as genuinely different from the other exercise types rather than pretending the framework handles them naturally in their current state.

**Amendment (2026-05-12, per Decision #57):** Decision #57 admits a K-substrate family for motor-primary substrates (finger independence, pivoting, pedal coordination, etc.). This does NOT pull fingering and improvisation back into scope. The placeholder status of this Decision applies specifically to:
 
- **Fingering selection** (X-4) — *cognitive* substrate (choosing which finger goes on which key is an algorithmic-aesthetic-biomechanical decision). Motor execution of the selected fingering is the Kinesthetic action layer over it, but the substrate identity is cognitive. X-4 remains a placeholder pending dedicated design.
- **Improvisation** (X-7) — open-ended creative transformation. Inherently challenges the exercise template (what is the "correct" output?). Remains deferred per Decision #45 framing and this Decision.

K-substrate family admission resolves the *adjacent* question of motor-execution exercises (Hanon-style, pedal drills, technique drills generally), which now have catalog homes. The placeholder status of fingering and improvisation is unchanged by Decision #57.

---

## Decision 14: Data Model — Added Exercise Definition and Instance Schemas

**The gap:** Your notes didn't discuss data modeling at all.

**Decision made:** I added a data model summary at the end of the Architecture Doc (Section 8) with two schemas: Exercise Definition (the template) and Exercise Instance (a specific playable configuration). These are pseudo-schema, not tied to any implementation language.

**Reasoning:** Engineering will need a data model to implement the exercise system, and the distinction between "an exercise type" and "a specific exercise the user plays" needs to be explicit. The Exercise Definition captures the combinatorial matrix; the Exercise Instance captures what Optimal Grip™ generates at runtime.

**Alternative:** This may be premature — you might prefer to let engineering design the data model based on the architecture doc rather than prescribing it. If so, Section 8 can be removed or marked as "suggested, not prescriptive."

---

## Decision 15: Document Set — Chose Four Core Docs + This Log

**The gap:** You asked me to propose "whatever other canon docs you think would be important" beyond the Project Bible and Architecture Doc.

**Decision made:** I created five documents total: (1) Project Bible, (2) System Architecture, (3) Exercise Taxonomy & Catalog Spec, (4) Glossary & Terminology Canon, (5) This Design Decisions Log.

**Reasoning:** The Bible and Architecture Doc capture the *what* and *how*. The Taxonomy captures the *specific catalog*. The Glossary ensures terminological consistency as the team works from these docs. The Decisions Log ensures transparency about gap-filling.

**Documents I considered but didn't create:**
- **Implementation Roadmap**: A phased plan for which exercise families to build first. I didn't create this because it depends on product priorities, engineering capacity, and business context I don't have.
- **Assessment & Scoring Spec**: How each training method's responses are evaluated (partial credit, timing scoring, pitch tolerance, etc.). Important but deeply implementation-specific.
- **Adaptive Difficulty / Optimal Grip™ Spec**: The algorithm for adjusting the three difficulty axes based on user performance. Important but requires product/data science input beyond what's in your notes.
- **UI/UX Patterns Document**: How exercises are visually presented, how interactions work, animation and feedback patterns. Entirely in the design domain.

Any of these could be drafted as a follow-up.

---

# Decisions Added After Team Meeting Review (March 31 Standing Meeting)

The following decisions were made after reviewing the transcript from the March 31 MuseFlow standing meeting, which included extensive discussion of the exercise section design.

---

## Decision 16: Strategic Positioning — Exercises + Repertoire as Universal Pillars

**Source:** Steven's argument in the meeting that exercises and repertoire serve users at every skill level, unlike the curriculum which is level-bounded.

**Decision made:** I added a "Strategic Context" section (Section 2) to the Project Bible that frames the Exercise Section and Repertoire Section as the two universal pillars of MuseFlow, with the Curriculum as the guided pathway between them. This isn't an architecture decision — it's a product positioning statement that affects prioritization.

**Reasoning:** This framing was clearly important to Steven and was agreed to by the team. It elevates the exercise section from "supplementary feature" to "core product pillar," which affects how much design investment it deserves.

**Amendment (May 2026, post-standup integration):** The "two universal pillars" framing has been refined to a content modes vs. path modes architecture (see Decision #41). The original argument that Exercises and Repertoire are level-agnostic foundational content surfaces still holds — they are now described as the two confirmed *content modes*. The architecture additionally accommodates anticipated content modes (Sight Reading) and a candidate future content mode (Open Play — open-ended improvisation; deferred indefinitely; renamed from "Free Play" by Decision #49 Part 2), and distinguishes content modes from path modes (Curriculum, User Paths, Projects). The previously-listed "Theory" candidate was resolved by Decision #48 as a substrate family within Exercises rather than a separate content mode. The leverage argument for investing in Exercises is unaffected by the refinement.

---

## Decision 17: V1/V2/V3 Phasing on Product Features

**Source:** Staley's comment that the exercise section should start simple — "like LeetCode, where you choose what you want to practice" with a filter system — and then layer in recommendations once user data exists.

**Decision made:** I added phasing annotations (V1/V2/V3) to the Product Features table in the Project Bible. V1 = filter/browse interface with manual exercise selection. V2 = recommended exercises, Optimal Grip™ adaptive difficulty, User Skill Rating (ELO). V3 = AI-generated warmup rituals, spaced repetition, sandbox/workshop.

**Reasoning:** The meeting made clear that the team wants to avoid over-building before validation. The phasing keeps the architecture forward-looking while scoping the initial build to what's practical.

**Alternative:** The exact V1/V2/V3 boundaries are judgment calls. You might want to pull some V2 features forward (e.g., basic Optimal Grip™ in V1) or push some V1 features back (e.g., defer certain exercise blueprints). The phasing is a starting proposal, not a commitment.

**Reconfirmation (April 28, 2026 standup):** Steven reaffirmed the V1/V2/V3 phasing during the April 28 MuseFlow standing meeting: "Complexity in the exercise section may be a V2 feature, essentially because complexity is not a feature anywhere else in the app yet. So we probably need to make sure that there's the capacity for it, but if we build it into V1 it just wouldn't serve much of a function yet." Team agreed: schema must accommodate complexity, but V1 ships without it.

**Note (May 2026, post-standup integration):** Per A1 integration principle, new capabilities surfaced in the April 28 / May 5 standups (exercise generation on demand, custom authoring, teacher tools, mobile parity per atom, pricing gating, lit-keys/completion handicap, agent-prescribable atom metadata) are recorded with phasing left open — to be determined in the open-question triage and PRD-authoring phases.

---

## Decision 18: Cross-Section Complexity Language

**Source:** Staley's emphasis on a shared numeric tagging structure for complexity that works across exercises, repertoire, and curriculum. Steven agreed: "We need a common language of complexity."

**Decision made:** I added Section 9 to the Architecture Doc defining the Cross-Section Complexity Language and the Complexity Vector — a multi-dimensional descriptor that tags every exercise, curriculum level, and repertoire piece with standardized complexity axes (pitch, rhythm, harmony, key, texture, tempo, cognitive load).

**Reasoning:** Without this shared language, the three sections of the app are islands. With it, the app can make connections: "You mastered X in exercises, so try Y in repertoire." This is the "fundamental linking" Staley described.

**Alternative:** The specific axes of the Complexity Vector are a first proposal. You may want to add, remove, or redefine axes based on pedagogical judgment. The important thing is that the concept exists and the data model supports it from V1, even if the full vector isn't populated until V2.

**Reconfirmation (April 28, 2026 standup):** Patrick reaffirmed during the April 28 meeting: "All this stuff needs to kind of be tied together from the start because we need that info, but I think we've got a good idea of how to do that with this whole complexity characteristic concept." The MAGE complexity pipeline conversation between Staley and Patrick remains the working approach. Note: as of May 5, MAGE-related ownership has shifted (Staley moving toward AI/ML infrastructure, Andrew taking over repertoire), and the cross-section complexity pipeline conversation has a clearer owner unblocking Steven.

---

## Decision 19: Exercise Result Schema

**Source:** The meeting discussion about analytics and the need to define "atomic measurement units" for MuseFlow data. The team discussed minutes played, completions, and conversions as candidate units.

**Decision made:** I added an Exercise Result schema to the Architecture Doc (Section 8.3) that captures: completion status, accuracy score, response time, specific errors, training method used, constraint values, complexity vector, and session context.

**Reasoning:** This is the atomic unit of exercise analytics. Every dashboard metric, ELO computation, and adaptive difficulty decision ultimately derives from Exercise Results. Defining this schema now means engineering builds the right data collection from day one.

**Amendment (May 2026, post-standup integration):** Consumers of the Exercise Result include future re-engagement logic (Andrew's proactive nudging system, surfaced in the April 28 standup). The Result should be persisted in a queryable location that downstream systems can read. No new schema field is added at this time — Andrew's logic can derive engagement signals (atoms cleared, time-since-last-practice, completion state) from the existing fields. If a future implementation reveals a real gap, this can be revisited.

---

## Decision 20: Contextual Transfer Design Principle

**Source:** Steven's extended analogy about learning Chinese — training vocabulary flashcards in isolation, then finding those same words unrecognizable when embedded in real conversation. He specifically identified this transfer gap as a design problem the exercise section should solve.

**Decision made:** I added "Contextual Transfer" as Design Principle 8.8 in the Project Bible, and added "Contextual embedding exercises" to the coverage gaps section of the Exercise Taxonomy.

**Reasoning:** This principle captures a specific pedagogical problem: isolated drilling doesn't automatically transfer to contextual performance. The exercise system should explicitly bridge this gap by offering exercises where trained substrates appear embedded in larger musical structures, not just in isolation.

---

## Decision 21: Exercise Blueprints Specification — New Document

**Source:** Steven's direction that the documents should serve as handoff artifacts for both UI/UX design and engineering, and that exercises should be organized into "blueprints" or "categories" where each blueprint has common design mechanics.

**Decision made:** I created a new document — the Exercise Blueprints Specification — that defines 13 reusable UI/interaction templates. Each blueprint specifies the screen layout, interaction pattern, prompt presentation, response mechanism, feedback model, applicable PTA/FTA classifications, compatible training methods, performance constraints, and which exercises from the taxonomy map to it.

**Reasoning:** The taxonomy tells you *what* exercises exist. The blueprints tell you *how they look and work on screen*. This is the layer that designers and engineers actually build from. Steven was explicit that the documents need to serve both audiences.

---

## Decision 22: Replayability as Product Concept

**Source:** Steven's meeting discussion about stress-testing the same exercise in different ways — speed, accuracy, memory chain length, recall delay — and his statement that "it's fundamentally the same exercise, it's just increasing the difficulty in certain ways."

**Decision made:** I added Section 6.3 ("Replayability Through Constraint Variation") to the Project Bible, framing performance constraints not just as difficulty levers but as replayability multipliers that let a compact exercise catalog produce a vast number of distinct practice experiences.

**Reasoning:** This is a product-level insight, not just a technical one. It means the exercise section can feel enormous to users even with a modest number of underlying exercise definitions, which is important for both user value perception and development efficiency.

---

# Decisions Added During Extended Design Session

The following decisions were made during a continued conversation refining the exercise system UX, navigation model, and exercise identity framework.

---

## Decision 23: GMTF Integration — Use Existing System, Don't Reinvent

**Source:** Steven's direction that the GMTF complexity scoring system already exists in the MuseFlow codebase.

**Decision made:** Replaced the proposed "Complexity Vector" concept in the Architecture Doc with a reference to the existing GMTF system. The exercise framework should integrate with GMTF rather than defining a new complexity vocabulary.

**Action required:** The mapping between exercise atoms and GMTF scores needs to be defined. This is a V2 task.

---

## Decision 24: Micro-PTA Loop Exercises — Deferred Beyond V1

**Source:** Steven's assessment that dedicated micro-PTA exercises (play with eyes closed, error recovery drills, etc.) may be overly complicated for V1.

**Decision made:** Added deferral notes to the micro-PTA section of the Architecture Doc. The theoretical framework remains documented but dedicated micro-PTA exercises are not in V1 scope. The architecture supports them for future activation.

**Note (2026-05-12, Track B Phase 3):** Triage entry T-022 (open-question register UX Spec §9 #17) formally retired by this Decision. The original "V1 or deferred" question is fully answered here.

---

## Decision 25: Core Unit Refinement → Exercise Atom Identity

**Source:** Extended analysis of the "identify major and minor triads by ear" example, which revealed that the original "core unit" concept (substrate + modality + content scope) was insufficiently granular. Output modality, target variables, and pitch reference mode all change what the exercise fundamentally IS.

**Decision made:** Defined the Exercise Atom as the fundamental unit, identified by six dimensions: substrate family, input modality, output modality, target variables, pitch reference mode, and content scope. Training methods and performance constraints are practice modes applied to atoms, not part of their identity. Created the atom/molecule/strand/cluster hierarchy.

**Reasoning:** The triads example showed that "hear a triad → name the quality" and "hear a triad → notate it" and "hear a triad → play it" are fundamentally different exercises, not configurations of the same exercise. Similarly, "name the quality" (relative pitch) and "name the exact chord" (perfect pitch) are different exercises. The atom definition captures these distinctions.

**Open question:** This produces a very large combinatorial space (potentially 500–2,000 atoms). The framework for navigating this space (atom/molecule/strand/cluster hierarchy with progressive zoom) is proposed but not yet validated through design exploration.

---

## Decision 26: Exercise Section Navigation — Three-Screen Flow

**Source:** Iterative conversation about navigation models. Steven rejected pure library (too utilitarian), rejected deep folder-structure drill-down (too many back-and-forth navigations), and wanted all exercises accessible from a single page while still supporting engagement and progressive depth.

**Decision made:** Proposed a three-screen flow: Screen A (Exercise Home with hook/mirror/library zones), Screen B (Exercise Detail/Config), Screen C (Exercise + Results). The Library zone supports progressive zoom through the hierarchy but doesn't require it — users can filter and browse flat if they prefer.

**Status:** Proposed, not finalized. The exact visual metaphor and interaction design need exploration.

---

## Decision 27: User Configuration Model

**Source:** Steven's preference for some degree of exercise customization in V1, but uncertainty about how much.

**Decision made:** Proposed that atom identity (substrate, modalities, target variables, pitch reference, content scope) is chosen by navigation (not configurable), while training method, performance constraints, and session shape are configurable on Screen B with sensible defaults. Users can accept defaults and start immediately or adjust settings.

**Status:** Directionally agreed, but details (which specific constraints are exposed, preset difficulty levels vs. individual sliders) are open questions.

---

## Decision 28: Perfect Pitch Handling

**Source:** Steven's concern that users without perfect pitch shouldn't see perpetual incomplete progress.

**Decision made:** Atoms with absolute pitch reference mode are tagged as optional/bonus and hidden by default. They are excluded from completion calculations. Users can opt into perfect pitch mode in their profile to reveal these atoms.

**Reasoning:** The vast majority of piano students don't have perfect pitch. Making perfect-pitch atoms required for "completion" would be frustrating and pedagogically inappropriate. Treating them as bonus challenges respects both populations.

---

## Decision 29: Agentic Vision — Documented as Future Architecture

**Source:** Team standup discussion about a future agentic MuseFlow interface where users describe goals and the system builds custom roadmaps.

**Decision made:** Added Section 8 to the UX & Navigation Spec documenting this vision and its architectural implications, without attempting to design it now. Noted that the exercise atom framework supports this vision (atoms are the right granularity for agent prescription, the hierarchy provides navigable structure, the progress model provides assessment data).

**Architectural implication noted:** The data model should support creation of custom atoms (not just selection from a fixed catalog) to enable agent-generated exercises for specialized goals.

---

## Decision 30: Distractor Logic — Derived from Atom Identity

**Source:** Steven's detailed breakdown of how multiple-choice options for triad exercises vary depending on what's being tested (quality vs. root vs. inversion).

**Decision made:** Established the principle that distractor generation rules are deterministic functions of the atom's target variables and pitch reference mode. Distractors hold constant everything that is NOT a target variable and vary what IS. This logic is documented in the UX & Navigation Spec, Section 6.2.

**Reasoning:** This removes distractor design from the manual authoring burden and makes it systematic. It also ensures that the multiple-choice options actually test what the atom is designed to test, rather than accidentally testing something else.

---

## Decision 31: Team Member Attribution Correction

**Source:** Steven's correction that contributions attributed to "Tucker" in the transcript analysis were actually from Staley. "AC" was a mis-transcription of "Asif" by the transcript tool.

**Decision made:** Corrected attribution throughout. Staley's contributions include: data model primacy principle, LeetCode-style V1 navigation, cross-section complexity language, ELO as user-facing metric. Asif is the primary engineering collaborator for exercise section implementation.

**Amendment (May 2026):** Steven clarified that **Austin Clifton and Staley are different people**. Austin Clifton was a separate engineer who briefly worked with the team early on and is no longer with the company; Staley is the CTO. Earlier canon (including the original text of this decision and several other documents) incorrectly used "Staley (Austin Clifton)" as a parenthetical, conflating the two. The parenthetical has been removed from current canon. The underlying decision — that Staley is the correct attribution for contributions previously misattributed to "Tucker," and that "AC" was a mis-transcription of "Asif" — remains correct.

---

## Decision 32: Agentic "Projects" Vision Elevated to Near-Term R&D Track

**Source:** April 28 and May 5, 2026 standups. Staley volunteered to drive an agentic learning system; the team agreed to adopt the "Projects" naming pattern from Claude/ChatGPT; Patrick is targeting it as the wedge for the $1.5M raise; Steven contributed the exercise-generation-on-demand framing in the May 5 brainstorm. An "Emergent Curriculum" working session was scheduled for the Thursday following May 5.

**Decision made:** The agentic vision (originally logged in Decision #29 as "documented as future architecture") is elevated to an **active R&D track** with investor-demo target status. Documents are updated to reflect this:
- UX Spec §8 reframed from "Future Vision" to "Agentic Exercise System (Active R&D Track)"
- Project Bible §2 reframed to position Projects as one of three path modes (see Decision #41)
- A new freestanding document (Doc 09 — Agentic MuseFlow Vision) is being drafted as part of A1 to capture the vision in detail

**Reasoning:** The original framing ("future, not in scope") is no longer accurate to the team's posture. Treating the agentic system as a future consideration would understate its strategic importance and might lead to design choices in V1 that don't anticipate the Projects layer.

**Phasing:** TBD. The exercise-section's V1/V2/V3 scope relative to agentic capabilities is not committed in this entry and is a topic for the open-question triage and PRD-authoring phases.

**Cross-references:** Decisions #29 (extended, not superseded), #33 (generation on demand), #34 (custom authoring), #41 (content/path mode architecture).

---

## Decision 33: Exercise Generation on Demand as First-Class Capability

**Source:** Steven's contribution to the May 5, 2026 "Emergent Curriculum" brainstorm: exercises should be generatable on command by user, teacher, or MuseFlow itself, because exercises don't carry the stylistic-fidelity constraints that repertoire and sight-reading material do — they're "variations on scales and chords and stuff."

**Decision made:** Exercise generation on demand is recognized as a first-class capability of the exercise system, distinct from selection from a fixed catalog. Three triggers are anticipated:
- **User-triggered**: the user requests a custom exercise targeting specific skills or constraints
- **Teacher-triggered**: a teacher generates an exercise to assign to a student
- **Agent-triggered**: the MuseFlow AI generates an exercise as part of a Project roadmap

Generated exercises are first-class citizens of the Exercise content mode, tagged with `authoring_origin` (see Decision #40), and accessible via Browse-by-origin filtering (see Decision #41).

**Reasoning:** The exercise atom framework is inherently combinatorial — atoms are defined by patches across modalities, substrates, target variables, and content scope. This makes generation on demand a natural extension of the existing architecture, not a new feature requiring a parallel stack. Treating generation as first-class also better serves the agentic system, which depends on the ability to create custom content for goal-specific gaps.

**Phasing:** TBD. Whether generation on demand ships in V1, V2, or later — and through which mechanism (MAGE, future LLM, hybrid) — is open and will be addressed in subsequent design phases.

**Cross-references:** Decisions #32 (Agentic Projects), #34 (custom authoring), #39 (MAGE long-term role), #40 (atom schema additions).

---

## Decision 34: Custom Authoring Path via Andrew's Repertoire Builder

**Source:** Andrew's May 5, 2026 demo of an in-app music editor (click-to-add notes, drag-to-reposition, save to user library, notation editing, MIDI playback, three play modes). Patrick's framing during the demo: "I think this would be to give to instructors as well. They can write their own exercises, upload them, then share with their students, all within the MuseFlow ecosystem."

**Decision made:** Andrew's Repertoire Builder is the natural authoring surface for custom exercises (and custom repertoire) authored by users and teachers. The data flow is: editor → exercise atom (or repertoire entity) → mode catalog (with `authoring_origin` set to user or teacher) → assignable / shareable / browsable.

**Reasoning:** Building a separate exercise-authoring tool would duplicate functionality the Repertoire Builder already provides. Treating the editor as a multi-purpose authoring surface unifies the user-content-creation story across modes and reduces engineering load.

**Phasing:** TBD. Specific UX flows for exercise authoring (vs. repertoire authoring) within the editor are not yet designed. Teacher-authored exercise assignment is part of the elevated teacher-tools scope (see Decision #35).

**Cross-references:** Decisions #33 (generation on demand), #35 (teacher tools), #40 (atom schema — `authoring_origin`), #41 (Content Mode and Path Mode Architecture), #61 (Universal Affordance Symmetry); Doc 09 §3.3 (Four Authorship Origins); Doc 04 Glossary "Repertoire Builder" (naming history).

**Amendment (2026-05-12, per Doc 14 §2.5):** The canonical name for the surface this Decision describes is **Repertoire Builder**, not "Repertoire Editor" (the original title). The team settled on Repertoire Builder during the May 12 standup after Patrick's loose usage of "composer dashboard" triggered a naming check; Steven clarified that "composer dashboard" is reserved for a different (currently unspecified) surface. The functional scope of this Decision is unchanged by the rename. All in-canon references to "Repertoire Editor" have been updated to "Repertoire Builder" alongside this amendment; the Glossary entry preserves the naming history.

**Amendment (2026-05-12, per Doc 14 §2.2 + §1.6):** The `authoring_origin` field's applicability is hereby reaffirmed as canonical at **every authored hierarchy level**, not only at the atom level — atoms, blueprints, paths, roadmaps, and Projects all carry an `authoring_origin` value drawn from the four-origin vocabulary in Doc 09 §3.3 (MuseFlow preset / user-generated / AI-generated / community-generated). This was already articulated in Doc 09 §3.3 ("the same vocabulary applies across content and paths, content modes and path modes") but had not been elevated into the Decision Log. The May 12 standup explicitly extended the principle to roadmaps in conversation (Steven: roadmaps come in *preset / user-generated / AI-generated / community-sourced* flavors, parallel to atoms); this amendment makes that elevation canonical. Practical consequence: any V1 surfacing model for authoring-origin discrimination (filters, badges, etc.) must operate uniformly across hierarchy levels, not only at the atom/content-mode level. See Doc 12 T-099 (V1 surfacing model — open).

---

## Decision 35: Teacher Tools and Assignment Flows Elevated to Active Design Scope

**Source:** Recurring themes across both standups: Earnest is a paying instructor with three students using MuseFlow; Patrick wants the instructor portal shipped so it can be handed off to him. The Arizona-teacher quote Patrick periodically cites: she needs (1) student-data visibility, (2) audio recognition — both now within sight. The two-sided marketplace is the long-term commercial vision (3–5 year deck).

**Decision made:** Teacher tools and assignment flows are elevated from "open future item" (the prior status) to an active design scope. Specific capabilities anticipated:
- Teachers can view student progress per atom / molecule / strand / cluster
- Teachers can assign specific atoms, molecules, strands, or paths to specific students
- Teachers can author custom exercises (via the Repertoire Builder; see Decision #34) and assign them to students

**Reasoning:** Earnest is paying. The instructor portal has commercial pressure on it. The exercise section's design needs to anticipate these capabilities so the data model and UX can accommodate teacher-as-viewer-of-student-data and assignment-as-first-class-object without later restructuring.

**Phasing:** TBD. Whether teacher tools ship in V1 or V2 is open. The instructor portal is being driven by Patrick and Staley separately; the exercise section's contribution is the schema and capability hooks, not the portal itself.

**Cross-references:** Decision #34 (custom authoring), Decision #40 (atom schema — `authoring_origin`).

---

## Decision 36: Mobile Parity Specified Per Atom and Per Blueprint

**Source:** Patrick's May 5, 2026 statement: "I fully accepted the fact that mobile is going to be a limited experience. We'll just need to present that to the user somehow — a little note up top, hey, full disclosure, mobile doesn't have all the features." Andrew's PRD note that exercise definitions need to work across mobile, iPad, and laptop, including UX language ("tap" vs. "click"). Asif is doing mobile work currently.

**Decision made:** Every atom and every blueprint carries a `mobile_supported` field with three values: `full`, `partial`, `none` (see Decision #40). The PRD and downstream documentation must mark which atoms and blueprints are mobile-supported. Atoms that require physical-keyboard input (e.g., Performance training method on a piano) will typically be marked `none` or `partial` for mobile.

**Reasoning:** Mobile parity is an explicit constraint, not an afterthought. Marking it on the atom/blueprint level allows the UI to gate and filter appropriately, the user to understand what's available on their device, and engineering to scope mobile work clearly.

**Phasing:** TBD. Specific values for each atom / blueprint are not committed in this entry — they will be filled in during catalog authoring (Track D in the A1→PRD plan).

**Cross-references:** Decision #40 (atom schema — `mobile_supported`).

---

## Decision 37: Pricing/Tier Gating Not Yet Encoded in Schema

**Source:** Pricing-tier discussion across both standups (free unlimited / mid / premium at $15.99 floated; the custom-authoring Repertoire Builder and transposition floated as premium-tier candidates). No tier structure is committed.

**Decision made:** Tier gating is **not currently encoded as a field on the atom schema**. A `tier_gating` field was considered (see Q&A history during A1) and dropped on the rationale that adding speculative fields creates noise and falsely signals that pricing is a near-term design surface. When pricing is designed, adding the field is an additive non-breaking schema change.

**Reasoning:** Schema additions for capabilities not yet being designed are a form of overdesign. The schema should reflect what the system needs to do today, with provisions for tomorrow only when those provisions are cheaply-reversible *and* there is a strong reason to encode them now. Pricing meets the cheap-to-add-later criterion but fails the strong-reason-now criterion.

**Phasing:** TBD. When pricing is designed, the `tier_gating` field (or equivalent) will be added to atoms, blueprints, and other gateable entities as needed.

**Cross-references:** Decision #40 (atom schema — what was added and what was deliberately deferred).

---

## Decision 38: Lit-Keys Mode and Completion Handicap as Cross-Atom Configurable Assistance

**Source:** Patrick's April 28, 2026 floated idea of a piano view with keys lit up to show what to press. Team consensus: useful as an option, but using the assist mode flags or asterisks the user's 100% completion. Steven's framing: "You don't get full credit for really knocking this song out of the park if a possibility exists that you would be cheating the whole time."

**Decision made:** Lit-keys assistance is a configurable assistance level applicable across many atoms (and across repertoire), not a new blueprint or atom type. The completion-handicap concept — using assistance flags the user's session as assisted, which affects completion display or scoring — applies identically. Both are atom-level (and blueprint-level) configuration options that engage when applicable.

**Reasoning:** Treating lit-keys as a new blueprint would proliferate blueprints unnecessarily; treating it as configuration generalizes the concept (other forms of assistance — slow-motion, pre-highlighted notation, etc. — fit the same pattern). The completion-handicap rule preserves the integrity of completion tracking without preventing users from benefiting from the assist when they want it.

**Phasing:** TBD. Specific atoms and blueprints that support lit-keys assistance are not enumerated in this entry — they will be tagged during catalog authoring.

**Cross-references:** Future blueprint specifications will need a "supported_assistance_levels" property; this is a candidate for a future schema addition once the set of assistance modes stabilizes.

---

## Decision 39: MAGE's Long-Term Role — Logged as Open Architectural Question

**Source:** May 5, 2026 standup. Steven's working position: "If a more AI-based approach were to replace MAGE, it would integrate MAGE into it. It would be an upgraded AI-enhanced version of MAGE to me. It wouldn't just be a separate thing that we build." Staley's framing: MAGE exists to generate training data for an eventual fine-tuned LLM; once enough data exists, the LLM replaces MAGE. The two framings were not reconciled in the standup.

**Decision made:** MAGE's long-term role is logged as an **open architectural question**. Steven's working position — that AI augments / is built on top of MAGE rather than replacing it — is recorded as the current working assumption, with the question genuinely unresolved. The architecture is described in a way that does not silently bake in either framing.

**Reasoning:** Forcing a resolution at this stage is premature. The Emergent Curriculum brainstorm is the appropriate venue for this conversation, and the question affects roadmap and cost modeling more than it affects the exercise section's near-term schema. Logging it openly prevents documentation drift toward an unagreed-upon assumption.

**Phasing:** N/A — open question, to be resolved in a future architectural conversation.

**Note for Glossary:** MAGE = Music Algorithmic Generation Engine. Distinct from Opusmodus (one word), which is the notation/printing engine that does only what it is told. The MAGE / Opusmodus distinction has been confused in two recent standups; the Glossary entries are reinforced.

**Amendment (May 2026, post-May-7-brainstorm):** Per Decision #44, the team's working position is amended toward the **augmentation framing**: MAGE persists as a permanent algorithmic generation engine, with the AI adjusting MAGE's music-XML output for musicality, stylistic fitness, and goal-specific shaping. The May 7, 2026 Emergent Curriculum brainstorm produced directional alignment across Steven, Patrick, and Staley (Patrick's articulation of the AI-adjusts-MAGE-output mechanism, Steven's concurrence, Staley's non-pushback). The training-data-then-replacement framing (Staley's earlier articulation) is no longer the team's working framing. The question remains formally open pending Staley's explicit retirement of that framing; full closure of the open status is deferred to that confirmation. See Decision #44.

**Amendment (2026-05-12, per Decision #53):** **Formally closed.** The open status retained per the prior amendment (pending Staley's explicit retirement of the training-data-then-replacement framing) is retired. Decision #53 confirms augmentation framing as canonical without further procedural blocker; Staley remains free to articulate framing-retirement independently. See Decision #53.

---

## Decision 40: Exercise Atom Schema — Five Field Additions

**Source:** Standup-derived capabilities (agent-prescribability, custom authoring origins, generation on demand, mobile parity) require schema metadata that the original atom identity model (Doc 07 §2.1) did not include. Eight fields were considered during A1; three were dropped on reflection.

**Decision made:** Five fields are added to the Exercise Atom Schema in Architecture Doc §8.1:

| Field | Purpose |
|---|---|
| `prerequisite_atoms` | List of atom_ids that should be cleared before this one. Empty list = no prerequisites. Required for agent path-building. |
| `mastery_thresholds` | Map from training_method to clearance criteria (e.g., "REC: 90% accuracy across 20 prompts"). Makes implicit clearance criteria explicit. |
| `mobile_supported` | Enum: `full` / `partial` / `none`. Per Decision #36. |
| `authoring_origin` | Enum: `system` / `teacher` / `user` / `agent`. Default `system`. Generalizes to all content entities (repertoire, sight-reading levels) when those modes formalize. |
| `generation_mode` | Enum: `fixed_content` / `parameterized_content` / `on_demand_content`. Distinguishes how content is produced per session within an atom — separate from how the atom itself came to exist (`authoring_origin`). |

**Three fields considered and dropped:**
- `expected_time_to_clear` — dropped because we have no data to populate it; would seed bad estimates.
- `agent_prescribable` — dropped because default-true is the rule; per-atom booleans that are always true are noise.
- `tier_gating` — dropped per Decision #37.

**Reasoning:** Each retained field has a current real-world reason to exist (not speculative), defensible defaults that don't presume design choices we haven't made, and enables a capability discussed in the standups. Dropped fields fail one or more of these criteria.

**Phasing:** TBD. Specific atoms' values for each field are populated during catalog authoring (Track D). The schema fields exist from V1 onward; population may be partial in V1 with completion in subsequent phases.

**Cross-references:** Decisions #32–#36 (capabilities that motivate the fields), #37 (tier_gating dropped), #41 (Content/Path Mode Architecture — `authoring_origin` generalizes there).

---

## Decision 41: Content Mode and Path Mode Architecture

**Source:** April 28 / May 5 standups, plus the A1 framing conversation that synthesized standup outputs into a unified architectural pattern. Steven's clarifications during A1 (especially around AI-averse user respect, custom content residing in content modes regardless of authorship, and User Paths as a third path mode) shaped the final framing.

**Decision made:** The Project Bible §2 is reframed from "two universal pillars" (Decision #16) to a content modes / path modes architecture with the following structure:

**Content modes** are surfaces where musical material lives and is engaged with directly:
- Confirmed: **Exercises** (targeted skill drilling), **Repertoire** (free-choice performance)
- Anticipated: **Sight Reading** (currently within Curriculum; envisioned as a custom-level generator)
- Candidate: **Open Play** (open-ended improvisation without notation guidance; deferred indefinitely; renamed from "Free Play" by Decision #49 Part 2). Note: "Theory" was previously listed here as a candidate pending A2 evaluation; that evaluation resolved it as a substrate family within Exercises rather than a separate content mode — see Decision #48.

**Path modes** are structured progressions through content modes:
- **Curriculum** (preset, MuseFlow-authored, used by many)
- **User Paths** (custom, user-authored, used by one — naming TBD; alternatives include "Playlists" or "Plans")
- **Projects** (AI-mediated, goal-driven, generated per-user)

Path modes are sibling experiences in the UI. AI-averse users can engage fully with the product without invoking the AI surface.

**The three-flow pattern** applies within every content mode:
- **Browse** — explore available content, filterable by authorship origin
- **Generate** — create custom content using the mode's generation tool
- **Project** — declare a goal and work with MuseFlow's AI guidance, drawing from this content mode and others

**Four authorship origins** classify content (and paths) within each mode:
- MuseFlow presets
- User-generated
- AI-generated (created in service of a Project goal or direct user command)
- Community-generated (future)

Browse-by-authorship-origin is a primary filter axis in both content-mode and path-mode browsing experiences.

**Architectural principle:** Content lives in content modes; paths reference content; authorship is a property of content and of paths, not of mode.

**Cross-cutting engagement layer:** A separate engagement/nudging layer reads from Project goals, free-exploration patterns, and aggregate skill data, surfacing re-engagement signals. Orthogonal to the three flows. Specific design TBD.

**Reasoning:** The unified pattern was discovered during A1 to collapse five previously-separate items (exercise generation on demand, custom authoring, sight-reading evolution, agentic Projects, atom `authoring_origin`) into a single architectural primitive that applies across modes. This both clarifies the framing and makes the architecture genuinely extensible — new content modes inherit the pattern automatically.

**Phasing:** TBD. Specific UX implementations of the three flows, the dashboard surfaces, the User Paths feature, and the engagement layer are open design questions. The architectural pattern is committed; the implementations are not.

**Cross-references:** Decisions #16 (amended), #29 (Agentic Vision — superseded in framing by this entry, though the underlying intent persists), #32 (Agentic Projects elevated), #33 (generation on demand), #34 (custom authoring), #40 (`authoring_origin` field on atom schema).

**Note (2026-05-12, per Decision #56):** Decision #56 (Novelty-Automaticity Spectrum) recontextualizes the three confirmed and anticipated content modes (Exercises, Repertoire, Sight Reading) as **manifestations of the Spectrum at distinct points**: Sight Reading at the Novelty pole, Exercises at the Automaticity pole, Repertoire at the synthesis midpoint with an artistic-intent overlay. The mode architecture defined in this Decision is unchanged; the Spectrum framing explains *why* this particular three-mode structure is pedagogically principled rather than arbitrary. The architectural principle ("content lives in content modes; paths reference content; authorship is a property of content and of paths, not of mode") is reinforced by the Spectrum's Shapeless Content corollary: at the level of raw musical material, all three modes generate or reference the same underlying content, differing only in scheduling and bounding policy.

---
## Decision 42: The Auto-Looping / Perfect-Practice Tree Algorithm

**Source:** May 7, 2026 Emergent Curriculum brainstorm. Patrick described an algorithm he claims to have already designed in his PRD: read the green-note JSON history, identify the first section with two-or-three-notes-in-a-row errors, dynamically determine loop boundaries (one or two measures before/after the errored section), perfect that section, auto-progress to the next errored section, and combine perfected sections in a tree structure (small section → small section → combined → next pair → combined → larger combination, recursively). Staley's read: largely algorithmic, with the LLM as "voice/text sugar on top." Steven concurred but flagged that AI judgment may need to override the algorithm for "break the rules" cases (e.g., the actual issue is the previous measure, not the errored one).

**Decision made:** The auto-looping / perfect-practice tree algorithm is recognized as a **first-class algorithmic capability for repertoire practice**. Specifically:
- It is the algorithmic execution layer that connects performance data (green-note JSON history) to looping decisions in repertoire
- It is **one capability within the broader agent-controllable repertoire practice control surface** (see Decision #46) — not a standalone architectural primitive
- It is the load-bearing capability for the engineering-critical step 4 of the integrated investor demo (Doc 10 §8.1)
- It is invokable by the agentic system as part of Project execution (a Project's roadmap node for "practice this piece" can prescribe auto-looping as the practice mode)

**Scope constraints (what auto-looping is not):**
- Optimal Grip is about session-level adaptive difficulty (chevron count, tempo targets); auto-looping is distinct from it. Both are forms of adaptive difficulty, but they operate at different levels.
- Game Mode is sight-reading-specific pass-condition mechanics, distinct from repertoire practice orchestration.
- The algorithm operates on a piece's note-history JSON (a repertoire artifact). Exercises would have analogous mechanics, not the same algorithm ported.

**Reasoning:** The algorithm exists. Patrick has implemented it (or specified it in detail) in his existing PRD. It is the strongest single demo capability the team has. Recognizing it explicitly in canon prevents it from sitting implicit in a PRD the rest of the team hasn't read, and it earns a canonical reference for downstream work.

**Phasing:** TBD. The algorithm itself is implementable now (per Patrick); the AI-judgment override and voice-feedback layer are speculative-near-term. V1 / demo / V2+ scoping is open.

**Cross-references:** Decision #46 (broader control surface). Patrick's PRD as the implementation source. Doc 09 §6 (AI Surface) — voice feedback as the language layer atop the algorithm.

---

## Decision 43: Performance Constraints Generalize Across Content Modes

**Source:** May 7, 2026 brainstorm. Steven's articulation that the exercise section's performance-constraint vocabulary (time-based pass conditions, accuracy thresholds, memory-chain length) ports directly to sight reading and possibly repertoire. Staley: "the exercise section can also maybe be a version of this game mode thing." Bible §6.3 currently treats performance constraints as exercise-internal.

**Decision made:** Performance constraints are promoted from exercise-section-internal to a **cross-content-mode primitive**. Any "completable" engagement with content (exercise atom session, sight-reading level attempt, repertoire practice session) carries performance constraints that determine pass conditions and shape the practice experience.

The schema impact:
- Exercise atoms already carry performance constraints (per Architecture Doc §5)
- Sight-reading levels gain a performance-constraints schema entry (parallel to atom configuration)
- Repertoire practice sessions may carry performance constraints (e.g., "play this passage at 80% accuracy or higher for 5 minutes to clear")

**Reasoning:** The exercise framework's most useful product-level concept (replayability through constraint variation) generalizes with no architectural cost. Treating performance constraints as a cross-mode primitive avoids reinventing similar mechanics per mode and provides the agentic system a unified vocabulary for prescribing practice intensity.

**Phasing:** TBD. Specific application to sight reading and repertoire is V2+. The conceptual promotion is V1; per-mode implementation phases independently.

**Cross-references:** Decision #22 (replayability), Bible §6.3, Architecture Doc §5, Decision #41 (the cross-mode pattern this extends), Decision #46 (performance constraints are part of the per-content-mode control surface).

---

## Decision 44: MAGE Long-Term Role — Augmentation Direction Confirmed

**Source:** May 7, 2026 brainstorm. Patrick: "the AI would probably be adjusting the mage output to make it more musical or to fit the like genre that they're trying to learn or to specifically work specific techniques that are in the piece of repertoire that they want to learn... There's like many reasons why the AI would adjust the music XML outputed by Mage." Steven concurred. Staley did not push back; his earlier articulations during the call ("I love mage. Yeah") and his agreement with Patrick's framing position him in alignment.

**Decision made:** Decision #39 (MAGE's long-term role logged as open) is **amended toward the augmentation framing**. The team's working position, with directional alignment across all three brainstorm participants, is:
- MAGE persists as a permanent algorithmic generation engine
- The AI's role is to adjust MAGE's output for musicality, stylistic fitness, and goal-specific shaping
- The training-data-then-replacement framing (Staley's earlier articulation) is no longer the team's working framing

**Reasoning:** Patrick's articulation provides the concrete mechanism (AI adjusts music XML output by MAGE) that the augmentation framing previously lacked. Steven's concurrence and Staley's non-pushback constitute directional alignment.

**Caveats / what remains open:**
- ~~Staley has not explicitly retired the training-data-then-replacement framing. The amendment records the convergence; full closure of the question awaits Staley's explicit confirmation.~~ *(Retired by Decision #53, 2026-05-12 — procedural caveat closed; augmentation framing is canon's working framing without further blocker. Staley remains free to articulate framing-retirement independently.)*
- Cost implications of the augmentation framing differ from the replacement framing (per Doc 09 §10.4): MAGE+AI is a hybrid stack, not a single LLM. This is a feature, not a bug, but architectural commitment must reflect it.

**Phasing:** N/A — architectural framing, not a feature.

**Cross-references:** Decision #39 (amended, not superseded; formally closed by Decision #53). Doc 09 §10.3, §10.4. Decision #53 (procedural caveat retired).

---

## Decision 45: User-Generated Sight-Reading Mode Resolved as User-Generated Within Sight Reading Content Mode

**Source:** May 7, 2026 brainstorm. Steven articulates user-constructed sight-reading levels with custom parameters as falling cleanly within the Sight Reading content mode's user-generated authorship origin. Staley and Patrick aligned during the call.

**Decision made:** User-generated sight-reading mode (custom-parameterized levels with explicit musical parameters, performance constraints, and completion settings) is **resolved as user-generated content within the Sight Reading content mode**. Specifically:
- The user invokes Sight Reading's Generate flow
- Configures parameters (notes, rhythms, time signature, complexity metrics, performance constraints, completion criteria)
- The system constructs the level
- The level is stored with `authoring_origin = user`
- The level may carry "no completion criteria, just play endlessly" as one of the configurable options

**Crucial scope clarification:** This decision does **not** resolve "Open Play" in the original A1 sense (renamed from "Free Play" by Decision #49 Part 2). Open Play (original) refers to user improvisation without notation guidance — open-ended musical exploration. That capability remains deferred (per Decision #41's candidate content modes list, Open Play is "deferred indefinitely"); status unchanged. An earlier draft of this decision conflated user-generated sight-reading with what was then called "Free Play"; this decision narrows to the sight-reading capability only. *(Amended by Decision #49 Part 2 to use the renamed term "Open Play" in place of "Free Play original sense" throughout.)*

**Reasoning:** The May 7 articulation closes the long-standing ambiguity for the specific capability of user-parameterizable sight-reading. The user-generated authorship origin (Decision #41) provides the primitive. No new content mode is required for this specific capability. Open Play original sense (renamed from "Free Play original sense" by Decision #49 Part 2) remains a separate question with its own deferral status.

**Phasing:** N/A — architectural framing. Specific UI labels and Generate-flow UX are V1+ design questions.

**Cross-references:** Decision #41 (user-generated authorship origin, and Open Play deferral within candidate content modes — unchanged in substance, renamed in vocabulary by Decision #49 Part 2). Decision #49 Part 2 (amended this Decision's scope clarification to use "Open Play" in place of "Free Play original sense"). Bible §2.1.1 (status update for sight-reading-mode clarity, NOT Open Play status).

---

## Decision 46: Agent-Controllable Repertoire Practice Control Surface

**Source:** May 7, 2026 brainstorm. The agentic system's repertoire-practice job is orchestrating decisions across a defined set of practice tools, of which auto-looping (Decision #42) is one specific algorithmic pattern. Steven's enumeration of the surface during the call.

**Decision made:** The agentic system operates over an enumerable **per-content-mode control surface** — the set of practice tools, settings, and behaviors the agent can manipulate during a session. For repertoire, the surface includes:
- **Song position** — where to place the user for the next take
- **Tempo controls** — when and how much to adjust
- **Metronome settings** — on/off; accent vs unaccented downbeats; flexible vs fixed count-in
- **Hand assignment** — which hand(s) to play at any given time
- **Accuracy controls** — track or not; which hand(s); real-time feedback on/off; color preservation across takes; success threshold (e.g., 95% / 85%)
- **Audio playback** — silent / dueting / app-only / no MIDI
- **Looping controls** — start/end points; seamless vs paused; takes-required; tempo adaptation per take
- **Cursor toggle** — show/hide playhead cursor on sheet music
- **Note names / finger numbers** — display either as overlay aids

The agent's repertoire-practice orchestration is the policy by which it manipulates this surface in service of a Project goal (and possibly user preferences).

**Implication.** Each content mode has its own control surface:
- **Exercises:** training method selection, performance constraints, content scope, blueprint configuration
- **Sight reading:** parameter generation, level construction, game-mode toggles, performance constraints

The agentic system's job-per-content-mode is enumerable in terms of these surfaces. Phase 2 sketches the exercise and sight-reading surfaces; full enumeration follows in subsequent design work.

**Reasoning:** Without enumerating the surface, the agent's repertoire-practice job is undefined. Enumeration also enables progressive implementation — each surface element is independently buildable, and the agent's policy can grow over time as the surface stabilizes. Auto-looping is a meta-policy that bundles several surface elements together; other meta-policies will emerge.

**Phasing:** TBD. The repertoire surface enumeration is V1 documentation work; agent policy implementation phases independently. Exercise and sight-reading surfaces are sketched in Phase 2.

**Cross-references:** Decision #42 (auto-looping as one capability within the surface), Decision #43 (cross-mode performance constraints — also part of each mode's surface), Doc 09 §6 (AI Surface) — should reference this as the operational scope.

---

## Decision 47: User-Modeling Layer Recognized as Foundational Architectural Commitment

**Source:** May 7, 2026 brainstorm (the "Steven MD file" / "Patrick MD file" framing) + Steven's redline elevating the user-modeling layer's strategic significance.

**Decision made:** The per-user accumulating user-model — the architectural layer that observes, synthesizes, stores, and retrieves user-specific context across sessions — is recognized as a **foundational architectural commitment**, on par with the content/path-mode architecture (Decision #41) and the AI augmentation of MAGE (Decision #44). Specifically:

- The user-modeling layer is named explicitly as a vision pillar in Doc 09 §1 — not buried as auxiliary infrastructure under the LLM/agentic-layer framing in §10
- It is the load-bearing capability that distinguishes MuseFlow structurally from competitor piano-learning products (Simply Piano, Yousician, Skoove, Flowkey), all of which treat the user as roughly anonymous within content
- It is the technical substrate that justifies the "AI company" framing in front of technically literate investors — without it, the framing reads as positioning; with it, it reads as a defensible architectural claim
- Its implementation pattern is closer to "per-user RAG layer over conversation history, exercise/repertoire/sight-reading event data, and AI-extracted summaries" than to a single growing markdown file (the "Steven MD file" / "Patrick MD file" analogy is a user-facing metaphor, not implementation spec — see Doc 10 §3.9)

**Reasoning:** The May 7 call surfaced this as a strategic claim, and Steven's redlines elevated its significance. Recognizing it as a numbered Decision (rather than only as a Doc 09 §1 vision-pillar update) makes the commitment load-bearing in the Decision Log, where downstream architectural decisions can reference it explicitly. It also signals to the team that the user-modeling layer is a first-class architectural concern, not an emergent property of LLM choices.

**What this Decision does NOT do:**
- It does not specify the implementation architecture in detail. The implementation pattern is sketched in Doc 09 §10.5 and Doc 10 §3.9; concrete schema and retrieval logic are out of scope for this Decision.
- It does not assign team ownership. The LLM-layer vs user-modeling-layer ownership question remains open per Doc 10 §6 #13 — that is a team-organization question separate from this architectural commitment.
- It does not commit pricing or unit-economics implications. Those flow downstream once the user-modeling layer's compute profile is concrete.

**Phasing:** N/A — architectural framing, not a feature. The vision-pillar update in Doc 09 §1 is V1 documentation work. Implementation phasing is a downstream question once team ownership is resolved.

**Cross-references:** Doc 09 §1 (vision pillar to add), §5.3 (persistence and reusability), §10.5 (RAG architecture sketch). Doc 10 §3.7 and §3.9 (substantive analysis and the metaphor-vs-implementation distinction). Decision #41 (the architecture this layer operates within). Doc 10 §6 #13 (open question on team ownership).

---

## Decision 48: Theory Naming Resolution (Path c)

**Source:** A2 evaluation of Patrick Boylan's "Theory Library & Exercise Section: Comprehensive Feature Brainstorm & Design Specification" (Doc 11). Patrick's doc uses "Theory" to name a separate video-content surface (Theory Library); Bible §2.1.1 had "Theory" as a candidate content mode for theory-practice exercises. The collision required resolution.

**Decision made:** Resolve the "Theory" naming collision via Path (c) — neither Patrick's framing nor the candidate content mode framing keeps the name "Theory" alone:

1. **Remove "Theory" from Bible §2.1.1's candidate future content modes list.** Theory practice exercises are correctly handled as Semantic-output exercises across multiple existing substrate clusters (Frequency-Domain, Time-Domain) within the Exercises content mode. Adding a separate "Theory" content mode would either duplicate atoms or fragment clusters; both are worse than absorbing the pattern into Exercises.

2. **Rename Patrick's video-library surface to "Knowledge Library"** (working name). Patrick's surface scope is broader than music theory — it explicitly includes technique videos, genre, performance psychology, sight-reading tips, and repertoire-context videos. "Theory Library" was misnamed in his own doc. "Knowledge Library" is the working name for the surface; the final naming call is deferred until the feature actually enters scope (user testing or brand work will inform it better than committing now).

3. **The renamed Knowledge Library is deferred beyond V1** — see Decision #51.

4. **Glossary "Content Mode" entry updates accordingly** — Theory is removed from the candidate list; the renamed Open Play candidate (formerly "Free Play original sense" per Decision #49 Part 2) replaces it.

5. **Doc 09 §13.11 #51 marks Theory as resolved by this Decision.** The remaining cluster questions (#52 Interactive Tutorial placement, #53 Video Library placement, #55 Tutorial-as-roadmap-node phasing) remain open within the cluster.

**Reasoning:** Patrick's "Theory Library" is misnamed in his own doc — its scope is broader than music theory and includes technique, genre, performance psychology, and song-context videos. Theory-practice exercises don't warrant a separate content mode because they decompose cleanly into Semantic-output atoms across existing substrate clusters. Adding a "Theory" content mode would either duplicate atoms or fragment clusters; both are worse than absorbing the pattern into Exercises. The candidate content mode entry was always conditional on this doc review, and Path (c) is the resolution that doc review converged on.

**Phasing:** V1 documentation work (Bible §2.1.1, Glossary, Doc 09 §13.11 updates). The renamed Knowledge Library feature itself is deferred beyond V1 per Decision #51.

**Cross-references:** Bible §2.1.1 (candidate content modes list — updated by this Decision); Glossary "Content Mode" (updated by this Decision, paired with Decision #49 Part 2); Decision #41 (content/path mode architecture); Decision #45 (clarified for the renamed Improvisation candidate per Decision #49 Part 2); Decision #49 Part 2 (paired update — Improvisation rename); Decision #51 (Knowledge Library deferral); Doc 09 §13.11 (cluster home); Doc 11 §7 (full reasoning).

---

## Decision 49: Free Play as Completion-Policy Element of the Exercise Control Surface (with Naming-Collision Resolution)

**Source:** A2 evaluation (Doc 11) of Patrick's Game Mode / Free Play framing (his §2.1), corrected to recognize the pattern's existing MuseFlow Sight Reading precedent. The Game / Free Play toggle ships in production today as a top-of-screen tab in the SRT — Patrick is echoing an established pattern into the exercise context, not inventing it.

**Decision made (two parts):**

**Part 1 — Absorb Free Play into the Exercise content mode as a completion-policy element of the exercise control surface (Doc 09 §6A.2).** Extend the existing Sight Reading Game / Free Play pattern into the Exercise content mode. The exercise control surface gains a `completion_policy` element with two values:
- **`practice`** (default) — assessable, contributes to mastery thresholds, produces ExerciseResult with completion status
- **`free_play`** — non-assessable, no completion contribution, but stats (accuracy, tempo, errors) are still tracked and displayed

The completion-policy element is **live-toggleable during a session**, preserving the existing SRT affordance where the user flips between Game and Free Play mid-exercise without backing out and reconfiguring. Whether the agent can also flip the toggle mid-session is a separate question per Decision #46 (the agent's policy operates over the surface elements; live-toggle by user and by agent are not mutually exclusive) and remains open pending further agent-policy design.

Free Play is available on any atom that supports a continuous-practice interaction (most PRF atoms; some REC/RCL atoms). Specific applicability per blueprint is open and is a Track D scoping concern.

This placement parallels Decision #45's "no completion criteria, just play endlessly" option for user-generated sight-reading; both are completion-policy settings within their respective mode's control surface, not new content modes.

**Part 2 — Rename the deferred candidate content mode currently called "Free Play (original sense)" to "Open Play."** "Free Play" as completion-policy collides with "Free Play" as the deferred candidate content mode for open-ended improvisation. Sharing the name is unworkable. Since the deferred candidate is uncommitted and not yet user-visible, renaming it costs nothing in production-vocabulary terms; renaming the completion-policy would fight established SRT terminology.

"Open Play" (rather than "Improvisation," considered and rejected) is selected to keep future-feature naming space clean. "Improvisation" has a loaded meaning in music-pedagogy contexts that implies structured improvisation (over chord changes, in a key) — closer to Patrick's F category (Decision #13 territory). If a structured-improvisation feature emerges later, "Improvisation" should remain available for it. "Open Play" accurately captures the original-sense intent (open-ended musical exploration without notation guidance) without pre-committing pedagogically loaded terminology.

Specific changes:
- **Bible §2.1.1**: rename the deferred candidate from "Free Play" to "Open Play"
- **Glossary "Content Mode"**: updated entry refers to "Open Play" as the candidate (paired with Decision #48 Theory removal)
- **Decision #45's scope clarification** is amended to refer to "Open Play (formerly 'Free Play original sense')"
- **Doc 09 §13.11 #54** updates to refer to "Open Play original-sense status" rather than "Free Play original-sense"

**Reasoning:** Free Play is a real practice need (warm-up, experimentation, indefinite practice without pass/fail pressure), and a pattern already ships in production via the SRT. Placing it in the exercise control surface (an architecture that already exists per Decision #46 and Doc 09 §6A.2) is the smallest change with the most reusability. The live-toggle requirement preserves what users expect from the existing SRT pattern. The naming-collision resolution removes a real ambiguity that would otherwise confuse users, the team, and downstream design work; selecting "Open Play" over "Improvisation" keeps future-feature naming space clean.

**Phasing:** V1 for Part 1 — the control surface element addition is non-breaking; the UI surface for Free Play in exercises mirrors the existing SRT toggle UI. V1 for Part 2 — a documentation/naming change with no implementation cost.

**Cross-references:** Doc 09 §6A.2 (exercise control surface); Decision #46 (control surface enumeration; agent-driven toggle scope remains open); Decision #45 (parallel for sight-reading; scope clarification amended by Part 2); Decision #48 (paired update — Theory removal from candidate list); Bible §2.1.1 (candidate list updated by Part 2); Glossary "Content Mode" (updated by Part 2); Doc 09 §13.11 #54 (Open Play original-sense status); Standup Synthesis §1 (Staley's "free-play interlude as part of the path"); Doc 11 §5.1 (full reasoning).

---

## Decision 50: Patrick's Mastery-Threshold Patterns as Candidate Starting Baselines

**Source:** A2 evaluation (Doc 11 §5.4, §8.3) of Patrick's passing criteria across his ~50 exercise templates. The criteria are remarkably consistent and suggest a recurring pattern shape worth absorbing — but the specific numbers are one possible configuration in the n-dimensional matrix of cross-mode performance-constraint settings (per Decision #43), not committed canon defaults.

**Decision made:** Atoms in the V1 preset inventory carry `mastery_thresholds` (the schema field added by Decision #40), populated during catalog authoring. Patrick's recurring passing-criteria patterns are recognized as **candidate starting baselines for Track D**, easily overridable per atom by AI generation, preset judgment, or user input.

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

**Reasoning:** Patrick's templates are consistent enough to suggest a recurring pattern, and that pattern gives Track D a defensible starting point. Treating the specific numbers as committed defaults would over-constrain Track D and pre-empt judgment that's better made during atom-level authoring. Treating the methodology as committed (defaults exist; Patrick's patterns are the baseline) gives Track D a working scaffold without prematurely closing decisions.

**Phasing:** V1, applied during catalog authoring (Track D).

**Cross-references:** Decision #40 (`mastery_thresholds` field); Decision #43 (cross-mode performance constraints); Decision #33 (generation on demand — agent may compute thresholds dynamically); Bible §2.3 (cross-mode primitive framing); Doc 02 §5.1 (cross-mode tech spec scope); Architecture Doc §8.1; Doc 11 §5.4 and §8.3 (full pattern derivation).

---

## Decision 51: Knowledge Library / Video Resource Surface — Deferred Beyond V1

**Source:** A2 evaluation (Doc 11 §4.6 and §10) of Patrick's Theory Library proposal (his Part 1, lines 9–164). The video-library concept is well-developed (Smart Feed / Quick Theory / Deep Dives sub-surfaces, with curation logic and a proactive suggestion modal), but its V1 implementation cost is high relative to its V1 value, and the right architectural placement remains formally open.

**Decision made:** The renamed video-resource surface (working name: "Knowledge Library" per Decision #48) is **deferred beyond V1**. Patrick's design — Smart Feed / Quick Theory / Deep Dives architecture with curation logic and proactive suggestion modal — is preserved as design input for the deferred feature.

**Architectural placement remains formally open** at Doc 09 §13.11 #53 (Video Library architectural placement). Two framings are tracked:
- Patrick's framing: content-mode-like (a top-level browsable video surface)
- Staley's framing: roadmap-node primitive (agent-surfaced video as a node type within Project roadmaps)

The current team-recommendation lean is toward Staley's framing — agent-surfaced video parallels how Interactive Tutorial is positioned and matches the 2024+ pattern of agent-surfaced contextual content over standalone browsable libraries. But this is a *lean*, not a *commitment*; the §13.11 #53 placement question stays open pending more development of both framings.

**Two specific elements are absorbed earlier (not deferred):**

- **Patrick's Proactive Suggestion System** (his §1.5) is absorbed as candidate engagement-layer behavior, scaffolded against three canon layers: the **user-modeling layer** (Decision #47, Doc 09 §1.2) as the substrate that detects the patterns Patrick's triggers depend on; the **per-mode agent control surfaces** (Decision #46, Doc 09 §6A) as the action vocabulary for interventions the modal can offer (suggesting an exercise atom, starting a repertoire session with auto-looping engaged, opening the Sight Reading Generate flow with parameters pre-filled, etc., not just videos); and the **engagement layer** (Decision #19 amendment, Glossary "Engagement Layer") as the interaction surface where the modal pattern lives. Trigger conditions and modal pattern apply generically; the content surfaced by the modal generalizes from "video" to "any helpful intervention available on the relevant control surface."

- **Patrick's content tagging vocabulary** (concept tags, instrument focus tags, genre tags — his §1.3) is flagged as candidate metadata extension for catalog authoring conversations. Genre tags in particular are high-priority given Doc 10 §5.4 goal-category alignment — goal categories 3 (specific technique), 4 (play like specific artist), 5 (specific genre) all depend on genre/style tagging for Projects to assemble coherent goal-bound roadmaps.

**The Knowledge Library as a top-level content surface waits until:** (a) the engagement layer ships, (b) Projects ships and the "agent surfaces a relevant video as part of a Project node" pattern is testable, (c) compliance / licensing for embedded video is cleared, and (d) the §13.11 #53 placement question resolves.

**Reasoning:** Patrick's Theory Library design is well-considered but its V1 build effort is large relative to its V1 value, and the proactive-suggestion innovation in his design — the most generically valuable piece — applies equally to non-video interventions and is better absorbed once into the engagement layer than built twice. Deferring the surface itself preserves Patrick's design as input without committing V1 scope to it.

**Phasing:** V1 documentation (this Decision); the feature itself deferred beyond V1 with no committed phase.

**Cross-references:** Decision #19 amendment (engagement layer); Decision #41 (content/path mode architecture); Decision #46 (per-mode control surfaces — the agent's action vocabulary for suggested interventions); Decision #47 (user-modeling layer — the substrate the suggestion system depends on); Decision #48 (paired update — the renaming this Decision references); Doc 09 §13.11 #53 (formal cluster home for Video Library placement); Doc 09 (Projects as the natural home for agent-surfaced video); Doc 11 §4.6 and §5.2 (full reasoning).

---

## Decision 52: B/I/A as a Candidate Derived Label (Not a Schema Axis)

**Source:** A2 evaluation (Doc 11 §4.3) of Patrick's flat Beginner / Intermediate / Advanced difficulty axis (applied across most of his templates). The flat axis conflicts with our 3-axis difficulty model (Decision #7), and the conflict is sharper post-Phase-2 given Decision #43's cross-mode promotion of performance constraints.

**Decision made:** **B/I/A is not added to the atom schema as a primary difficulty field.** The 3-axis difficulty model (Decision #7: substrate complexity × training method scaffolding × constraint tightness) remains the difficulty engine.

If the UX exploration later determines a user-facing summary label is needed (per UX Spec §9 Open Question #5: "Named presets vs. individual sliders"), B/I/A or a similar label can be **derived from atom configuration at filter time** — it does not exist as a stored schema field.

Per Decision #43 (cross-mode performance constraints), if a B/I/A-style summary label is wanted across content modes (exercises, sight reading, repertoire), the derivation rules are likely **per-mode rather than shared** — the same B/I/A bucket means materially different things for an exercise atom (substrate complexity + method + constraints) vs. a sight-reading level (parameter difficulty + accuracy thresholds + time pressure) vs. a repertoire practice session (success threshold + tempo target + hand-isolation settings). When the UX exploration happens, per-mode derivation rules will need to be designed deliberately.

**Reasoning:** Flat B/I/A is a brittle simplification of our richer 3-axis model, and the brittleness compounds across content modes per Decision #43. Storing it as a schema field would require ongoing maintenance to keep B/I/A in sync with the underlying axes, and the mapping isn't deterministic anyway (a Compound substrate at REC method with loose constraints is "easier" than an Atomic substrate at PRF method with tight constraints, but in different ways). Derive-on-filter is the right level of commitment. The job of this Decision is to *prevent* a future bad schema commitment, not to enable a future feature.

**Phasing:** V1 — at the schema level, this is a non-decision (don't add the field). UX exploration may surface B/I/A or alternatives later, at which point per-mode derivation rules are designed.

**Cross-references:** Decision #7 (3-axis difficulty model); Decision #43 (cross-mode performance constraints — sharpens the case against a flat schema label); UX Spec §9 Open Question #5; Doc 11 §4.3 (full reasoning).

---

# Decisions Added by Track B Phase 3 (Decide-Now Session, 2026-05-12)

## Decision 53: Decision #39's Open-Status Caveat Formally Retired

**Source:** Track B Phase 3 (T-067). Decision #44 (May 7 augmentation amendment) carried a procedural caveat — "Staley has not explicitly retired the training-data-then-replacement framing. The amendment records the convergence; full closure of the question awaits Staley's explicit confirmation." That caveat has held Decision #39's open-question status open as a matter of bookkeeping rather than substance.

**Decision made:** The procedural "awaits-Staley-explicit-confirmation" caveat in Decision #44 is **retired**. Decision #39's open-question status is **formally closed** — augmentation framing (MAGE persists as a permanent algorithmic generation engine, with AI adjusting MAGE's music-XML output for musicality, stylistic fitness, and goal-specific shaping) is canon's working framing without procedural blocker. Staley remains free to articulate framing-retirement independently; canon does not wait on it.

**Reasoning:** The May 7 brainstorm produced directional alignment across Steven, Patrick, and Staley toward augmentation (Patrick articulating the AI-adjusts-MAGE-output mechanism, Steven concurring, Staley not pushing back and expressing positive sentiment toward MAGE). The convergence is substantive; the procedural caveat introduced a paperwork dependency on a confirmation that may or may not be made explicit. Holding a canonical open-question status open for that paperwork creates triage noise (the question recurs across UX Spec §8.6, §9, Doc 09 §13.7 with PARTIALLY STALE flags) without changing the substantive position. The cleaner state is: substantive position is closed; the framing-retirement is something Staley can do or not do on his own timeline; canon doesn't hinge on it.

**Phasing:** V1 documentation work. Decision #39 amended to mark Closed (resolved by Decision #44 + #53). Decision #44 amended to retire the "awaits-Staley-explicit-confirmation" caveat. UX Spec §8.6 Q5, §9 Q27, and Doc 09 §13.7 #32 amended to note formal closure rather than partial-stale status. Triage entry T-067 marked Resolved.

**Cross-references:** Decision #39 (formally closed); Decision #44 (caveat retired); UX Spec §8.6 Q5, §9 Q27 (status updates); Doc 09 §13.7 #32 (status update); Doc 12 T-067 (formally resolves).

---

## Decision 54: "Large Music Model" Framing — Internal-Only Pending Architecture Justification

**Source:** Track B Phase 3 (T-074); Doc 09 §13.7 #39 ("As positioning, it's powerful. As implementation, it could imply training a single foundation model on music — which is not the team's direction. Whether this language enters customer- or investor-facing material warrants deliberate decision.").

**Decision made:** The "Large Music Model" framing is **reserved as internal and aspirational vocabulary only**. It is NOT used in customer-facing or investor-facing material — pitch decks, marketing copy, product surfaces, demo narration, public communications — until and unless the team's architecture commitments justify the framing (e.g., commitment to a fine-tuned music-specific foundation model with substantial training). Internal team usage is unrestricted; the framing can be discussed, sketched, and aspired to internally without constraint.

**Reasoning:** The most natural implementation reading of "Large Music Model" is *a single foundation model trained on music* — which is not the team's current direction. The actual direction (augmented MAGE + LLM adjustment, per Decision #44) is a hybrid stack, not a foundation-model play. Using the framing externally would create a positioning-vs-implementation mismatch that investor and user diligence would surface, with reputational cost. The safer near-term positioning is to describe the system in terms of its actual capabilities (augmented MAGE generation, AI-driven musical-XML adjustment, goal-specific shaping). The framing is preserved as internal aspiration so the team can continue to discuss and pursue architecture directions that might one day justify reactivating it externally.

**Phasing:** V1 documentation and comms call. Affects the investor pitch deck (Patrick), marketing surfaces (Patrick), any demo narration, and Doc 09's customer-facing positioning sections. Internal docs (Doc 09's architecture sections, Doc 10's analogy discussion) are unaffected — they can continue to engage with the framing as design input. If architecture commitments shift to justify the framing, this Decision can be revisited at that point.

**Cross-references:** Doc 09 §13.7 #39 (open question this resolves); Decision #44 (the augmentation framing this Decision aligns with — augmentation is not foundation-model training); Doc 10 §3.9 (analogy-vs-implementation distinction); Doc 12 T-074 (formally resolves).

---

## Decision 55: Generation-Cost-Gating as Canonical Pricing Framing

**Source:** Track B Phase 3 (T-085); Doc 11 §11.9 lean ("Recommended lean: (b)" — generation-gating wins).

**Decision made:** The pricing conversation uses **generation-cost-gating** (per Doc 09 §16) as the canonical framing. Patrick's atom-gating proposal — the "50% atom gating" framing in his Theory Library & Exercise Section doc — is preserved as a discussion artifact and pre-§16 thinking that the team superseded; it is not the forward-design direction. This Decision resolves only the *framing*; the actual pricing structure remains deferred (Decision #37). Generation-cost-gating treats LLM tokens (and possibly MAGE compute under the augmentation framing — see open question T-084) as the variable expense.

**Reasoning:** Atom-gating presumes exercises are scarce and curated, which contradicts the generative architecture committed in Decisions #33 (generation-on-demand) and #41 (substrate × modality combinatorial space). Generation-cost-gating aligns with the actual cost driver: LLM inference, with MAGE compute as a related-but-separate question (T-084). Doc 11 §11.9 recommended this lean; this Decision formalizes it as team-aligned canon. Without explicit alignment, pricing-conversation drift could reintroduce atom-gating framing under deadline pressure, creating downstream rework. Setting the framing now — independent of structure design — protects the eventual pricing-design work from re-litigating the framing question.

**Phasing:** V1 documentation work. Pricing structure design (Decision #37) remains deferred — this Decision is the framing-vocabulary commitment that pricing-design work will operate within. T-079 through T-084 (the C-14 pricing cluster open questions) remain explicit-punt pending pricing-design start; Decision #55 sets the framing they will be answered within.

**Cross-references:** Decision #37 (pricing structure deferred); Doc 09 §16 (cost framework, the basis for generation-gating); Doc 11 §11.9 (full reasoning); Doc 12 T-085 (formally resolves); related open questions T-079–T-084 (pricing cluster).

---

## Decision 56: The Novelty-Automaticity Spectrum as Foundational Pedagogy
 
**Source:** Track C-17 substrate-architecture refinement work; D23 framework conversation (May 12); the recognition that the three content modes (Sight Reading, Exercises, Repertoire) are not independent product surfaces but distinct manifestations of a single pedagogical spectrum.
 
**Decision made:** The **Novelty-Automaticity Spectrum** is canonical pedagogical philosophy. Skill acquisition operates between two poles:
 
- **Novelty pole** — content never repeats; trains *generalization* (the ability to apply skills to unseen material). Pedagogical research (contextual interference effect; Shea & Morgan 1979 forward) establishes that high contextual variation produces worse immediate performance but stronger retention and transfer.
- **Automaticity pole** — content repeats with varied performance constraints; trains *automatic execution* (skills performed without conscious load). Low contextual interference produces faster immediate gains but weaker transfer if practiced exclusively.
**Fluency** is the outcome the spectrum produces when both poles are engaged. A learner needs both: pure novelty produces frustrated, unautomatized players; pure repetition produces context-bound performers who can't generalize. Mastery requires deliberate interleaving.
 
The three content modes are **manifestations of the spectrum**:
- **Sight Reading** manifests the Novelty pole (each piece served at most once; drawn from an infinite generator)
- **Exercises** manifests the Automaticity pole (same atom-content served repeatedly until mastery; finite content scope with varying constraints)
- **Repertoire** manifests synthesis (finite content with internal novelty and internal repetition, with composed artistic structure as a second axis)
Two supporting principles attach:
- **Shapeless Content** — at the level of raw musical material, all three modes generate or reference the same underlying content. They differ in *scheduling and bounding policy*, not in content type. One generator, three policies.
- **Meaning-making as telos** — fluency removes limitations on movement, which removes limitations on expression, which enables the user to make meaning through music. The spectrum serves this end; it is not an end in itself.
**Reasoning:** The spectrum framing resolves several latent architectural tensions simultaneously. It explains why the three modes are level-agnostic (Decision #16) — they're orthogonal pedagogical axes, not separate user tiers. It justifies one-content-many-policies architecture (consistent with Decisions #33 generation-on-demand and #34 custom authoring). It gives the agentic system a principled reasoning axis for roadmap composition (interleave deliberately along the spectrum, not pick a single mode). It explains the existing "songs vs. skills" pitch evolution: the original framing critiqued competitors over-indexing on automaticity; the matured framing is that MuseFlow operates the entire spectrum deliberately. Without this philosophy, the three-mode architecture reads as three independent product surfaces with arbitrary boundaries; with it, the architecture is a single coherent pedagogical system.
 
**Phasing:** Foundational and immediate. Codified in Doc 01 §2.4 (new section). Cross-referenced across Doc 02 (substrate-engagement framing), Doc 09 (agentic roadmap composition), and Doc 13 (pitch deck register). Does not commit V1 implementation work directly; it commits the framing all subsequent design work operates within.
 
**Cross-references:** Decision #16 (Exercises + Repertoire as universal pillars — Sight Reading now joins as the third pillar at the Novelty pole); Decision #20 (Contextual Transfer — Spectrum makes the mechanism explicit); Decision #33 (generation-on-demand — Shapeless Content corollary); Decision #41 (Content Mode and Path Mode Architecture — modes refined as spectrum manifestations); Decision #57 (K-substrate family — admitted under the spectrum's content-shape neutrality); Doc 01 §2.4 (canonical home); Doc 09 §5 (spectrum-driven roadmap composition).
 
---
 
## Decision 57: K-Substrate Family — Motor-Primary Substrates Admitted to the Catalog
 
**Source:** Track C-17 cluster (T-026, T-027, T-097). The realization, surfaced by working through the Hanon goal (finger dexterity/independence/strength) and the pedaling goal (foot coordination across complexity), that the substrate catalog as previously defined had no way to distinguish a Hanon atom from a beginner-sight-reading atom at the schema level — a clear contradiction with Decision #25's atom-identity principle.
 
**Decision made:** Admit a **K-substrate family** (Kinesthetic / motor-primary substrates) parallel-axis to F (Frequency), T (Time), and A (Amplitude). The substrate catalog admits any substrate whose **primary training value is motor** (physical execution: finger patterns, hand coordination, pedal coordination, etc.), where:
 
- **Primary** means the trained skill is motor, not cognitive. Cognitive substrates with kinesthetic *execution* (any current substrate with a Kinesthetic output modality — playing a scale from name SC-006, playing a chord CH-006, etc.) stay in their F/T/A homes.
- **Substrate (not constraint)** means the entry has its own learning curve, recognizable identity ("the X technique"), and isn't adequately covered as a modulation on an existing cognitive substrate.
The K- family is structured by the same atomic/molecular/compound levels as F/T/A. Concrete catalog (full tables in Doc 02 §3.1):
 
**K-A (atomic):** K-A1 Finger independence; K-A2 Finger strength (weak fingers); K-A3 Five-finger coordination pattern; K-A4 Pivoting (thumb-under ascending, finger-over descending); K-A5 Stretching (anchored finger, others expand); K-A6 Squeezing (anchored finger, others contract); K-A7 Whole-hand translation (jumps, leaps, slides); K-A8 Wrist rotation; K-A9 Octave technique; K-A10 Trill technique; K-A11 Finger staccato; K-A12 Wrist staccato; K-A13 Arm/forearm staccato; K-A14 Single-hand chord voicing (motor).
 
**K-M (molecular):** K-M1 Parallel-oblique motion (both hands stationary on their respective notes); K-M2 Parallel motion (same direction, same interval); K-M3 Strict contrary motion (mirrored exactly); K-M4 Similar motion (same direction, different intervals); K-M5 Contrary motion (opposite directions, intervals may differ); K-M6 Oblique motion (one hand stationary, other moves); K-M7 Hand independence (rhythm); K-M8 Hand independence (dynamics); K-M9 Hand-crossing; K-M10 Polyrhythm execution; K-M11 Damper pedal — pulse; K-M12 Damper pedal — chord change; K-M13 Damper pedal — legato change; K-M14 Damper pedal — half-pedal / flutter; K-M15 Sostenuto pedal coordination; K-M16 Una corda usage.
 
**K-C (compound):** K-C1 Three-system integration (LH + RH + pedal); K-C2 Arm-weight transfer; K-C3 Forearm rotation in extended passages.
 
**Reasoning:** Decision #25 established that atoms differing on any identity dimension are different atoms because they train fundamentally different skills. The Hanon case exposed a contradiction: under the cognitive-only substrate model, a Hanon atom and a beginner five-finger sight-reading atom were identical on every identity dimension (substrate F-A1/F-A2, Visual input, Kinesthetic+Aural output, etc.). They are manifestly different skills with different training values. The cleanest resolution is to recognize that the substrate catalog serves two functions: (a) naming the Transformation stage of PTA (cognitive operations), and (b) indexing what an exercise *trains*. For cognitive-primary exercises these coincide; for motor-primary exercises they diverge, and the catalog must index by *what is trained*, not by *what the cognitive Transformation is*. K-substrates extend the catalog along that axis.
 
Alternative considered: tagging cognitive substrates with a motor-skill attribute. Rejected because pure motor drills (E1–E5 in Patrick's catalog, K-A2 finger strength) have no meaningful cognitive substrate to tag — the whole exercise IS the motor skill. Tagging cannot create a home where there is none.
 
Alternative considered: treating motor work as a distinct content class (Technique) outside Exercise. Rejected because once motor-primary substrates exist in the framework, technique drills are exercises like any other — their substrate is K- rather than F/T/A. Patrick's E category becomes a filterable cluster within Exercise ("Technique"), not a parallel content class. This collapses T-027 cleanly.
 
**Phasing:** Catalog admission is immediate (Doc 02 §3.1 amendment). V1 scope inclusion of specific K-atoms is a separate decision for Track D — phasing-TBD per project conventions. Likely lean: at least minimal K- coverage in V1 given how foundational finger-independence and pedaling are to early learners, but the actual V1 cut is Track D's call.
 
**Cross-references:** Decision #4 (substrate catalog formal ID system — K- follows same convention); Decision #5 (Kinesthetic modality — K-substrate family and Kinesthetic modality are conceptually adjacent and reinforce each other, but are distinct: modality is the channel, substrate is the trained skill); Decision #13 (fingering and improvisation placeholders — see amendment below; motor-primary substrates do NOT pull fingering-selection back into scope, which remains a cognitive substrate placeholder); Decision #25 (atom identity — preserved; single-substrate identity remains canonical); Decision #56 (Novelty-Automaticity Spectrum — K-atoms manifest at the Automaticity pole within the Exercise mode); Decision #58 (semi-lattice engagement — explains how K-atoms incidentally engage F/T substrates and vice versa); Doc 02 §3.1 (canonical catalog); Doc 03 §12 (taxonomy parallel); Doc 12 T-026, T-027, T-097 (resolved).
 
**Naming note:** "K-" letter chosen to reinforce conceptual link with Kinesthetic modality (Decision #5). K-substrate family and Kinesthetic-modality are NOT the same thing — modality is the perception/action channel; substrate is the trained skill. They reinforce each other (K-substrate atoms are typically executed via Kinesthetic output modality) but operate at different levels of the framework. Footnote in Doc 02 §3.1 makes this distinction explicit.
 
---
 
## Decision 58: Substrate Engagement as a Semi-Lattice Overlay
 
**Source:** Track C-17 work; the recognition (informed by Christopher Alexander's "A City is Not a Tree") that single-substrate atom identity is correct for navigation and mastery but misses the architectural reality that every kinesthetic-output atom engages multiple substrates simultaneously.
 
**Decision made:** Two distinct architectural layers govern substrate relationships:
 
1. **Atom identity (tree).** An atom has exactly one **primary substrate**. This defines the atom, indexes navigation, and serves as the axis for mastery tracking. Single-substrate identity preserves Decision #25's clean atom typing; user-facing catalog stays tree-structured.
2. **Substrate engagement (semi-lattice).** An atom *engages* other substrates derivatively — through its input modality (Visual input engages reading substrates F-A2 + T-A2), through its output modality (Kinesthetic output engages relevant K-substrates appropriate to the content), and through its content scope (e.g., Hanon-style content engages five-finger coordination K-A3 even when the primary substrate is F-A2 sight-reading). Engagement is a graph (semi-lattice in Alexander's sense — overlapping membership without strict tree containment), not a tree.
3. **Engagement is computable, not stored.** Given an atom's existing identity dimensions, incidental engagement is derivable at runtime by the agentic system. The atom schema does NOT carry an engagement field. Computation rules (e.g., "Visual input → F-A2 + T-A2 engaged; Kinesthetic output + content scope encoding motor pattern → relevant K-substrates engaged") live in the agent's recommendation engine, not in stored atom metadata.
**Reasoning:** Two functions are in tension:
- Atom identity wants to be **clean and singular** so users can navigate, so mastery is single-axis trackable, and so the schema stays simple. Decision #25 settled this.
- Substrate relationships are **inherently overlapping** — a Hanon atom is K-A3 primary AND incidentally engages F-A2 (notation reading) and T-A2 (rhythm reading); a five-finger-position sight-reading level is the *inverse*: F-A2/T-A2 primary, K-A3 incidental. Same training value mix, different primary.
The semi-lattice overlay resolves the tension by separating layers. **Tree for users, semi-lattice for the agent.** Users see a clean hierarchy; the agent reasons over the richer graph to compose roadmaps that route the same training goal through multiple modes (e.g., for "improve finger independence": primary route is Exercise K-A1 atoms; alternative routes include Sight Reading scoped to five-finger positions and Repertoire pieces rich in finger-independence demands).
 
Computed-not-stored avoids three failure modes: (a) schema bloat from a field that's redundant with existing identity dimensions, (b) staleness if the computation rule evolves but stored values don't, (c) inconsistency if some atoms have engagement metadata and others don't.
 
**Open question deferred:** Whether engagement-weights (intensity of incidental engagement — Hanon engages F-A2 lightly because pitches are repetitive; sight-reading engages F-A2 intensely) need to be encoded in the computation rule, or whether qualitative engagement (engaged / not engaged) is sufficient. Leaning qualitative for V1; revisit if the agent's recommendation engine needs weighted indexing for ranking quality.
 
**Phasing:** Conceptual canon now (Doc 02 §3.1 footnote + Doc 09 §5 agentic roadmap composition). Implementation phasing: engagement-graph computation lands when the agentic system's recommendation engine is built; not a V1 commitment for the static catalog.
 
**Cross-references:** Decision #25 (atom identity preserved); Decision #57 (K-substrate family — engagement layer is what makes K-atoms interoperable with F/T/A atoms in agent reasoning); Decision #56 (Spectrum — the engagement graph is what enables cross-mode routing of training goals along the Spectrum); Doc 02 §3.1 (canonical home); Doc 09 §5 (agentic roadmap composition); Doc 12 T-097 (resolved).
 
---
 
## Decision 59: The Three AI Roles Framework
 
**Source:** Track C-17 conversation; the recognition that MuseFlow AI is multi-purpose across multiple levels of scope, and that articulating these roles explicitly serves both internal prioritization and external pitch communication.
 
**Decision made:** MuseFlow AI operates across three role scopes, layered from broadest to narrowest:
 
**The Coach** — relationship-scoped AI, operating across the user's journey:
- Skill model maintenance (continuously updates a model of user's skill profile across all substrate families, performance-constraint capacity, motor competencies, repertoire history)
- Goal interpretation (translates user-stated natural-language goals into pedagogically actionable directives)
- Pedagogical dialogue (conversational coaching partner)
- Curriculum / roadmap generation (composes sequenced practice plans deliberately interleaving along the Novelty-Automaticity Spectrum)
- Plan adaptation (repairs the roadmap when the user goes off-plan)
- Cross-mode orchestration (decides when to switch modes)
**The Composer-Librarian** — content-scoped AI, operating within each content mode:
- Sourcing (selects from existing libraries — Repertoire library, preset exercise catalog, etc.)
- Generating (creates new content on demand: sight-reading material, exercise instances, etudes — AI-generated repertoire with training intent)
- Modifying (transforms existing content: simplifying/complexifying repertoire, transposing, generating variations on a theme)
- Evaluating (judges whether existing or generated content matches a pedagogical need)
**The Practice Partner** — moment-scoped AI, operating within a single content piece in a single session:
- Performance constraint control (real-time tempo, accuracy thresholds, mastery thresholds, loop boundaries)
- Insight surfacing (contextual observations, hints, advice)
- App orchestration (automates auto-looping, start-position movement, next-step decisions — the way a teacher in the room would)
- Engagement sensing (detects frustration, boredom, flow state; signals up to the Coach for journey-level adaptation)
**Reasoning:** Without an explicit role framework, AI capability discussions become surface-level and unprioritized. Each role has different latency requirements, different data dependencies, different infrastructure, and different cost profiles. The Coach is high-context, low-frequency, and can be expensive per call. The Composer-Librarian is medium-context, medium-frequency, and benefits from caching and reuse. The Practice Partner is low-context, high-frequency, and must be cheap and fast. Conflating them produces poor engineering decisions (e.g., using Coach-grade reasoning for Practice-Partner-scoped decisions, or trying to make the Practice Partner stateful in ways that should live in the Coach).
 
The role framework also clarifies the Mage/Opusmodus positioning question (Decision #39, #44, #53): both are implementation tools within the **Composer-Librarian** role. Mage is the algorithmic generator; Opusmodus is a renderer Mage uses. The team's recurring confusion about their relationship dissolves when both are placed inside a single role-scoped layer.
 
The framework also gives the pitch deck a clean three-line summary: *"MuseFlow's AI plays three roles you'd recognize from any great teacher: a coach who knows your goals and journey, a composer-librarian who creates and curates the right music for you, and a practice partner who's in every session with you."* Each role decomposes into 4–6 specific capabilities, so the pitch can drill from three-line summary to specific functionality without losing the through-line.
 
**Phasing:** Conceptual canon now (Doc 09 §1.6 new subsection + Doc 09 §10 MAGE/Opusmodus recontextualization). Implementation phasing per-role: Practice Partner functionality is partially present today (auto-looping, etc.) under non-AI logic; AI-mediated Practice Partner is V2+. Composer-Librarian generation capabilities are R&D-active (Mage, Decision #44). Coach is the most ambitious; demo-defensible scope for the investor demo (Doc 09 §15.2) is the V1 target.
 
**Cross-references:** Decision #29 (Agentic Vision documented); Decision #32 (Projects elevated to near-term R&D); Decision #33 (Exercise Generation on Demand — Composer-Librarian capability); Decision #34 (Custom Authoring — Composer-Librarian capability); Decision #44 (MAGE augmentation direction — clarified as Composer-Librarian-role implementation); Decision #46 (Agent-Controllable Repertoire Practice Control Surface — Practice Partner capability); Decision #47 (User-Modeling Layer — foundational to the Coach role); Decision #60 (Etudes + Variations — Composer-Librarian generation modes); Doc 09 §1.6 (canonical home for role framework); Doc 09 §10 (MAGE/Opusmodus recontextualized); Doc 13 (pitch deck register).
 
---
 
## Decision 60: Etudes and Variations on a Theme as AI-Generated Repertoire Modes
 
**Source:** D23 framework conversation (May 12); the question of whether AI should generate repertoire and, if so, in what form to avoid pretending machine-generated music is art for its own sake.
 
**Decision made:** AI-generated content in the Repertoire content mode takes two distinct forms:
 
1. **Etudes** — AI-generated repertoire designed with explicit training intent. Sits between Exercise and Repertoire: enough artistic shape to be playable as music; a fundamental guiding principle behind the composition is to train a target technique or substrate. "No one plays an etude and is like, *huh? this is a masterpiece.* Of course not — it's an etude." The framing acknowledges artistic intent without overclaiming artistic merit.
2. **Variations on a Theme** — AI-mediated *modification* of existing repertoire (not generation from scratch). Takes a known piece and simplifies it or complexifies it along a complexity spectrum, enabling accessibility (adapt Chopin to a beginner's current level) and progression (rebuild toward the original as skill grows). Operates on user-selected source repertoire; output is the variant, with the source preserved for eventual return.
**Reasoning:** Naïvely framing AI-generated repertoire as "AI-composed music" creates a positioning trap: it implicitly competes with human composers on artistic merit, a domain where AI music is currently weak and likely to remain pedagogically suspect for some time. The etude framing reframes the question: AI generates content where artistic intent is *subordinate* to training intent, in a category that musical tradition already accepts on those terms. Czerny etudes are not Chopin nocturnes; nobody confuses them; both have value.
 
Variations on a Theme is the second use case because it does NOT require AI to compose music from scratch — it operates on a human-composed source. This neatly sidesteps the artistic-merit question entirely while delivering substantial pedagogical value (a learner can engage with real repertoire at their current level instead of waiting until they "deserve" it). User feedback informed this choice: "people have come to you" (Speaker B in the D23 transcript) with this need.
 
**Phasing:** Both are Composer-Librarian role capabilities (Decision #59). Phasing per Decision #59: R&D-active under Mage's generation work. Investor demo scope (Doc 09 §15.2) is the V1 target for at least Variations on a Theme; full etude generation is V1–V2 depending on Mage's generation maturity.
 
**Cross-references:** Decision #33 (Generation on Demand — etudes are repertoire-scope generation); Decision #34 (Custom Authoring — Variations is the repertoire-mode custom-authoring path); Decision #44 (MAGE augmentation — the generation engine); Decision #56 (Novelty-Automaticity Spectrum — etudes manifest near the synthesis midpoint; Variations are scheduling/complexity transforms over repertoire); Decision #59 (Three AI Roles — both are Composer-Librarian capabilities); Doc 09 §9 (Custom Content Generation — canonical home); Doc 13 (pitch deck register).

---

## Decision 61: Universal Affordance Symmetry

**Source:** May 12, 2026 standup discussion (Doc 14 §1.6, §2.1). Steven's explicit articulation, with team alignment: *"there really is nothing that the AI on MuseFlow could do that a user could not also do."* Surfaced in the context of presenting the Three AI Roles (Decision #59) framework and explaining the relationship between AI-mediated and user-driven affordances.

**Decision made:** **Universal Affordance Symmetry is a canonical product-architecture principle.** For every capability MuseFlow's AI can perform, the equivalent capability is also available to the user as a manual, user-driven affordance. AI mediation is an option layered over user-accessible primitives, never a replacement for them. This applies across all three AI Roles (Coach, Composer-Librarian, Practice Partner) and across all of MuseFlow's content modes and path modes:

- **Coach capabilities** — what the Coach does (goal interpretation, roadmap composition, plan adaptation, cross-mode orchestration) the user can also do manually (state a goal, build a User Path, edit their own roadmap, switch modes themselves).
- **Composer-Librarian capabilities** — what the Composer-Librarian does (sourcing, generating, modifying, evaluating content) the user can also do (browse the preset catalog, author custom content via the Repertoire Builder, simplify or complexify pieces themselves, choose their own content).
- **Practice Partner capabilities** — what the Practice Partner does in-session (control tempo, accuracy thresholds, looping, next-step decisions) the user can also do manually (the existing control surfaces remain user-operable).
- **Authoring origins** — the four-origin vocabulary (MuseFlow preset / user-generated / AI-generated / community-generated; see Doc 09 §3.3) applies uniformly at every authored hierarchy level (atoms, blueprints, paths, roadmaps, Projects). AI-generated content is one origin among four; it does not displace the others.

**Reasoning:** Three converging reasons make this principle load-bearing rather than aspirational.

*Product positioning.* MuseFlow's positioning as a tooling ecosystem (Doc 13 §2.1) — composable manually or autonomously — depends on every tool being a tool. If AI-only capabilities exist alongside manual capabilities, the "tooling ecosystem" framing fractures: the AI becomes a separate product instead of a layer over the same product. Universal Affordance Symmetry is the principle that holds the ecosystem framing together.

*The AI-averse-user constraint.* Decision #41 (Content Mode and Path Mode Architecture) and the broader project working principle commit MuseFlow to serving users who prefer to engage with the product without AI mediation. That commitment requires that every product capability be accessible without invoking AI. The principle here makes that commitment structural rather than aspirational: a feature that fails the symmetry test fails the AI-averse-user constraint by construction.

*Design discipline against silent AI-only features.* Without an explicit principle, individual feature designs can quietly assume AI mediation and become AI-only by oversight. The principle gives the PRD and downstream design work a load-bearing constraint to test against: *what's the user-driven equivalent of this AI capability?* If the question has no answer, the feature design is incomplete.

The principle is not a constraint that *every* feature must ship the manual equivalent in the same release as the AI-mediated version. It is a constraint that the design contains the user-driven affordance as a first-class element, even if shipping phasing differs. (Example: the agent's roadmap-composition capability and the User Path manual-authoring capability are both first-class per Decision #41, even if their release timing is different.)

**Interaction with pricing tier gating (open).** The principle is silent on whether tier-gating applies to *AI mediation only* or to *both AI mediation and the manual equivalent* of a given capability. Two readings are possible: (a) tier-gating gates only the AI-mediated path, leaving the manual path universal; (b) tier-gating may apply to either path independently. The choice has substantive UX and pricing implications. Recorded as open question T-098 in Doc 12 (C-14 pricing cluster); resolution gated on the pricing-design work (Decision #37) beginning.

**Phasing:** Conceptual canon now. Canonical home Doc 09 §1.7 (parallel to the Three AI Roles section §1.6). Cross-referenced in Doc 01 §8.9 (new Design Principle). The principle constrains all subsequent design work — PRD, Track C2 UI-shape work, Track D catalog authoring, future Track G (community/network-effects) scoping. No V1 implementation commitment is created by this Decision alone; it is the constraint within which V1 work proceeds.

**Cross-references:** Decision #29 (Agentic Vision — symmetry is the principle that keeps the agent layer composable with user-driven affordances); Decision #34 (Custom Authoring — manual equivalent for Composer-Librarian content generation); Decision #41 (Content Mode and Path Mode Architecture — the User Path mode is the symmetry partner of AI-mediated Projects); Decision #46 (Agent-Controllable Repertoire Practice Control Surface — the user-controllable equivalent already exists, validating the principle); Decision #56 (Novelty-Automaticity Spectrum — symmetry applies across all three content modes); Decision #59 (Three AI Roles — symmetry applies per-role); Doc 01 §8.9 (Design Principle); Doc 09 §1.7 (canonical home); Doc 09 §3.3 (Four Authorship Origins — uniform across hierarchy levels); Doc 13 §2.1 (Tooling Ecosystem framing); Doc 12 T-098 (interaction with pricing — open); Doc 14 §1.6, §2.1, §12.1 (source).

---
