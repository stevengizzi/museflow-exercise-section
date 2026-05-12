# MuseFlow Exercise System: UX & Navigation Specification

> **Status: Working Draft.** This document captures the current state of UX and navigation thinking for the exercise section. Several elements are proposals under review, not finalized decisions. Open questions are flagged inline and collected in Section 9.

---

## 1. Overview

This document specifies how users navigate, discover, configure, and track progress through the exercise section. It bridges the abstract exercise architecture (substrates, modalities, training methods, performance constraints) with the concrete user experience.

The core challenge: the combinatorial exercise space is vast (potentially 500–2,000 distinct exercise atoms), but any individual user session is focused on a small region. The framework must be **wide in storage, narrow in presentation, and progressive in revelation**.

---

## 2. The Exercise Hierarchy

The exercise space is organized into four levels of granularity, from most specific to most general.

### 2.1 Exercise Atom

The smallest indivisible unit of "this is a distinct thing you can practice." An atom is defined by:

```
Exercise Atom = {
  substrate_family,         // e.g., Chords
  input_modality,           // e.g., Aural
  output_modality,          // e.g., Semantic
  target_variables,         // e.g., [quality, inversion]
  pitch_reference_mode,     // e.g., relative
  content_scope             // e.g., major & minor triads only
}
```

Two atoms that differ on *any* of these properties are different atoms. Each atom represents a fundamentally distinct skill to practice.

**What is NOT part of the atom's identity** (these are practice-mode configurations applied to an atom):
- Training method (REC, VER, ASM, RCL, PRF, etc.)
- Performance constraints (speed, memory load, error tolerance, etc.)
- Session shape (number of prompts, timed vs. untimed)

Each atom inherits a set of **available training methods** from its output modality and blueprint mapping. It also inherits available **performance constraints** from its blueprint. These aren't part of the atom's identity, but they are properties of the atom.

#### Atom Identity Dimensions Explained

**Substrate Family**: What musical content is being trained (Pitches, Intervals, Scales, Chords, Chord Progressions, Rhythm Sequences, etc.).

**Input Modality**: How the user receives the prompt. User-facing labels:
| Internal | User-Facing |
|---|---|
| Aural | "By Ear" |
| Visual (notation) | "By Reading" |
| Kinesthetic (keyboard diagram) | "By Keyboard Diagram" |
| Semantic (text/name) | "By Name / Description" |

**Output Modality**: How the user produces their response. User-facing labels:
| Internal | User-Facing |
|---|---|
| Semantic | "Identify / Name It" |
| Visual (notation) | "Notate It" |
| Kinesthetic + Aural (piano) | "Play It" |
| Kinesthetic (screen tap) | "Tap It" |
| Aural (voice) | "Sing It" (deferred) |

**Target Variables**: What specifically is being assessed. For chords, this could be:
- Quality only (major/minor/dim/aug)
- Inversion only
- Quality + Inversion
- Root + Quality (requires perfect pitch or reference)
- Root + Quality + Inversion (requires perfect pitch or reference)

For intervals: size only, size + quality, direction + size + quality, etc.
For rhythms: pattern identification, beat counting, subdivision identification, etc.

**Pitch Reference Mode**: Whether absolute pitch identification is required.
- **Relative**: Root/reference is provided or irrelevant; trains relative pitch skills
- **Absolute**: Root/reference must be identified; requires or trains perfect pitch
- **N/A**: Not applicable (rhythm-only exercises, theory computation)

**Content Scope**: The specific musical material in the pool, arranged as a difficulty level within a strand. For chords: major/minor only → all triads → 7th chords → extended. For intervals: perfect intervals → diatonic intervals → all intervals → compound intervals.

#### 2.1.5 Atom Identity Confirmed Single-Substrate (per Decisions #25, #57, #58)
 
