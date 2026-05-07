# MuseFlow Exercise System: Architecture Document

## 1. System Overview

The exercise system is a compositional engine that generates exercises from the intersection of four independent dimensions:

1. **Modality Pair** — Input modality × Output modality (the I/O patch)
2. **Transformation Substrate** — The mental model being trained (what gets processed)
3. **Training Method** — How the user produces their response (the interaction pattern)
4. **Performance Constraints** — The parameters that regulate difficulty and measure fluency (the tech spec envelope)

An exercise is fully specified when all four dimensions are defined. The system's generative power comes from the combinatorial composition of these dimensions.

Each exercise is realized through an **Exercise Blueprint** — a reusable UI/interaction template that defines the screen layout, prompt presentation, response mechanism, and feedback behavior. Multiple exercises with different substrates and content can share the same blueprint if their interaction mechanic is identical. See the Exercise Blueprints Specification for the full blueprint catalog.

---

## 2. Dimension 1: Modality Architecture

### 2.1 The Four Modalities

The system defines four modalities that function as both input (perception) and output (action) channels:

| Modality | As Input (Perception) | As Output (Action) |
|---|---|---|
| **Visual** | Reading notation, chord charts, staff symbols, piano roll, key signature diagrams | Writing/placing notation, drawing on staff, constructing visual representations |
| **Aural** | Hearing pitched sounds, rhythms, chords, scales, dynamics, timbres | Playing piano keys (producing sound), singing, humming, clapping, tapping |
| **Kinesthetic** | Feeling key positions, seeing highlighted keys on onscreen keyboard, hand shape awareness | Pressing physical piano keys, tapping onscreen keyboard, performing motor patterns |
| **Semantic** | Reading text labels — pitch names, interval names, chord symbols, rhythm value names, music theory terms | Producing text labels — naming, selecting from named options, writing verbal answers |

### 2.2 Modality Clarifications

**Semantic as a first-class modality.** Semantic is not merely "the transformation leaking out" — it represents a genuine perceptual and productive mode. Reading the text "C♯" is a categorically different perceptual act from seeing a note on a staff or hearing a pitch. Similarly, producing the label "minor 3rd" is a categorically different action from playing the interval or notating it. Semantic modality handles the **symbolic-linguistic** representation of music, which is essential for theoretical understanding and verbal communication about music.

**Kinesthetic input scope.** In the context of this system's UI, kinesthetic input most commonly means a highlighted key on an onscreen keyboard that the user visually perceives but cognitively processes as a *spatial/positional* input (which key is it?) rather than a *notational* input. In physical playing contexts, kinesthetic input includes proprioceptive feedback — but this falls under the endogenous micro-PTA loop architecture (see Section 6).

**Multi-modal inputs.** Some exercises combine modalities at the input stage (e.g., reading notation while hearing playback simultaneously). These are treated as compositions: `Visual + Aural → Substrate → Output`. The framework supports multi-modal input and output natively.

### 2.3 The Patch Matrix

The modality pair defines the I/O patch for an exercise. The full 4×4 matrix of possible patches:

| | → Visual Out | → Aural Out | → Kinesthetic Out | → Semantic Out |
|---|---|---|---|---|
| **Visual In →** | V→V | V→A | V→K | V→S |
| **Aural In →** | A→V | A→A | A→K | A→S |
| **Kinesthetic In →** | K→V | K→A | K→K | K→S |
| **Semantic In →** | S→V | S→A | S→K | S→S |

Not every cell in this matrix produces a meaningful exercise for every substrate. Same-modality patches (V→V, A→A, K→K, S→S) are often trivial or meaningless — "see a note, write the same note" or "hear a pitch, produce the same pitch" — though some exceptions exist (S→S becomes meaningful when the substrate involves a non-trivial transformation, such as "given the name of a scale degree and key, name the pitch"). The combinatorial matrix is generated first, then pruned.

### 2.4 Pruning Rules for Modality Patches

A modality patch combination is marked N/A (pruned) when:

1. **Identity pass-through**: Input and output are in the same modality AND the substrate involves no meaningful transformation (copying notation, echoing a sound with no cognitive processing).
2. **Substrate irrelevance**: The patch routes around the substrate entirely — e.g., "see two notated notes, play two piano keys" doesn't require interval recognition; it's just two instances of single-note reading.
3. **Redundancy with simpler exercise**: The exercise reduces to a simpler one that already exists in the matrix — e.g., "see a notated interval, play the notes" is just "sight-read two notes," not an interval exercise.
4. **Technical infeasibility**: The exercise requires capabilities the platform cannot support (e.g., assessing sung pitch quality without reliable pitch detection).
5. **Pedagogical emptiness**: The exercise trains no meaningful skill or trains a skill more effectively covered by another combination.

---

## 3. Dimension 2: Transformation Substrate Architecture

### 3.1 Substrate Catalog

Substrates are organized by structural complexity (atomic → molecular → compound) and by FTA dimension (frequency-domain, time-domain, amplitude-domain, or cross-domain).

#### 3.1.1 Frequency-Domain Substrates

**Atomic:**
| Substrate ID | Substrate Name | Transformation | Input → Output |
|---|---|---|---|
| F-A1 | Pitch-name mapping | Map a pitch to/from its letter name | Pitch ↔ Name |
| F-A2 | Pitch-notation mapping | Map a pitch to/from its staff position | Pitch ↔ Staff position |
| F-A3 | Pitch-key mapping | Map a pitch to/from its piano key location | Pitch ↔ Key |
| F-A4 | Pitch-audiation mapping | Map a pitch to/from its sounded/imagined tone | Pitch ↔ Sound |
| F-A5 | Enharmonic equivalence | Recognize that two pitch names refer to the same frequency | Name ↔ Name |
| F-A6 | Accidental application | Apply sharps, flats, naturals to modify a pitch | Pitch + modifier → Pitch |

**Molecular:**
| Substrate ID | Substrate Name | Transformation | Input → Output |
|---|---|---|---|
| F-M1 | Melodic interval recognition | Identify the distance between two sequential pitches | Pitch pair → Interval name/size |
| F-M2 | Harmonic interval recognition | Identify the distance between two simultaneous pitches | Pitch pair → Interval name/size |
| F-M3 | Interval construction | Given a starting pitch and interval, produce the target pitch | Pitch + Interval → Pitch |
| F-M4 | Interval manipulation | Invert, augment, diminish, or compound an interval | Interval + operation → Interval |
| F-M5 | Pitch direction detection | Determine if pitch motion is ascending, descending, or static | Pitch pair → Direction |
| F-M6 | Melodic contour recognition | Identify the shape of a short pitch sequence | Pitch sequence → Contour pattern |

**Compound:**
| Substrate ID | Substrate Name | Transformation | Input → Output |
|---|---|---|---|
| F-C1 | Scale recognition | Identify a scale/mode from its pitch content | Pitch set → Scale name |
| F-C2 | Scale construction | Produce the pitches of a named scale from a given root | Scale name + root → Pitch set |
| F-C3 | Scale degree mapping | Map a pitch to its function within a given scale | Pitch + Scale → Degree |
| F-C4 | Key signature recognition | Identify the key/mode from a key signature | Key signature → Key name |
| F-C5 | Chord quality recognition | Identify a chord's quality from its pitch content | Pitch set → Chord quality |
| F-C6 | Chord construction | Produce the pitches of a named chord quality from a root | Chord symbol → Pitch set |
| F-C7 | Chord inversion identification | Determine which inversion a chord is in | Voiced chord → Inversion label |
| F-C8 | Chord voicing | Select specific pitch arrangements for a chord | Chord symbol + context → Voiced pitch set |
| F-C9 | Chord manipulation | Extend, alter, modify, or transpose a chord | Chord + operation → Chord |
| F-C10 | Chord-scale mapping | Identify which scale(s) a chord implies, or vice versa | Chord ↔ Scale |
| F-C11 | Functional harmony analysis | Assign Roman numeral / functional role to a chord within a key | Chord + Key → Function |
| F-C12 | Chord progression recognition | Identify a sequence of harmonic functions | Chord sequence → Function sequence |
| F-C13 | Secondary dominant/leading-tone recognition | Identify chromatic chords by their tonicizing function | Chord + context → Secondary function |
| F-C14 | Modal harmony analysis | Identify borrowed or modal chord relationships | Chord + tonic → Modal relationship |
| F-C15 | Reharmonization | Generate alternative chord choices for a given melodic/harmonic context | Progression + constraints → New progression |
| F-C16 | Bitonal/polychordal recognition | Identify layered triadic structures | Complex chord → Component labels |

