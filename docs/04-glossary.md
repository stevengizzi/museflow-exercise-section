# MuseFlow Exercise System: Glossary & Terminology Canon

This document is the authoritative reference for all terminology used in the exercise system. When these terms appear in any MuseFlow document, spec, or conversation, they carry the definitions specified here.

---

## Foundational Frameworks

### PTA Loop
**Perception → Transformation → Action.** The three-stage cognitive circuit that models every musical task. Sensory input is perceived, processed through internal mental models, and converted into output. The PTA Loop is the cognitive operator of the exercise system. Every exercise is an instance of this loop.

### FTA Field
**Frequency × Time × Amplitude.** The three-dimensional space within which all music exists, whether experienced physically or conceptually. Frequency encompasses pitch, harmony, melody, and tonality. Time encompasses rhythm, duration, meter, tempo, and form. Amplitude encompasses dynamics, loudness, accent, and articulation weight. The FTA Field is the ground on which the PTA Loop operates.

### Patching Principle
The design rule that any input modality can be connected to any output modality through any transformation substrate to produce a potential exercise. Named by analogy with audio patch bays. The combinatorial composition of all valid patches generates the exercise catalog.

---

## PTA Loop Components

### Perception Stage
The first stage of the PTA Loop. Receives input data through one or more modalities. The training goal is to increase input resolution, granularity, and speed.

### Transformation Stage
The second stage of the PTA Loop. Processes input data through internal mental models (substrates) to produce structured output. The "black box" where cognition happens. The training goal is to build, optimize, and automate these internal models.

### Action Stage
The third stage of the PTA Loop. Converts transformed data into output through one or more modalities. The training goal is to execute output without data loss or distortion.

### Endogenous Micro-PTA Loop
A nested PTA loop that runs inside the Action stage during physical performance. Provides real-time feedback through visual (seeing hands), aural (hearing output), and kinesthetic (feeling keys) channels. Feeds validation or correction signals back into the ongoing macro Action stage. Also called the "feedback loop" or "error correction loop."

---

## Modalities

### Visual Modality
Perception: reading notation, chord charts, staff symbols, key signature diagrams, piano roll. Action: writing/placing notation, constructing visual representations on staff or screen.

### Aural Modality
Perception: hearing pitched sounds, rhythms, chords, scales, dynamics, timbres. Action: producing sound — playing piano keys, singing, humming, clapping, tapping.

### Kinesthetic Modality
Perception: spatial/tactile information from the body and instrument — key positions, hand shapes, finger span, topographic keyboard orientation. In the app context, also includes seeing highlighted keys on an onscreen keyboard processed as positional information. Action: pressing physical piano keys, tapping onscreen keyboard, performing motor patterns.

### Semantic Modality
Perception: reading symbolic/linguistic representations — pitch names, interval names, chord symbols, rhythm value names, music theory terminology. Action: producing symbolic/linguistic output — naming, selecting from named options, writing verbal answers, specifying identities or categories.

### Multi-Modal Input/Output
The combination of two or more modalities at the perception or action stage of a single exercise. Example: reading notation while hearing playback (Visual + Aural input). Treated as a composition of atomic modalities.

---

## Transformation Substrates

### Substrate
An internal mental model housed in the Transformation stage that processes input data and converts it into structured output. Substrates range from simple mappings to complex conceptual structures.

### Atomic Substrate
The simplest substrate type. Performs a direct 1:1 mapping between a single input element and a single concept. Example: mapping a pitch name to its piano key location.

### Molecular Substrate
A relational substrate that maps the relationship between neighboring atomic units. Example: recognizing a melodic interval (the relationship between two sequential pitches).

### Compound Substrate
A multi-element conceptual structure capable of variation, modulation, and inversion. Serves dual functions: anchoring cognition through pattern recognition and training embodied motor patterns. Examples: scales, chords, chord progressions, rhythm patterns.

### Rhizomatic Structure
The interconnection pattern of compound substrates. Unlike a strict hierarchy where each concept has a single parent, compound substrates interconnect laterally in a semi-lattice structure. Chord functions emerge from the intersection of chords and scales; voice leading emerges from chord voicings and melodic intervals. Named after Deleuze and Guattari's concept of the rhizome.

