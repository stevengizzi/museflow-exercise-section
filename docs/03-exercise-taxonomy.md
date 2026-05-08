# MuseFlow Exercise System: Exercise Taxonomy & Catalog Specification

## 1. Overview

This document specifies the complete exercise catalog generated from the system architecture. It extends the initial combinatorial matrix (which covered single pitches, single rhythm values, and intervals) to include all substrate families: scales, chords, chord progressions, and rhythm sequences.

Each section follows the generation pipeline: enumerate input/output combinations, apply pruning rules, and document the surviving exercises with their training methods and configuration parameters.

---

## 2. Catalog Structure

### 2.1 Exercise Numbering

Exercises are numbered by substrate family prefix and sequential ID:

- **P-###** — Single Pitch exercises
- **R-###** — Single Rhythm Value exercises
- **INT-###** — Interval exercises
- **SC-###** — Scale exercises
- **CH-###** — Chord exercises
- **CP-###** — Chord Progression exercises
- **RS-###** — Rhythm Sequence exercises
- **AMP-###** — Amplitude/Dynamics exercises
- **X-###** — Cross-domain exercises

### 2.2 Exercise Entry Format

Each exercise is documented with:
- **ID** and **Title**
- **Patch**: Perception Modality → [Substrate] → Action Modality
- **Input Format** and **Output Format**
- **Training Methods**: Compatible methods from the spectrum
- **Configurations**: Available scope parameters
- **Notes**: Pedagogical rationale, special requirements, or dependencies

---

## 3. Single Pitch Exercises (P-###)

### 3.1 Combinatorial Matrix

**Substrate**: Pitch-name mapping, Pitch-notation mapping, Pitch-key mapping, Pitch-audiation mapping

**Input Formats**: Named pitch (Semantic), Notated pitch (Visual), Selected/highlighted key (Kinesthetic), Sounded pitch (Aural)

**Output Formats**: Named pitch (Semantic), Notated pitch (Visual), Selected/played key (Kinesthetic), Sung/sounded pitch (Aural)

### 3.2 Active Exercises

| ID | Input (Modality) | Substrate | Output (Modality) | Training Methods | Notes |
|---|---|---|---|---|---|
| P-001 | Named pitch (S) | Pitch notation | Notated pitch (V) | REC, RCL | Tap correct staff position or choose from options |
| P-002 | Named pitch (S) | Piano key location | Selected key (K) | REC, PRF | Tap correct key on onscreen/physical keyboard |
| P-003 | Named pitch (S) | Pitch audiation | Sounded pitch (A) | REC | Choose correct audio clip. Requires perfect pitch |
| P-004 | Named pitch (S) | Pitch audiation | Sung pitch (A) | PRF | Sing/hum the named pitch. Requires perfect pitch |
| P-005 | Notated pitch (V) | Pitch name | Named pitch (S) | REC | Choose correct pitch name for the notation |
| P-006 | Notated pitch (V) | Piano key location | Selected key (K) | REC, PRF | Identify/play the correct key from notation |
| P-007 | Notated pitch (V) | Pitch audiation | Sounded pitch (A) | REC | Choose correct audio clip. Requires perfect pitch |
| P-008 | Notated pitch (V) | Pitch audiation | Sung pitch (A) | PRF | Sing the notated pitch. Requires perfect pitch |
| P-009 | Highlighted key (K) | Pitch name | Named pitch (S) | REC | Name the highlighted key |
| P-010 | Highlighted key (K) | Pitch notation | Notated pitch (V) | REC, RCL | Notate the pitch of the highlighted key |
| P-011 | Highlighted key (K) | Piano key location | Played key (K) | PRF | Play the matching key on physical keyboard |
| P-012 | Highlighted key (K) | Pitch audiation | Sounded pitch (A) | REC | Choose correct audio clip. Requires perfect pitch |
| P-013 | Highlighted key (K) | Pitch audiation | Sung pitch (A) | PRF | Sing the pitch of the highlighted key. Requires perfect pitch |
| P-014 | Sounded pitch (A) | Pitch name | Named pitch (S) | REC | Name the pitch you hear. Requires perfect pitch |
| P-015 | Sounded pitch (A) | Pitch notation | Notated pitch (V) | REC, RCL | Notate the pitch you hear. Requires perfect pitch |
| P-016 | Sounded pitch (A) | Piano key location | Selected/played key (K) | REC, PRF | Select/play the key matching the pitch you hear. Requires perfect pitch |
| P-017 | Sounded pitch (A) | Pitch audiation | Sung pitch (A) | PRF | Sing back the pitch you hear. Does not require perfect pitch (relative matching) |
| P-018 | Named pitch (S) | Enharmonic equivalence | Named pitch (S) | REC, RCL | Given "D♭", respond "C♯" (or vice versa). Only S→S exercise for pitches that survives pruning, because the transformation is non-trivial |

