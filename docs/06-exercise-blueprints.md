# MuseFlow Exercise System: Exercise Blueprints Specification

## 1. Overview

This document defines the **Exercise Blueprints** — the reusable UI/interaction templates that exercises are built from. Each blueprint specifies a distinct screen type with its own prompt presentation, response mechanism, and feedback behavior.

Blueprints are the primary unit of work for two audiences:

- **UI/UX Design**: Each blueprint = one screen type to design. Designers produce a screen layout, visual language, animation/transition behavior, and responsive variants for each blueprint.
- **Engineering**: Each blueprint = one interaction template to build. Engineers implement the prompt rendering, input capture, response validation, scoring logic, and data recording for each blueprint.

Musical content is authored separately and plugged into blueprints at runtime. A single blueprint can serve dozens of different exercises from the taxonomy — what changes is the content, not the interaction.

### 1.1 How Blueprints Relate to the Architecture

Each blueprint is determined by a combination of:

- **Perception Modality** (how the prompt is presented)
- **Action Modality** (how the user responds)
- **Training Method** (the interaction mechanic)
- **Multi-modal flag** (whether input combines multiple modalities)

Exercises from the taxonomy that share the same combination of these four properties share the same blueprint. The substrate and musical content vary; the screen does not.

### 1.2 Blueprint Entry Format

Each blueprint entry includes:

- **ID and Name**
- **Interaction Pattern**: What the user sees, what they do, what happens
- **Screen Components**: The UI elements required
- **PTA Classification**: Which modality patches this blueprint serves
- **FTA Dimensions**: Which dimensions of the FTA field this blueprint can operate in
- **Training Methods**: Which methods from the seven-level spectrum this blueprint implements
- **Performance Constraints**: Which tech-spec parameters apply and how they manifest in the UI
- **Taxonomy Coverage**: Which exercise IDs from the taxonomy map to this blueprint
- **Content Requirements**: What musical content must be authored or generated for exercises using this blueprint
- **Feedback Model**: How correctness is assessed and communicated to the user
- **Design Notes**: UI/UX considerations specific to this blueprint

---

## 2. Blueprint Catalog

---

### BP-01: Listen → Label

**The ear training workhorse. Audio plays, user picks from text options.**

#### Interaction Pattern
1. System plays an audio prompt (a pitch, interval, chord, scale, rhythm, or progression).
2. A set of labeled text options appears on screen (2–8 options, depending on configuration).
3. User taps the option they believe is correct.
4. System provides immediate feedback (correct/incorrect) and optionally replays the audio.
5. Next prompt loads.

#### Screen Components
- Audio playback control (play/replay button)
- Grid or list of tappable text option buttons
- Feedback indicator (correct/incorrect state on the selected option)
- Progress indicator (current prompt number / total)
- Score display (running accuracy)

#### PTA Classification
| Perception | Transformation | Action |
|---|---|---|
| **Aural** | Any substrate where the input is sounded and output is a label | **Semantic** |

Specific patches: A→S

#### FTA Dimensions
- **Frequency**: Pitch identification, interval naming, chord quality, scale mode, chord-scale implication, functional analysis
- **Time**: Rhythm value naming, beat division identification, tempo identification
- **Amplitude** (deferred): Dynamic level identification

#### Training Methods
- **Recognition (REC)**: Standard multiple choice — select one correct answer
- **Selection (SEL)**: Select-all-that-apply variant — multiple correct answers possible

#### Performance Constraints
| Constraint | How It Manifests |
|---|---|
| Speed | Time limit per prompt; auto-advance after timeout |
| Memory Load | Number of elements in the audio prompt (single note → melody); delay between prompt and response options appearing |
| Error Tolerance | Number of allowed incorrect attempts per prompt; accuracy threshold for exercise completion |
| Answer Optionality | Number of multiple-choice options (fewer = easier, more = harder) |

#### Taxonomy Coverage
P-014, R-003, R-006, R-007, INT-003, INT-007, INT-008, SC-004, SC-005 (Recognition variant), SC-012, CH-004, CH-005, CH-011, CP-001, CP-003, CP-004, CP-005, CP-007, CP-011, CP-012, RS-001, RS-012, AMP-002 (deferred), AMP-003 (deferred), AMP-004 (deferred), AMP-007 (deferred)

This is the single most populated blueprint — it covers the vast majority of ear training exercises.

#### Content Requirements
- Audio clips or real-time audio generation for every prompt
- Correct answer label for each prompt
- Distractor labels for multiple-choice options (pedagogically appropriate — common confusions, not random)
- Metronome track where rhythm exercises require it