### Substrate Hierarchy
The organizational model for substrates: Atomic → Molecular → Compound, with rhizomatic interconnections at the compound level.

---

## Training Methods

### Training Method
The interaction pattern that defines how a user produces their response in an exercise. Ordered from most-scaffolded to least-scaffolded.

### Verification (VER)
Binary judgment: "Is this correct or not?" The most scaffolded method — requires evaluation but not production.

### Recognition (REC)
Multiple choice: select the correct answer from a limited set of options. The answer is visible among the options.

### Selection (SEL)
"Select all that apply" from a field of options. Multiple correct answers possible. Also called "Find-and-Select."

### Assembly (ASM)
Construct the correct answer by ordering or arranging provided components. Drag-and-drop, tile sequencing, ordering operations. Components are given; arrangement is not.

### Alteration (ALT)
Modify existing material to meet new specifications. Add accidentals to form a scale, transpose a chord, reharmonize a passage. Starting material is given; the transformation must be derived.

### Recall (RCL)
Free generation: produce the answer from memory with no scaffolding. Free text entry, free notation placement, open response. Also called "Tabula Rasa" when emphasizing the absence of scaffolding.

### Performance (PRF)
Real-time motor execution: play keys, sing, clap, tap. No scaffolding, with temporal pressure. The least-scaffolded method.

### Tabula Rasa
A general term for unscaffolded training — producing a correct response "from nothing," with no hints, options, or starting material. Recall and Performance are both tabula rasa methods. Contrasted with scaffolded methods like Recognition and Verification.

### Limited Choice
A general term for scaffolded training — the user's response options are constrained or pre-filtered. Recognition, Selection, and to some extent Assembly are limited-choice methods. Serves as "training wheels" when full tabula rasa is impractical.

---

## Performance Constraints (Tech Specs)

### Tech Specs
The set of performance constraints that model the technical limitations and capabilities of the user's cognitive system. Named by analogy with computer hardware specifications. These constraints make the same exercise easier or harder without changing the musical content.

### Processing Speed
The rate at which the user can complete a full PTA loop or any stage within it. Measured by tempo thresholds, response time limits, and prompt pacing. Musical fluency requires processing speed sufficient to keep up with the temporal demands of live music.

### Working Memory (RAM)
The amount of musical information the user can hold in active cognition simultaneously. Regulated by sequence length, information scarcity (hiding prompts after display), and the number of elements to track at once. By analogy with computer RAM.

### Long-Term Memory (Cache)
The internal store of pre-computed results available for rapid retrieval. When the user instantly recognizes that C to E♭ is a minor 3rd without computing it, that's a cache hit. Trained through spaced repetition and high-frequency exposure. By analogy with a lookup cache.

### Cache Retrieval
The process of accessing a stored result from long-term memory. One of two strategies for completing a transformation (the other being live computation). The training goal is to maximize cache size, retrieval speed, and retrieval accuracy.

### Live Computation
The process of deriving a result from first principles using the substrate's transformation function when the cache doesn't contain the answer. The training goal is to minimize computation time and error rate.

### Multithreading
The ability to run multiple PTA loops simultaneously. Engaged when an exercise involves multiple FTA dimensions (reading pitch and rhythm at once), multiple substrates (identifying a chord while maintaining metric awareness), or multi-voice textures. By analogy with CPU multithreading.

### Compression / Chunking
The ability to group individual elements into higher-order units for more efficient processing. Recognizing a scale pattern as "D Dorian" rather than processing seven individual pitches. Recognizing a rhythmic figure as "dotted-eighth-sixteenth" rather than computing each duration independently. By analogy with data compression.

### Bottleneck
A point in the PTA pipeline where processing speed is significantly slower than other stages, causing the overall loop to slow down. Example: a user whose pitch recognition is fast but whose finger coordination is slow has a bottleneck at the Action stage.