### 3.3 Pruned Combinations

- **S→S (identity)**: Named pitch → Named pitch with no substrate transformation. Trivial.
- **V→V (identity)**: Notated pitch → Notated pitch. Copying notation.
- **A→A (identity)**: Sounded pitch → Sounded pitch (without singing). Echoing.
- **K→K (identity)**: Highlighted key → Selected key (same keyboard). Trivial unless physical keyboard output.
- **S→A (Reproduce - Sung)**: Named pitch → Sung pitch without perfect pitch is not assessable as a pitch exercise (it becomes a vocal exercise).

### 3.4 Configuration Parameters

| Parameter | Values | Applies To |
|---|---|---|
| Clef(s) | Treble, Bass, Grand Staff | Exercises with visual notation |
| Pitch range | Configurable range, e.g., C3–C6 | All |
| Included/excluded pitches | Whitelist or blacklist specific pitches | All |
| Lines only / Spaces only | Restrict to staff line or space notes | Visual notation exercises |
| Key signature | None, or specific key signature context | Visual notation exercises |
| Accidentals | On/off, or specific types (sharps/flats/naturals) | All |
| Keyboard range | Restricted to user's physical keyboard size | Kinesthetic exercises |
| Vocal tessitura | Restricted to user's singing range | Aural output (singing) |
| Enharmonic display | Allow/disallow enharmonic spelling variants | Semantic output exercises |

---

## 4. Single Rhythm Value Exercises (R-###)

### 4.1 Active Exercises

| ID | Input (Modality) | Substrate | Output (Modality) | Training Methods | Notes |
|---|---|---|---|---|---|
| R-001 | Named rhythm value (S) | Rhythm notation | Notated rhythm (V) | REC | Choose correct notation symbol |
| R-002 | Named rhythm value (S) | Rhythm duration | Played rhythm (K) | PRF | Tap and hold key/button with metronome |
| R-003 | Named rhythm value (S) | Rhythm audiation | Sounded rhythm (A) | REC | Choose correct audio clip with metronome |
| R-004 | Notated rhythm (V) | Rhythm value name | Named rhythm value (S) | REC | Name the notated rhythm |
| R-005 | Notated rhythm (V) | Rhythm duration | Played rhythm (K) | PRF | Perform the notated rhythm with metronome |
| R-006 | Notated rhythm (V) | Rhythm audiation | Sounded rhythm (A) | REC | Choose correct audio clip with metronome |
| R-007 | Sounded rhythm (A) | Rhythm value name | Named rhythm value (S) | REC | Name the rhythm you hear |
| R-008 | Sounded rhythm (A) | Rhythm notation | Notated rhythm (V) | REC | Choose correct notation symbol |
| R-009 | Sounded rhythm (A) | Rhythm duration | Played rhythm (K) | PRF | Tap back the rhythm you hear |

### 4.2 Pruned Combinations