The atom-identity model defined above carries **exactly one primary substrate** per atom. This is preserved across the K-substrate family admission (Decision #57): K-substrate atoms have a K-substrate as their primary substrate; cognitive substrate atoms (F-, T-, A-, X-) have a cognitive substrate as their primary substrate. No atom has two primary substrates. Multi-substrate engagement is handled at a separate architectural layer (the **semi-lattice substrate-engagement layer**, Decision #58), which is computable at agent-reasoning time from existing atom identity dimensions and is NOT stored as a schema field. See Architecture Doc §3.2.1 for full treatment.
 
The slogan: **tree for users, semi-lattice for the agent.** Navigation, mastery tracking, and atom identity stay tree-structured for human comprehensibility. The agentic system reasons over the richer semi-lattice for cross-mode roadmap composition. Both layers coexist; neither dominates.

### 2.2 Exercise Molecule

A cluster of atoms that share the same substrate family, input modality, output modality, and content scope. Atoms within a molecule differ only on target variables and pitch reference mode.

**User-facing concept**: A molecule is "one box of related exercises at a specific difficulty level." For example, "Major & Minor Triads by Ear → Identify" is a molecule containing atoms for quality-only, quality+inversion, and (optionally, for users with perfect pitch) exact chord identification.

**Molecule example — "Major & Minor Triads × Ear Training × Identify":**
| Atom | Target Variables | Pitch Reference | Difficulty |
|---|---|---|---|
| Identify quality | [quality] | Relative | Primary |
| Identify inversion | [inversion] | Relative | Secondary |
| Identify quality + inversion | [quality, inversion] | Relative | Secondary |
| Identify exact chord | [root, quality] | Absolute | Bonus (PP) |
| Identify exact chord + inversion | [root, quality, inversion] | Absolute | Bonus (PP) |

**Atom ordering within a molecule**: Atoms within a molecule have a natural difficulty progression from fewer target variables to more. The first atom (simplest target variable set, relative pitch) is the **primary atom** — it's the default when a user enters the molecule, and it's the one that must be cleared for the molecule to count as "complete."

### 2.3 Exercise Strand

An ordered sequence of molecules that share the same substrate family, input modality, and output modality, but differ on content scope. A strand is a **difficulty ladder** — a progression from easiest to hardest content scope.

**User-facing concept**: A strand is "one learning path." For example, "Chords by Ear → Identify" is a strand containing molecules for major/minor triads → all triads → 7th chords → extended chords.

**Strand example — "Chords × Ear Training × Identify":**
1. Major & Minor Triads (molecule, containing quality-only, quality+inversion, exact chord atoms)
2. All Triad Qualities (molecule, same atom structure)
3. Seventh Chords (molecule, same atom structure but with 7th chord target variables)
4. Extended Chords (molecule)

### 2.4 Exercise Cluster

A group of strands that share the same substrate family (when grouped by substrate) or the same input modality (when grouped by modality). Clusters are the top-level navigation unit.

**Substrate-grouped clusters**: Pitches, Intervals, Scales, Chords, Chord Progressions, Rhythms
**Modality-grouped clusters**: Ear Training, Note Reading, Keyboard Skills, Music Theory, Sight-Playing, Transcription

Both groupings lead to the same atoms — they are different traversal paths through the same graph.

### 2.5 Hierarchy Summary

```
Cluster (substrate family OR modality group)
  └─ Strand (substrate + input modality + output modality)
       └─ Molecule (strand + content scope level)
            └─ Atom (molecule + target variables + pitch reference mode)
```

---

## 3. Navigation Model

### 3.1 The Three-Screen Flow

**Screen A — The Exercise Home / Universe**
The entry point to the exercise section. Contains three zones:

1. **Hook zone** (top): Engagement-oriented content — suggested practice, daily focus, recently attempted exercises, teacher assignments (future). In V1, this could be as simple as "Continue where you left off" and a featured/rotating exercise.

2. **Mirror zone** (middle): Progress overview showing the user's coverage across clusters. Visual representation (progress rings, fill indicators, constellation map, or similar) that makes gaps obvious and invites exploration. The user can toggle between substrate-grouped and modality-grouped views here.

3. **Library zone** (bottom / main area): The full browsable, filterable exercise catalog. Shows clusters, and can be zoomed into strands, molecules, and atoms. Filtering and sorting available across multiple dimensions: substrate family, modality, difficulty, completion status.

The universe is navigable through **progressive zoom**: Cluster → Strand → Molecule → Atom. But the user can also see a flat/filtered view of all atoms or all strands if they prefer. The zoom is an option, not a requirement.

**Screen B — Exercise Detail / Configuration**
Reached by tapping a specific atom (or a molecule, which defaults to its primary atom). Contains:

1. **Exercise description**: What this exercise is, in plain language. Brief animated preview or one-sentence explainer of the interaction.

2. **History panel**: Past performance on this atom — attempts count, best score, last attempt date, scores over time. Also shows which training methods have been completed and at what mastery tier.

3. **Configuration panel**: Pre-filled with sensible defaults, expandable for customization.
   - **Training method selector**: Available methods for this atom, with mastery state visible per method.
   - **Performance constraints**: Speed/tempo, response time window, number of choices (for REC), replays allowed, error tolerance. Only shows constraints applicable to the selected training method and blueprint.
   - **Session shape**: Number of prompts, timed vs. untimed.

4. **Start button**: Launches the exercise with current configuration.

**Screen C — The Exercise**
The blueprint screen. The user is actively practicing. When finished, a **results overlay** appears showing:
- Score and accuracy
- Comparison to previous best
- Training method mastery progress update (if applicable)
- Suggested next actions: "Try Again," "Adjust & Retry" (returns to Screen B), "Next Challenge" (suggests the next atom in the molecule or next molecule in the strand), "Back to Library"

### 3.2 Navigation Shortcuts

Not every session requires full universe traversal. Common shortcuts:

- **"Continue" from Hook zone**: Goes directly to Screen B for the user's most recent atom.
- **Deep link from recommendations**: Goes directly to Screen B for a specific suggested atom.
- **Search / quick filter**: User types "chords" or "ear training" in the library and immediately sees matching strands/atoms.
- **From results screen**: "Next Challenge" jumps directly to Screen B for the next logical atom.

---

## 4. Configuration Model

### 4.1 What's Configurable vs. What's Identity

| Dimension | Part of Atom Identity? | User-Configurable? |
|---|---|---|
| Substrate family | Yes | No — chosen by navigating to the atom |
| Input modality | Yes | No — chosen by navigating to the atom |
| Output modality | Yes | No — chosen by navigating to the atom |
| Target variables | Yes | No — chosen by navigating to the atom |
| Pitch reference mode | Yes | No — chosen by navigating to the atom |
| Content scope | Yes | No — chosen by navigating to the atom (the molecule level) |
| Training method | No | Yes — selected on Screen B |
| Performance constraints | No | Yes — adjusted on Screen B |
| Session shape | No | Yes — adjusted on Screen B |

### 4.2 User-Facing Configuration Options

Organized by category, with user-friendly labels:

**Training Method** (presented as "Practice Mode" or similar):
| User-Facing Label | Internal Code | Description |
|---|---|---|
| "True or False" | VER | Judge if a presented answer is correct |
| "Multiple Choice" | REC | Pick from options |
| "Select All" | SEL | Pick all correct answers |
| "Build It" | ASM | Arrange components in order |
| "Modify It" | ALT | Change existing notation to match |
| "From Memory" | RCL | Produce the answer with no hints |
| "Play It" | PRF | Perform on your instrument |

**Performance Constraints** (presented as "Difficulty Settings" or similar):
| User-Facing Label | Internal | Applicable Blueprints |
|---|---|---|
| "Speed" / "Tempo" | Processing Speed | BP-05, BP-06, BP-08 |
| "Time Limit" | Response time window | BP-01, BP-02, BP-10 |
| "Number of Choices" | Answer Optionality | BP-01, BP-02, BP-04, BP-10, BP-11, BP-12 |
| "Replays Allowed" | Memory Load (replays) | BP-01, BP-07, BP-08, BP-11, BP-12 |
| "Sequence Length" | Memory Load (length) | BP-07, special configs |
| "Accuracy Required" | Error Tolerance | All |

**Session Shape:**
| User-Facing Label | Internal |
|---|---|
| "Quick" | 10 prompts |
| "Standard" | 20 prompts |
| "Deep Practice" | 50 prompts |
| "Endless" | No limit, user stops when ready |

### 4.3 Defaults and Presets

Every atom ships with a **default configuration**: a sensible training method (usually the easiest applicable one), moderate performance constraints, and a standard session length. The user can accept defaults and start immediately.

> **Open question**: Should atoms also have named presets beyond the default? E.g., "Easy / Medium / Hard" presets that adjust constraints? Or is the training method selector + individual constraint sliders sufficient? See Section 9.

---

## 5. Progress Tracking Model

### 5.1 Atom-Level Progress

For each atom, the system tracks:

**Per training method**:
- Mastery state: Untouched → Attempted → Cleared (met accuracy threshold) → Mastered (cleared at tighter constraints)
- Best accuracy score
- Best speed (if timed)
- Number of attempts
- Last attempt date

**Aggregate**:
- Number of training methods cleared / available
- Primary training method mastery state (used for molecule-level rollup)

### 5.2 Molecule-Level Progress

A molecule's progress is derived from its atoms:

- **Incomplete**: No atoms cleared
- **Complete**: Primary atom cleared (simplest target variable set, relative pitch)
- **Advanced**: Multiple atoms cleared, including secondary atoms
- **Mastered**: All applicable atoms cleared (excluding perfect-pitch-only atoms for users without perfect pitch)

### 5.3 Strand-Level Progress

A strand's progress is derived from its molecules:

- Shows how far up the content scope ladder the user has progressed
- "Current level" = highest molecule that's Complete or above
- Visual indicator (progress bar, path with nodes, etc.) showing all molecules in the strand and their states

### 5.4 Cluster-Level Progress

Aggregate across strands:
- Number of strands with any activity
- Average/total progress across strands
- Visual indicator for the Universe View (progress ring, fill amount, etc.)

### 5.5 Section-Level Metrics

An Exercise Metrics view (accessible from the Exercise Home but separate from the main flow) provides:

- Overall exercise statistics: total time, total attempts, overall accuracy trend
- Substrate coverage heatmap: where are strengths, where are gaps
- Modality coverage: balance between ear training, reading, playing, theory
- Training method distribution: does the user always do multiple choice and never free recall?
- Recent activity timeline
- (V2) ELO / skill rating
- (V2) Personalized recommendations based on gap analysis

**Note on engagement layer (May 2026):** Atom and molecule progress events — atoms cleared, molecules completed, time-since-last-practice, completion-state changes — are anticipated to be consumed by a cross-cutting engagement layer (the proactive nudging system Andrew Urbanowicz described in the April 28 standup) and by the agentic Project system. The Exercise Result schema (Architecture Doc §8.3) is the source-of-truth data primitive; ensuring it is persisted in a queryable location is sufficient at V1, no additional event-emission infrastructure required. See Decision #19 amendment.

### 5.6 Perfect Pitch Handling

Atoms with `pitch_reference_mode = absolute` are tagged as **perfect pitch atoms**. These atoms:

- Are **hidden by default** from users who haven't opted into perfect pitch training
- Are **excluded from completion calculations** — a molecule can be "Complete" and "Mastered" without clearing its perfect pitch atoms
- Appear as **bonus challenges** for users who enable perfect pitch mode in their profile settings
- When visible, are displayed with a distinct visual indicator (icon, badge, or color) so the user understands they're optional

Users can enable/disable perfect pitch mode at any time. Enabling it reveals the additional atoms and adds them as optional goals; disabling it hides them and removes them from progress calculations without losing any stored progress data.

---

## 6. Distractor and Content Generation Logic

### 6.1 Training Method Inheritance

Each atom inherits its available training methods from the combination of its output modality and its target variables. This is deterministic:

| Output Modality | Available Training Methods |
|---|---|
| Semantic (name/identify) | VER, REC, SEL (where applicable), RCL |
| Visual (notate) | VER, REC, ALT, RCL |
| Kinesthetic + Aural (play) | PRF |
| Kinesthetic (tap) | PRF |
| Aural (sing — deferred) | PRF |

Assembly (ASM) is available when the output involves ordering or constructing from components — primarily for progression ordering, scale degree sequencing, and rhythm construction.

### 6.2 Distractor Generation Rules

For Recognition (REC) exercises, the distractor options are generated according to rules derived from the atom's target variables and pitch reference mode:

**Principle**: Distractors hold constant everything that is NOT a target variable, and vary what IS a target variable.

| Target Variables | Pitch Ref | Distractor Rule |
|---|---|---|
| [quality] | Relative | Same root, same inversion → vary quality |
| [inversion] | Relative | Same root, same quality → vary inversion |
| [quality, inversion] | Relative | Same root → vary quality and inversion |
| [root, quality] | Absolute | Vary root and quality |
| [root, quality, inversion] | Absolute | Vary root, quality, and inversion |

For Verification (VER) exercises, the system generates a proposed answer that is either correct or one distractor-rule-violation away from correct.

For Alteration (ALT) exercises, the pre-populated starting material is determined by what the user does NOT need to modify, and the modification targets are the target variables.

### 6.3 Content Scope as Difficulty Ladder

Within each strand, content scope levels are ordered by pedagogical difficulty. The exact progressions are substrate-family-specific and need to be authored. Template examples:

**Intervals content scope progression:**
1. Perfect intervals (P4, P5, P8)
2. Perfect + Major/Minor 3rds
3. All diatonic intervals with qualities (m2, M2, m3, M3, P4, P5, m6, M6, m7, M7, P8)
4. All simple intervals including tritone
5. Compound intervals (9ths, 10ths, etc.)

**Chords content scope progression:**
1. Major and Minor triads only
2. All triad qualities (major, minor, diminished, augmented)
3. Suspended chords added (sus2, sus4)
4. Seventh chords (maj7, min7, dom7, half-dim7, dim7)
5. All seventh chord qualities (minMaj7, augMaj7, etc.)
6. Extended chords (9ths, 11ths, 13ths)

**Scales content scope progression:**
1. Major and Natural Minor
2. All major modes (Dorian, Phrygian, Lydian, Mixolydian, Aeolian, Locrian)
3. Melodic and Harmonic minor
4. Melodic/Harmonic minor modes
5. Symmetric scales (whole tone, diminished)
6. Pentatonic and Blues scales

**Rhythm content scope progression:**
1. Quarter and half notes only
2. Add eighth notes
3. Add dotted rhythms
4. Add sixteenth notes
5. Add syncopation
6. Add tuplets

These progressions need review and refinement by Steven and the team.

### 6.4 K-Substrate Atoms — Distractor Pattern Differs
 
The distractor generation logic in §6.2 is designed for cognitive substrates with multiple-choice or constructive output (Recognition, Verification, Alteration training methods). For **K-substrate atoms** (motor-primary; Decision #57), the training method is almost exclusively Performance (PRF), and assessment is on motor execution quality — evenness, tempo compliance, articulation crispness, pedal-change cleanness — rather than on selection among distractors.
 
K-substrate atoms therefore do not generate distractors in the §6.2 sense. They are assessed against execution criteria appropriate to the motor pattern being trained. Specific assessment dimensions for each K-substrate are Track D catalog-authoring work; this section flags the general principle.
 
Cross-references: Architecture Doc §3.1.5 (K-substrate family); Architecture Doc §5 (Performance Constraint Architecture — the assessment-dimension catalog will likely extend here); Decision #57 (K-substrate family admission).

---

## 7. Blueprint Mapping

Each atom maps to exactly one blueprint based on its output modality and training method:

| Output Modality | Training Method | Blueprint |
|---|---|---|
| Semantic | REC | BP-01 (if input is Aural) or BP-02 (if input is Visual/Kinesthetic) or BP-10 (if input is Semantic) |
| Semantic | VER | BP-10 (True/False variant) |
| Semantic | RCL | BP-10 (free entry variant) |
| Semantic | ASM | BP-07 |
| Semantic | SEL | BP-01 or BP-02 (select-all variant) |
| Visual (notation) | REC | BP-12 (if input is Aural) or BP-02 variant |
| Visual (notation) | ALT | BP-09 (if modifying existing) or BP-03 (if constructing) |
| Visual (notation) | RCL | BP-03 |
| Kinesthetic + Aural | PRF | BP-05 |
| Kinesthetic (screen tap) | PRF | BP-06 (if rhythm) or BP-04 (if key selection) |
| Aural (voice) | PRF | BP-13 (deferred) |
| Multi-modal (A+V input) | SEL/REC | BP-08 |
| Aural (match audio) | REC | BP-11 (if input is Visual) |

---

## 8. Agentic Exercise System (Active R&D Track)

> **Note**: This section describes an active R&D track being driven jointly by Steven and Staley, targeted at investor-demo readiness as part of the $1.5M raise. The atom framework in this document was designed with this track's requirements in mind. Specific phasing within the exercise section's V1/V2/V3 roadmap is TBD and will be addressed in subsequent design phases. The freestanding **MuseFlow Agentic Vision** document (Doc 09) covers this system in depth; this section captures the implications for the exercise section specifically.

### 8.1 The Core Idea

Users describe their goals in natural language (e.g., "I want to prepare for my Grade 5 ABRSM exam," "Help me learn to play this piece," "I want to get better at hearing jazz chord progressions"), and the MuseFlow AI builds out a personalized **Project** containing:

- A goal definition with context
- An assessment of the user's current skill level (using exercise atom mastery data, repertoire performance data, and curriculum progress)
- A custom **roadmap** from current state to goal mastery, composed of nodes that reference:
  - Specific exercise atoms to complete (drawing from the exercise hierarchy)
  - Repertoire to practice (drawing from the Repertoire content mode)
  - Sight-reading targets (drawing from the Curriculum, or — when Sight Reading formalizes as its own content mode — directly from Sight Reading)
  - Custom-generated exercises for gaps not covered by the standard exercise catalog (see §8.3)

Projects are one of three **path modes** in MuseFlow's architecture (alongside Curriculum and User Paths — see Project Bible §2.1). They sit alongside, not above, the other path modes; AI-averse users can engage fully with the product without invoking the Project flow.

### 8.2 Why the Atom Framework Supports This

The exercise atom model was designed with agent prescribability as a first-class requirement:

- **Atoms are the right granularity for an agent to prescribe.** "Practice this specific atom until you clear it at the Recall level" is a complete, executable instruction. Coarser granularity (e.g., "practice chords") leaves the agent's intent ambiguous; finer granularity (individual prompts) is below the level the agent should reason at.
- **The hierarchy provides navigable structure.** "This user needs work on the Chords × Ear Training cluster, specifically molecules 3 and 4 in the strand" is a coherent agent-level statement.
- **The progress tracking model provides the data the agent reads.** Per-atom mastery state, per-method clearance, and the Exercise Result schema (Architecture Doc §8.3) give the agent everything it needs to assess current state and measure improvement.
- **The atom schema includes agent-prescribability metadata** (Architecture Doc §8.1, Decision #40): `prerequisite_atoms` for path-building, `mastery_thresholds` for clearance criteria, `mobile_supported` for device-aware prescription, and `authoring_origin` for distinguishing system, teacher, user, and agent-authored atoms.

### 8.3 Exercise Generation on Demand (Decision #33)

Exercises are inherently combinatorial — atoms are defined by patches across modalities, substrates, target variables, and content scope. This makes generation on demand a natural extension of the existing architecture, distinct from selection from a fixed catalog.

Three generation triggers are anticipated:

- **User-triggered**: a user requests a custom exercise targeting specific skills or constraints from inside the Exercise content mode's **Generate** flow
- **Teacher-triggered**: a teacher generates an exercise (typically via the repertoire editor surface, see §8.5) to assign to a student
- **Agent-triggered**: the MuseFlow AI generates an exercise as part of a Project roadmap, in service of a goal-specific gap

Generated exercises are first-class citizens of the Exercise content mode, tagged with `authoring_origin` (system / teacher / user / agent) and accessible via Browse-by-origin filtering. They persist beyond the originating context — a Project-generated atom can be revisited outside the Project, and a teacher-generated atom can be assigned to multiple students.

Steven's framing on why this is tractable (May 5 standup): exercises are easier to generate than repertoire because they don't carry stylistic-fidelity constraints — they are "variations on scales and chords and stuff."

### 8.4 Custom Authoring Paths (Decision #34)

Beyond agent-generated exercises, three additional authoring paths are anticipated:

- **User authoring**: a user constructs a custom exercise atom via parameter selection (substrate, modality, target variables, content scope) or via the repertoire editor surface
- **Teacher authoring**: a teacher constructs custom exercises through the same surface, with the ability to assign them to specific students
- **Community authoring** (future): exercises shared between users, eventually via a marketplace

The repertoire editor (Andrew's May 5 demo) is the natural authoring surface for content of any kind. Specific UX for exercise authoring (vs. repertoire authoring) within the editor is open; see §8.6.

### 8.5 Where Projects Live in the Navigation

The Project flow is reachable from two entry points:

- **Top-level Projects dashboard** (proposed): a parallel-navigation surface where users see all their Projects, zoom into individual ones, and review roadmap progress. Sibling to the content-mode entry points (Exercises Home, Repertoire Home, etc.).
- **Inside each content mode**: when a user is browsing or generating within a content mode, they can pivot to the Project flow ("ask MuseFlow to build a roadmap that includes this kind of practice").

The dashboard's specific UX — how Projects are listed, how roadmaps render, how cross-Project orchestration is visualized, how zoom-in works — is open. See §8.6 and Doc 09.

### 8.6 Open Architectural Questions for the Agentic System

The following questions are explicitly open and shape ongoing design work:

1. **Where does the Project flow live in the navigation?** A top-level Projects dashboard, an entry point inside each content mode, both, or some other configuration. (Lean: both — see §8.5.)
2. **What metadata do atoms need beyond the current schema for full agent prescribability?** The five fields added in Decision #40 (`prerequisite_atoms`, `mastery_thresholds`, `mobile_supported`, `authoring_origin`, `generation_mode`) are the load-bearing additions. Whether further metadata is needed (e.g., tags expressing pedagogical role, agent-readable descriptions) is open and may surface during catalog authoring.
3. **Generation on demand UX**: who triggers, with what input, what gets generated, and how is the result surfaced? Three triggers (user, teacher, agent) imply at least three distinct flows. Specific UX is unspecified.
4. **Custom atom authoring UI**: how does the editor → atom flow work? Where do custom atoms live (private library, shareable, gradeable)? How are user-authored atoms validated for pedagogical coherence?
5. **MAGE's long-term role** (Decision #39, amended per Decision #44, formally closed per Decision #53): augmentation framing is canon — MAGE persists as a permanent algorithmic generation engine, with the AI adjusting MAGE's music-XML output for musicality, stylistic fitness, and goal-specific shaping. The May 7, 2026 Emergent Curriculum brainstorm produced directional alignment across Steven, Patrick, and Staley (Patrick articulating the AI-adjusts-MAGE-output mechanism, Steven concurring, Staley not pushing back). Decision #53 (Track B Phase 3, 2026-05-12) retired the procedural "awaits-Staley-explicit-confirmation" caveat that had held the open-question status open; the question is formally resolved.
6. **Cross-Project orchestration**: how is the agent's "air-traffic control" view (sequencing across multiple Project goals) surfaced to the user? Is it visible when zooming into individual Projects, or only at the dashboard level?
7. **Engagement layer integration**: how do Project goals and roadmap progress interact with the engagement/nudging layer (Decision #19 amendment)? Re-engagement triggered by Project deadlines vs. by Project-agnostic activity patterns?
8. **Pedagogical safety**: an AI generating exercises and roadmaps could produce pedagogically unsound combinations. What guardrails or review layers prevent this?
9. **Pricing/tier gating** (Decision #37): not currently encoded in the schema. When pricing is designed, decisions about Project access, generation volume limits, and custom atom limits will need to be made.

These questions will be addressed as the agentic vision matures. The atom-framework decisions made in this document should remain stable regardless of how these questions resolve — the architecture is intended to absorb all answers without restructuring.

---

## 9. Open Questions

The following questions are unresolved and should be addressed in subsequent design sessions:

### Navigation & UX
1. **Universe visual metaphor**: What does the cluster/strand/molecule/atom hierarchy look like visually? Planetary orbits, constellation map, skill tree, folder structure, or something else? Needs design exploration.
2. **Zoom vs. flat**: Should the Library zone always start at the cluster level and require progressive zoom-in, or should users be able to toggle between a zoomed/hierarchical view and a flat/filtered list view?
3. **Toggle between substrate-grouped and modality-grouped**: How does this toggle work in the UI? Two tabs? A dropdown? Does it restructure the whole page or just re-sort?
4. **Exercise card design**: What information does each card show at each level of the hierarchy? How much progress detail is visible before tapping in?

### Configuration
5. **Named presets vs. individual sliders**: Should performance constraints be presented as named difficulty presets ("Easy / Medium / Hard"), individual configurable sliders, or both? Presets are simpler; sliders give more control. Could presets be the default view with an "Advanced" toggle revealing sliders?
6. **Configuration persistence**: When a user adjusts settings for an atom, do those settings persist for next time, or reset to defaults? Per-atom persistence could be convenient but adds data storage complexity.

### Progress & Completion
7. **Mastery tier system**: Should progress within an atom be tracked as a simple cleared/not-cleared per training method, or should there be sub-tiers within each method (e.g., "cleared Multiple Choice at Easy," "cleared Multiple Choice at Hard")? More tiers = more granularity but more visual complexity.
8. **Completion incentives**: What visual reward system marks progress? Stars, badges, checkmarks, fill colors, numeric scores? Needs design exploration aligned with MuseFlow's brand.
9. **Streak and gamification**: How does streak tracking interact with the exercise atom system? Daily streak across any exercise? Per-strand streaks? Per-atom consistency tracking?

### Content Authoring
10. **Content scope progressions**: The exact difficulty ladders for each substrate family need to be authored and reviewed for pedagogical accuracy. Who does this authoring — Steven, or can it be partially automated?
11. **Distractor quality**: The distractor generation rules provide structure, but specific distractor selection within those rules affects exercise quality. Are distractors randomly selected from valid options, or curated to target common confusions?
12. **Total atom count**: How many atoms does the V1 exercise section contain? This depends on how many substrate families × modality combinations × content scope levels × target variable sets are included. An enumeration exercise is needed.

### Architecture
13. **Atom/Molecule/Strand/Cluster naming**: Are these the right names for internal and/or external use? They're useful metaphors for the team, but users should never see "atom" or "molecule." What are the user-facing equivalents?
14. **GMTF integration**: The existing GMTF complexity scoring system in the codebase needs to be mapped to the exercise atom framework. How does a GMTF score attach to an atom? Is it derived from the content scope, the target variables, or both?
15. **Custom atom creation**: For the agentic future vision, the system needs to support creating new atoms that aren't in the standard catalog. What are the constraints on atom creation? Can any valid combination of the identity dimensions produce an atom, or are there additional validation rules?

### Scope
16. **V1 exercise catalog**: Which substrate families, modality combinations, and content scope levels ship in V1? This is the most important scoping question and determines the total build effort.
17. **Micro-PTA exercises**: Should exercises that explicitly train the endogenous micro-PTA loop (play with eyes closed, error recovery drills, etc.) be included in V1 or deferred? *(Resolved by Decision #24 — deferred beyond V1; formally retired from open-question inventory per Track B Phase 3, 2026-05-12.)*

### Mode Architecture (added May 2026 from standups)
18. **Default Browse view**: When a user enters a content mode's Browse flow, do they see all content together (with origin tags visible) or only MuseFlow presets, with custom/AI/community content opt-in? AI-averse users argue for preset-default; full-power users argue for all-mixed-default. Open.
19. **User Paths naming**: "User Paths" is a placeholder. Alternatives include "Playlists" (familiar music-app metaphor) and "Plans." User-facing name TBD.
20. **Mobile parity per blueprint**: Each of the 13 blueprints needs a `mobile_supported` value (`full` / `partial` / `none`). Default values per blueprint are unspecified and will be set during catalog authoring (Track D). See Decisions #36, #40.

### Pricing & Gating (added May 2026)
21. **Pricing structure**: Tier ideas were floated (free / mid / premium at $15.99) but no structure is committed. Until pricing is designed, no atom-, blueprint-, or capability-level gating decisions can be made. See Decision #37.
22. **Are exercises gated by tier?** If so, by atom, by blueprint, by training method, by feature category, or some combination? Open until pricing structure exists.
23. **Generation volume limits**: AI-generated exercise content has inference cost. Whether on-demand generation is unlimited, rate-limited, or premium-gated is open.

### Agentic System (added May 2026 — see also §8.6)
24. **Project flow entry points**: A top-level Projects dashboard, an entry point inside each content mode, both, or some other configuration? Lean is "both."
25. **Generation-on-demand UX**: User-triggered, teacher-triggered, and agent-triggered generation are likely distinct flows. Specific UX is unspecified.
26. **Custom atom authoring UI**: how does the editor → atom flow work? Where do custom atoms live (private library, shareable, gradeable)? How are user-authored atoms validated for pedagogical coherence?
27. **MAGE's long-term role**: *Resolved by Decision #44 (augmentation direction) and Decision #53 (procedural caveat retired, 2026-05-12).* The May 7, 2026 Emergent Curriculum brainstorm produced directional alignment across Steven, Patrick, and Staley toward the augmentation framing — MAGE persists as a permanent algorithmic generation engine, with the AI adjusting MAGE's music-XML output. Decision #53 closed Decision #39's open-question status; the question is formally resolved. See Doc 09 §10.3.

### Teacher Tools (added May 2026)
28. **Teacher → student data visibility**: Teachers should see student progress per atom / molecule / strand / cluster. Specific UX (per-student dashboard, class roster view, etc.) is unspecified.
29. **Assignment flows**: Teachers should assign atoms / molecules / strands / paths to specific students. Whether assignment is a first-class object (with deadlines, completion tracking, teacher feedback) or lighter-weight (just a "recommended" tag) is open.
30. **Custom exercise sharing**: Teacher-authored exercises can presumably be shared with students. Whether they can be shared more broadly (all of a teacher's students, all teachers, public marketplace) is open.

### Cross-cutting (added May 2026)
31. **Lit-Keys Mode applicability**: Which atoms and blueprints support Lit-Keys assistance? Default values per blueprint are unspecified. See Decision #38.
32. **Completion handicap behavior**: When the user invokes any non-default assistance, the session is flagged as assisted. How does this affect display (asterisk, visual flag, separate "assisted-clear" state) and downstream computation (does an assisted clear count toward molecule completion)? Open.
33. **Cross-mode performance-constraints UI**: Per Decision #43, performance constraints are a cross-content-mode primitive (exercises, sight reading, repertoire). The UI vocabulary should be consistent enough that a user recognizes a constraint they've configured in one mode when they encounter it in another, but specific enough to each mode that the affordances make sense locally. The shared-vs-mode-specific UX pattern is open. See Bible §6.3, Architecture Doc §5.1, Doc 09 §6A.

### Agentic UX & Onboarding (added May 2026 — post-May-7 brainstorm)
34. **Voice/text default modality for AI feedback**: Voice vs. text vs. both, configurable per user, configurable per content mode? Steven OK with text-first per Doc 09 §6.5. Default behavior in V1 of voice-feedback capability is undefined.
35. **Vertical roadmap visualization details**: Working direction is vertical tree with branching (Doc 09 §7.2). Specific rendering details remain open: pan/zoom across long roadmaps, mobile rendering, progress indicators, node-state visualization.
36. **Onboarding path-split logic**: Multiple onboarding paths exist (Projects-first per Staley's May 7 framing; exploration-first; possibly others). How does the system decide which path to surface to which user? Chooser, default rule, declared user type at signup, or some combination? See Doc 09 §12.2 item 5.
37. **Token-based pricing surfacing**: Do users see token meters directly (Staley: "we could even surface tokens directly")? Or opaque "AI generations remaining"? Different UX implications. See Doc 09 §13.9 #46, Doc 09 §16.
38. **Game Mode / Free Play toggle collapse**: Current Sight Reading curriculum levels have Game Mode and Free Play toggles (existing app functionality). As the new content/path mode architecture is implemented, these may subsume into other functionality — Decision #49 Part 1 specifically extends the Free Play side of this pattern into the Exercise content mode as a completion-policy element of the exercise control surface. UX consolidation pattern across modes remains open. Distinct from Open Play original-sense status (deferred per Decision #41; renamed from "Free Play original-sense" by Decision #49 Part 2).

### Content Class Placement (added May 2026 — post-May-7 brainstorm)
39. **Interactive Tutorial UX placement**: Per Doc 09 §13.11 #52. Interactive Tutorials are existing canonical content (animated video + live-action hand clips + Phaser-JS exercises gated mid-flow), but their architectural placement is open. The UX question: where do tutorials live in navigation? Inside Curriculum only (current state)? Browsable as their own content surface? Surfaced as roadmap nodes within Projects (per Doc 09 §5.2 candidate node type)? Hybrid? Clusters with #40.
40. **Tutorial-as-roadmap-node UX**: If Interactive Tutorials become a roadmap-node type, how is the node rendered, how is mid-tutorial state persisted across sessions, and how do completion criteria interact with surrounding nodes? Sub-question of #39. See Doc 09 §13.11 #55.