### Bottleneck Detection / Targeting
Exercises specifically designed to stress a single PTA stage in isolation, exposing which stage is the weakest link. Perception-only drills, transformation-only drills, and execution-only drills.

### Error Tolerance
The accuracy threshold required for exercise completion. Strict error tolerance (zero mistakes allowed) versus loose (e.g., 80% accuracy passes). Also includes retry policies (number of attempts per prompt).

### External Conditions
Environmental and physiological factors that affect performance: time of day, session duration, break frequency, fatigue level, recent practice history. These are inputs to the adaptive difficulty system and to AI-generated warmup ritual design.

### Cross-Mode Performance Constraints
Performance constraints (time-based pass conditions, accuracy thresholds, memory-chain length, error tolerance, etc.) treated as a primitive that applies across content modes — not exclusive to exercises. Any "completable" engagement (exercise atom session, sight-reading level attempt, repertoire practice session) carries performance constraints that determine pass conditions and shape the practice experience. Exercise atoms already carry them (Architecture Doc §5); sight-reading levels gain a parallel schema entry; repertoire practice sessions may carry them (e.g., "play this passage at 80% accuracy or higher for 5 minutes to clear"). Provides the agentic system a unified vocabulary for prescribing practice intensity. See Decision #43.

---

## Exercise Architecture

### Universal Exercise Template
The sentence format that describes every exercise:
> Take [input format] via [perception modality], convert it through [transformation substrate], and output it by [training method] as [output format] via [action modality].

### Input Format
The specific form of the data presented to the user. Examples: "notated pitch," "sounded chord," "named interval," "chord symbol." Determined by the perception modality and the substrate.

### Output Format
The specific form of the data the user must produce. Examples: "played key," "notated rhythm," "named chord quality." Determined by the action modality and the training method.

### Exercise Configuration
Parameters that scope the musical content of an exercise without changing its fundamental structure. Includes content scope (which pitches, intervals, chords, etc.), notation scope (clef, key signature), instrument scope (keyboard range, vocal range), and FTA dimensional scope.

### Exercise Instance
A specific, playable configuration of an exercise — with all parameters set, prompt material generated, and expected response defined.

### Pruning
The process of eliminating exercise combinations from the combinatorial matrix that are invalid, trivially simple, pedagogically empty, or redundant with simpler exercises.

### Exercise Blueprint
A reusable UI/interaction template that defines the screen layout, prompt presentation, response mechanism, and feedback behavior for a class of exercises. Multiple exercises with different substrates and musical content can share the same blueprint if their interaction mechanic is identical. Blueprints are the primary unit of work for UI/UX design (each blueprint = one screen type) and engineering (each blueprint = one interaction template). See the Exercise Blueprints Specification.

### Exercise Result
The atomic measurement unit for exercise analytics. A record of what happened when a user completed a specific exercise instance: completion status, accuracy score, response time, errors made, constraint values, and session context. Exercise Results feed the analytics layer, the adaptive difficulty system (V2), and the User Skill Rating (V2).

---

## Product Features

### Optimal Grip™
MuseFlow's adaptive difficulty scoring system. Positions the user at the intersection of substrate complexity, training method scaffolding, and performance constraint tightness where they are maximally challenged but still succeeding more often than failing. Named after Csikszentmihalyi's concept of flow, where grip strength on a climbing wall must match the difficulty of the hold.

### Workshop / Sandbox
An open-ended environment for free exploration, improvisation, and unstructured practice. Complements the structured exercise system. Provides a space for creative application of skills trained through exercises.

### AI-Generated Warmup Rituals
Personalized exercise sequences assembled from the exercise taxonomy, adapted to the user's performance history, time of day, session length, and external conditions. Uses spaced repetition data and Optimal Grip™ levels to determine which substrates need attention.

### Streak Tracking
An engagement and consistency layer built on exercise completion data. Tracks consecutive days of practice and exercise completion patterns.

### Spaced Repetition
A scheduling algorithm that determines when substrates should be revisited based on cache decay curves and retrieval performance. Substrates where the user's cache hit rate is declining get scheduled for review before the memory fades completely.

