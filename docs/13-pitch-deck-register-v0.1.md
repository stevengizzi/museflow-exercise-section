# Doc 13: Pitch Deck & External Communications Register

**Version:** v0.1
**Last updated:** 2026-05-12
**Maintainer:** Steven Gizzi
**Consumer:** Patrick Boylan (pitch deck assembly), plus any other external-comms needs

---

## What this document is

A living register of material intended for external communication: pitch decks, investor conversations, marketing copy, demo narration, partner introductions, hiring narratives. Distinct from the design canon (Docs 01–12) in that its content is *deliberately pitched for non-internal audiences* and is therefore distilled, jargon-stripped, and chosen for narrative impact rather than internal precision.

The register is **not a pitch deck itself**. It is the source material from which pitch deck slides, investor memos, marketing copy, and demo narration get assembled. Patrick (or anyone else doing external communication) consumes this and selects what fits the audience and format.

**Updating cadence:** Updated whenever the design canon adds material that is pitch-worthy, or when external communication surfaces a need the register doesn't yet cover. Not phase-gated; appends and revisions ongoing.

**Style:** Each section is written to be excerptable. Slides will have to compress further; this document is the medium-length version that the slide compression starts from.

---

## 1. Philosophy & Pedagogy

### 1.1 The Novelty-Automaticity Spectrum (one-paragraph version)

Skill acquisition operates between two poles. **Novelty**: content never repeats; trains generalization — the ability to apply skills to unseen music. **Automaticity**: content repeats with varied performance constraints; trains automatic execution — skills performed without conscious load. Pedagogical research is unambiguous that learners need both poles to reach fluency. MuseFlow operates the entire Spectrum deliberately.

### 1.2 The Novelty-Automaticity Spectrum (extended version)

A learner needs both poles. Pure novelty produces frustrated, unautomatized players who can read anything but execute nothing fluently. Pure repetition produces context-bound performers who play their drills perfectly but can't transfer those skills to new music. Mastery requires deliberate interleaving along the Spectrum.

Most existing music-learning products live at a single pole. Drill apps (ear trainers, theory trainers, scale practice) live at the Automaticity pole. Sight-reading-only apps live at the Novelty pole. Curated piece libraries live near the synthesis midpoint but lack pedagogical interleaving. **MuseFlow's positioning is that it operates the entire Spectrum deliberately, and the agentic system composes practice along it.**

MuseFlow's three content modes are distinct manifestations of the Spectrum:

| Mode | Spectrum position | What it does |
|---|---|---|
| **Sight Reading** | Novelty pole | Each piece served at most once; generator-driven; trains generalization |
| **Exercises** | Automaticity pole | Same content served repeatedly with varied constraints; trains automatic execution |
| **Repertoire** | Synthesis midpoint, with artistic-intent overlay | Real music; the medium where skill becomes meaning |

The architectural consequence: **one content generator, three policies**. At the level of raw musical material, the same generative pipeline produces content for all three modes; the mode determines how the material is scheduled, bounded, and presented. *Music is shapeless until we manifest it into one of the modes.*

### 1.3 What the Spectrum is in service of

Fluency removes limitations on movement. Movement freedom enables expression. Expression enables the user to make meaning through music. The Spectrum is the mechanism; meaning-making is the why. (This is the deepest framing; pitch contexts may surface this lightly rather than centrally.)

### 1.4 Positioning evolution: "songs vs. skills" → "the entire Spectrum"

MuseFlow's original pitch framing was "songs vs. skills" — implicitly a critique of competitors over-indexing on the Automaticity pole (drill apps, ear-training trainers) without sufficient novelty exposure. The matured framing is broader: MuseFlow operates the entire Spectrum deliberately. We no longer pitch as "the song-based alternative to drill apps"; we pitch as the system that interleaves novelty and automaticity in service of fluency and meaning-making. This evolution itself is investor-narratable: *we found the missing piece in our own product framing, which is why we know what the missing piece is in the category.*

---

## 2. Product Vision

### 2.1 MuseFlow as Tooling Ecosystem

MuseFlow is a **tooling ecosystem for piano learning**, composable by users (free-building) or by the MuseFlow AI (guided Projects). The ecosystem is the product. Individual modes, tools, and features are components within it.

This framing is load-bearing: the value of MuseFlow is not any single mode, any single AI capability, or any single content corpus. It is the integration — the ability to compose those components into a personalized learning experience that matches the user's goals, skill level, and pacing. *The ecosystem itself is the product.*