#### Feedback Model
- Immediate: selected option highlights green (correct) or red (incorrect)
- On incorrect: correct answer highlights; optional audio replay
- End of exercise: summary score (accuracy %, time, streak data)

#### Design Notes
- Audio playback must be prominent and easily re-triggerable (users will replay frequently)
- Option buttons should be large enough for comfortable tapping on mobile
- For Selection (SEL) variant, add a "Submit" step after selections are made
- Consider a "reference tone" persistent indicator for exercises that use a reference pitch

---

### BP-02: Read → Label

**The theory identification standard. Notation or diagram shown, user picks from text options.**

#### Interaction Pattern
1. System displays a visual prompt (notated pitch, interval, chord, scale, key signature, or keyboard diagram).
2. A set of labeled text options appears on screen.
3. User taps the option they believe is correct.
4. System provides immediate feedback.
5. Next prompt loads.

#### Screen Components
- Visual prompt area (staff renderer, keyboard diagram renderer, or both)
- Grid or list of tappable text option buttons
- Feedback indicator
- Progress and score displays

#### PTA Classification
| Perception | Transformation | Action |
|---|---|---|
| **Visual** or **Kinesthetic** | Any substrate where the input is visual/spatial and output is a label | **Semantic** |

Specific patches: V→S, K→S

#### FTA Dimensions
- **Frequency**: Note naming, interval identification from notation, chord quality from notation, scale identification, key signature identification
- **Time**: Rhythm value naming from notation

#### Training Methods
- **Recognition (REC)**: Standard multiple choice

#### Performance Constraints
| Constraint | How It Manifests |
|---|---|
| Speed | Time limit per prompt |
| Memory Load | Sequence length (how many notes/chords in the prompt); flash-and-hide (show notation briefly, then cover it) |
| Error Tolerance | Accuracy threshold; retry policy |
| Prompt Assistance | Staff position labels on/off; ledger line hints on/off |

#### Taxonomy Coverage
P-005, P-009, P-010, P-012, P-013, R-004, INT-005, INT-006, SC-001, SC-002, SC-003, SC-009, SC-011, CH-001, CH-002, CH-003, CP-009

#### Content Requirements
- Rendered notation for each prompt (pitch, rhythm, interval, chord, scale, key signature)
- Keyboard diagrams with highlighted keys where applicable
- Correct answer label and distractor labels

#### Feedback Model
- Same as BP-01: immediate highlight on selected option
- Optional: highlight the correct element on the notation/diagram as part of feedback

#### Design Notes
- Staff rendering must be clean and scalable across screen sizes
- For keyboard-input exercises (K→S), the onscreen keyboard diagram is the prompt, not a response mechanism
- Clef, key signature, and accidental display are configuration-driven

---

### BP-03: Label → Staff Placement

**The construction workbench. Text prompt given, user places or modifies notes on an interactive staff.**

#### Interaction Pattern
1. System displays a text prompt (e.g., "Place the note C♯ on the treble clef staff" or "Add accidentals to form a D Dorian scale").
2. An interactive staff is rendered. Depending on the exercise, it may be blank or pre-populated with some notes.
3. User taps/drags to place notes on the staff, add accidentals, or modify existing notation.
4. User submits their answer.
5. System validates against the expected answer and provides feedback.

#### Screen Components
- Text prompt area
- Interactive staff with tap/drag note placement
- Accidental palette (sharp, flat, natural buttons)
- Submit button
- Feedback overlay showing correct vs. submitted answer

#### PTA Classification
| Perception | Transformation | Action |
|---|---|---|
| **Semantic** | Construction or alteration substrates (building notation from a name/description) | **Visual** |

Specific patches: S→V

#### FTA Dimensions
- **Frequency**: Pitch construction, interval construction, scale construction, chord construction, key signature construction

#### Training Methods
- **Recall (RCL)**: Blank staff — place notes from scratch
- **Alteration (ALT)**: Pre-populated staff — modify existing notes to meet new specifications (add accidentals, transpose, invert)

#### Performance Constraints
| Constraint | How It Manifests |
|---|---|
| Speed | Time limit for construction |
| Memory Load | Hide the prompt after initial display; multi-note construction from memory |
| Error Tolerance | Strict (exact match required) vs. lenient (partial credit for partially correct placements) |

#### Taxonomy Coverage
P-001 (RCL), P-002, INT-001 (ALT), INT-009 (ALT), SC-006, SC-010, CH-006