#### 3.1.2 Time-Domain Substrates

**Atomic:**
| Substrate ID | Substrate Name | Transformation | Input → Output |
|---|---|---|---|
| T-A1 | Rhythm value naming | Map a rhythm value to/from its name | Duration ↔ Name |
| T-A2 | Rhythm value notation | Map a rhythm value to/from its notation symbol | Duration ↔ Symbol |
| T-A3 | Rhythm value audiation | Map a rhythm value to/from its sounded/performed duration | Duration ↔ Sound |
| T-A4 | Beat counting | Determine how many beats a rhythm value or sequence occupies | Duration(s) → Beat count |

**Molecular:**
| Substrate ID | Substrate Name | Transformation | Input → Output |
|---|---|---|---|
| T-M1 | Rhythmic cell recognition | Identify common short rhythmic patterns | Rhythm sequence → Pattern name |
| T-M2 | Rhythmic cell construction | Produce a rhythm sequence from a pattern description | Pattern description → Rhythm sequence |
| T-M3 | Metric placement | Identify where within a measure a rhythmic event falls | Rhythm + meter → Beat position |
| T-M4 | Subdivision recognition | Identify the subdivision level of a rhythmic passage | Rhythm → Subdivision type |

**Compound:**
| Substrate ID | Substrate Name | Transformation | Input → Output |
|---|---|---|---|
| T-C1 | Meter recognition | Identify the time signature / metric framework | Rhythm pattern → Meter |
| T-C2 | Rhythm sequence recognition | Identify a complete rhythmic pattern within a measure or phrase | Sounded/notated rhythm → Notation/name |
| T-C3 | Polyrhythm recognition | Identify layered rhythmic patterns | Multi-layer rhythm → Component patterns |
| T-C4 | Hypermeter and phrase structure | Identify larger-scale metric groupings | Extended rhythm → Phrase boundaries |
| T-C5 | Tempo recognition | Identify or reproduce a specific tempo | Pulse → BPM / BPM → Pulse |
| T-C6 | Song form recognition | Identify structural sections (verse, chorus, bridge, etc.) | Musical passage → Form labels |

#### 3.1.3 Amplitude-Domain Substrates