- **Kinesthetic input for single rhythms**: "Selected rhythm" as input is not well-defined — rhythm is temporal, not spatial. Unlike a piano key (which has a fixed location), a single rhythm value cannot be "highlighted" on a keyboard in a way that communicates duration. All kinesthetic-input rhythm combinations are pruned.
- **S→S, V→V, A→A identity**: Same pruning logic as pitch exercises.
- **S→A (Reproduce - Sung)**: Singing a rhythm value (e.g., "sing a quarter note") is functionally identical to performing it. Merged into R-002 / R-005 where the output is kinesthetic performance.

### 4.3 Configuration Parameters

| Parameter | Values |
|---|---|
| Included rhythm values | Whole, half, quarter, eighth, sixteenth, dotted variants, triplet variants |
| Time signature / meter context | Simple (4/4, 3/4, 2/4), Compound (6/8, 9/8, 12/8) |
| Metronome tempo | BPM range |
| Rest inclusion | On/off — include rests as possible rhythm values |
| Tied notes | On/off |

---

## 5. Interval Exercises (INT-###)

### 5.1 Active Exercises

| ID | Input (Modality) | Substrate | Output (Modality) | Training Methods | Notes |
|---|---|---|---|---|---|
| INT-001 | Named interval (S) | Interval notation | Notated interval (V) | REC, ALT | Choose or construct the interval on staff |
| INT-002 | Named interval (S) | Interval key locations | Selected/played keys (K) | REC, PRF | Play the interval on keyboard |
| INT-003 | Named interval (S) | Interval audiation | Sounded pitches (A) | REC | Choose correct audio clip |
| INT-004 | Named interval (S) | Interval audiation | Sung pitches (A) | PRF | Sing the second pitch to complete the interval |
| INT-005 | Notated interval (V) | Interval name | Named interval (S) | REC | Name the notated interval |
| INT-006 | Highlighted keys (K) | Interval name | Named interval (S) | REC | Name the interval shown on keyboard |
| INT-007 | Sounded pitches (A) | Pitch direction | Interval directionality (S) | REC | Higher, lower, or same? |
| INT-008 | Sounded interval (A) | Interval name | Named interval (S) | REC | Name the interval you hear |
| INT-009 | Sounded interval (A) | Interval notation | Notated interval (V) | REC, ALT | Notate the interval you hear |
| INT-010 | Named interval + starting pitch (S) | Interval computation | Named target pitch (S) | REC, RCL | "What note is a minor 3rd above D?" |

### 5.2 Pruned Combinations

- **V→K, V→A for intervals**: Seeing two notated notes and playing/singing them is just sight-reading two individual pitches — the interval substrate is not engaged. These reduce to two instances of P-006 or P-008.
- **K→V, K→K, K→A for intervals**: Same logic — seeing two highlighted keys and notating/playing/singing them is just two instances of single-pitch exercises.
- **A→K for intervals**: Hearing an interval and playing both notes is just ear-to-keyboard pitch matching twice — only meaningful if the task is specifically about the interval relationship, which is better captured by INT-008 (naming) plus separate pitch-matching exercises.

### 5.3 Configuration Parameters

| Parameter | Values |
|---|---|
| Interval temporal disposition | Melodic, Harmonic, or both |
| Interval quality filter | Generic (2nd, 3rd, etc.) or Specific (minor 2nd, major 3rd, etc.) |
| Interval quality resolution | Generic, Specific, or Spatial (by half-step count) |
| Included intervals | Whitelist specific intervals |
| Interval direction | Ascending, Descending, or both |
| Simple / compound | Restrict to within-octave or allow compound intervals |
| Starting pitch constraints | Range, key context |
| Clef and staff options | Same as pitch exercises |

---

## 6. Scale Exercises (SC-###)

### 6.1 Active Exercises