#### Content Requirements
- Text prompt specifying what to construct or how to alter
- Expected note positions on the staff (for validation)
- Pre-populated staff content (for Alteration exercises)
- Clef and key signature context

#### Feedback Model
- On submit: side-by-side or overlay comparison of submitted vs. correct placement
- Highlight correctly placed notes in green, incorrectly placed in red, missing notes in outline
- For Alteration: show which modifications were correct and which were missed

#### Design Notes
- Staff interaction must feel natural on touch devices — tap to place, drag to reposition
- Accidental buttons should be contextually positioned near the note being modified
- Support undo/redo for multi-step construction
- This is one of the more complex blueprints to implement — prioritize clean interaction design

---

### BP-04: Label → Key Selection

**Onscreen keyboard targeting. Text prompt given, user taps the correct key on a virtual keyboard.**

#### Interaction Pattern
1. System displays a text prompt (e.g., "Tap the key for E♭" or "Tap the keys that form a C minor chord").
2. An interactive onscreen piano keyboard is rendered.
3. User taps the key(s) they believe are correct.
4. System provides immediate feedback.

#### Screen Components
- Text prompt area
- Interactive onscreen piano keyboard (scrollable/zoomable for range)
- Feedback state on each key (correct/incorrect highlight)
- Progress and score displays

#### PTA Classification
| Perception | Transformation | Action |
|---|---|---|
| **Semantic** | Pitch-key mapping, chord construction, interval construction | **Kinesthetic** |

Specific patches: S→K

#### FTA Dimensions
- **Frequency**: Pitch-to-key, interval-to-keys, chord-to-keys, scale-to-keys

#### Training Methods
- **Recognition (REC)**: Tap one correct key from the full keyboard (essentially multiple choice with many options)
- **Selection (SEL)**: Tap all correct keys (for chords, scales)

#### Performance Constraints
| Constraint | How It Manifests |
|---|---|
| Speed | Time limit per prompt |
| Memory Load | Hide prompt after display; multi-note recall |
| Keyboard Range | Restrict visible keyboard range (narrows the "search space") |

#### Taxonomy Coverage
P-003, INT-002 (REC), SC-007 (onscreen variant), CH-007 (onscreen variant)

#### Content Requirements
- Text prompt specifying the target key(s)
- Correct key position(s) for validation
- Keyboard range configuration

#### Feedback Model
- Tapped key highlights green (correct) or red (incorrect)
- For multi-key exercises: all correct keys highlight on submit

#### Design Notes
- Keyboard must be large enough to tap accurately on mobile — this may require a scrollable/zoomable keyboard
- Consider highlighting the target octave region to reduce spatial search difficulty for beginners
- Distinct from BP-05 (physical keyboard) — this is entirely onscreen

---

### BP-05: Prompt → Physical Key Performance

**The MIDI bridge. A prompt is given (text, notation, or audio), user plays the answer on their physical instrument.**

#### Interaction Pattern
1. System displays a prompt — this could be text (semantic), notation (visual), or audio (aural), depending on the exercise.
2. User plays the answer on their physical piano/MIDI keyboard.
3. System captures MIDI input and validates against the expected response.
4. System provides immediate feedback (correct/incorrect note, timing accuracy).

#### Screen Components
- Prompt area (text, staff renderer, or audio playback — varies by exercise)
- MIDI input indicator (shows what notes the system is receiving)
- Real-time feedback overlay (note-by-note correct/incorrect as played)
- Metronome (for rhythm-based exercises)
- Progress and score displays

#### PTA Classification
| Perception | Transformation | Action |
|---|---|---|
| **Semantic**, **Visual**, or **Aural** | Any substrate involving pitch-to-key or rhythm-to-performance mapping | **Kinesthetic + Aural** (pressing a key produces sound) |

Specific patches: S→K+A, V→K+A, A→K+A

#### FTA Dimensions
- **Frequency**: Playing named pitches, notated pitches, heard pitches, intervals, chords, scales
- **Time**: Playing named rhythms, notated rhythms, heard rhythms
- **Frequency + Time**: Sight-reading (notation → performance), chord chart reading

#### Training Methods
- **Performance (PRF)**: Real-time motor execution

#### Performance Constraints
| Constraint | How It Manifests |
|---|---|
| Speed | Tempo / BPM requirement; metronome enforced |
| Memory Load | Sequence length; flash-and-hide prompts (memorize then play) |
| Error Tolerance | Wrong-note tolerance (strict = any wrong note fails; lenient = percentage threshold); timing tolerance (how far off-beat is acceptable) |
| Continuous Mode | Play without stopping — exercise doesn't pause between prompts |