> **Deferral note:** Amplitude substrates are fully specified in the architecture to maintain FTA completeness, but amplitude-specific exercises (AMP-### family) are **deferred beyond V1**. The schema supports them; they will be implemented when programmatic assessment of dynamics becomes reliable.

**Atomic:**
| Substrate ID | Substrate Name | Transformation | Input → Output |
|---|---|---|---|
| A-A1 | Dynamic level recognition | Identify a loudness level | Sound/symbol → Dynamic name (pp, p, mp, mf, f, ff) |
| A-A2 | Dynamic marking reading | Map a dynamic symbol to its meaning | Symbol → Loudness level |
| A-A3 | Accent recognition | Identify accented vs. unaccented events | Sound → Accent pattern |

**Molecular:**
| Substrate ID | Substrate Name | Transformation | Input → Output |
|---|---|---|---|
| A-M1 | Dynamic contour recognition | Identify crescendo, decrescendo, subito changes | Sound sequence → Contour description |
| A-M2 | Articulation weight mapping | Map articulation markings to their dynamic/timbral effect | Marking → Execution quality |
| A-M3 | Relative dynamic comparison | Compare loudness levels between two events | Sound pair → Relative dynamic |

**Compound:**
| Substrate ID | Substrate Name | Transformation | Input → Output |
|---|---|---|---|
| A-C1 | Phrase-level dynamic shaping | Recognize or produce the dynamic arc of a musical phrase | Phrase → Dynamic contour |
| A-C2 | Dynamic balance (voicing) | Manage relative loudness between simultaneous voices | Multi-voice texture → Balance profile |

#### 3.1.4 Cross-Domain Substrates

| Substrate ID | Substrate Name | Transformation | Domains |
|---|---|---|---|
| X-1 | Note reading (full) | Pitch + rhythm simultaneously | F + T |
| X-2 | Sight-reading | Real-time note reading with performance constraints | F + T + (A) |
| X-3 | Score interpretation | Reading all musical parameters from a score | F + T + A |
| X-4 | Fingering selection | Choosing optimal finger assignments for a passage | F + T + Kinesthetic |
| X-5 | Expressive performance | Integrating dynamics, timing, and tone quality | F + T + A |

### 3.2 Substrate Interaction Model

Substrates do not exist in isolation. A single exercise may engage multiple substrates in sequence or in parallel:

- **Sequential chaining**: A chord progression exercise chains F-C5 (chord quality recognition) → F-C11 (functional analysis) → F-C12 (progression recognition).
- **Parallel loading**: Sight-reading engages F-A2 (pitch-notation mapping) + T-A2 (rhythm-value notation) + F-A3 (pitch-key mapping) simultaneously, which is a core driver of cognitive load.

The number and complexity of substrates engaged in an exercise directly maps to the "multithreading" performance constraint.

---

## 4. Dimension 3: Training Method Architecture

### 4.1 The Training Method Spectrum

Training methods are ordered from most-scaffolded to least-scaffolded:

| Level | Method | Code | User Action | Cognitive Demand |
|---|---|---|---|---|
| 1 | **Verification** | VER | Judge whether a presented answer is correct or incorrect | Evaluative recognition — lowest production demand |
| 2 | **Recognition** | REC | Select the correct answer from a limited set of options | Discriminative recognition — answer is visible |
| 3 | **Selection** | SEL | Select all correct answers from a larger field | Exhaustive discriminative recognition |
| 4 | **Assembly** | ASM | Arrange provided components into the correct order/structure | Constructive sequencing — parts are given, arrangement is not |
| 5 | **Alteration** | ALT | Modify existing material to meet new specifications | Transformative construction — starting point given, target must be derived |
| 6 | **Recall** | RCL | Produce the answer from memory with no scaffolding | Generative retrieval — nothing given |
| 7 | **Performance** | PRF | Execute the answer physically in real time | Real-time motor generation — no scaffolding, temporal pressure |

### 4.2 Method-Substrate Compatibility

Not every training method is meaningful for every substrate. Compatibility guidelines:

- **Atomic substrates** typically support Verification, Recognition, and Recall. Assembly and Alteration are less relevant because atomic units don't have internal structure to rearrange.
- **Molecular substrates** support the full range. Assembly becomes meaningful (arrange two pitches to form an interval). Alteration becomes meaningful (modify an interval to change its quality).
- **Compound substrates** are where Assembly and Alteration shine. Constructing a scale from degrees, reharmonizing a progression, re-voicing a chord — these are inherently assembly/alteration tasks.
- **Performance** is available for any substrate that has a kinesthetic/aural output, regardless of complexity level.

### 4.3 Training Method Progression Model

The training path for any given substrate follows a standard progression:

```
Verification → Recognition → Selection → Assembly → Alteration → Recall → Performance
```

Users enter this progression at the level appropriate to their current mastery of the substrate. Optimal Grip™ scoring determines the appropriate entry point and advancement pace.

A user might start with Recognition (multiple choice) for a new substrate, advance to Recall (free generation) once accuracy is high, and progress to Performance (real-time execution with tempo constraints) once recall is fluent.

---

## 5. Dimension 4: Performance Constraint Architecture

### 5.1 The Tech Spec Model

Performance constraints model the technical limitations and capabilities of the user's cognitive system. They are the parameters that make the same exercise easier or harder without changing the musical content.

### 5.2 Constraint Definitions and Exercise Parameters

| Tech Spec Concept | Exercise Parameter(s) | What It Measures |
|---|---|---|
| **Processing Speed** | Tempo, response time limit, prompt pacing | How fast the user can move through the full PTA loop |
| **Working Memory (RAM)** | Sequence length, information scarcity (hiding information after initial display), number of elements to hold simultaneously | How much musical data the user can hold in active cognition |
| **Long-term Memory (Cache)** | Spaced repetition intervals, recognition-without-recomputation speed | How effectively pre-computed results are stored and retrieved |
| **Multithreading** | Number of active FTA dimensions, number of simultaneous substrates, multi-voice textures | How many parallel PTA loops the user can sustain |
| **Compression (Chunking)** | Pattern density, material that rewards chunk-level recognition, long sequences with internal repetition | How effectively the user groups elements into higher-order units |
| **Bottleneck Targeting** | Stage-specific stress tests — perception-only drills, transformation-only drills, execution-only drills | Identifying which PTA stage is the weakest link |
| **Error Tolerance** | Accuracy thresholds, allowed mistakes per exercise, retry policy | Precision requirements for completion |
| **External Conditions** | Time of day, session duration, break frequency, fatigue modeling | Environmental and physiological factors |

### 5.3 Difficulty Scaling

Difficulty in the exercise system is a function of three independent axes:

1. **Substrate complexity** — Atomic → Molecular → Compound → Cross-domain
2. **Training method scaffolding** — Verification → Performance (decreasing scaffolding)
3. **Performance constraint tightness** — Loose (slow tempo, long time, many retries) → Tight (fast tempo, strict time limits, no retries)

These three axes are orthogonal, meaning they can be adjusted independently. A user might work on a compound substrate (high complexity) with Recognition method (high scaffolding) and loose constraints — or an atomic substrate (low complexity) with Performance method (no scaffolding) and tight constraints. Both are valid exercises at different points in the training landscape.

### 5.4 Adaptive Difficulty (Optimal Grip™)

> **Phasing note:** Optimal Grip™ is a V2 feature. For V1, users manually select exercises and configure difficulty parameters. The architecture supports adaptive difficulty from the start so that V2 can layer it on without structural changes.

The Optimal Grip™ system uses performance data to position the user at the intersection of these three axes where they are maximally challenged but still succeeding more often than failing. It adjusts:

- Which substrates to present (based on mastery levels)
- Which training methods to use (based on substrate mastery progression)
- Which performance constraints to apply (based on speed/accuracy trends)
- Which FTA dimensions to combine (based on multithreading capacity)

---

## 6. Endogenous Micro-PTA Loop Architecture

> **Deferral note:** Exercises that explicitly train the micro-PTA loop (play with eyes closed, error recovery drills, motor automaticity drills) are **deferred beyond V1**. The micro-PTA loop is a valid theoretical component of the framework, but dedicated exercises targeting it add complexity that may not be warranted initially. The architecture is documented here for completeness; implementation is deferred pending validation of the core exercise system.

### 6.1 Structure

During the Action stage of any exercise involving physical performance (playing keys, singing, tapping), the user's nervous system runs a continuous feedback loop:

```
Macro-PTA:  Perception → Transformation → Action
                                            │
                                            ▼
Micro-PTA:                        ┌─── Micro-P ◄── Visual feedback (seeing hands)
                                  │                  Aural feedback (hearing output)
                                  │                  Kinesthetic feedback (feeling keys)
                                  │
                                  ├─── Micro-T ──── Validate: correct or incorrect?
                                  │                  If incorrect: compute correction
                                  │
                                  └─── Micro-A ──── Adjust motor execution
                                                     Feed back into Macro-A
```

### 6.2 Micro-PTA Training Implications

The micro-loop can be trained explicitly through exercises that:

- **Stress kinesthetic awareness**: Play with eyes closed (remove visual micro-P, force reliance on kinesthetic micro-P)
- **Stress aural monitoring**: Play while hearing a reference and self-correcting in real time
- **Train error recovery speed**: Exercises that measure recovery time after a wrong note, not just accuracy
- **Train motor automaticity**: High-tempo performance exercises where the micro-loop must run faster than conscious correction allows, forcing embodied/cached motor patterns

---

## 7. Exercise Generation Pipeline

### 7.1 Generation Process

To generate the full exercise catalog, the system follows this pipeline:

```
1. Select a SUBSTRATE (from the substrate catalog)
2. Enumerate all valid INPUT FORMATS for that substrate
3. For each input format, enumerate all valid OUTPUT FORMATS
4. Map each input format to its PERCEPTION MODALITY
5. Map each output format to its ACTION MODALITY
6. Apply PRUNING RULES to eliminate invalid/empty/redundant patches
7. For each surviving patch, enumerate compatible TRAINING METHODS
8. For each exercise, define the available EXERCISE CONFIGURATION parameters
9. For each exercise, define the applicable PERFORMANCE CONSTRAINT parameters
10. Assign each exercise to an EXERCISE BLUEPRINT based on its interaction mechanic
```

### 7.2 Substrate → Format Mapping

Each substrate defines its own set of valid input and output formats:

| Substrate Family | Input Formats | Output Formats |
|---|---|---|
| **Single Pitch** | Named pitch, Notated pitch, Selected/highlighted key, Sounded pitch | Named pitch, Notated pitch, Selected/played key, Sung/sounded pitch |
| **Single Rhythm** | Named rhythm value, Notated rhythm, Sounded rhythm | Named rhythm value, Notated rhythm, Played rhythm, Sounded rhythm |
| **Interval** | Named interval, Notated interval, Selected keys, Sounded interval | Named interval, Notated interval, Selected/played keys, Sung/sounded pitches |
| **Scale** | Named scale, Notated scale, Highlighted keys, Sounded scale, Key signature + mode | Named scale, Notated scale, Played scale, Named scale degrees |
| **Chord** | Named chord, Notated chord, Highlighted keys, Sounded chord, Chord symbol | Named chord quality, Notated chord, Played chord, Named inversion |
| **Chord Progression** | Named progression (Roman numerals), Notated progression, Sounded progression | Named progression, Notated progression, Played progression |
| **Rhythm Sequence** | Notated rhythm sequence, Sounded rhythm sequence, Named rhythm pattern | Notated rhythm sequence, Played rhythm sequence, Named beat count |

---

## 8. Data Model Summary

> **Note:** The exercise data model is evolving. The atom/molecule/strand/cluster hierarchy defined in the UX & Navigation Specification (Document 07) refines the exercise identity model described here. The schemas below should be read in conjunction with that document.

### 8.1 Exercise Atom Schema

An exercise atom is the smallest indivisible unit of distinct practice. See UX & Navigation Spec, Section 2.1 for full definition.

```
ExerciseAtom {
  id: string
  substrate_family: SubstrateFamily
  input_modality: Modality
  output_modality: Modality
  target_variables: TargetVariable[]       // what's being assessed (quality, inversion, root, etc.)
  pitch_reference_mode: enum [relative, absolute, n_a]
  content_scope: ContentScopeLevel         // position in the strand's difficulty ladder
  blueprint: BlueprintID                   // determined by output modality + training method
  available_training_methods: TrainingMethod[]  // inherited from output modality
  available_performance_constraints: ConstraintSet
  substrates_engaged: SubstrateID[]        // which substrates from the catalog are involved
  fta_dimensions: Dimension[]
  gmtf_complexity: number                  // from existing GMTF system (V2)
  requires_perfect_pitch: boolean          // derived from pitch_reference_mode
  requires_physical_instrument: boolean
  notes: string
}
```

### 8.2 Exercise Instance Schema

An exercise instance is a specific, playable configuration of an atom:

```
ExerciseInstance {
  atom_id: string
  training_method: TrainingMethod
  configuration: ConstraintValues          // specific values for all constraint params
  session_shape: SessionShape              // prompt count, timed/untimed
  prompt_material: MusicalContent          // generated prompts for this instance
  distractor_material: DistractorSet       // generated distractors (for REC/VER methods)
  expected_responses: ResponseSpec[]       // what constitutes correct answers
}
```

### 8.3 Exercise Result Schema

An exercise result records what happened when a user completed an exercise instance. This is the atomic measurement unit for exercise analytics.

```
ExerciseResult {
  instance_id: string
  atom_id: string
  user_id: string
  timestamp: datetime
  training_method_used: TrainingMethod
  completion_status: enum [completed, abandoned, timed_out]
  accuracy_score: number                   // 0.0–1.0
  response_time_ms: number
  errors: Error[]
  constraint_values: ConstraintValues
  session_context: {
    session_id: string
    position_in_session: number
    session_duration_so_far_ms: number
    time_of_day: string
  }
}
```

---

## 9. Cross-Section Complexity Language

### 9.1 The Problem

MuseFlow has three major sections (Curriculum, Exercises, Repertoire) that each generate performance data about the user's skill level. For the app to function as a coherent system — where progress in one section informs recommendations in another — these sections must share a **common vocabulary for complexity**.

### 9.2 Existing System: GMTF

The GMTF complexity scoring system already exists in the MuseFlow codebase (GMTF repo). This system provides the foundation for cross-section complexity tagging. Rather than inventing a new complexity language, the exercise system should integrate with GMTF.

> **Action required**: Map the exercise atom framework to GMTF scores. Each exercise atom should carry a GMTF-derived complexity tag based on its content scope, target variables, and substrate family. The exact mapping needs to be defined in collaboration with engineering.

### 9.3 Cross-Section Linking

The GMTF complexity scores enable:

- **Exercise → Curriculum linking**: "User struggled with exercises at complexity level N; suggest curriculum review of the level where that complexity was introduced."
- **Exercise → Repertoire linking**: "User has mastered exercises at complexity level N; recommend repertoire pieces at or slightly above that level."
- **Curriculum → Exercise linking**: "User just completed a curriculum level introducing dominant 7th chords; recommend exercises that drill F-C5 and F-C6 with dominant 7th configurations."
- **User Skill Rating (ELO)**: A composite rating computed from performance across all three sections, weighted by the GMTF complexity of the content attempted.

> **Phasing note:** GMTF integration with exercises is a V2 feature. For V1, exercises are tagged with substrate family and content scope level, which provides basic filtering. Full GMTF tagging enables cross-section recommendations.

---

## 10. Exercise Blueprint Architecture

### 10.1 Blueprint Concept

An Exercise Blueprint is a reusable UI/interaction template that defines the screen layout, prompt presentation, response mechanism, and feedback behavior for a class of exercises. Multiple exercises from the taxonomy share a single blueprint when their interaction mechanic is identical, regardless of their substrate or musical content.

Blueprints are the primary unit of work for both **UI/UX design** (each blueprint = one screen type to design) and **engineering** (each blueprint = one interaction template to build). Musical content is plugged into blueprints at runtime.

The full blueprint catalog is specified in the Exercise Blueprints Specification document.

### 10.2 Blueprint Selection

Each exercise in the taxonomy is assigned to a blueprint based on its combination of perception modality, action modality, and training method. The mapping is deterministic:

```
Blueprint = f(perception_modality, action_modality, training_method, multi_modal_flag)
```

This means that when a new exercise is generated from the framework, its blueprint assignment is automatic — no design decision is needed per exercise.