| ID | Input (Modality) | Substrate | Output (Modality) | Training Methods | Notes |
|---|---|---|---|---|---|
| SC-001 | Notated scale (V) | Scale name recognition | Named scale mode (S) | REC | Identify the mode from notation |
| SC-002 | Notated scale (V) | Scale degree mapping | Named scale degrees (S) | REC, RCL | Label the degree of each note |
| SC-003 | Highlighted keys (K) | Scale name recognition | Named scale mode (S) | REC | Identify the mode from keyboard pattern |
| SC-004 | Sounded scale (A) | Scale name recognition | Named scale mode (S) | REC | Identify the mode by ear |
| SC-005 | Sounded scale (A) | Scale degree sequence | Ordered scale degrees (S) | ASM | Tap the ordered sequence of scale degrees heard |
| SC-006 | Named scale (S) | Scale construction | Notated scale (V) | ALT | Add accidentals to notated pitches to form the scale |
| SC-007 | Named scale (S) | Scale construction | Played scale (K) | PRF | Play the scale on keyboard |
| SC-008 | Named scale (S) | Scale degree mapping | Named pitch (S) | REC, RCL | "What is the 5th degree of D Dorian?" |
| SC-009 | Key signature + mode (V) | Key/scale recognition | Named scale root (S) | REC | Identify the tonic from key signature and mode |
| SC-010 | Named scale (S) | Key signature construction | Notated key signature (V) | REC, ALT | Select or construct the correct key signature |
| SC-011 | Note + scale name (V+S) | Scale degree mapping | Named scale degree (S) | REC, RCL | "What degree is F in Bb Major?" |
| SC-012 | Sounded chord (A) | Chord-scale implication | Named scale mode (S) | REC | "What modal scale does this voicing imply?" (Modal voicing exercises) |

### 6.2 Configuration Parameters

| Parameter | Values |
|---|---|
| Included scales/modes | Major modes, Melodic minor modes, Harmonic minor modes, Symmetric scales, Pentatonic/Blues, Bebop |
| Included tonics / key signatures | Whitelist specific keys |
| Clef(s) | Treble, Bass, Grand Staff |
| Note range | Configurable |
| Question mode (for visual exercises) | Full scale with accidentals, Full scale with key signature, Tonic + key signature |
| Scale play direction (for aural) | Ascending, Descending, Both |
| Audio playback parameters | Speed, timbre, pitch range |

---

## 7. Chord Exercises (CH-###)

### 7.1 Active Exercises

| ID | Input (Modality) | Substrate | Output (Modality) | Training Methods | Notes |
|---|---|---|---|---|---|
| CH-001 | Notated chord (V) | Chord quality recognition | Named chord quality (S) | REC | Identify chord quality from notation |
| CH-002 | Notated chord (V) | Chord inversion identification | Named inversion (S) | REC | Identify inversion from notation |
| CH-003 | Highlighted keys (K) | Chord quality recognition | Named chord quality (S) | REC | Identify chord quality from keyboard pattern |
| CH-004 | Sounded chord (A) | Chord quality recognition | Named chord quality (S) | REC | Identify chord quality by ear |
| CH-005 | Sounded chord (A) | Chord inversion identification | Named inversion (S) | REC | Identify inversion by ear |
| CH-006 | Named chord quality (S) | Chord construction | Notated chord (V) | ALT | Add accidentals to build the chord on staff |
| CH-007 | Named chord quality (S) | Chord construction | Played chord (K) | PRF | Play the chord on keyboard |
| CH-008 | Named chord + inversion (S) | Chord voicing | Played chord (K) | PRF | Play the chord in the specified inversion |
| CH-009 | Chord symbol (S) | Chord construction | Named pitches (S) | RCL | "What are the notes in Ebm7?" |
| CH-010 | Named chord + operation (S) | Chord manipulation | Named chord (S) | REC, RCL | "Invert this chord." "Add a 7th." "Transpose up a 4th." |
| CH-011 | Sounded chord (A) | Chord-scale mapping | Named scale (S) | REC | "What scale does this chord imply?" |

### 7.2 Configuration Parameters