### Cross-Section Complexity Language
The shared vocabulary of difficulty and complexity that allows MuseFlow's three major sections (Curriculum, Exercises, Repertoire) to talk to each other. Without it, skill mastery in one section cannot inform recommendations or difficulty calibration in another. Implemented through the Complexity Vector.

### Complexity Vector
A multi-dimensional descriptor attached to every exercise, curriculum level, and repertoire piece that captures its musical demands along standardized axes (pitch complexity, rhythmic complexity, harmonic complexity, key complexity, textural complexity, tempo range, cognitive load). Enables cross-section linking, ELO computation, and adaptive recommendations. V2 feature; exercises are tagged with basic metadata (substrate family, FTA dimensions) in V1.

### User Skill Rating (ELO)
A user-facing composite skill rating computed from performance data across exercises, repertoire, and curriculum. Analogous to chess ELO ratings. Depends on the Complexity Vector for meaningful computation — a user's ELO is only meaningful if the system knows the difficulty of what they attempted. V2 feature.

---

## Miscellaneous

### Musical Fluency
The ultimate training outcome. The state where the user's cognitive machinery for music operates with sufficient speed, accuracy, and automaticity that the gap between musical intention and musical execution is negligible. Fluency = Speed × Accuracy × Automaticity.

### Audiation
The internal hearing of music — imagining sound without external stimulus. A form of aural cognition that exists in the transformation stage. Coined by Edwin Gordon.

### Proprioception (Musical)
The body's awareness of its own position and movement in relation to the instrument. In piano, this includes awareness of hand shape, finger position, distance between keys, and keyboard topography. A primary input channel for the endogenous micro-PTA loop.

### FTA Dimensional Scope
The number and combination of FTA Field dimensions active in an exercise. Single-dimension (frequency only, time only), dual-dimension (frequency + time), or triple-dimension (frequency + time + amplitude). A primary driver of exercise complexity and multithreading demand.

### Contextual Transfer
The principle that skills trained in isolation must also be trainable in context. A user who can identify intervals flawlessly in a dedicated exercise must also recognize those intervals when they appear embedded in a chord progression or melodic passage. Contextual Transfer is the bridge between the Exercise Section (controlled isolation) and the Repertoire Section (uncontrolled context). See Project Bible, Design Principle 8.8.

### Replayability Multiplier
The property of performance constraints that allows a single exercise definition to yield many distinct practice experiences. The same exercise with the same substrate and modality patch becomes a fundamentally different challenge when different constraints are tightened (speed, memory, accuracy, delay). This means the exercise catalog gets enormous mileage from a relatively compact set of exercise definitions.

---

## Exercise Hierarchy

### Exercise Atom
The smallest indivisible unit of distinct practice in the exercise system. Defined by six identity dimensions: substrate family, input modality, output modality, target variables, pitch reference mode, and content scope. Two atoms that differ on any of these dimensions are different atoms. Training methods and performance constraints are NOT part of the atom's identity — they are practice modes applied to the atom. See UX & Navigation Spec, Section 2.1.

### Exercise Molecule
A cluster of atoms that share the same substrate family, input modality, output modality, and content scope. Atoms within a molecule differ only on target variables and pitch reference mode. A molecule is "one box of related exercises at a specific difficulty level." See UX & Navigation Spec, Section 2.2.

### Exercise Strand
An ordered sequence of molecules that share the same substrate family, input modality, and output modality, but differ on content scope. A strand is a difficulty ladder — a learning path from easiest to hardest content scope. See UX & Navigation Spec, Section 2.3.

### Exercise Cluster
A group of strands that share the same substrate family (when grouped by substrate) or the same input modality (when grouped by modality). Clusters are the top-level navigation unit in the exercise section. See UX & Navigation Spec, Section 2.4.

### Target Variables
The specific musical properties being assessed in an exercise atom. For chords, target variables might be quality only, inversion only, quality + inversion, root + quality, etc. Target variables determine what the user is being tested on and influence how distractors are generated for multiple-choice exercises.