#### Taxonomy Coverage
P-004, P-006 (PRF), P-011, P-016 (PRF), R-002, R-005, R-009, INT-002 (PRF), INT-004 (PRF — singing variant excluded, see BP-13), SC-007, CH-007, CH-008, CP-008, CP-010, RS-006, RS-007, RS-008, RS-013, RS-014, RS-015, X-001 through X-006

This is the most important blueprint for MuseFlow's core value proposition — it's where the app connects to the physical instrument.

#### Content Requirements
- Prompt material (text, notation, or audio depending on the exercise)
- Expected MIDI note sequence with timing data for validation
- Tolerance parameters for pitch and timing validation
- Metronome configuration

#### Feedback Model
- Real-time: each note played highlights as correct (green) or incorrect (red) immediately
- For rhythm exercises: timing accuracy shown as early/late/on-beat indicator
- End of exercise: summary with accuracy %, timing accuracy, note-by-note breakdown

#### Design Notes
- MIDI connection setup must be frictionless — this is a potential drop-off point
- Real-time feedback must have minimal latency to feel responsive
- For continuous/sight-reading mode, the display scrolls or advances automatically
- This blueprint encompasses the widest range of exercises because physical performance is the ultimate output for many substrate families
- Subsumes exercises with semantic, visual, AND aural prompts — the prompt area is polymorphic

---

### BP-06: Listen → Rhythm Tap

**Rhythm reproduction via screen tap. Audio plays (with metronome), user taps the rhythm back on screen.**

#### Interaction Pattern
1. System plays a rhythm pattern with an audible metronome.
2. Metronome continues; user taps a button or the screen to reproduce the rhythm.
3. System captures tap timing and validates against the expected rhythm.
4. Feedback on timing accuracy.

#### Screen Components
- Audio playback control
- Metronome with visual beat indicator
- Large tap target area (button or full-screen tap zone)
- Timing feedback visualization (timeline showing expected vs. actual tap positions)
- Progress and score displays

#### PTA Classification
| Perception | Transformation | Action |
|---|---|---|
| **Aural** | Rhythm reproduction / rhythm memory | **Kinesthetic** (screen tap, not piano key) |

Specific patches: A→K (non-pitched)

#### FTA Dimensions
- **Time**: Exclusively time-domain — rhythm values, beat patterns, tempo

#### Training Methods
- **Performance (PRF)**: Real-time rhythmic execution

#### Performance Constraints
| Constraint | How It Manifests |
|---|---|
| Speed | Metronome tempo / BPM |
| Memory Load | Sequence length; number of beats to reproduce; delay between hearing and reproducing |
| Error Tolerance | Timing tolerance window (how many milliseconds off-beat is acceptable) |

#### Taxonomy Coverage
RS-006 (tap variant), RS-007 (clap variant — same blueprint, different physical action), RS-008, RS-013, RS-014

#### Content Requirements
- Rhythm patterns (as onset timing sequences against a metronome grid)
- Metronome configuration (tempo, time signature)
- Timing tolerance parameters

#### Feedback Model
- Real-time: visual pulse on each tap
- Post-attempt: timeline visualization showing expected onsets vs. actual tap times
- Accuracy score based on timing deviation

#### Design Notes
- Tap latency is critical — even small delays make rhythm exercises feel wrong
- Tap target should be very large (ideally the majority of the screen)
- Visual metronome should be prominent and clearly synchronized with audio
- Distinct from BP-05 because no MIDI input is needed — just screen taps. This makes it accessible to users without a physical keyboard.

---

### BP-07: Listen → Sequence Assembly

**The ordering puzzle. Audio plays, user arranges provided tiles into the correct sequence.**

#### Interaction Pattern
1. System plays an audio prompt (a chord progression, scale degree sequence, melodic contour, or groove pattern).
2. A set of labeled tiles/chips appears in a scrambled order.
3. User drags/reorders the tiles into the sequence they heard.
4. User submits their arrangement.
5. System validates and provides feedback.

#### Screen Components
- Audio playback control
- Draggable tile/chip area with labeled options
- Drop zone / sequence track showing current arrangement
- Submit button
- Feedback overlay showing correct vs. submitted sequence

#### PTA Classification
| Perception | Transformation | Action |
|---|---|---|
| **Aural** | Sequence recognition and ordering | **Semantic** (ordering labels) or **Visual** (ordering notation tiles) |