| Parameter | Values |
|---|---|
| Included chord qualities | Triads (major, minor, dim, aug, sus2, sus4, Phrygian, Lydian), 7ths (maj7, min7, dom7, half-dim7, dim7, minMaj7, augMaj7, etc.), Extended (9ths, 11ths, 13ths), Add-note chords |
| Inversions | On/off, specific inversions |
| Clef(s) | Treble, Bass, Grand Staff |
| Note range | Configurable |
| Key signature context | None, or specific key |
| Chord play mode (for aural) | Harmonic, Melodic ascending, Melodic descending, Combined |
| Audio playback parameters | Speed, timbre, pitch range |
| Difficulty level | Affects accidental complexity |

---

## 8. Chord Progression Exercises (CP-###)

### 8.1 Active Exercises

| ID | Input (Modality) | Substrate | Output (Modality) | Training Methods | Notes |
|---|---|---|---|---|---|
| CP-001 | Sounded chords (A) | Functional harmony analysis | Named progression - Roman numerals (S) | REC | Identify two-chord cadential patterns (e.g., IV-I vs V-I) |
| CP-002 | Sounded chords (A) | Functional harmony analysis | Named progression - Roman numerals (S) | ASM | Identify and order a multi-chord progression |
| CP-003 | Sounded chords (A) | Secondary dominant recognition | Named secondary function (S) | REC | Identify secondary dominant chords |
| CP-004 | Sounded chords (A) | Secondary leading-tone recognition | Named secondary function (S) | REC | Identify secondary leading-tone chords |
| CP-005 | Sounded chords (A) | Modal harmony analysis | Named harmonic function (S) | REC | Identify modal chord relationships in a 3-chord sequence |
| CP-006 | Sounded chords (A) | Modal harmony analysis | Named harmonic function (S) | SEL, ASM | Identify multiple modal chords in a longer sequence |
| CP-007 | Sounded chords (A) | Reharmonization recognition | Named chord progression (S) | REC | Compare original and reharmonized progressions, identify the reharm |
| CP-008 | Named progression (S) | Progression performance | Played chords (K) | PRF | Play the chord progression on keyboard |
| CP-009 | Notated progression (V) | Functional harmony analysis | Named progression - Roman numerals (S) | REC, RCL | Analyze notated chords for harmonic function |
| CP-010 | Named progression - Roman numerals (S) | Chord construction | Played chords (K) | PRF | Given Roman numerals and a key, play the progression |
| CP-011 | Sounded chords (A) | Bitonal recognition | Named slash chord (S) | REC | Identify slash chords / upper-structure triads |
| CP-012 | Sounded chords (A) | Polychordal recognition | Named polychord (S) | REC | Identify polychords by their component triads |

### 8.2 Configuration Parameters

| Parameter | Values |
|---|---|
| Key center | Major, Minor, or specific key |
| Included chord functions | Diatonic triads, Diatonic 7ths, Secondary dominants, Secondary leading-tones, Modal interchange, Extended chords |
| Progression length | 2-chord, 4-chord, variable |
| Harmonic complexity tier | Tonal → Modal → Chromatic → Bitonal → Polychordal |
| Audio playback parameters | Tempo, voicing style, timbre |

---

## 9. Rhythm Sequence Exercises (RS-###)

### 9.1 Active Exercises