### Pitch Reference Mode
Whether an exercise atom requires absolute pitch identification. "Relative" means the root or reference pitch is provided or irrelevant. "Absolute" means the user must identify the root/pitch without a reference, requiring or developing perfect pitch. Atoms with absolute pitch reference mode are tagged as optional bonus challenges and excluded from default completion calculations.

### Primary Atom
The simplest atom within a molecule — typically the one with the fewest target variables and relative pitch reference mode. The primary atom must be cleared for its molecule to count as "complete." Other atoms in the molecule are secondary or bonus challenges.

### GMTF
The existing complexity scoring system in the MuseFlow codebase (GMTF repo). Provides cross-section complexity tagging that allows exercises, curriculum levels, and repertoire pieces to share a common difficulty vocabulary. Exercise atoms will be mapped to GMTF scores in V2 to enable cross-section recommendations.

---

## Mode Architecture

### Content Mode
A surface where musical material lives and is engaged with directly. MuseFlow's confirmed content modes are Exercises and Repertoire. Sight Reading is anticipated to evolve into its own content mode. Open Play (open-ended improvisation without notation guidance) is a candidate future content mode, deferred indefinitely (per Decision #45's clarification, renamed from "Free Play" by Decision #49 Part 2 to resolve a naming collision with the exercise control surface's completion-policy element). Theory was previously a candidate but resolved as a substrate family within Exercises rather than a separate content mode (Decision #48). See Project Bible §2.1.

### Path Mode
A structured progression through content modes. Path modes don't hold content of their own — they reference content held in content modes. MuseFlow has three path modes: Curriculum (preset, MuseFlow-authored), User Paths (custom, user-authored), and Projects (AI-mediated, goal-driven). See Project Bible §2.1.

### Three-Flow Pattern
The set of three primary user flows available within every content mode: Browse, Generate, and Project. The pattern applies identically across content modes, making the architecture extensible — new content modes inherit the pattern. See Project Bible §2.1.1.

### Browse (Flow)
The flow through which users explore available content within a content mode. Decomposes along the authorship-origin axis: users can view all content together (with origin tags visible) or filter to a single origin (presets, their own, AI-generated, community). See Project Bible §2.1.1, Decision #41.

### Generate (Flow)
The flow through which users create custom content using a mode's generation tool — for example, a custom exercise atom built from parameters, a custom sight-reading level, or (via Andrew's editor) a custom piece of repertoire. Generated content is tagged with `authoring_origin = user`. See Project Bible §2.1.1.

### Project (Flow)
The flow through which users declare a goal in natural language and work with MuseFlow's AI guidance to compose a roadmap that draws from any combination of content modes. Reachable both from a top-level Projects dashboard and from inside individual content modes. See Project Bible §2.1.1, Doc 09.

### Authorship Origin
The provenance of a piece of content (or a path). Four values are anticipated: **MuseFlow preset** (curated content shipped with the app), **user-generated** (created by the user), **AI-generated** (created by the MuseFlow AI in service of a Project goal or direct command), and **community-generated** (future, via marketplace). Encoded as `authoring_origin` on the atom schema and (when their content modes formalize) on repertoire and sight-reading entities. See Decision #40, Decision #41.

### Browse-by-Origin
A primary filter axis available in both content-mode browsing and path-mode browsing experiences. Allows users to view all content/paths together or filter to a specific authorship origin. Supports AI-averse users explicitly: a user who never wants to see AI-generated content can filter it out. See Decision #41.