Specific patches: A→S (ordering labels), A→V (ordering notation)

#### FTA Dimensions
- **Frequency**: Chord progression ordering, scale degree sequencing
- **Time**: Rhythm sequence construction from component tiles
- **Frequency + Time**: Melodic contour ordering

#### Training Methods
- **Assembly (ASM)**: Arrange provided components into correct order

#### Performance Constraints
| Constraint | How It Manifests |
|---|---|
| Speed | Time limit for assembly |
| Memory Load | Number of elements to order; replays allowed vs. limited |
| Sequence Length | Number of tiles (3–8+) |

#### Taxonomy Coverage
CP-002, CP-006, SC-005, RS-003, RS-011, RS-016

#### Content Requirements
- Audio prompt (progression, scale, rhythm)
- Set of tile labels representing the components to order
- Correct sequence for validation

#### Feedback Model
- On submit: each tile position highlights green (correct) or red (incorrect position)
- Optional: show the correct sequence alongside the submitted one
- Replay audio with the correct sequence highlighted

#### Design Notes
- Drag-and-drop must feel natural on mobile (consider tap-to-select + tap-to-place as an alternative to drag)
- Tiles should be clearly labeled and large enough to manipulate easily
- Replay button should be easily accessible during assembly

---

### BP-08: Listen + Read → Error Detection

**The spot-the-difference exercise. Audio plays while notation is shown, user identifies mismatches.**

#### Interaction Pattern
1. System simultaneously plays an audio track and displays notation on screen.
2. The notation intentionally contains errors (missing notes, wrong notes, wrong rhythms) relative to the audio.
3. User taps the notated elements that don't match the audio.
4. User submits their selections.
5. System reveals the correct mismatches.

#### Screen Components
- Audio playback control (synced with notation cursor/highlight)
- Interactive staff renderer with tappable note elements
- Selected-element indicator (highlights on tapped notes)
- Submit button
- Feedback overlay

#### PTA Classification
| Perception | Transformation | Action |
|---|---|---|
| **Aural + Visual** (simultaneous multi-modal) | Error detection, comparison | **Visual** (selecting notated elements) |

Specific patches: A+V→V

#### FTA Dimensions
- **Frequency + Time**: Comparing heard pitch/rhythm against notated pitch/rhythm

#### Training Methods
- **Selection (SEL)**: Select all mismatched elements — "Odd One Out"
- **Recognition (REC)**: Identify the missing element(s) — "Fill the Gap"

#### Performance Constraints
| Constraint | How It Manifests |
|---|---|
| Speed | Playback tempo (faster = harder to compare in real time) |
| Sequence Length | Number of notes/beats in the passage |
| Error Density | Number of mismatches to find (1 easy → multiple hard) |
| Replays | Number of allowed replays |

#### Taxonomy Coverage
RS-004 (Fill the Gap), RS-005 (Odd One Out)

#### Content Requirements
- Audio track of the "correct" version
- Notation of the "modified" version (with intentional errors)
- Map of which notated elements are errors

#### Feedback Model
- On submit: correctly identified errors highlight green; missed errors highlight yellow; false positives highlight red
- Replay with errors visually annotated

#### Design Notes
- Audio-to-notation synchronization is critical — the cursor/highlight must track the audio precisely
- Notation elements must be large enough to tap individually
- This is the most technically complex blueprint due to the synchronized multi-modal presentation

---

### BP-09: Read → Alteration

**The transformation workshop. Notation shown with instructions, user modifies the notation.**

#### Interaction Pattern
1. System displays notation on an interactive staff along with a modification instruction (e.g., "Transpose this melody up a perfect 4th" or "Add accidentals to form the specified key signature").
2. User modifies the existing notation (moving notes, adding/removing accidentals, changing note values).
3. User submits their modification.
4. System validates and provides feedback.

#### Screen Components
- Instruction text area
- Interactive staff with pre-populated notation
- Modification tools (accidental palette, note-dragging, note value selector)
- Submit button
- Before/after comparison in feedback

#### PTA Classification
| Perception | Transformation | Action |
|---|---|---|
| **Visual + Semantic** (see notation + read instructions) | Alteration substrates (transposition, inversion, reharmonization) | **Visual** (modified notation) |

Specific patches: V+S→V

#### FTA Dimensions
- **Frequency**: Transposition, accidental modification, inversion, chord re-voicing
- **Time**: Rhythmic augmentation/diminution