| ID | Input (Modality) | Substrate | Output (Modality) | Training Methods | Notes |
|---|---|---|---|---|---|
| RS-001 | Notated rhythm sequence (V) | Rhythm audiation | Sounded rhythm (A) | REC | Choose the matching audio clip (Bar Ear) |
| RS-002 | Sounded rhythm sequence (A) | Rhythm notation recognition | Notated rhythm (V) | REC | Choose the matching notation (Bar Eye) |
| RS-003 | Sounded rhythm sequence (A) | Rhythm notation construction | Notated rhythm (V) | ASM | Construct the notation from rhythmic value tiles (Beat) |
| RS-004 | Sounded rhythm + notated rhythm (A+V) | Gap identification | Notated rhythm (V) | REC | Identify the missing beat(s) from the notation (Fill the Gap) |
| RS-005 | Sounded rhythm + notated rhythm (A+V) | Error detection | Notated rhythm (V) | SEL | Identify which notated values don't match the audio (Odd One Out) |
| RS-006 | Notated rhythm (V) | Rhythm performance | Played rhythm - tap (K) | PRF | Tap out the rhythm to match the notation |
| RS-007 | Notated rhythm (V) | Rhythm performance | Played rhythm - clap (K) | PRF | Clap the rhythm to match the notation |
| RS-008 | Sounded rhythm (A) | Rhythm reproduction | Played rhythm - tap (K) | PRF | Tap back the rhythm you heard |
| RS-009 | Visual rhythm sequence (V) | Beat counting | Named beat count (S) | RCL | "How many beats are in this sequence?" |
| RS-010 | Sounded rhythm sequence (A) | Beat counting | Named beat count (S) | RCL | "How many beats are in this sequence?" |
| RS-011 | Named beat count (S) | Rhythm construction | Notated rhythm (V) | ASM | "Which rhythm sequence adds up to N beats?" |
| RS-012 | Sounded rhythm (A) | Beat division recognition | Selected beat divisions (S) | SEL | Select which subdivisions have onsets (grid-based) |
| RS-013 | Sounded rhythm (A) | Tempo matching | Played rhythm (K) | PRF | Tap to match the tempo you hear |
| RS-014 | Sounded rhythm (A) | Tempo memory | Played rhythm (K) | PRF | Reproduce a previously-heard tempo from memory |
| RS-015 | Sounded rhythm (A) | Groove reproduction | Played rhythm (K) | PRF | Reproduce a multi-layer rhythmic groove |
| RS-016 | Named groove components (S) | Groove construction | Played/assembled rhythm (K/V) | ASM | Build a groove from component patterns |

### 9.2 Configuration Parameters

| Parameter | Values |
|---|---|
| Included rhythm values | Quarter, Eighth, Sixteenth, Dotted, Triplet, Syncopated patterns |
| Time signature | 4/4, 3/4, 2/4, 6/8, 9/8, 12/8, odd meters |
| Playback tempo | BPM range |
| Notation system | Staff, Line, Boxes/grid, Kodály syllables, Takadimi, Gordon, Numbers, Eastman |
| Playback timbre | Click, drum, pitched instrument |
| Number of beats per exercise | Configurable |
| Sequence note count | 1, 2, 3, 4, variable |
| Subdivision resolution | Quarter level, Eighth level, Sixteenth level |

---

## 10. Amplitude/Dynamics Exercises (AMP-###)

> **V1 Deferral:** The AMP exercise family is fully specified here to maintain FTA completeness in the architecture, but these exercises are **deferred beyond V1**. They are included in the schema so that engineering can build the data model to accommodate them and they can be activated later without structural changes. Amplitude assessment depends on reliable MIDI velocity analysis and/or waveform amplitude detection, which adds technical scope.

### 10.1 Active Exercises

| ID | Input (Modality) | Substrate | Output (Modality) | Training Methods | Notes |
|---|---|---|---|---|---|
| AMP-001 | Dynamic marking (V) | Dynamic level naming | Named dynamic level (S) | REC | "What does 'mf' mean?" |
| AMP-002 | Sounded note at dynamic level (A) | Dynamic level recognition | Named dynamic level (S) | REC | Identify the approximate dynamic of a sounded note |
| AMP-003 | Two sounded notes (A) | Relative dynamic comparison | Louder/softer/same (S) | REC | Compare the dynamics of two sounds |
| AMP-004 | Sounded phrase (A) | Dynamic contour recognition | Named contour (S) | REC | Identify crescendo, decrescendo, subito, terraced dynamics |
| AMP-005 | Dynamic marking sequence (V) | Dynamic contour performance | Played phrase with dynamics (K+A) | PRF | Play a passage following the dynamic markings |
| AMP-006 | Notated phrase with dynamics (V) | Expressive performance | Played phrase (K+A) | PRF | Sight-read with dynamic expression |
| AMP-007 | Sounded phrase (A) | Accent pattern recognition | Selected accented beats (S) | SEL | Identify which beats are accented |
| AMP-008 | Articulation markings (V) | Articulation execution | Played notes with articulation (K+A) | PRF | Play staccato, legato, tenuto, accent, etc. |