### Interactive Tutorial
A current canonical content class in MuseFlow. Each tutorial is an animated video with embedded live-action hand clips and Phaser-JS interactive exercises gated mid-flow — concept introduction → guided exercise → continuation. Each Sight Reading curriculum level is preceded by one. Architectural placement within the content/path-mode framing is open: candidate placements include its own content mode, a path-mode primitive embedded in Curriculum (matches current state), a roadmap node type prescribable by the agent, or a hybrid. Production is currently human-bottlenecked (live-action hand clips are the slowest step); AI-generation is hard, expensive, and deferred. The architectural placement question clusters with the broader open question of what content classes exist beyond the core three (Exercise, Repertoire, Sight Reading), alongside Open Play (formerly "Free Play original sense"; renamed per Decision #49 Part 2) and Video Library. Theory was previously in this cluster but resolved per Decision #48 as a substrate family within Exercises rather than a separate content mode. See Doc 09 §13.11, Doc 10 §4.3, §6 #15–#16.

---

## Agentic System (Projects, Goals, Paths)

### Project
A goal-bound, AI-mediated path through MuseFlow's content modes, composed by the MuseFlow AI in conversation with the user. A Project has two faces: a **conversational AI surface** for goal-setting and clarification, and a **roadmap container** that holds the structured path. Projects don't contain content directly — their roadmaps reference content that lives in content modes. See Doc 09.

### Goal
A statement of user intent, expressed in natural language, that anchors a Project. Goals can be specific ("learn this piece," "prepare for Grade 5 ABRSM") or general ("get better at hearing jazz progressions"). Goals decompose into roadmap nodes. See Doc 09.

### Roadmap
The structured plan inside a Project. Composed of nodes that reference specific atoms in Exercises, pieces in Repertoire, sight-reading targets (when Sight Reading formalizes as a content mode), or other content. Roadmaps may include AI-generated nodes (custom content created on demand) and may participate in cross-project orchestration. See Doc 09.

### User Path
A custom path authored by a user themselves, without AI involvement and without using a MuseFlow-preset Curriculum. Tagged with `authoring_origin = user`. Naming TBD; alternatives under consideration include "Playlist" and "Plan." See Decision #41.

### Cross-Project Orchestration
The agent's ability to identify overlap between multiple Projects' goals and sequence content in service of multiple goals at once ("air-traffic control"). Steven's framing from the May 5 standup: "If you do this, this will advance you towards three of your goals. If you do this, this will only advance you towards one." See Doc 09.

### Generated Exercise (or Generated Content)
Content produced by the MuseFlow AI (or by MAGE, or by a hybrid system) on demand, in service of a Project goal or a direct user command. Lives in the appropriate content mode tagged with `authoring_origin = agent` (or `user` if the user invoked the generator manually). Accessible via Browse-by-origin filtering and persistent — generated content can be revisited outside the originating Project context.

### Custom Atom
An exercise atom that is not part of MuseFlow's preset catalog. May be authored by a teacher, by a user (via the editor), or generated by the AI. Carries the same identity dimensions as preset atoms (substrate family, input modality, output modality, target variables, pitch reference mode, content scope) plus an `authoring_origin` tag. See Decision #40.

### Engagement Layer
A cross-cutting layer (orthogonal to the three flows) that reads from Project goals, free-exploration patterns, and aggregate skill-progression data, surfacing re-engagement signals and proactive nudges. Andrew Urbanowicz's proposed proactive notification system is the leading anticipated implementation. Specific design TBD. See Decision #19 (amended), Decision #41.

### User-Modeling Layer
The architectural layer that observes, synthesizes, stores, and retrieves user-specific context across sessions. The per-user accumulating user-model is the load-bearing capability that distinguishes MuseFlow structurally from competitor piano-learning products (Simply Piano, Yousician, Skoove, Flowkey), all of which treat the user as roughly anonymous within content. Implementation pattern is closer to a per-user RAG layer over conversation history, exercise/repertoire/sight-reading event data, and AI-extracted summaries than to a single growing markdown file (the "Steven MD file" / "Patrick MD file" framing from the May 7 brainstorm is a user-facing metaphor, not implementation spec). Recognized as a foundational architectural commitment per Decision #47. Distinct from the LLM/agentic-orchestration layer; the two are separable engineering investments. Team ownership is open. See Decision #47, Doc 09 §5.3, §10.5.

### Agent Control Surface
The enumerable set of practice tools, settings, and behaviors the agentic system can manipulate during a session within a given content mode. Each content mode has its own surface. The repertoire surface is enumerated in Decision #46: song position, tempo controls, metronome settings, hand assignment, accuracy controls, audio playback, looping controls, cursor toggle, note names / finger numbers. The exercise surface (training method selection, performance constraints, content scope, blueprint configuration) and sight-reading surface (parameter generation, level construction, game-mode toggles, performance constraints) are sketched. The agent's per-content-mode job is a *policy* over its surface — given Project goal, performance data, and user preferences, decide which surface elements to engage and how to set them. Specific algorithmic patterns (such as auto-looping) bundle several surface elements together. See Decision #46.

### Auto-Looping Algorithm / Perfect-Practice Tree
A first-class algorithmic capability for repertoire practice. Reads the green-note JSON history, identifies the first section with two-or-three-notes-in-a-row errors, dynamically determines loop boundaries (one or two measures before/after the errored section), perfects that section, auto-progresses to the next errored section, and combines perfected sections in a tree structure (small section → small section → combined → next pair → combined → larger combination, recursively). Largely algorithmic; the LLM acts as voice/text "sugar on top" and may override the algorithm for "break the rules" cases (e.g., the actual issue is the previous measure, not the errored one). One capability within the broader repertoire control surface (Agent Control Surface) — not a standalone primitive. Distinct from Optimal Grip (session-level adaptive difficulty operating at a different level) and Game Mode (sight-reading-specific pass-condition mechanics). The load-bearing capability for the engineering-critical step 4 of the integrated investor demo. See Decision #42.

### Diagnostic Agent / Auto-Engaged Plan Mode
The agentic system's behavior of firing follow-up questions until enough context exists to construct a roadmap, when goal-articulation signals are present from the user. The team's framing references Claude Code's auto-engagement of plan mode when a goal is detected. The behavior the team wants is clear; the implementation pattern is open. Two candidate implementations have very different cost / control / failure-mode profiles: **prompt-level** (the system prompt has a "diagnostic" section that activates when the model classifies the user's message as goal-articulation — cheap, flexible, depends on LLM zero-shot classification reliability) and **application-level** (explicit modes between which the user or system navigates, gating available actions/tools — more deterministic, requires explicit UI affordances). Used as a behavioral spec, not an implementation specification. See Doc 09 §4.3, Doc 10 §3.6.