#### Training Methods
- **Alteration (ALT)**: Modify existing material to meet new specifications

#### Performance Constraints
| Constraint | How It Manifests |
|---|---|
| Speed | Time limit for modification |
| Error Tolerance | Exact match required vs. partial credit |
| Complexity | Number of notes to modify; number of simultaneous operations |

#### Taxonomy Coverage
SC-006 (ALT variant), SC-010 (ALT variant), CH-006 (ALT variant), CH-010 (operational)

Shares significant UI infrastructure with BP-03 (Label → Staff Placement) — the interactive staff with note placement and accidental tools. The distinction is that BP-03 starts from a blank or sparse staff, while BP-09 starts from a fully populated staff that needs modification.

#### Content Requirements
- Starting notation (pre-populated staff content)
- Modification instruction
- Expected result notation (for validation)

#### Feedback Model
- Before/after comparison: original notation vs. modified notation vs. expected result
- Element-by-element highlighting of correct and incorrect modifications

#### Design Notes
- Reuse the interactive staff component from BP-03
- Clear visual distinction between "original" (unmodifiable) and "modifiable" elements
- Undo/redo is essential for multi-step modifications

---

### BP-10: Label → Label (Computation)

**The theory quiz. Text prompt, text answer — pure cognitive transformation.**

#### Interaction Pattern
1. System displays a text-based theory question (e.g., "What note is a minor 3rd above D?" or "What are the notes in E♭m7?" or "What is the 5th degree of D Dorian?").
2. User provides a text answer — either by selecting from options (REC) or typing/entering freely (RCL).
3. System validates and provides feedback.

#### Screen Components
- Text prompt area
- Response area: either multiple-choice buttons (REC) or text input field (RCL)
- Feedback indicator
- Progress and score displays

#### PTA Classification
| Perception | Transformation | Action |
|---|---|---|
| **Semantic** | Computation substrates (interval computation, chord construction, scale degree mapping) | **Semantic** |

Specific patches: S→S (with non-trivial transformation)

#### FTA Dimensions
- **Frequency**: Interval computation, enharmonic equivalence, chord note listing, scale degree naming
- **Time**: Beat counting, rhythm arithmetic

#### Training Methods
- **Recognition (REC)**: Multiple choice
- **Recall (RCL)**: Free text entry
- **Verification (VER)**: "Is this correct? True/False" variant

#### Performance Constraints
| Constraint | How It Manifests |
|---|---|
| Speed | Time limit per question; speed rounds |
| Memory Load | Multi-step computation without scratch paper; chained questions where previous answers feed the next question |
| Error Tolerance | Strict (exact answer) vs. lenient (accept enharmonic equivalents) |

#### Taxonomy Coverage
P-018, INT-010, SC-008, SC-011, CH-009, CH-010, RS-009, RS-010

#### Content Requirements
- Question text
- Correct answer(s) — including acceptable variants (enharmonic spellings, etc.)
- Distractor answers for REC variant

#### Feedback Model
- Immediate: correct/incorrect with correct answer shown
- For RCL: show the correct answer if the user's free-text entry was wrong

#### Design Notes
- Simplest blueprint to implement — no audio, no notation rendering, no MIDI
- Free text entry needs smart parsing (accept "Eb" and "E♭" and "e flat" etc.)
- Good candidate for speed-drill mode with rapid-fire prompts
- This blueprint also covers the VER (Verification) training method — prompt + "True/False" buttons

---

### BP-11: Visual → Audio Matching

**Notation-to-audio matching. See notation, choose the audio clip that matches.**

#### Interaction Pattern
1. System displays notation (a rhythm, melody, or chord).
2. Multiple audio clips are playable as options.
3. User listens to each option and selects the one that matches the notation.
4. System validates.

#### Screen Components
- Visual prompt area (staff renderer)
- Audio option buttons (each plays a distinct clip when tapped)
- Selection indicator (which option is currently selected)
- Submit button
- Feedback indicator

#### PTA Classification
| Perception | Transformation | Action |
|---|---|---|
| **Visual** | Audiation — converting notation to internal sound | **Aural** (selecting the matching sound) |

Specific patches: V→A

#### FTA Dimensions
- **Frequency**: Matching notated pitch to sounded pitch
- **Time**: Matching notated rhythm to sounded rhythm
- **Frequency + Time**: Matching notated melody to sounded melody

#### Training Methods
- **Recognition (REC)**: Select the matching audio clip

