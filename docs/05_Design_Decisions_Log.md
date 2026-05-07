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

---

## Decision 17: V1/V2/V3 Phasing on Product Features

**Source:** Staley's comment that the exercise section should start simple — "like LeetCode, where you choose what you want to practice" with a filter system — and then layer in recommendations once user data exists.

**Decision made:** I added phasing annotations (V1/V2/V3) to the Product Features table in the Project Bible. V1 = filter/browse interface with manual exercise selection. V2 = recommended exercises, Optimal Grip™ adaptive difficulty, User Skill Rating (ELO). V3 = AI-generated warmup rituals, spaced repetition, sandbox/workshop.

**Reasoning:** The meeting made clear that the team wants to avoid over-building before validation. The phasing keeps the architecture forward-looking while scoping the initial build to what's practical.

**Alternative:** The exact V1/V2/V3 boundaries are judgment calls. You might want to pull some V2 features forward (e.g., basic Optimal Grip™ in V1) or push some V1 features back (e.g., defer certain exercise blueprints). The phasing is a starting proposal, not a commitment.

---

## Decision 18: Cross-Section Complexity Language

**Source:** Staley's emphasis on a shared numeric tagging structure for complexity that works across exercises, repertoire, and curriculum. Steven agreed: "We need a common language of complexity."

**Decision made:** I added Section 9 to the Architecture Doc defining the Cross-Section Complexity Language and the Complexity Vector — a multi-dimensional descriptor that tags every exercise, curriculum level, and repertoire piece with standardized complexity axes (pitch, rhythm, harmony, key, texture, tempo, cognitive load).

**Reasoning:** Without this shared language, the three sections of the app are islands. With it, the app can make connections: "You mastered X in exercises, so try Y in repertoire." This is the "fundamental linking" Staley described.

**Alternative:** The specific axes of the Complexity Vector are a first proposal. You may want to add, remove, or redefine axes based on pedagogical judgment. The important thing is that the concept exists and the data model supports it from V1, even if the full vector isn't populated until V2.

---

## Decision 19: Exercise Result Schema

**Source:** The meeting discussion about analytics and the need to define "atomic measurement units" for MuseFlow data. The team discussed minutes played, completions, and conversions as candidate units.

**Decision made:** I added an Exercise Result schema to the Architecture Doc (Section 8.3) that captures: completion status, accuracy score, response time, specific errors, training method used, constraint values, complexity vector, and session context.

**Reasoning:** This is the atomic unit of exercise analytics. Every dashboard metric, ELO computation, and adaptive difficulty decision ultimately derives from Exercise Results. Defining this schema now means engineering builds the right data collection from day one.

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

**Source:** Steven's correction that contributions attributed to "Tucker" in the transcript analysis were actually from Staley (Austin Clifton). Also, "AC" should be "Asif."

**Decision made:** Corrected attribution throughout. Staley's contributions include: data model primacy principle, LeetCode-style V1 navigation, cross-section complexity language, ELO as user-facing metric. Asif is the primary engineering collaborator for exercise section implementation.