---

## Configurable Assistance

### Mobile-Supported
A property tagged on every atom and blueprint with three values: `full`, `partial`, `none`. Reflects the team's accepted reality that mobile is "a limited experience" and certain atoms (e.g., those requiring physical-keyboard input) cannot be supported on mobile. The user's UI surfaces appropriate atoms based on device capability. See Decision #36, Decision #40.

### Lit-Keys Mode
A configurable assistance level that highlights piano keys on a visual keyboard to show the user what to press. Anticipated to be applicable across many atoms (and across repertoire), not a separate exercise type or blueprint. See Decision #38.

### Completion Handicap
A rule that flags a session as assisted when the user invokes any non-default assistance (e.g., Lit-Keys Mode), affecting completion display or scoring. Steven's framing: "You don't get full credit for really knocking this song out of the park if a possibility exists that you would be cheating the whole time." Preserves the integrity of completion tracking without preventing users from benefiting from assistance when they want it. See Decision #38.

---

## MuseFlow Engineering Concepts

### MAGE (Music Algorithmic Generation Engine)
The MuseFlow codebase containing the algorithmic logic that decides what music to generate, simplify, modify, or analyze. MAGE handles complexity analysis, intentional downgrading of complexity metrics, and other generative operations on music data. **MAGE is distinct from Opusmodus.** Whether MAGE persists as a permanent generative engine that future AI augments, or serves only as training-data scaffolding for an AI that eventually replaces it, is an open architectural question. Steven's working position is augmentation. See Decision #39.

### Opusmodus
A music notation/printing engine integrated with MuseFlow. Opusmodus has no logic of its own — it does only what it is told to do, executing the instructions MAGE provides. **Opusmodus is one word**, frequently miscapitalized as "Opus Modus" in casual conversation. The MAGE / Opusmodus distinction has been confused multiple times in recent team discussions; the names are not interchangeable. Opusmodus = printing engine. MAGE = generative logic.

---