#### Performance Constraints
| Constraint | How It Manifests |
|---|---|
| Speed | Time limit; limit on number of replay listens |
| Answer Optionality | Number of audio clips to choose from |

#### Taxonomy Coverage
P-003 (S→A variant), P-007, P-010, R-003, R-006, RS-001

#### Content Requirements
- Notated prompt
- Correct audio clip
- Distractor audio clips (similar but distinct)

#### Feedback Model
- Selected audio clip highlights green (correct) or red (incorrect)
- Correct audio replays on feedback

#### Design Notes
- Each audio option must be individually playable — user needs to A/B compare
- Visual prompt stays visible while user listens to options
- Audio clips should be clearly labeled (Option A, B, C…) for accessibility

---

### BP-12: Audio → Notation Matching

**Audio-to-notation matching. Hear audio, choose the notation that matches.**

#### Interaction Pattern
1. System plays an audio prompt.
2. Multiple notation options are displayed on screen.
3. User selects the notation that matches what they heard.
4. System validates.

#### Screen Components
- Audio playback control
- Multiple rendered notation options (staff snippets)
- Selection indicator
- Feedback overlay

#### PTA Classification
| Perception | Transformation | Action |
|---|---|---|
| **Aural** | Transcription — converting sound to notation recognition | **Visual** (selecting the matching notation) |

Specific patches: A→V

#### FTA Dimensions
- **Frequency**: Matching sounded pitch to notated pitch
- **Time**: Matching sounded rhythm to notated rhythm

#### Training Methods
- **Recognition (REC)**: Select the matching notation

#### Performance Constraints
| Constraint | How It Manifests |
|---|---|
| Speed | Time limit; replay limits |
| Answer Optionality | Number of notation options |

#### Taxonomy Coverage
P-015 (REC), INT-009 (REC), RS-002, RS-008 (variant)

#### Content Requirements
- Audio prompt
- Correct notation
- Distractor notations (similar but distinct — e.g., same rhythm different pitch, or vice versa)

#### Feedback Model
- Selected notation highlights green/red
- Audio replays alongside the correct notation

#### Design Notes
- Notation options must be rendered at a consistent size for fair comparison
- Replay button must be very accessible — users will listen multiple times
- Distractor design is pedagogically important: distractors should represent common errors

---

### BP-13: Prompt → Sing/Hum

**Vocal production. A prompt is given, user produces vocal output assessed via microphone.**

#### Interaction Pattern
1. System displays a prompt (text name, notation, or audio reference).
2. User sings, hums, or vocalizes the answer.
3. System captures audio via microphone and runs pitch detection.
4. System validates the sung pitch(es) against the expected answer.
5. Feedback on pitch accuracy.

#### Screen Components
- Prompt area (text, notation, or audio playback)
- Recording indicator (microphone active state)
- Real-time pitch visualization (optional — shows detected pitch against target)
- Start/stop recording buttons
- Feedback display (pitch accuracy, deviation amount)

#### PTA Classification
| Perception | Transformation | Action |
|---|---|---|
| **Semantic**, **Visual**, or **Aural** | Audiation — producing internal pitch as external sound | **Aural** (vocal production) |

Specific patches: S→A (vocal), V→A (vocal), A→A (vocal matching)

#### FTA Dimensions
- **Frequency**: Singing named pitches, singing intervals, singing back heard pitches

#### Training Methods
- **Performance (PRF)**: Real-time vocal production

#### Performance Constraints
| Constraint | How It Manifests |
|---|---|
| Pitch Tolerance | How close to the target pitch the sung note must be (in cents) |
| Speed | Time limit to produce the pitch |
| Memory Load | Delay between hearing a reference and singing the response |

#### Taxonomy Coverage
P-004, P-008, P-013, P-017, INT-004 (singing variant)

Many of these exercises require perfect pitch (singing a named pitch without a reference) or relative pitch (singing an interval from a given reference). Configuration should indicate which type is expected.

#### Content Requirements
- Target pitch(es) for validation
- Reference pitch audio (for relative pitch exercises)
- Pitch tolerance parameters

#### Feedback Model
- Real-time pitch meter showing detected pitch vs. target
- Post-attempt: cents deviation, correct/incorrect judgment

#### Design Notes
- **This is a later-phase blueprint** due to the technical complexity of reliable pitch detection from microphone input
- Microphone permissions and ambient noise handling are significant UX challenges
- Consider making this opt-in rather than required for exercise completion
- Pitch detection accuracy varies significantly across devices

---