### 10.2 Configuration Parameters

| Parameter | Values |
|---|---|
| Dynamic range | pp–ff, or finer gradations |
| Included dynamic markings | Absolute (pp, p, mp, mf, f, ff), Relative (cresc., decresc., sfz, fp) |
| Included articulations | Staccato, legato, tenuto, accent, marcato, slur |
| Phrase length | Number of notes/beats |
| Assessment method | MIDI velocity analysis, waveform amplitude analysis |

---

## 11. Cross-Domain Exercises (X-###)

These exercises combine substrates across multiple FTA dimensions.

| ID | Description | FTA Dimensions | Substrates Engaged | Notes |
|---|---|---|---|---|
| X-001 | Sight-read a single note (pitch + rhythm) | F + T | Pitch-notation + Rhythm-notation → Key + Timing | The core "note reading" exercise |
| X-002 | Sight-read a melodic passage | F + T | Pitch sequence + Rhythm sequence → Performance | Multi-note sight-reading |
| X-003 | Sight-read with dynamics | F + T + A | Full notation → Expressive performance | Three-dimensional reading |
| X-004 | Fingering selection | F + T + K | Note sequence → Optimal finger assignment | Both recognition (identify correct fingering) and performance (execute it) |
| X-005 | Continuous sight-reading (flow mode) | F + T | Real-time reading without pause | Performance constraint: no stopping, speed threshold enforced |
| X-006 | Chord chart reading | F + T | Chord symbols + Rhythm → Voiced chord performance | Real-time chord realization |
| X-007 | Improvisation exercises | F + T + A | Open-ended creative transformation | Sandbox/Workshop territory — scored on constraint adherence (stay in key, maintain rhythm, etc.) |

---

## 12. Competitive Audit Mapping

The following table maps exercises from existing products onto the MuseFlow framework, demonstrating coverage.

### 12.1 Beato Ear Training Coverage

| Beato Category | MuseFlow Exercise IDs | Coverage Notes |
|---|---|---|
| Intervals - Harmonic | INT-008 (configured for harmonic pairs) | All Beato harmonic interval exercises map to a single MuseFlow exercise with interval-quality configuration varied |
| Intervals - Melodic | INT-008 (configured for melodic pairs) | Same exercise, different disposition configuration |
| Chords - Triads | CH-004 (quality filter = triads) | All triad quality identification exercises map here |
| Chords - 7ths | CH-004 (quality filter = 7ths) | Same exercise, different quality filter |
| Chord Progressions - Tonal | CP-001, CP-002 | Two-chord cadences (CP-001) and multi-chord ordering (CP-002) |
| Chord Progressions - Secondary | CP-003, CP-004 | Secondary dominant and secondary leading-tone exercises |
| Chord Progressions - Modal | CP-005, CP-006 | Modal triad identification and modal progression ordering |
| Chord Progressions - Extended | CH-004 (quality filter = extended) | Extended chord quality identification |
| Chord Progressions - Reharmonization | CP-007 | Reharmonization comparison exercises |
| Chords - Bitonal | CP-011 | Slash chord identification |
| Chords - Polychords | CP-012 | Polychord identification |
| Chord-Scales - Modal Voicings | SC-012 | Modal voicing → implied scale |
| Rhythm | RS-012 | Beat division selection exercises |
| Scales | SC-004, SC-005 | Scale identification (SC-004) and degree sequencing (SC-005) |
| Interval Progressions - Melodic | Special configuration of INT-008 with reference pitch and streak tracking | Sequential pitch identification with persistent reference tone |
| Interval Progressions - Harmonic | Special configuration requiring "inner note" identification | Shell voicing exercises |