Two composition paths:
- **Guided Projects** — the user states a goal in natural language; MuseFlow AI composes a personalized roadmap through the ecosystem
- **Free-building** — the user composes their own path through the ecosystem without AI mediation (per Decision #41's Path Modes architecture and the AI-averse user constraint)

Both paths are first-class. The product is designed so that AI-averse users can engage fully without invoking AI; AI-engaged users get a personalized experience.

**The underlying principle** is what we call Universal Affordance Symmetry (Decision #61): *every capability the MuseFlow AI can perform has a manual, user-driven equivalent.* AI is a layer over the same product, not a separate product. The pitch line: *"MuseFlow's AI doesn't replace what you can do. It does what you'd do, in service of what you've said you want."*

### 2.2 The Three AI Roles

MuseFlow AI is not a single agent. It plays three distinct roles you'd recognize from any great teacher:

**The Coach** — relationship-scoped AI that knows your goals and journey. Maintains a model of your skill profile across all dimensions; interprets your goals; converses with you about progress; generates personalized roadmaps composed along the Novelty-Automaticity Spectrum; adapts when you go off-plan; decides when to switch modes.

**The Composer-Librarian** — content-scoped AI that creates and curates the right music for you. Sources from existing libraries; generates new content on demand (sight-reading material, exercise instances, etudes); modifies existing content (simplifying or complexifying repertoire, generating variations on a theme); evaluates content fit.

**The Practice Partner** — moment-scoped AI that's in every session with you. Controls performance constraints in real time (tempo, accuracy, looping); surfaces insights and advice ("your left hand is rushing at bar 12"); orchestrates the app the way a teacher in the room would (auto-looping, start-position movement, next-step decisions); senses engagement (frustration, boredom, flow state) and signals back to the Coach.

Each role decomposes into 4–6 specific capabilities. Each operates at different scope, latency, and cost profile. Together they constitute the AI ecosystem within the broader product ecosystem.

> **Team alignment note (2026-05-12):** The Three AI Roles framing was presented to the full team at the May 12 standup (Doc 14 §1.2) and received unforced convergence — Andrew, the team member who had not been on the May 7 brainstorm where the framework was developed, received it as natural, and Patrick and Staley reinforced the framing for pitch use. The Practice Partner example ("'Let's narrow in on this second line… I'm going to bring your tempo down 20 BPM…'") landed especially well as a demonstration of the role's scope. The framing is validated for pitch-deck and investor-conversation use.

### 2.3 What AI-Generated Content Looks Like

AI generation in MuseFlow is precise, not vague. Two patterns worth surfacing:

- **Etudes** — AI-generated music designed with explicit training intent. Sits between Exercise and Repertoire. Enough artistic shape to be playable; a fundamental guiding principle of the composition is to train a target skill. *Nobody plays an etude and is like, "this is a masterpiece" — and that's the point.* The framing acknowledges artistic intent without overclaiming artistic merit, sidestepping the trap of competing with human composers on artistic ground.

- **Variations on a Theme** — AI-mediated *modification* of existing repertoire (not generation from scratch). Takes a known piece (e.g., Chopin) and simplifies it to the learner's current level — or complexifies it as their skill grows. Operates on user-selected source repertoire. Sidesteps the artistic-merit question entirely while delivering substantial pedagogical value: the learner engages with real repertoire at their current level instead of waiting until they "deserve" it.

### 2.4 Why the user-modeling layer matters

The Coach's effectiveness depends entirely on its skill model of the user. The user-modeling layer (Decision #47) is the foundational architectural commitment that makes the agentic system work. Every roadmap, every content recommendation, every adaptive response builds on the skill model. This is why MuseFlow's substrate-level skill granularity matters: the model has the precision to make recommendations a less granular system cannot.

---

## 3. Technical Architecture (pitch-ready)

### 3.1 The substrate catalog as a foundation

MuseFlow's pedagogical model treats every piano skill as composed of named, addressable **substrates** — the discrete cognitive and motor operations that make up musical performance. Pitch-naming, interval recognition, chord-quality identification, scale construction, finger independence, hand coordination, pedaling — all are substrates with formal identifiers in MuseFlow's catalog. This granularity is the foundation that lets the AI reason precisely about what a user can and can't do, and prescribe practice that targets specific gaps.

The catalog is organized along four dimensions:
- **Frequency** (F-): pitch-domain substrates — what you hear and read in the pitch dimension
- **Time** (T-): rhythm-domain substrates — what you hear and read in time
- **Amplitude** (A-): dynamics-domain substrates (V2+)
- **Kinesthetic** (K-): motor-primary substrates — the physical-execution skills (finger patterns, hand coordination, pedaling)
- **Cross-domain** (X-): substrates that span multiple dimensions (sight-reading, fingering selection, expressive performance)

(For investor audiences who want detail, the catalog totals roughly 100 substrates across the families. For audiences who don't, the key claim is that this granularity exists and is what makes the AI's reasoning precise.)

### 3.2 Combinatorial exercise generation

Exercises in MuseFlow are not curated one-at-a-time. They are *generated combinatorially* from substrate × input-modality × output-modality × content-scope × training-method, with pruning rules removing trivial or invalid combinations. The result: a catalog of hundreds to thousands of distinct exercises from a small number of substrates and modalities — and the ability for the AI to generate new exercise instances on demand matching any user's specific needs.

### 3.3 The agentic system

The Coach reasons over the substrate catalog plus the user's skill model to compose Roadmaps — sequenced practice plans that interleave content along the Novelty-Automaticity Spectrum. The Composer-Librarian (powered by Mage as the algorithmic generation engine, with Opusmodus as the rendering tool, plus AI-mediated adjustment for musicality and goal-specific shaping) produces the content the Roadmap calls for. The Practice Partner operates in-session, controlling performance constraints and surfacing insights.

The cross-mode routing capability — same training goal served through Exercise, Repertoire, or Sight Reading — is enabled by the semi-lattice substrate-engagement layer: an atom's primary substrate defines its identity, but it engages other substrates derivatively through its modalities and content. This is why the Coach can decide to train finger independence through a Czerny exercise, a Bach invention, or a sight-reading level rich in five-finger patterns — they all engage the same underlying skill.

### 3.4 The user-modeling layer

A persistent model of each user's skill profile across the entire substrate catalog, performance-constraint capacity, motor competencies, repertoire history, learning rate, and characteristic struggles. This model is what the Coach reasons over. It is updated continuously as the user practices. (Per Decision #47, the user-modeling layer is recognized as a foundational architectural commitment, not an optional feature.)

### 3.5 What this means for cost economics

The three AI roles have very different cost profiles. The Coach is high-context and expensive per call, but low-frequency (users invoke it for goal-setting, plan revisions, major reflections). The Composer-Librarian is middle-cost but benefits enormously from content reuse across users (a generated etude valuable for one user is likely valuable for others with similar profiles). The Practice Partner must be cheap and fast — high-frequency, low-context per call; benefits from local-execution models or cached decision policies generated by the Coach in advance. This three-tier cost structure is what makes the economics work; flattening it (every AI call at Coach scope) would be unaffordable. (See Doc 09 §16 for detailed cost framework.)

---

## 4. Market Positioning

### 4.1 The category we define

MuseFlow does not fit neatly into existing music-learning product categories. We are not a drill app, not a sight-reading-only app, not a piece library, not a video lesson platform, not a teacher-replacement chatbot. We are a **tooling ecosystem for piano learning** that operates the entire Novelty-Automaticity Spectrum, composed for the user by an AI (or by the user themselves) into personalized learning experiences.

### 4.2 The competitive landscape (sketched)

Existing categories MuseFlow overlaps with — and what we add:

| Category | Examples | What they do | What MuseFlow adds |
|---|---|---|---|
| Drill apps | Tenuto, EarMaster, Functional Ear Trainer | Automaticity-pole training; isolated skill drilling | Spectrum interleaving; integration with repertoire and sight-reading; substrate granularity; AI-mediated personalization |
| Sight-reading apps | Sight Reading Factory, Note Rush | Novelty-pole generation | Substrate-driven generation; integration with the rest of the ecosystem; Spectrum framing |
| Piece libraries | Tonara, Soundslice | Repertoire access and practice tools | AI personalization; variations on a theme; integration with skills training |
| Video lesson platforms | Pianote, Skoove | Curriculum-driven video content | Live practice mediation (Practice Partner role); skill-model-driven personalization; substrate granularity |
| AI music tutors (emerging) | (Various early entrants) | AI-mediated lessons | Substrate-granular reasoning; user-modeling layer; tree-and-semi-lattice architectural depth |

The defensible moat is the **architectural integration** — the substrate catalog, the user-modeling layer, and the Spectrum-driven Roadmap composition that ties everything together. Any single competitor can build a drill app or a sight-reading app; what's hard to replicate is the integrated ecosystem with the user-modeling depth.

### 4.3 Positioning summary line

*"MuseFlow is the AI-powered piano-learning ecosystem that operates the entire spectrum from novelty to automaticity, composing personalized practice for each learner from a substrate-granular skill model."*

(Compression candidate for a single-line pitch. Subject to Patrick's pitch-deck-level refinement.)

---

## 5. Roadmap Proposals

**Status:** Skeleton. Detailed phasing is in flux per the V1 design work; this section is updated as Track D (V1 preset atom catalog), Track E (PRD), and the agentic system's investor-demo scope (Doc 09 §15.2) firm up.

### 5.1 V1 (investor-demo target)

- Exercise content mode with preset atom catalog (Track D output)
- Sight Reading content mode with parameter-driven generation
- Repertoire content mode with library access and practice tools
- Coach role: roadmap generation for goal-driven Projects; demo-defensible scope per Doc 09 §15.2
- Composer-Librarian role: generation-on-demand for Exercise and Sight Reading content; Variations on a Theme for Repertoire
- Practice Partner role: partial — performance constraint control, auto-looping (non-AI logic acceptable)
- User-modeling layer foundation (Decision #47)

### 5.2 V2 (post-demo expansion)

- Practice Partner role: AI-mediated insight surfacing, app orchestration
- Optimal Grip™ adaptive difficulty (V2 per Decision #17)
- ELO-style skill rating (V2 per Decision #17)
- Etude generation (Composer-Librarian extension)
- Amplitude-domain (A-) exercises (deferred per Decision #3)

### 5.3 V3+ (longer-horizon)

- AI warmup rituals and spaced repetition (V3 per Decision #17)
- Teacher tools and assignment flows (Decision #35; deferred phasing)
- Community-generated content marketplace (anticipated; not committed)
- Micro-PTA-targeted exercises (deferred per Doc 02 §6)

**Phasing-TBD discipline:** Most decisions in the canon describe *what* is being designed and explicitly leave *when it ships* open. Pitch communication should avoid binding phasing claims that the canon hasn't committed to.

---

## 6. Target Market

### 6.1 User taxonomy

MuseFlow serves piano learners across a wide skill range. Surface-level user goals cluster:
- **Repertoire goal** — "I want to play [specific piece]"
- **Utilitarian goal** — exams, credentialing, structured curriculum requirements (e.g., RCM, ABRSM)
- **Sight-reading goal** — improve fluency with new material
- **Technique goal** — specific skill (pedaling, finger independence, hands-together coordination)
- **Genre / style goal** — "I want to play like [artist]" or "I want to play [genre]"

Underneath these surface goals, the deeper telos is meaning-making — the desire to make music as an expressive act. The agentic system holds both layers: serves the surface goal directly while keeping the deeper goal in view.

### 6.2 The AI-averse user constraint

A meaningful segment of MuseFlow users do not want AI mediation in their practice. The product respects this: AI-averse users can engage with all content modes, browse catalogs, and use User Paths (self-authored progressions) without invoking the AI surface at all. The agentic system is opt-in, not the default user experience. (Per Doc 09 §12.)

This constraint has design consequences pitch-relevant to note: the modes are first-class without AI, the catalog is browsable directly, and User Paths are a peer to Projects rather than a degraded version of them.

### 6.3 Initial target segments (TBD per fundraising / GTM work)

(Placeholder; to be filled in coordination with Patrick's GTM strategy.)

---

## 7. KPIs

**Status:** TBD per V1 build and metrics work. Placeholder.

Candidate metric categories to develop:
- Engagement: practice time per user; session frequency; session arc completion
- Skill progression: substrate-mastery progression rate; cross-mode transfer signals
- Project completion: Roadmap node-completion rate; goal-attainment rate
- Engagement-sensing health: detected frustration/boredom episodes; recovery rate
- Cost: AI invocations per user; cost per active user; LTV/CAC if applicable

---

## 8. Investor Asks

**Status:** TBD per Patrick's fundraising work. Placeholder.

---

## 9. Team & Advisors

### 9.1 Current MuseFlow team

- **Steven Gizzi** — Founder/CEO. First-principles systems thinker; architect of MuseFlow's pedagogical framework (PTA Loop, FTA Field, Novelty-Automaticity Spectrum, substrate catalog, Three AI Roles framework). Leads product design.
- **Staley** — CTO. Engineering at the highest level; agentic system architecture; AI/ML infrastructure. Drives the technical platform that the AI roles operate on.
- **Andrew Urbanowicz** — VP of Engineering. Repertoire Builder, audio recognition, proactive notification system.
- **Asif** — Contractor. Primary implementer for the Exercise section.
- **Patrick Boylan** — Co-founder. Product, marketing, pitch deck, fundraising. Decomposes the macro PRD into MVP work.

### 9.2 Advisors and former team

- **Tom Urbanowicz** — Andrew's father; small angel investor and advisor; sales/marketing assistance.

(Former team members — Tucker Dean, Austin Clifton, Alayna L. Goss — are referenced in older canon documents but are not active.)

---

## 10. Pitch-Ready Glossary

> Concise, jargon-stripped definitions of MuseFlow-specific framework terms. Written for non-pedagogues. Each entry ≤ 2 sentences. For full definitions, see Doc 04 (internal glossary).

| Term | One-line definition |
|---|---|
| **Novelty-Automaticity Spectrum** | The central pedagogical axis: skill acquisition requires both novelty (unfamiliar content for generalization) and automaticity (repeated content for fluent execution). MuseFlow operates the entire spectrum deliberately. |
| **Fluency** | What the Spectrum produces when both poles are engaged — the ability to encounter unseen music and play it with embodied confidence. The goal of MuseFlow's pedagogical work. |
| **Shapeless Content** | The architectural insight that the same musical material can be served as Sight Reading, Exercises, or Repertoire depending on policy. One generator, three modes. |
| **The Three AI Roles** | The Coach (relationship-scoped), the Composer-Librarian (content-scoped), the Practice Partner (moment-scoped). |
| **The Coach** | Relationship-scoped AI. Maintains the user's skill model; generates personalized roadmaps; adapts to user progress. |
| **The Composer-Librarian** | Content-scoped AI. Sources, generates, and modifies music for the user. Mage is the implementation engine. |
| **The Practice Partner** | Moment-scoped AI. In-session real-time mediation — performance constraints, insights, app orchestration, engagement sensing. |
| **Substrate** | A named, addressable cognitive or motor skill in MuseFlow's catalog. Examples: pitch-naming, interval recognition, finger independence, pedaling-on-chord-change. |
| **Exercise Atom** | The smallest distinct skill to practice. Defined by substrate + input modality + output modality + target variables + pitch reference + content scope. |
| **Roadmap** | The Coach's output — a sequenced practice plan composed along the Spectrum. |
| **Project** | An AI-mediated path through MuseFlow's ecosystem. User states a goal; the Coach builds a Roadmap; the Composer-Librarian sources/generates the content; the Practice Partner mediates the sessions. |
| **Etude** | AI-generated music designed with explicit training intent. Sits between Exercise and Repertoire. Acknowledges artistic intent without overclaiming artistic merit. |
| **Variations on a Theme** | AI-mediated modification of existing repertoire — simplifying or complexifying along a complexity spectrum. Operates on user-selected source. |
| **MAGE** | The algorithmic music generation engine that powers the Composer-Librarian's generative work. |
| **Opusmodus** | The music-rendering tool MAGE uses to produce final notation. |
| **User-Modeling Layer** | The persistent model of each user's skill profile, performance capacity, repertoire history, learning rate, and characteristic patterns. Foundation of the Coach. |

---

## 11. Document Status

**Current version:** v0.1 (2026-05-12)
**Scope of v0.1:** Initial register with sections 1–4 substantively populated; sections 5–8 sketched or placeheld; section 9 current; section 10 stable.

**Anticipated next updates:**
- Section 5 expansion as Track D (V1 atom catalog) and Track E (PRD) firm up
- Section 6.3 (Initial target segments) when Patrick's GTM work surfaces them
- Section 7 (KPIs) when V1 metrics work begins
- Section 8 (Investor Asks) per fundraising round

**Consumer note for Patrick:** Sections 1–4 are pitch-ready as written. Sections 5–8 should not be excerpted until they firm up. Section 9 is current. Section 10 is the cleanest source of jargon-stripped definitions for slide copy.

---