## 3. Blueprint-to-Taxonomy Cross-Reference Summary

| Blueprint | Training Methods | Primary FTA | Exercises Covered | Build Priority |
|---|---|---|---|---|
| **BP-01** Listen → Label | REC, SEL | F, T, (A) | ~30+ exercises | **V1 — High** |
| **BP-02** Read → Label | REC | F, T | ~17 exercises | **V1 — High** |
| **BP-03** Label → Staff Placement | RCL, ALT | F | ~7 exercises | **V1 — Medium** |
| **BP-04** Label → Key Selection | REC, SEL | F | ~4 exercises | **V1 — Medium** |
| **BP-05** Prompt → Physical Key Performance | PRF | F, T, F+T | ~25+ exercises | **V1 — High** |
| **BP-06** Listen → Rhythm Tap | PRF | T | ~5 exercises | **V1 — Medium** |
| **BP-07** Listen → Sequence Assembly | ASM | F, T, F+T | ~6 exercises | **V1 — Medium** |
| **BP-08** Listen + Read → Error Detection | SEL, REC | F+T | ~2 exercises | **V2** |
| **BP-09** Read → Alteration | ALT | F, T | ~4 exercises | **V2** |
| **BP-10** Label → Label (Computation) | REC, RCL, VER | F, T | ~8 exercises | **V1 — Medium** |
| **BP-11** Visual → Audio Matching | REC | F, T | ~6 exercises | **V1 — Low** |
| **BP-12** Audio → Notation Matching | REC | F, T | ~4 exercises | **V1 — Low** |
| **BP-13** Prompt → Sing/Hum | PRF | F | ~5 exercises | **V3 (deferred)** |

### V1 Build Order Recommendation

1. **BP-01 (Listen → Label)** + **BP-02 (Read → Label)** — Together these cover the majority of identification/recognition exercises. They share a common interaction pattern (prompt → multiple choice) and primarily differ in prompt type (audio vs. visual). Ship these first to have a functional exercise section.

2. **BP-05 (Prompt → Physical Key Performance)** — This is the blueprint that connects exercises to the physical instrument, which is core to MuseFlow's value proposition. High technical complexity (MIDI input) but high value.

3. **BP-10 (Label → Label)** — Low implementation cost (text only, no audio or notation rendering), covers the pure theory exercises.

4. **BP-04 (Label → Key Selection)** + **BP-06 (Listen → Rhythm Tap)** + **BP-07 (Listen → Sequence Assembly)** — Second wave of V1 blueprints. Each adds a distinct interaction mechanic.

5. **BP-03 (Label → Staff Placement)** + **BP-11/BP-12 (Audio/Visual Matching)** — Round out V1 with construction and matching exercises.

---

## 4. Shared UI Components

Several UI components appear across multiple blueprints and should be built as reusable modules:

| Component | Used By | Notes |
|---|---|---|
| **Staff Renderer** | BP-02, BP-03, BP-08, BP-09, BP-11, BP-12 | Must support treble/bass/grand staff, key signatures, accidentals, dynamic clef switching. Interactive (tappable notes) for BP-03, BP-08, BP-09; static for others. |
| **Onscreen Keyboard** | BP-04 | Interactive tappable keyboard with configurable range and key highlighting. |
| **Audio Playback Engine** | BP-01, BP-05, BP-06, BP-07, BP-08, BP-11, BP-12, BP-13 | Play/replay controls, metronome integration, multiple simultaneous playable clips for matching exercises. |
| **MIDI Input Handler** | BP-05 | MIDI device connection, note-on/note-off capture, velocity capture, real-time validation against expected input. |
| **Multiple Choice Button Grid** | BP-01, BP-02, BP-04, BP-10, BP-11, BP-12 | Configurable number of options, correct/incorrect state styling, single-select and multi-select modes. |
| **Draggable Tile Sequencer** | BP-07 | Horizontal sequence track, draggable labeled tiles, submit action. |
| **Metronome** | BP-05, BP-06, BP-08 | Audio click + visual beat indicator, configurable tempo and time signature. |
| **Tap Input Capture** | BP-06 | High-precision timestamp capture on screen taps, minimal latency. |
| **Progress/Score Display** | All | Current prompt number, running accuracy, timer (when speed constraint is active). |
| **Feedback Overlay** | All | Correct/incorrect state, correct answer reveal, end-of-exercise summary. |
| **Microphone Input / Pitch Detection** | BP-13 | Microphone capture, real-time pitch detection, pitch-to-note mapping. V3 component. |