### 12.2 Musictheory.net / Tenuto Coverage

| Tenuto Category | MuseFlow Exercise IDs | Coverage Notes |
|---|---|---|
| Note Identification | P-005 | Notated pitch → Named pitch |
| Key Signature Identification | SC-009 | Key signature + mode → Named root |
| Interval Identification | INT-005 | Notated interval → Named interval |
| Scale Identification | SC-001 | Notated scale → Named mode |
| Chord Identification | CH-001 | Notated chord → Named quality |
| Note Construction | P-001 (Recall method) | Named pitch → Notated pitch |
| Key Signature Construction | SC-010 | Named scale → Notated key signature |
| Interval Construction | INT-001 (Alteration method) | Named interval → Notated interval |
| Scale Construction | SC-006 | Named scale → Notated scale (add accidentals) |
| Chord Construction | CH-006 | Named chord → Notated chord (add accidentals) |
| Keyboard Identification exercises | P-009, INT-006, SC-003, CH-003 | Highlighted keys → Named entity |
| Keyboard Reverse Identification | P-006 (Recognition) | Notated pitch → Selected key |
| All Ear Training | P-014, INT-008, SC-004, CH-004 | Sounded entity → Named entity |

### 12.3 4four Coverage

| 4four Category | MuseFlow Exercise IDs | Coverage Notes |
|---|---|---|
| Bar Ear | RS-001 | See notation, match audio |
| Bar Eye | RS-002 | Hear rhythm, match notation |
| Beat | RS-003 | Hear rhythm, construct notation |
| Fill the Gap | RS-004 | Multi-modal: identify missing notation |
| Odd One Out | RS-005 | Multi-modal: identify mismatched notation |
| Tap It / Clap It | RS-006, RS-007 | Read and perform rhythm |
| Tempo Tap / Memory | RS-013, RS-014 | Tempo reproduction |
| Build the Groove | RS-016 | Groove construction |

---

## 13. Coverage Gaps and Expansion Opportunities

### 13.1 Areas Where MuseFlow Exceeds Competitors

- **Semantic input exercises**: No competitor systematically covers Semantic → Visual/Kinesthetic patches (construction/building exercises across all substrates)
- **Multi-modal input exercises**: Cross-modal (A+V) exercises like 4four's Fill the Gap and Odd One Out are rare in the market
- **Amplitude dimension**: No competitor systematically trains dynamics and articulation
- **Training method variety**: Competitors are almost exclusively Recognition (multiple choice). MuseFlow's Assembly, Alteration, and Verification methods are differentiated
- **Performance constraint parameterization**: No competitor offers the granularity of difficulty tuning that the tech spec model enables

### 13.2 Remaining Gaps to Address

- **Fingering exercises**: The substrate exists (X-004) but the exercise format and assessment method need detailed specification
- **Improvisation/free-play templates**: X-007 is a placeholder — needs detailed design for how open-ended exercises are structured, constrained, and scored
- **Multi-voice / polyphonic exercises**: Exercises involving two independent voices (left hand + right hand) are not yet fully specified
- **Transposition exercises**: Transforming music from one key to another is a compound substrate that cuts across many exercise types but isn't yet broken out as a dedicated exercise family
- **Notation-to-notation transformation**: Some exercises involve converting between notation systems (standard notation ↔ chord chart ↔ Roman numerals ↔ Nashville numbers) — this is a Visual → Visual patch with non-trivial transformation
- **Contextual embedding exercises**: Exercises where a trained substrate appears embedded within a larger musical context rather than in isolation. For example, identifying an interval that appears mid-phrase in a melody, or recognizing a chord quality within a progression where harmonic context creates ambiguity. These exercises operationalize the Contextual Transfer design principle (see Project Bible, Section 8.8) and bridge the gap between isolated drilling and real-world repertoire performance.
- **Amplitude exercises (deferred)**: The AMP-### family is fully specified in this document and in the substrate catalog but is deferred beyond V1 pending reliable programmatic dynamics assessment.

