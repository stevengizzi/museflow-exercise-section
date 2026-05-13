# MuseFlow Agentic Vision

> **Status: Working Draft (May 2026).** This document captures MuseFlow's current thinking on the agentic system — the AI-mediated layer that helps users define goals, build personalized roadmaps, and generate custom content. It is **a freestanding artifact intended to be readable independently of the rest of the MuseFlow Exercise Section canon**, while cross-referencing that canon where useful. Substantial portions are speculative; speculation is marked inline with explicit tags. The document is expected to evolve as the Emergent Curriculum brainstorm and follow-on design work mature.
>
> **Audience:** Internal MuseFlow team (Steven, Staley, Andrew, Asif, Patrick), advisors (Tom), prospective investors and advisors via Patrick's pitch deck work, and future design-conversation partners (including potential subsequent Claude conversations seeded with this content).
>
> **Scope:** Vision, architectural framing, goals and roadmaps, AI surface, dashboard, custom content generation, MAGE-and-AI relationship, engagement layer integration, AI-averse user design constraints, open questions, and relationship to existing Exercise Section design work.
>
> **Version 0.1 (May 2026)** — Initial draft synthesized from the April 28 and May 5 standups, the Emergent Curriculum brainstorm follow-up, and the A1 doc-sync conversation that produced canonical document updates across the Exercise Section project.

---

## 1. Vision

### 1.1 The Strategic Claim

MuseFlow is building a music-learning system in which **the user states a goal in natural language and the product builds a personalized journey to that goal**, drawing on the full range of MuseFlow's capabilities — exercises, repertoire, sight-reading, and (over time) other content modes — and generating custom content as needed for gaps the standard catalog doesn't cover.

This goal-bound, AI-mediated layer is called **Projects**. The name is borrowed from the Claude/ChatGPT pattern, on the rationale that investors and educated users will recognize the idiom and immediately understand the shape of the feature.

Projects are not a wrapper that subsumes the rest of MuseFlow. They are a **first-class path mode** that sits alongside the existing Curriculum and a forthcoming "User Paths" feature that lets users author their own custom progressions without AI involvement. All three path modes are sibling experiences in the UI. The design explicitly respects users who do not want AI involvement and ensures they can engage fully with content and paths through MuseFlow without ever invoking the agentic surface.

### 1.2 The User-Modeling Layer

The strategic claim above is load-bearing only if the system can actually build a personalized journey for *this* user — which means the system needs to know who *this* user is, deeply, accumulating across sessions. **The per-user accumulating user-model is the technical capability that makes Projects work,** and it is recognized as a foundational architectural commitment (Decision #47), on par with the content/path-mode architecture (Decision #41) and the AI augmentation of MAGE (Decision #44).

**What it is.** The user-modeling layer is the architectural layer that observes, synthesizes, stores, and retrieves user-specific context across sessions: skill state, practice history, preferences, prior goals, prior generated content, conversational history, audio/MIDI performance signals, and AI-extracted summaries derived from all of the above. The agentic system reads from this layer to construct roadmaps, prescribe next steps, generate custom content tailored to the user, and conduct conversations that remember what was said before.

**What it is not.** It is not a single growing markdown file, despite team-internal framings like "Steven MD file" / "Patrick MD file" that surfaced in the May 7 brainstorm. Those framings are user-facing metaphors; the actual implementation pattern is closer to a per-user RAG layer over conversation history, structured event data from exercise/repertoire/sight-reading sessions, and curated AI-extracted summaries — with retrieval, summarization, and drift-correction logic that a single growing file does not provide. See §10.5 for the implementation sketch and §10.7 for the metaphor-vs-implementation distinction.

**Why it matters strategically.** Every other piano-learning product (Simply Piano, Yousician, Skoove, Flowkey) treats the user as roughly anonymous within content — the content is the product; the user consumes it. MuseFlow's per-user accumulating model is structurally different. It compounds over time. A user's MuseFlow account becomes more valuable to them the longer they use it, in a way competitors cannot easily replicate without the same architectural commitment from day one. This is the same dynamic that makes ChatGPT memory a stickiness lever, applied to a domain (skill development) where the per-user data is genuinely unique and pedagogically rich. It is not a feature comparison; it is a positional difference in what the product fundamentally *is*.

**Why it matters for "MuseFlow as AI company."** Two distinct interpretations of that framing exist, and they imply different team focuses. **LLM-layer expertise** — prompt design, model selection, inference cost optimization, fine-tuning — is the competitive edge under one reading. **User-modeling-layer expertise** — the data structures, retrieval logic, and synthesis pipelines that turn MuseFlow's playing/practice data into actionable agent decisions — is the competitive edge under the other. Both are defensible and they can coexist, but they are substantively different engineering investments. The implicit assumption that they are the same job will create gaps; team ownership of the user-modeling layer is a separate question from LLM-layer ownership and is currently open. See §13.7 #33.

**Cross-references.** §5.3 (persistence and reusability of generated content — the user-model's content-side substrate). §10.5 (the LLM and RAG architecture — the user-model's compute-side substrate). §10.7 (metaphor vs implementation discipline). §13.7 #33 (team-ownership question). §13.7 #34 (user-modeling-layer implementation architecture).

### 1.3 The Pitch Lines

Two lines that have crystallized in team conversations capture the essence of what MuseFlow is building:

> **"MuseFlow is what you do while your agents are doing everything else."** — Steven Gizzi

This line operates on two levels. The surface reading is positional: in an AI-economy world where automation handles the tasks people don't want to do, the time and attention liberated can be redirected to creative pursuits — and MuseFlow is the best way to spend that time on music. The deeper reading is structural: even within MuseFlow itself, agents are doing some of the work — building roadmaps, generating exercises, identifying gaps — so that the human can focus on the irreducibly human part: actually playing the instrument, hearing the music, refining the craft.

> **"MuseFlow is an app, an experience, that decides every step for you basically — it helps you, it knows every step that you need and it knows how much you need to practice. Every step of the way to mastery is figured out."** — Patrick Boylan, paraphrasing Steven

This is the customer-facing version of the value proposition: the friction of "what do I practice today?" disappears, replaced by a system that has answered that question for you given your stated goals.

### 1.4 Why Now

The shift to AI-native consumer products has created an opening for music-learning experiences that previous generations of edtech could not deliver. Existing music-learning products (Simply Piano, Yousician, Skoove, etc.) are largely fixed-curriculum experiences with limited adaptation; existing music theory and ear-training tools (Tenuto, Musictheory.net, 4four, Beato Ear Training) are largely fixed-catalog drilling apps. None of them stitch together exercises, repertoire, sight reading, and goal-bound progression in a way that meets the user where they are, with content custom-built for their specific objectives.

MuseFlow is positioned to deliver this for three reasons:

1. **The core engineering substrate exists.** MAGE (Music Algorithmic Generation Engine), MuseFlow's algorithmic music generation and complexity-analysis system, can already simplify a piece of repertoire by intentionally downgrading specific complexity metrics. The piece-simplification capability central to the Project demo (upload a piece → simplified version → roadmap to mastery) exists in algorithmic form today and needs only musical-similarity preservation logic to be demo-ready.
2. **The exercise framework is generative-first.** The MuseFlow Exercise Section is being designed from first principles as a combinatorial system (Project Bible §2; UX Spec §2): exercise atoms emerge from compositions of substrates, modalities, target variables, and content scopes. This means generation on demand is a natural extension of the existing architecture, not a parallel feature — the agentic system can inherit the exercise framework directly.
3. **The team composition is unique.** Two engineers (one a classically trained pianist), one music educator and performer, one engineer who is also a pianist, plus product, marketing, and content perspectives. Per Patrick: "Nobody else can do what we're doing right now... and what we decide to build is inherently going to be very unique because we have an incredible amount of skill across the four of us."

### 1.5 What This Document Is and Is Not

**This document is** an articulation of MuseFlow's current thinking about the agentic layer, written to be useful for team alignment, investor conversations, and seeding follow-on design work.

**This document is not** a finished spec. The agentic system is in early-design state. UX is unspecified, schema details are minimal, the AI architecture is genuinely open (see §10), and many of the most interesting questions are explicitly listed as open in §13. Readers should treat the architectural framing in §3 and the conceptual boundaries laid out in §2 as committed thinking, and treat most everything else as **subject to revision**.

### 1.6 The Three AI Roles
 
MuseFlow AI is not a single agent. It is a system that plays **three distinct roles**, each operating at a different scope, with different latency requirements, different data dependencies, different infrastructure, and different cost profiles. Articulating the roles explicitly serves two ends: internal prioritization (each role has different engineering paths and cost economics) and external communication (the role framework gives the pitch a clean three-line summary that decomposes into specific capabilities). Per Decision #59.
 
The three roles, layered from broadest scope to narrowest:
 
#### 1.6.1 The Coach (Relationship-Scoped)
 
The Coach operates across the user's entire journey with MuseFlow — weeks, months, years. It is the role most analogous to a human teacher who knows the student and their goals over time.
 
**Functions:**
 
- **Skill model maintenance.** Continuously builds and updates a model of the user's current skill profile across all dimensions: substrate mastery (per the catalog in Doc 02 §3.1, including the K-substrate family per Decision #57), performance-constraint capacity, motor competencies, repertoire history, learning rate, characteristic struggles. The user-modeling layer (Decision #47) is foundational to this function.
- **Goal interpretation.** Translates user-stated natural-language goals into pedagogically actionable directives. ("I want to play Clair de Lune" → inferred prerequisite skills, current gaps, realistic timeline, modular sub-goals.)
- **Pedagogical dialogue.** Converses with the user about goals, progress, struggles, and adjustments. The non-judgmental coaching partner. Lives in the AI Surface (§6).
- **Curriculum / roadmap generation.** Composes a sequenced practice plan — the Roadmap (§5) — deliberately interleaving along the Novelty-Automaticity Spectrum (see §5.6). Per Decisions #56 and #59.
- **Plan adaptation.** When the user goes off-plan (skips sessions, plateaus, jumps ahead, gets bored), repairs the roadmap rather than failing rigidly. Per §5.5.
- **Cross-mode orchestration.** Decides when to switch modes — when to move the user from Exercise drilling to Repertoire practice to Sight Reading challenge. This decision is the Coach's Spectrum-routing operation; without it, the user gets a mode-pinned experience that misses the Spectrum's interleaving discipline.
**Characteristics:** High-context, low-frequency, can be expensive per call. Acceptable latency: seconds to tens of seconds. Cost profile: most expensive AI calls in the system are Coach-level reasoning; users should not invoke them frequently. (See §16 Cost Considerations.)
 
#### 1.6.2 The Composer-Librarian (Content-Scoped)
 
The Composer-Librarian operates within each content mode, producing or selecting the actual musical content the user practices with. It is the role analogous to a teacher choosing or composing the right material for a specific lesson.
 
**Functions:**
 
- **Sourcing.** Selects from existing content libraries — most prominently the Repertoire library (likely external sources curated for MuseFlow); also the preset Exercise atom catalog, and increasingly the user's own previously-generated content as it accumulates.
- **Generating.** Creates new content on demand. Three concrete sub-cases: (a) sight-reading material matched to parameters; (b) exercise instances within an atom's content scope per Decision #33; (c) **etudes** — AI-generated repertoire designed with explicit training intent per Decision #60.
- **Modifying.** Transforms existing content. Concrete sub-cases: (a) **variations on a theme** — simplifying or complexifying existing repertoire along a complexity spectrum per Decision #60; (b) transposing; (c) isolating sections; (d) generating drill-friendly versions of repertoire excerpts.
- **Evaluating.** Judges whether existing or generated content matches a pedagogical need — necessary for sourcing to work intelligently and for the Coach to specify content requirements abstractly without micromanaging every detail.
**Characteristics:** Medium-context, medium-frequency, benefits from caching and reuse. Acceptable latency: seconds. Cost profile: middle-cost; benefits enormously from content reuse across users (a generated etude that proves pedagogically valuable for one user is likely valuable for others with similar profiles — see Decision #33's downstream implications).
 
Mage and Opusmodus are implementation tools within this role — see §10.
 
#### 1.6.3 The Practice Partner (Moment-Scoped)
 
The Practice Partner operates within a single content piece in a single session — the next few seconds to the next few minutes. It is the role analogous to a teacher physically in the room with the student during practice.
 
**Functions:**
 
- **Performance constraint control.** Real-time modulation of tempo, accuracy thresholds, mastery thresholds, loop boundaries. Per Decision #46 (Agent-Controllable Repertoire Practice Control Surface) and the parallel control surfaces for Exercise and Sight Reading (§6A).
- **Insight surfacing.** Contextual observations, hints, advice delivered at the right moment. *"Your left hand is rushing at bar 12." "Try this section with a slower tempo first." "You've nailed this; let's add the pedal."*
- **App orchestration.** Automates the interaction layer the way a teacher in the room would: triggers auto-looping, moves the user's start position automatically, makes decisions about next steps, manages the session arc. Akin to having an actual music teacher controlling the app's repertoire controls on the user's behalf.
- **Engagement sensing.** Detects frustration, boredom, flow state from interaction patterns (latency, error patterns, session abandonment). Signals up to the Coach for journey-level adaptation; signals laterally to the Composer-Librarian when content-fit appears off.
**Characteristics:** Low-context (per call — though built on top of skill-model state from the Coach), high-frequency, must be cheap and fast. Acceptable latency: milliseconds to a second. Cost profile: lowest per-call cost; aggregate cost can dominate if naively implemented (called every few seconds during practice); benefits from local-execution models, on-device inference, or cached decision policies generated by the Coach in advance.
 
#### 1.6.4 Why This Framing Matters
 
**For engineering:** The three roles have fundamentally different infrastructure requirements. Conflating them produces poor decisions — using Coach-grade reasoning for Practice-Partner-scoped decisions, or trying to make the Practice Partner stateful in ways that should live in the Coach. Explicit role-scoping prevents this category of error.
 
**For prioritization:** Each role has its own R&D path. The Practice Partner is partially present today (auto-looping, basic constraint control) under non-AI logic; AI-mediated Practice Partner is a future expansion. The Composer-Librarian is R&D-active (Mage generation work, Decision #44). The Coach is the most ambitious; demo-defensible scope for the investor demo (§15.2) is the V1 target.
 
**For pitch:** *"MuseFlow's AI plays three roles you'd recognize from any great teacher: a coach who knows your goals and journey, a composer-librarian who creates and curates the right music for you, and a practice partner who's in every session with you."* Each role decomposes into 4–6 specific capabilities, so the pitch can drill from the three-line summary down to specific functionality without losing the through-line. See Doc 13.
 
**For team alignment:** The recurring "Mage vs. Opusmodus" framing tension dissolves under role-scoping. Both are implementation tools within the Composer-Librarian role; their relationship is renderer-and-generator within a single layer, not a competition. See §10.

---

### 1.7 Universal Affordance Symmetry

The principle that holds the agentic layer composable with the rest of MuseFlow: **every capability the MuseFlow AI can perform has a manual, user-driven equivalent.** AI mediation is a layer over user-accessible primitives, not a replacement for them. Settled as canon on May 12, 2026 — see Decision #61 in the Design Decisions Log; sourced from the May 12 standup discussion where Steven articulated the principle and the team aligned.

#### 1.7.1 What the Principle Says

For every capability the AI exposes, the equivalent user-driven affordance exists as a first-class part of the product. Per AI Role:

- The **Coach** interprets a stated goal, composes a roadmap, adapts plans, switches modes. The user-driven equivalent: state a goal manually (or skip stating one), construct a User Path (Decision #41), edit the roadmap directly, switch modes through the navigation.
- The **Composer-Librarian** sources from libraries, generates new content on demand, modifies existing content (simplify / complexify / transpose), evaluates fit. The user-driven equivalent: browse the preset catalog and library, author custom content via the Repertoire Builder (Decision #34), choose simplification/transposition manually, judge fit themselves.
- The **Practice Partner** controls tempo / accuracy / looping in real time, surfaces insights, orchestrates auto-loop and start-position movement, senses engagement. The user-driven equivalent: every control surface already exists as a manually-operable affordance — the Practice Partner controls what the user can also control directly.

Authoring origins (§3.3) follow the same symmetry: AI-generated content is one of four origins (alongside MuseFlow preset, user-generated, community-generated). It does not displace the others; it sits parallel to them at every authored hierarchy level (atoms, blueprints, paths, roadmaps, Projects).

#### 1.7.2 Why This Matters

*The Tooling Ecosystem framing depends on it.* MuseFlow's product positioning (Doc 13 §2.1) is that the ecosystem is composable manually or by AI. That positioning works only if every tool in the ecosystem is, in fact, a tool — accessible to direct manipulation. If AI-only capabilities exist, the ecosystem fractures into two products: the manual MuseFlow and the AI MuseFlow. The symmetry principle prevents that bifurcation.

*The AI-averse-user constraint becomes structural.* MuseFlow commits to serving users who prefer to engage without AI mediation (Decision #41 and the broader project working principle). Symmetry makes that commitment structural rather than aspirational: a user who never touches AI features must still have access to the full product.

*Design discipline against silent AI-only features.* Each feature designed under this principle is testable: *what's the user-driven equivalent?* A feature design that fails the test is incomplete. The principle becomes a load-bearing constraint on the PRD, Track C2 UI-shape work, and all subsequent design work.

#### 1.7.3 What the Principle Does Not Say

The principle does **not** require that every feature ship its manual equivalent in the same release as the AI-mediated version. Phasing per capability is open. It requires only that the design contains the user-driven affordance as a first-class element. (Example: AI-mediated Projects and manually-authored User Paths are both first-class per Decision #41; their release timing may differ.)

The principle is **silent on tier-gating**. Whether pricing tiers gate the AI-mediated path only, or both the AI-mediated and the manual paths independently, is an open question (Doc 12 T-098) gated on pricing-design work beginning (Decision #37).

The principle does **not** assert that the AI-mediated and user-driven paths are equally rich. The AI-mediated path may operate over more context (the agent has access to the full skill model, the full atom-engagement graph, the full corpus) and produce results the user could not practically derive themselves at scale. The symmetry is *categorical*, not *capacity-equivalent*: the user can do the same kind of thing, even if not at the same scope.

#### 1.7.4 Cross-Reference Map

The principle touches multiple existing canon items:

| Canon item | Relationship |
|---|---|
| Decision #29 (Agentic Vision) | The agent layer is composable because of symmetry |
| Decision #34 (Repertoire Builder custom authoring) | The Composer-Librarian's manual equivalent |
| Decision #41 (Content Mode + Path Mode Architecture) | User Path is the symmetry partner of AI-mediated Projects |
| Decision #46 (Agent-Controllable Repertoire Practice Control Surface) | Pre-existing user-controllable surface validates symmetry was already de-facto canon |
| Decision #59 (Three AI Roles) | Symmetry applies per role |
| §3.3 Four Authorship Origins | Symmetry at the authoring-origin level |
| §6.4 (The AI Surface Is Not the Only Way to Use MuseFlow) | Restates the principle at the AI-Surface level |
| Doc 13 §2.1 (Tooling Ecosystem) | Pitch-deck-level expression of the principle |
| Doc 12 T-098 | Open question on tier-gating interaction |

---

## 2. The Project Concept

### 2.1 Definition

A **Project** is a goal-bound, AI-mediated path through MuseFlow's content modes, composed by the MuseFlow AI in conversation with the user. A Project has:

- A **goal** — a statement of user intent, expressed in natural language
- A **roadmap** — a structured plan of steps that, if followed, advance the user toward the goal
- A **conversational surface** — the AI interface where the user articulates and refines goals, asks for adjustments, gets explanations, and converses with the system about their progress

A Project does **not** contain content directly. Its roadmap consists of **references** to content that lives in MuseFlow's content modes (Exercises, Repertoire, and — when it formalizes — Sight Reading). When the agent identifies that the standard catalog is missing something the goal requires, it triggers the creation of new content, which is generated and stored in the appropriate content mode tagged with `authoring_origin = agent`. The Project's roadmap then references that new content, just as it references preset content.

### 2.2 The Two Faces of a Project

A Project is best understood as having two distinct user-facing surfaces:

**The conversational surface** is where the user interacts with the AI: stating goals, refining them, asking questions, requesting adjustments to the roadmap, getting explanations of why a particular exercise was prescribed, asking the AI to simplify or expand on the plan. This surface is fundamentally a chat-like interaction.

**The roadmap container** is where the user views and works through the structured plan. It is fundamentally a navigable artifact — an ordered (or partially-ordered) sequence of nodes, each pointing at a piece of content (an exercise atom, a piece of repertoire, a sight-reading target, a free-play interlude, etc.). The user can see what's coming, mark progress, jump ahead, revisit completed sections.

These two surfaces serve different purposes and may be presented differently in the UI. A user editing their goal is in conversation; a user practicing their next prescribed exercise is in the roadmap container; a user reviewing their progress against the goal is consulting both. The relationship between the two surfaces — how they're navigated, when each is dominant, how they share state — is an open UX question (see §13).

### 2.3 The Architectural Principle

Projects exemplify a principle that runs throughout MuseFlow's architecture:

> **Content lives in content modes; paths reference content; authorship is a property of content and of paths, not of mode.**

This principle has several practical consequences:

- A custom exercise generated by the AI for a Project remains in the Exercise content mode after the Project concludes. The user can revisit it, refer to it, or reuse it in subsequent Projects.
- A user can browse to "AI-generated exercises" within the Exercise content mode and see all exercises the AI has ever generated for them, regardless of which Project triggered each.
- A teacher's hand-authored exercise is interchangeable in roadmap nodes with a system preset exercise — both are valid content references.
- Adding a new authorship origin (e.g., when the community marketplace launches) does not require restructuring how Projects work. New content shows up in the modes; Projects can reference it.

This principle is what makes the agentic system architecturally clean: it doesn't introduce a parallel content pipeline. It introduces a new layer (path mode) that operates on the same content store every other layer operates on.

---

## 3. Architectural Foundation

### 3.1 Where Projects Sit in MuseFlow's Architecture

MuseFlow is organized into two categories of mode (see Project Bible §2):

**Content modes** are surfaces where musical material lives and is engaged with directly. Currently confirmed: Exercises, Repertoire. Anticipated: Sight Reading. Candidate (status open): Theory, Free Play.

**Path modes** are structured progressions through content modes. Three path modes:
- **Curriculum** — preset paths authored by MuseFlow, used by many users
- **User Paths** — custom paths users author for themselves (naming TBD)
- **Projects** — AI-mediated, goal-driven paths composed per-user (this document's subject)

The three path modes are **sibling experiences** in the UI. None is a primary path mode; none is a fallback for the others. Users choose between them based on whether they want a preset, self-curated, or AI-built journey. All are first-class.

### 3.2 The Three-Flow Pattern

Each content mode supports three primary user flows:

- **Browse** — explore available content, with a filter axis along authorship origin
- **Generate** — create custom content using the mode's generation tool
- **Project** — declare a goal and work with the MuseFlow AI to compose a roadmap

Two important consequences:

**The Project flow is reachable from inside any content mode.** A user browsing Exercises can pivot to "ask the AI to build a roadmap that includes this kind of practice" without first going to a separate destination. This is in addition to the top-level Projects dashboard (see §7). The Project flow effectively has two doors: dashboard-first and content-first.

**The flow pattern generalizes.** A new content mode (whether Sight Reading, Theory, or something not yet imagined) inherits the three-flow pattern automatically. The Project flow is one of the things that makes a content mode a content mode.

### 3.3 The Four Authorship Origins

Content within a content mode (and paths within a path mode) carry one of four authorship origins:

| Origin | Description |
|---|---|
| **MuseFlow preset** | Curated content shipped with the app |
| **User-generated** | Created by the user through the mode's generation tool |
| **AI-generated** | Created by the MuseFlow AI in service of a Project goal or direct user command |
| **Community-generated** | Content from other users or shared via a marketplace (future) |

Projects are paths with `authorship_origin = AI`. Custom exercises generated for a Project are content with `authorship_origin = AI`. User Paths are paths with `authorship_origin = user`. Curriculum is paths with `authorship_origin = MuseFlow preset`. The same vocabulary applies across content and paths, content modes and path modes.

Browse-by-authorship-origin is a primary filter axis in both content-mode browsing (e.g., "show me only AI-generated exercises") and path-mode browsing (e.g., "show me only my own User Paths"). This filter is what gives AI-averse users the ability to engage fully with the product without seeing AI-generated content if they don't want to.

### 3.4 Why This Architecture Supports the Agentic Vision

Three architectural properties make the agentic vision feasible:

**1. Atoms are agent-prescribable.** The Exercise Atom (UX Spec §2.1) is the smallest indivisible unit of distinct practice — defined by substrate family, input modality, output modality, target variables, pitch reference mode, and content scope. The atom is the right granularity for an agent to prescribe: "practice this specific atom until you clear it at the Recall level" is a complete, executable instruction. Coarser granularity ("practice chords") is too vague for an agent; finer granularity (individual prompts) is below the level where reasoning happens.

The atom schema (Architecture Doc §8.1, Decision #40) includes metadata explicitly designed for agent path-building:
- `prerequisite_atoms` — what must be cleared first
- `mastery_thresholds` — per-method clearance criteria
- `mobile_supported` — device-aware prescription
- `authoring_origin` — distinguishes system, teacher, user, agent
- `generation_mode` — flags atoms whose content is produced on demand

**2. The content space is hierarchical and navigable.** Atoms cluster into molecules; molecules into strands; strands into clusters (UX Spec §2). The agent can reason at any level: "this user needs work on the Chords × Ear Training cluster, specifically molecules 3 and 4 in the strand" is a coherent agent statement. The hierarchy gives the agent a structured space to plan within.

**3. Generation is a first-class capability.** Because atoms are combinatorial (UX Spec §2.1), the agent can construct novel atoms (specific combinations of identity dimensions not present in the catalog) and instantiate them with parameterized or on-demand content. This is true today and need not wait for AI infrastructure to mature — the framework supports it now.

---

## 4. Goals

### 4.1 What a Goal Is

A goal is a statement of user intent, expressed in natural language, that anchors a Project. Goals are the input to the AI; the roadmap is the output.

### 4.2 Types of Goals

Goals span a wide range of specificity and ambition. The conceptual types below are the primary categorization; the May 7 brainstorm surfaced five concrete categories that drive demo and Track D / E prioritization, mapped to the conceptual types where each fits.

**Conceptual types:**

- **Repertoire-bound**: "I want to learn this piece" (with an upload of the score, or a search for an existing piece in the MuseFlow library)
- **Curriculum-bound**: "I need to pass the music theory portion of my college audition exam" / "I want to prepare for Grade 5 ABRSM"
- **Performance-bound**: "I want to get a gig at a piano bar" / "I want to be able to accompany my church choir"
- **Skill-bound**: "I want to get better at hearing jazz chord progressions" / "I want to improve my left-hand independence"
- **Experience-bound**: "I want to spend 30 minutes a day doing music in a way that feels like progress"
- **Open-ended**: any natural-language statement of musical intent

**The five demo-relevant categories (per May 7 brainstorm).** These are the user-story shapes the team is targeting for the integrated demo and for near-term Track D / E prioritization. They map onto the conceptual types but cut differently:

1. **"I want to learn this specific piece"** — Repertoire-bound. Same as canonical.
2. **"I'm studying for this specific exam"** — Curriculum-bound. Same as canonical. (ABRSM grades, audition prep, music-theory exam, etc.)
3. **"I want to get better at this specific technique"** — narrower than Skill-bound; targets a specific named technique (e.g., Alberti bass, ornamentation, scales-in-thirds).
4. **"I want to play like this specific musician/artist"** — new framing not exactly in the conceptual types. Goal is style-matching, often blending Repertoire- and Skill-bound elements (e.g., "play like Bill Evans" implies both specific pieces and stylistic techniques like rootless voicings).
5. **"I'm really interested in this specific genre"** — new framing. Genre-bound exploration (e.g., "I want to learn bluegrass"); typically blends Repertoire-, Skill-, and Curriculum-bound elements depending on whether the user wants pieces, technique mastery, or theory understanding.

Patrick (May 7, line 1540): "all of those will be a combination of exercises, sight reading and repertoire." Steven adds theory and (per Patrick) videos. Goals can be specific (a single piece, a single skill) or broad (general improvement). They can have explicit deadlines (an audition date) or be open-ended. The agent's job is to take whatever the user states and decompose it into a roadmap that's actionable.

### 4.3 Goal Articulation

The user articulates a goal through the conversational surface. The agent may ask clarifying questions to refine the goal:

- "When is the audition?" → adds a deadline constraint
- "What level of experience do you have with this kind of repertoire?" → calibrates the starting point
- "How many days a week can you practice, and for how long?" → bounds the roadmap pacing
- "Do you want this Project to focus only on this piece, or should it also work on related skills you'll need?" → bounds the scope

This is a design surface, not a rigid script. The conversation should feel like talking to a knowledgeable teacher who's helping you shape a practice plan — not like filling out a form.

**The diagnostic-agent / auto-engaged-plan-mode behavior.** When goal-articulation signals are present in the user's message, the agent operates in a "diagnostic" or "auto-engaged plan" mode — it fires follow-up questions until enough context exists to construct a roadmap. The behavior is borrowed by analogy from Claude Code's plan mode (the system enters a planning posture before acting). The behavioral specification is clear: when the user signals goal-articulation, the agent prioritizes context-gathering over immediate action; once enough context is gathered, the agent transitions to roadmap construction.

**Behavioral spec, not implementation spec.** The implementation pattern is open and has at least two candidate shapes with very different cost / control / failure-mode profiles:

- **Prompt-level** — the system prompt has a "diagnostic" section that activates when the model classifies the user's message as goal-articulation. Cheap, flexible, depends on LLM zero-shot classification reliability. Failure modes: too-eager (the user gets interrogated when they just wanted to chat) or too-slow (the conversation drifts before transitioning to planning).
- **Application-level** — the app has explicit modes between which the user (or the system) navigates, gating available actions and tools. More deterministic, requires explicit UI affordances and probably an explicit "start a Project" entry point that puts the user into diagnostic mode.

The two are different to build, with different cost profiles and failure modes. The team should pick deliberately rather than adopt the analogy as if it specified the implementation. See §10.7 for the broader metaphor-vs-implementation discipline this exemplifies, and §13.4 for the open question.

### 4.4 Goal Decomposition

[Speculative — the specific decomposition logic is not yet designed.] When the user states a goal, the agent should be able to identify:

- **What skills the goal requires** (e.g., to play this piece you'll need a comfortable left-hand jump of a tenth, fluent reading in three flats, and some experience with rubato)
- **What the user's current state is on those skills** (drawn from atom mastery data, repertoire performance data, sight-reading history)
- **What the gap is between current state and goal**
- **A roadmap that closes the gap** (a sequence of exercises, repertoire pieces, sight-reading targets, custom-generated content as needed)

The decomposition is the agent's most ambitious job. It requires a model of how musical skills compose, what prerequisites cascade into what targets, and how to pace a learner through a sequence without losing them. None of this is solved. See §13.

### 4.5 Multi-Goal Projects (Speculative)

[Speculative — design implication of cross-project orchestration; see §5.4.] A user may want a single Project to encompass multiple related goals (e.g., "I'm preparing for an audition and I also want to improve my sight-reading"). Whether this is one Project with two goals, two Projects sharing context, or something else is open. Patrick's framing of MuseFlow as "an experience that decides every step for you" suggests the user shouldn't be required to manage Project boundaries themselves — the system should make it easy.

---

## 5. The Roadmap

### 5.1 What a Roadmap Contains

A roadmap is the structured output of the agent's goal-decomposition process. It consists of an ordered (or partially-ordered) sequence of **nodes**, each of which references a piece of content. The roadmap is the user-facing artifact; it's also the agent's plan, so it must be simultaneously interpretable by the user and executable by the system.

### 5.2 Node Types

Several node types are anticipated. This list is not exhaustive — it represents current thinking and may evolve.

**Content reference nodes**:
- **Exercise atom node** — points at a specific atom (from the system catalog or AI-generated)
- **Repertoire node** — points at a specific piece (preset, user-uploaded, or AI-arranged simplification). When the agent prescribes a repertoire node, it can also prescribe a *practice mode* — the orchestration policy the agent applies during the session. The auto-looping / perfect-practice tree algorithm (Decision #42) is one such practice mode: identify problem sections from green-note history, set up looping with specific start/end and takes-required, optionally adjust tempo and accuracy threshold. Other practice modes will emerge as the broader repertoire control surface (Decision #46; see §6A) is built out.
- **Sight-reading node** — points at a sight-reading target (preset level, user-generated custom level per Decision #45, or AI-generated custom level)

**Structural nodes**:
- **Milestone marker** — a non-executable node that represents an achievement or checkpoint ("you've completed the foundation phase")
- **Conditional gate** — a node whose advancement depends on demonstrating mastery of preceding nodes ("clear molecule X at REC level before advancing")
- **Free-play interlude** — [Speculative] a node that prompts unstructured play between drill blocks; status as a content mode vs. roadmap primitive vs. neither is open. Open Play (original sense — improvisation without notation guidance; renamed from "Free Play original sense" by Decision #49 Part 2) is deferred indefinitely per Decision #41's candidate-content-modes list. See Bible §2.1.1.

**Adaptation nodes**:
- **Reassessment node** — a moment where the agent re-evaluates the user's state and may modify the remaining roadmap
- **Branch point** — a node where the user chooses between alternative paths (rare, but useful when goals admit multiple valid sequences)

**Candidate node types (deferred / placement open)**:
- **Tutorial node** — points at an Interactive Tutorial (animated video + live-action hand clips + Phaser-JS exercises gated mid-flow; see Glossary). Each Sight Reading curriculum level is preceded by one in current canon. Whether tutorials should be prescribable as roadmap nodes by the agent — vs. living only inside Curriculum, vs. having their own content mode — is open. Per Staley's framing in the May 7 brainstorm: "those would actually fit very well into these custom generated paths or road maps or like plans, but like as single nodes that are just like, okay, here's like a concept that this person needs to know." See Doc 10 §4.3, §6 #15–#16.
- **Video node** — points at a video-only resource (no interactive component). Surfaced as a candidate during the May 7 brainstorm; placement open and clusters with the broader open question of what content classes exist beyond the core three (Exercise, Repertoire, Sight Reading). See Doc 10 §6 #11, §6 #15.

The set of node types is open. New types should be added as they're discovered to be needed. The architectural placement of Tutorial and Video nodes — whether they are roadmap primitives, members of a separate content class, or both — clusters with the broader content-classes-beyond-the-core-three question and is tracked as an open architectural cluster in §13.

### 5.3 Persistence and Reusability of Generated Content

When the agent generates new content (a custom exercise atom, a simplified repertoire arrangement, a custom sight-reading level), that content is stored in its respective content mode tagged with `authoring_origin = agent`. Two consequences:

1. **Generated content is persistent.** A Project that ends doesn't take its generated content with it. The user retains all the custom exercises the AI built for them; they show up in Browse-by-origin filtered to "AI-generated" within the Exercise content mode.

2. **Generated content is reusable.** A subsequent Project can reference content the user already has, including content the AI generated for an earlier Project. The agent doesn't have to regenerate from scratch each time; it can identify existing content that fits the new goal.

This persistence-and-reuse property has practical implications: the user's content library grows over time, and earlier AI investments compound. It also has cost implications (see §10): generation is a one-time cost; reuse is free.

### 5.4 Cross-Project Orchestration ("Air-Traffic Control")

Steven's framing from the May 5 brainstorm:

> "First of all, why don't we take these three steps first? Because you're going to need to do all three… If you do this, this will advance you towards three of your goals. If you do this, this will only advance you towards one."

When a user has multiple active Projects, the agent should be able to identify overlap between their roadmaps and sequence content in service of multiple goals at once. A single exercise might count toward Project A, Project B, and Project C; a single piece of repertoire might serve two Projects; a foundational skill needed by all three should be addressed early because it has the highest leverage.

This is an aspirational capability, not a designed one. Several questions are open:

- How is cross-project overlap visualized? Is it a separate view (a unified "what should I do today" dashboard) or part of each Project's individual roadmap?
- Does the agent ever propose merging Projects? Or does it always preserve their separation while routing content efficiently?
- How does the user weigh in if they disagree with the agent's prioritization across goals?

These questions are tracked in §13.

### 5.5 Roadmap Adaptation

[Speculative.] A roadmap is not static. As the user practices, the agent observes their performance (via Exercise Result data, repertoire performance data, etc.) and may update the roadmap:

- **Promotion** — the user is clearing nodes faster than expected; the agent advances them to harder material
- **Remediation** — the user is struggling on a node; the agent inserts prerequisite work before the original target
- **Reassessment** — the agent's initial gap estimate was wrong; the goal needs more or less work than originally planned

The mechanics of adaptation — how often the agent re-evaluates, how much it can change without consulting the user, how the user is informed — are open design surfaces.

### 5.6 Spectrum-Driven Roadmap Composition
 
The Coach role's roadmap generation function (§1.6.1) is not arbitrary content sequencing. It is **deliberate interleaving along the Novelty-Automaticity Spectrum** (Doc 01 §2.4; Decision #56). This section specifies the discipline.
 
#### 5.6.1 The Composition Principle
 
A strong roadmap rotates content along the Spectrum:
 
- **Block practice through Exercise** to build a skill (Automaticity pole). The user repeats atom content with varied performance constraints until mastery thresholds clear.
- **Mixed practice through Repertoire** to integrate the skill in artistic context (synthesis midpoint). The user plays real music where the skill recurs alongside others, in composed structure.
- **Random practice through Sight Reading** to generalize the skill to unseen material (Novelty pole). The user encounters the skill in unfamiliar contexts, forcing transfer.
This is **contextual interference applied as design philosophy**. Pedagogical research (Shea & Morgan 1979 forward) establishes that high-interference practice produces worse immediate performance but stronger retention and transfer. Pure block practice (one mode only, repeated drilling) feels efficient but generalizes poorly; pure random practice (sight-reading only) builds adaptable skill but no fluent execution. The Spectrum framework prescribes deliberate mixing.
 
#### 5.6.2 What Makes Cross-Mode Routing Possible
 
The same training goal can be served via different modes because each mode's atoms incidentally engage substrates beyond their primary. This is the **semi-lattice substrate-engagement layer** (Decision #58). Per Doc 02 §3.2:
 
- A Hanon atom (primary K-A3) incidentally engages F-A2 (notation reading) and T-A2 (rhythm reading) via Visual input modality
- A five-finger sight-reading level (primary F-A2 / T-A2) incidentally engages K-A3 via content scope + Kinesthetic output
Same training value mix, different primary. The Coach reasons over the engagement graph to compose routes:
 
| User goal | Primary route | Alternative routes via incidental engagement |
|---|---|---|
| Improve finger independence (K-A1) | Exercise K-A1 atoms (Automaticity pole) | Sight Reading scoped to five-finger positions (Novelty pole); Repertoire pieces rich in finger-independence demands (synthesis midpoint) |
| Improve pedaling (K-M12 / K-M13) | Exercise K-M12/13 atoms (Automaticity pole) | Sight Reading scoped to chorale-textured content with pedal markings (Novelty pole); Repertoire excerpts from pedaling-rich literature (synthesis midpoint) |
| Improve chord recognition (F-C5) | Exercise F-C5 atoms (Automaticity pole) | Sight Reading with chord-symbol content (Novelty pole); Repertoire with analytical practice — "identify the chords as you play" (synthesis midpoint) |
 
#### 5.6.3 The Discipline in Practice
 
The Coach's roadmap-composition routine, when serving a specific training goal:
 
1. **Identify primary substrate(s) for the goal.** Translate the natural-language goal into a primary substrate or cluster.
2. **Compose along the Spectrum.** Allocate roadmap nodes across the three modes per the user's current proficiency, the goal's nature, and the user's pacing preferences. Early goals lean Automaticity-heavy (build the skill); midstream goals balance the three; late-stage goals lean Novelty + Repertoire (consolidate transfer).
3. **Route alternatives via engagement.** When the goal admits cross-mode routing (most do, per §5.6.2), include atoms from secondary modes whose engagement graph touches the primary substrate. This is what makes the roadmap a coherent training plan rather than a single-mode drill list.
4. **Respect user preferences and constraints.** Some users prefer block practice (slower transfer but feels productive); some want maximum variety. The Coach has a default interleaving discipline but adapts to user-stated preferences.
5. **Hold meaning-making as the destination.** Even when surface goals are utilitarian (exam prep, specific technique), the roadmap should eventually surface Repertoire engagement — the act of making meaning through music. Per Doc 01 §2.4.5.

#### 5.6.4 Why This Differentiates MuseFlow
 
Most existing music-learning products operate at a single Spectrum pole. Drill apps (ear trainers, theory trainers, scale practice apps) live at the Automaticity pole. Sight-reading-only apps live at the Novelty pole. Repertoire-only apps (curated piece libraries) live near the synthesis midpoint but lack pedagogical interleaving. **MuseFlow's positioning is that it operates the entire Spectrum deliberately, and the agentic system composes practice along it.** This is the matured "songs vs. skills → entire spectrum" pitch evolution. See Doc 13 for pitch deck register.

---

## 6. The AI Surface

### 6.1 What the AI Surface Does

The AI surface is the conversational layer where the user interacts with the agentic system. Anticipated functions:

- **Goal articulation and refinement** — taking the user's stated goal and clarifying it. When goal-articulation signals are present, the agent operates in a "diagnostic" or "auto-engaged plan" mode (a behavioral analogy borrowed from Claude Code's plan mode): it fires follow-up questions until enough context exists to construct a roadmap. The behavior is clear; the implementation pattern (prompt-level vs application-level) is open and the analogy works at the behavior level only — see §10.7. Cross-reference §4.3.
- **Roadmap construction** — building the initial plan
- **Roadmap review** — explaining why specific nodes are in the plan and how they serve the goal
- **Roadmap adjustment** — accommodating user requests ("I don't want to spend so much time on theory" / "Can we add more sight-reading?" / "I'm tired of this piece, can we work on something else?")
- **Status reporting** — answering questions about progress, projecting time-to-goal, surfacing recent achievements
- **Custom content commands** — letting the user explicitly request a generated exercise, simplified piece, or custom sight-reading level outside the roadmap context
- **Real-time interruptive cues during practice** — short instructions while the user is playing ("slow down," "louder," "breathe"). Highest UX risk; voice-only or lightweight visual.
- **Notification + spoken/text prompt** — chime followed by spoken or text cue tied to existing notification messages (auto-tempo, flexible metronome). Patrick's framing from the May 7 brainstorm.
- **End-of-round feedback with action proposal** — between attempts: "here's what I noticed; here's what I'd recommend; I'm setting up the loop for you right now." Closely paired with the agent's manipulation of the practice control surface (§6A).
- **Conversational dialogue** — Socratic / tutor-mode persona for understanding theory and concepts: "you can just ask every stupid ass question you want and it will keep talking to you until you actually get it." (Steven, May 7.)

The functions above describe *what* the agent does at the conversational layer. The mechanical actions the agent takes during a practice session — what tools it manipulates, what settings it changes — are described in §6A (Agent Control Surfaces per Content Mode). The two are tightly coupled: voice and text feedback are typically firing *about* surface manipulations the agent is performing in parallel.

### 6.2 Levels of Agency

[Speculative — this is a load-bearing UX question.] The agent could operate at different levels of autonomy:

- **Suggest-only**: the agent proposes; the user must approve every roadmap entry, every adaptation, every custom-generated piece of content. Slow but maximally legible.
- **Approve-by-default**: the agent acts; the user can override or roll back. Faster, but the user is in less control.
- **Mixed**: certain high-stakes actions (changing the goal, deleting content, advancing past large sections) require approval; routine adaptations don't.

The right level may differ per user, per Project, or per action type. The default for V1 of the agentic system is open. The team has not yet discussed this in depth.

### 6.3 Where the AI Surface Lives in the UI

Two architectural options:

- **A dedicated AI panel** — a chat-style surface that's always available, perhaps via a persistent UI element (sidebar, drawer, floating button). The user can summon the agent from anywhere in the app.
- **Surfaced in context** — the AI surface lives inside the Project view (the roadmap container has the conversation built in), with possibly limited surfacing elsewhere.

Probably both, in different forms — a global "ask MuseFlow" affordance plus a richer in-Project surface. Specific design TBD.

### 6.4 The AI Surface Is Not the Only Way to Use MuseFlow

It is essential that the AI surface feel **optional**, not central. Users who don't invoke it should not feel that they're using MuseFlow incorrectly, missing out, or being nudged. The product is designed for users at multiple AI-comfort levels:

- **AI-native users** want to use Projects and the AI surface heavily
- **AI-curious users** may use Projects occasionally but spend most of their time in direct content engagement
- **AI-averse users** may never use Projects and want a product that respects that

All three are first-class. See §12.

### 6.5 Modality and Phasing

The AI surface can present in two modalities — **text** and **voice/audio** — with distinct phasing implications.

**Text-first.** V1 of the AI surface ships text. Steven's framing from the May 7 brainstorm: "I'm okay starting with text, especially like I understand the tricky part about that if it's trying to tell you things literally while you're playing, but if we're talking about this feedback in between plays, like I'm okay starting with text." Text is cheaper to build, easier to render reliably, and avoids the latency and reliability problems of real-time voice.

**Voice/audio later.** The four voice-feedback patterns enumerated in §6.1 (real-time interruptive cues, notification+spoken prompt, end-of-round feedback, conversational dialogue) constitute a parallel modality with phasing TBD. Per Staley's framing on May 7, voice-LLM latency is the central technical hurdle: "the technical hurdle is literally just figuring out how to get the voice LLM thing going... and after that, the hard part is the automatic looping." Once voice infrastructure is reliable, the four patterns can ship incrementally — the conversational and end-of-round patterns being easier and lower-risk than real-time interruptive cues during play.

**Parallel-track framing across content modes.** The AI session-management capability (AI-generated content + AI-driven session orchestration + voice/text feedback) is **not** repertoire-only. It is a parallel mechanic for both repertoire AND exercises, and arguably faster to build for exercises (smaller content space, simpler completion criteria, less performance variability) than for repertoire. Repertoire's lead is incidental — driven by the substrate that exists in the app today (audio recognition, MAGE, looping infrastructure) — not architectural. The two tracks should be built in parallel rather than strictly sequenced. Sight reading is a third surface where the same mechanic applies. See §6A for the per-content-mode control surfaces the agent operates over.

**Phasing summary:** text in V1, voice in V2+. Repertoire and exercise AI session management built in parallel rather than sequenced, with sight reading following. Specific UX details (when each pattern fires, how the user toggles, per-content-mode default modality) are open.

---

## 6A. Agent Control Surfaces per Content Mode

The AI surface (§6) describes *what the user perceives* — the conversational and feedback layer. The control surface described here is the orthogonal question: *what mechanical actions can the agent take* during a session within a given content mode? The agentic system's per-content-mode job is a **policy over its control surface** — given the Project goal, the user's performance data, and user preferences, the agent decides which surface elements to engage and how to set them. Specific algorithmic patterns (such as auto-looping, Decision #42) bundle several surface elements together into recognizable practice modes.

This section enumerates the repertoire surface and sketches the surfaces for exercises and sight reading. The repertoire surface is defined in detail because the team has the most concrete picture of it (May 7 brainstorm, Decision #46, Patrick's PRD); the others are sketched and will be elaborated as design progresses.

### 6A.1 The Repertoire Control Surface

Per Decision #46, the agent-controllable repertoire practice control surface consists of the following tools:

- **Song position** — where exactly to place the user in the song to start the next take
- **Tempo controls** — when to speed up or slow down, and by how much
- **Metronome settings** — on/off; accent vs unaccented downbeats; flexible vs fixed count-in (whether the metronome buffers vs counts exact beats)
- **Hand assignment** — which hand(s) to play at any given time
- **Accuracy controls** — track or not; which hand(s) to track for; show real-time color feedback or not (red/yellow/green for wrong-pitch / right-pitch-wrong-timing / correct); preserve note-color feedback across takes or reset; success threshold (e.g., 95% / 85%)
- **Audio playback** — silent / dueting (app plays alongside user) / app-only / no MIDI
- **Looping controls** — start/end points; seamless back-to-back vs paused between takes; takes-required threshold; tempo adaptation per take
- **Cursor toggle** — show/hide the playhead cursor moving along sheet music
- **Note names / finger numbers** — display either as overlay aids

The agent's repertoire-practice job is a *policy over this surface*: given Project goal, current performance data, and user preferences, decide which surface elements to engage and how to set them. **Auto-looping (Decision #42) is one such policy** — identify problem sections from green-note history, set up looping with specific start/end and takes-required, optionally adjust tempo, optionally adjust accuracy threshold, optionally engage hand-by-hand isolation. The algorithm bundles several surface elements into a coherent practice mode. Other meta-policies will emerge as the surface stabilizes and the agent's behaviors are extended.

Each surface element is independently buildable. The agent's policy can grow over time as elements are added; auto-looping can ship before the full surface is wired up, and additional practice modes can be layered in.

### 6A.2 The Exercise Control Surface (sketched)

The exercise control surface is parallel in shape to the repertoire surface but operates over different primitives. Initial enumeration (to be elaborated as design progresses):

- **Training method selection** — choosing among the seven training methods (Verification, Recognition, Selection, Assembly, Alteration, Recall, Performance) per the spectrum in Bible §7
- **Performance constraints** — time-based pass conditions, accuracy thresholds, memory-chain length, error tolerance (Decision #43, treating performance constraints as cross-content-mode primitive; see Bible §6.2)
- **Content scope** — which substrate combinations, which target variables, which difficulty axes are active for the session
- **Blueprint configuration** — selecting and configuring the appropriate UI/interaction template (per Doc 06)
- **Configurable assistance** — Lit-Keys Mode, Completion Handicap, and other cross-atom assistance settings (Decision #38)

The agent's exercise-practice job is a policy over this surface: given the user's Project goal and skill state, choose training method, set performance constraints, select content scope, configure the blueprint, and decide whether assistance is enabled. Generation-on-demand (Decision #33) is invoked when no existing atom matches the policy's needs.

### 6A.3 The Sight-Reading Control Surface (sketched)

The sight-reading surface is similarly parallel:

- **Parameter generation** — selecting musical parameters (notes, rhythms, time signature, complexity metrics) for level construction
- **Level construction** — invoking the Sight Reading Generate flow to build a level matching the parameters; the resulting level is stored with appropriate `authoring_origin` (per Decision #45)
- **Game-mode toggles** — which sight-reading game modes are active for the session
- **Performance constraints** — accuracy thresholds, time pressure, completion criteria (Decision #43); user-generated levels may carry "no completion criteria, just play endlessly" as a configurable option
- **Difficulty controls** — chevron count (Optimal Grip), tempo, error tolerance. The shipped Automatic Tempo Adjustment (ATA) feature is the Practice-Partner-controllable tempo modulator here; per Decision #62, ATA also exposes a user-controllable configuration panel (the Universal-Affordance-Symmetry-conforming manual equivalent).

The agent's sight-reading-practice job is a policy over this surface in the same shape as exercises and repertoire.

### 6A.4 Why Surface Enumeration Matters

Enumerating the per-content-mode control surface has three consequences:

1. **It defines the agent's job.** Without enumeration, the phrase "the AI manages the practice session" is undefined. With enumeration, the agent's job becomes specifiable — and testable — element by element.
2. **It enables progressive implementation.** Each surface element is independently buildable. The agent's policy can grow over time as elements are added; the team doesn't have to ship the complete surface before shipping any agent behavior.
3. **It clarifies what the demo requires.** Step 4 of the integrated investor demo (the AI-driven repertoire session — see §15.2) requires the repertoire surface implemented to the point where the agent can engage looping, tempo, and accuracy controls live. The demo's engineering-critical path is the implementation of the repertoire surface plus the auto-looping policy on top of it.

The surface enumeration is V1 documentation work; specific agent policies and UI implementations phase independently.

---

## 7. The Projects Dashboard

### 7.1 The Top-Level Surface

The Projects dashboard is the navigation home for path-mode-Project content. It is reachable from MuseFlow's top-level navigation as a sibling to the content mode entry points (Exercises Home, Repertoire Home, Sight Reading Home when it formalizes). On the dashboard, the user sees:

- **All their Projects** — current, paused, and completed, with status indicators
- **Project metadata** — goal text, target date if any, percent-complete, recent activity
- **Aggregate views** — possibly a unified "what should I work on today" view that draws from all active Projects

### 7.2 Per-Project Zoom

Tapping into a specific Project opens its individual view. This view contains:

- **The goal**, prominently displayed and editable
- **The roadmap**, rendered as a **vertical tree with branching** (current working direction; specific design TBD). The May 7 brainstorm narrowed visualization candidates toward this shape, inspired by Fez's branching-progression aesthetic. The vertical orientation supports long roadmaps better than horizontal layouts; branching accommodates conditional paths, multi-track sequences, and optional sections that the agent may surface. Specific rendering details — pan/zoom behavior across long roadmaps, mobile rendering, progress indicators, node-state visualization — remain open (see §13.6).
- **Progress indicators** — what's been completed, what's next, what's coming up
- **The conversational AI surface**, accessible in-context for asking questions, requesting changes, or reviewing the agent's reasoning

### 7.3 The Cross-Project View (Speculative)

If cross-project orchestration is a design feature, the dashboard probably needs a view that surfaces it: "across your three active Projects, here's what we recommend you do today, and here's how each item serves which goals." Whether this is a primary surface, a secondary view, or just an artifact of intelligent ordering on the main dashboard is open.

### 7.4 Browse-by-Origin Within Path Modes

The Projects dashboard, like content-mode browsing, supports filtering by authorship origin within the path-mode space. The user can view:
- Their own Projects (default)
- Their own User Paths (alongside or in a separate tab)
- MuseFlow Curriculum offerings
- Community-shared paths (future)

This filter axis treats all path types as siblings — consistent with the architectural framing in §3.

---

## 8. Project Flow Inside Content Modes

### 8.1 The Pivot from Browse to Project

A user browsing the Exercise content mode (looking at the catalog of available atoms, filtering by substrate or modality) should be able to pivot to "ask the agent to build a roadmap that includes this kind of practice" without first navigating to the Projects dashboard. This is the in-content-mode entry point to the Project flow.

The pattern is:
1. User is browsing/exploring content
2. They see something they're interested in or realize they want a structured plan
3. They invoke the Project flow ("build me a roadmap from here") via a button, command, or AI summon
4. The conversational surface engages, possibly pre-seeded with context from where they were browsing

The seed context matters: if the user was looking at "Major and Minor Triads × Ear Training" when they invoked the Project flow, the agent should incorporate that into its initial conversation ("Are you looking to build skills around triad ear training specifically? Or is this part of a broader goal?").

### 8.2 Why Both Entry Points

Having Projects reachable both from the dashboard and from inside content modes serves different use cases:

- **Dashboard-first** is for users who already know they want a Project. They navigate directly to where Projects live.
- **Content-first** is for users who are exploring or working in a specific content mode and decide mid-session that AI guidance would help. The pivot doesn't require them to reorient.

The two entry points share state — pivoting from inside a content mode results in the same Project that would have been created from the dashboard, just with different seed context.

### 8.3 The Project Flow Doesn't Require a Goal-First Frame

Some users will come to MuseFlow with a clear goal and want to start in Projects. Others will come exploring and discover that they want a Project mid-session. Some will never want a Project at all. The architecture supports all three by treating Projects as both a top-level destination and a flow available from inside content modes — never as a prerequisite for accessing the rest of the product.

---

## 9. Custom Content Generation

### 9.1 Generation as a First-Class Capability

Generation on demand is one of the three flows available in every content mode (see §3.2). When invoked, it produces new content via the mode's generation tool, tagged with the appropriate authorship origin, and stores the content in the mode's catalog.

In the context of Projects, generation is the agent's way of filling roadmap gaps the standard catalog doesn't cover. If the goal requires practice on a substrate combination that no preset atom addresses, the agent generates one.

### 9.2 What Gets Generated

Three types of content are anticipated to be generatable:

**Custom exercise atoms.** The atom space is combinatorial; new atoms are formed by selecting valid combinations of substrate family, input modality, output modality, target variables, pitch reference mode, and content scope. The system can construct the atom; MAGE (or future AI) generates the content material the atom prompts the user with.

Steven's framing from the May 5 standup on why exercises are tractable to generate:
> "That level of generation almost feels the easiest. Because it doesn't have to match stylistically something. It would be variations on scales and chords."

**Custom sight-reading levels.** When Sight Reading formalizes as a content mode (see Bible §2.1.1), it is anticipated to support custom-level generation: the user (or the agent) specifies difficulty parameters, complexity metrics, musical style, and other constraints, and the system generates a playable level. MAGE has the underlying capability today; the UI and parameterization layer needs to be built.

**Simplified repertoire arrangements.** [Speculative.] Per Steven's May 5 walk-through of MAGE's capabilities, MAGE can take a piece of existing repertoire, analyze its complexity along the standard MuseFlow dimensions, and intentionally downgrade specific complexity metrics to produce a simpler arrangement. The capability exists in algorithmic form; what's missing is logic to preserve key musical characteristics (so the simplification still sounds like the original piece). This is the canonical demo flow ("upload a piece → simplified version") and is central to the investor-demo story.

### 9.3 Where Generated Content Lives

All generated content lives in its respective content mode, tagged by authorship origin. A custom exercise atom generated for a Project lives in the Exercise content mode tagged `authoring_origin = agent`. A custom sight-reading level lives in the Sight Reading content mode (when it formalizes). A simplified repertoire arrangement lives in the Repertoire content mode tagged with provenance — possibly with a back-link to the original piece, since simplifications are derived rather than independent creations.

The user can find generated content by:
- Navigating to the content mode and filtering Browse to "AI-generated"
- Tapping the relevant node from inside a Project roadmap
- Asking the AI ("show me the exercises you generated for me last week")

### 9.4 Generation Triggers

Three trigger types are anticipated:

- **User-triggered (manual)**: the user explicitly requests generation via the Generate flow inside a content mode ("I want a custom exercise focused on minor 6th and minor 7th interval recognition with limited time")
- **Teacher-triggered**: a teacher generates an exercise (via the Repertoire Builder surface; see Decision #34 and §9.5) and assigns it to one or more students
- **Agent-triggered**: the AI generates content as part of a Project roadmap, in service of a goal-specific gap

These three triggers may share infrastructure but have different UX flows.

### 9.5 The Authoring Surface

The natural authoring surface for custom content is the in-app music editor demoed by Andrew Urbanowicz on May 5 (Decision #34). The editor supports:

- Click-to-add notes, drag-to-reposition
- Notation editing (sharps, flats, naturals)
- MIDI playback
- Multiple play modes (Practice, Listen, Sound — the last of which Steven flagged for renaming, possibly to "Play-Along")
- Save to user library

The editor is being developed primarily for repertoire authoring, but the underlying infrastructure (note input, notation rendering, save-to-library) generalizes to exercise authoring. The specific UX for "I want to author a custom exercise atom" vs. "I want to author a custom piece of repertoire" within the editor is open.

### 9.6 The Pedagogical Safety Question

[Open question — see §13.] An agent generating exercises and roadmaps could, in principle, produce pedagogically unsound combinations: an atom whose prerequisites haven't been respected, a roadmap that skips a critical foundational skill, an exercise that's too hard or too easy for the user's stated level. What guardrails or review layers prevent this?

Several candidates:
- **Atom validity rules** — the schema enforces certain constraints (e.g., perfect-pitch atoms can't be generated for users who haven't enabled perfect-pitch mode)
- **Prerequisite enforcement** — the agent must respect declared prerequisite relationships
- **Mastery-threshold gating** — the agent can't advance the user past a node before clearance criteria are met
- **Human-in-the-loop review** — for high-stakes Projects (preparing for an exam, learning a piece for performance), a teacher could be looped in for review

This is unresolved.

---

## 10. MAGE and the AI Layer

### 10.0 MAGE and Opusmodus Within the Three AI Roles
 
Per Decision #59, MuseFlow AI operates across three role scopes: the Coach (relationship-scoped), the Composer-Librarian (content-scoped), and the Practice Partner (moment-scoped). MAGE and Opusmodus are **implementation tools within the Composer-Librarian role**. Both serve content production and modification functions; neither operates at Coach scope (relationship-level reasoning) or Practice Partner scope (in-session moment-to-moment decisions).
 
The role-scoped placement clarifies a recurring framing tension:
 
- **MAGE** is the algorithmic content generation engine. It produces music — exercise content, sight-reading material, etude candidates — via algorithmic-pedagogical logic. Per Decision #44 (Augmentation direction), MAGE persists as a permanent generation engine with AI-mediated adjustment for musicality, stylistic fitness, and goal-specific shaping. MAGE is the Composer-Librarian's *generation function*.
- **Opusmodus** is a music-printing/rendering tool. It renders MAGE-output music-XML into the actual notation the user sees. Opusmodus is a tool MAGE uses to produce final renderable output; it is not a parallel generation system.
The relationship is **generator + renderer within a single role**, not two competing systems. The recurring "Mage vs. Opusmodus" team confusion (logged across Decisions #39, #44, #53, multiple standups) resolves when both are placed inside the Composer-Librarian layer with their respective sub-functions.
 
The remainder of §10 — MAGE's current capabilities, the augmentation question, alternative architectures, the metaphor-vs-implementation question — is unchanged by this recontextualization. It is a refinement of framing, not a change in technical commitments. The "Large Music Model" framing question (Decision #54 — internal-only pending architecture justification) is also unaffected; the framing is preserved for internal aspiration without compromising the Three Roles' practical scoping.
 
For the pitch deck (Doc 13), MAGE and Opusmodus are introduced as **what powers the Composer-Librarian** rather than as standalone systems. This avoids the technical-detail overload that surfacing MAGE first would create, and lets the role framework carry the narrative weight.

### 10.1 What MAGE Is

MAGE — Music Algorithmic Generation Engine — is the MuseFlow codebase containing the algorithmic logic that decides what music to generate, simplify, modify, or analyze. MAGE handles complexity analysis, intentional downgrading of complexity metrics, and other generative operations on music data.

MAGE is **distinct from Opusmodus**. Opusmodus is a music notation/printing engine that takes instructions and renders output; it has no generative logic of its own. MAGE generates the instructions; Opusmodus prints them. The distinction has been confused in two recent team standups; the names are not interchangeable. (See Glossary entries.)

### 10.2 Current MAGE Capabilities

Per Steven's May 5 walk-through:

> "It could take a piece of existing repertoire. It could analyze it for complexity. It could get all the specifics on its complexity. And then it could intentionally downgrade any or all of the individual complexity metrics in certain ways and find/make a piece that matches those downgraded metrics. It can do all of that. It just doesn't currently have logic that also says 'preserve the key musical characteristics, make this similar musically to the repertoire piece.' It could do that — I'd have to think about how to plan it and execute it."

The piece-simplification capability central to the investor demo (upload a piece → simplified arrangement → roadmap to mastery) exists in algorithmic form. The gap is the musical-similarity-preservation logic, which is also where AI augmentation would help most directly: the AI's strength is in pattern matching and stylistic preservation, exactly the part MAGE doesn't currently handle.

### 10.3 The Augmentation Question

[Open architectural question — see Decision #39, amended per Decision #44.] The team's working position has converged toward **augmentation**, with the question formally still open pending Staley's explicit retirement of the training-data-then-replacement framing.

**Steven's position (May 5):**
> "It is not obvious to me that MAGE would just be for training data, and that's not the assumption that I'm working on… If a more AI-based approach were to replace MAGE, it would integrate MAGE into it. It would be an upgraded AI-enhanced version of MAGE to me. It wouldn't just be a separate thing that we build."

**Staley's earlier framing (May 5):** MAGE exists primarily to generate training data for an eventual fine-tuned LLM; once enough data exists, the LLM replaces MAGE.

**The May 7 Emergent Curriculum brainstorm produced directional alignment.** Patrick articulated a concrete mechanism for the augmentation framing:
> "The AI would probably be adjusting the mage output to make it more musical or to fit the like genre that they're trying to learn or to specifically work specific techniques that are in the piece of repertoire that they want to learn... There's like many reasons why the AI would adjust the music XML outputed by Mage."

Steven concurred. Staley did not push back; his earlier articulations during the call ("I love mage. Yeah") and his agreement with Patrick's framing position him in alignment. **The team's working framing is now: MAGE persists as a permanent algorithmic generation engine, with the AI adjusting MAGE's music-XML output for musicality, stylistic fitness, and goal-specific shaping.** The training-data-then-replacement framing is no longer the team's working framing.

**What remains open.** Staley has not explicitly retired the training-data-then-replacement framing in writing, so Decision #39's open status remains until that confirmation. Cost implications of the augmentation framing differ from the replacement framing (per §10.4): MAGE+AI is a hybrid stack, not a single LLM. This is a feature, not a bug, but architectural commitment must reflect it.

This document records the augmentation framing as the current working position; the question is documented as resolving rather than fully resolved.

### 10.4 What an AI Augmentation Looks Like

[Speculative.] Under the augmentation model, the AI's role is to fill MAGE's gaps and extend its capabilities — not to replace its core. Possible augmentation surfaces:

- **Stylistic preservation in piece simplification** — the AI ensures simplified arrangements still sound musically faithful to the original
- **Style-conditioned generation** — the AI can generate exercise content (for parameterized atoms with `generation_mode = on_demand_content`) that matches stylistic constraints from a target piece or goal
- **Goal decomposition** — the AI converts user goals into MAGE-actionable parameters
- **Conversational interface to MAGE** — the AI is the natural-language wrapper that lets the user interact with MAGE via the AI surface

In this model, MAGE provides the deterministic, structured musical operations; the AI provides the flexible, stylistic, conversational layer on top. They're complementary, not redundant.

### 10.5 The LLM Choices

[Speculative — Staley's R&D track.] Staley's exploration direction crystallized at the end of the May 7 call:

> "I'm just going to start digging into like how to do LLM. I've watched some videos from AWS on using their like AWS bedrock stuff and that might be like the step one. I've also heard stuff about that being expensive. Maybe there's a way we can make calls to some external API that's like I don't know..."

The direction is **AWS Bedrock first, external-API alternatives if cost is prohibitive**. This is the first explicit tooling-exploration commitment per Decision #32 (Agentic Projects elevated to near-term R&D). The exploration includes:

- **AWS Bedrock as the primary substrate** — managed inference for fine-tuned and frontier models; potential for fine-tuning a smaller open-source model rather than calling proprietary frontier models (rationale: cost, control, on-prem-adjacent deployment)
- **External-API alternatives** as a near-term fallback distinct from the deeper "build out MAGE algorithmically" alternative — calls to providers like Claude API or OpenAI API if Bedrock economics don't work
- **Quantization** to reduce inference cost
- **Caching** — the same piece simplified into the same arrangement should be generated once and cached
- **Sparing use of inference** — LLM calls only where they materially help (piece-simplification, goal-decomposition, agent orchestration), not per-keypress
- **A RAG layer over user historical play data, conversation history, and current-song context**, with a vector DB on user data — this is the implementation surface for the user-modeling layer (§1.2) and a structural moat distinct from the LLM-layer choices above

The cost model is genuinely uncertain. Whether quantized open-source models can hit the quality bar at acceptable inference cost is the central engineering question Staley is exploring; the external-API path is the near-term fallback. Cost considerations are summarized in §16.

**A note on framing.** The LLM choices in this section are LLM-layer concerns. They are distinct from the user-modeling-layer concerns (data structures, retrieval logic, synthesis pipelines that turn MuseFlow's playing/practice data into actionable agent decisions). Both are AI-company concerns; both need owners. See §1.2.

### 10.6 Alternative Architectures

Other paths exist if both the Bedrock-fine-tuning direction and the external-API fallback (per §10.5) prove untenable:

- **Hybrid frontier-model + MAGE as architecture, not fallback** — adopt frontier-model API calls (e.g., Claude or a music-specific model) as the committed long-term architecture for the high-stakes generation calls, accept the cost, and build the cost model around it from the start
- **MAGE-only** — skip the LLM entirely, build out MAGE's musical-similarity logic algorithmically (slower to ship, cheaper to operate)
- **Crowd-sourced augmentation** — let teachers and advanced users hand-author the simplifications and custom content the system needs, treating AI generation as one source among several

These are not committed alternatives; they are options that exist if the primary path encounters obstacles. The first option overlaps in shape with the §10.5 external-API fallback but differs in commitment level: §10.5's fallback is "we use frontier APIs while we figure out the right home"; this option is "we commit to frontier APIs as the architecture."

### 10.7 Metaphor vs Implementation

The team uses analogies to communicate the agentic vision: "diagnostic agent" / "auto-engaged plan mode" (Claude Code's plan mode), "Steven MD file" / "Patrick MD file" (Claude's CLAUDE.md), "large music model" (large language models). These analogies are useful for team-internal communication and pitch language — they're vivid, they rhyme with patterns the team already knows, and they help externalize what the system is supposed to feel like.

**Analogies are not architectural specifications.** They can mislead in two specific ways: by hiding implementation complexity, and by implying implementation patterns that are not actually right for the underlying problem. Two examples from the May 7 brainstorm illustrate the pattern.

**Example 1: Diagnostic agent / auto-engaged plan mode.** The Claude Code plan-mode analogy works at the *behavior* level — when goal-articulation signals are present, the system fires follow-up questions until enough context exists to construct a roadmap. The analogy underspecifies the *implementation*. Two candidates with very different cost / control / failure-mode profiles:

- **Prompt-level**: the system prompt has a "diagnostic" section that activates when the model classifies the user's message as goal-articulation. Cheap and flexible. The load-bearing step is the LLM's reliability at zero-shot classifying "this is a goal-articulation moment." Failure modes: too-eager (user gets interrogated unnecessarily), too-slow (the conversation drifts).
- **Application-level**: the app has explicit modes between which the user (or the system) navigates, gating available actions/tools. Claude Code's plan mode specifically is this kind. More deterministic but requires explicit UI affordances and probably an explicit "start a Project" entry point that puts the user into diagnostic mode.

These are different to build. The team should pick deliberately, not adopt the analogy as if it specified the implementation.

**Example 2: "Steven MD file" / "Patrick MD file."** This analogy is more structurally misleading. CLAUDE.md is *human-authored, human-maintained* — Steven writes the file; Claude reads it. What the May 7 call described is *AI-authored, AI-maintained* — the system observes the user and writes notes about them. This is a fundamentally different problem class. AI-authored persistent memory has at least four real engineering challenges that the CLAUDE.md analogy hides:

- A **synthesis problem** — the LLM has to decide what's worth remembering from each interaction
- A **recency-vs-relevance retrieval problem** — which past observations should fire on the current context
- A **drift problem** — AI-encoded mistaken beliefs about the user compound over time and become hard to correct without explicit user-correction affordances
- A **context-window problem** — a growing file eventually exceeds budget and needs compression / summarization passes

These are real engineering problems with real solutions: vector stores with embedding-based retrieval, periodic LLM-driven summarization, explicit user-visible memory management, possibly user-correctable memory entries. **The shape is closer to "per-user RAG layer over conversation history, exercise/repertoire/sight-reading event data, and curated AI-extracted summaries"** — the architecture §10.5 sketches and §1.2 names as the user-modeling layer. Treating the CLAUDE.md analogy as implementation-spec could lead engineering toward a single growing markdown file when the real architecture is a structured store with retrieval logic.

**Example 3: "Large music model."** This framing is somewhat different — it's positioning rather than implementation specification. As positioning, it's powerful (it implicitly claims MuseFlow is doing for music what foundation models did for text). As implementation, it could imply "we are training a single foundation model on music," which is not the team's current direction. Worth being deliberate about whether this language enters customer- or investor-facing material.

**The discipline.** When an AI-product analogy is adopted, the team should:

1. Identify what behavior the analogy specifies (usually clear)
2. Identify what implementation the analogy implies (often unclear, sometimes wrong)
3. Decide deliberately whether to follow the implied implementation or pick a different one
4. Document the implementation choice separately from the user-facing metaphor

The analogies are good for team alignment and external communication. They are not architectural specifications. This subsection exists to make that distinction explicit and to establish it as a documentation discipline going forward.

**Cross-references.** Doc 10 §3.6 (diagnostic-agent / auto-engaged-plan-mode evaluation, full text). Doc 10 §3.9 (Steven MD file / Patrick MD file evaluation, full text). §1.2 (the user-modeling layer as the architectural commitment behind the "MD file" metaphor). §6.1 (diagnostic-agent behavior at the AI-surface layer).

---

## 11. Engagement & Nudging Integration

### 11.1 The Engagement Layer

A separate engagement layer reads from Project goals, free-exploration patterns, and aggregate skill-progression data, and surfaces re-engagement signals and proactive nudges. This layer is **orthogonal to the three flows** — it triggers entry into them rather than constituting one.

The engagement layer's leading anticipated implementation is Andrew Urbanowicz's proposed proactive notification system, described in the April 28 standup:

> "I want to integrate a model into pulling that data and then feeding it to a customized message… proactive messages like 'hey come back and finish up, you already finished tier 2 of level 9, come and finish tier 3'… because people who are engaged aren't going to cancel."

### 11.2 What Projects Contribute to Engagement

A Project provides engagement-relevant signals beyond what general activity tracking provides:

- **Stated goals** — the system knows what the user is trying to accomplish, so messages can reference progress toward something specific
- **Roadmap state** — the system knows what's next, so messages can prompt that ("you've completed phase 1, ready for phase 2?")
- **Time-to-goal projection** — for Projects with deadlines, the system can flag schedule risks proactively
- **Cross-project priorities** — the system knows which actions advance multiple goals at once and can prioritize those in nudges

### 11.3 Engagement Without Projects

[Important.] The engagement layer must work for users who don't use Projects at all. AI-averse users practicing without Projects should still get re-engagement messaging based on their direct activity in content modes. Projects are an additional input to engagement, not a prerequisite for it.

### 11.4 Implementation Note

No additional schema fields are needed at the atom or result level to support engagement (see Decision #19 amendment). The Exercise Result schema is the source-of-truth data primitive; ensuring it's persisted in a queryable location is sufficient. Andrew's logic can derive whatever engagement signals are needed (atoms cleared, time-since-last-practice, completion state) from the existing fields.

---

## 12. Respecting AI-Averse Users

### 12.1 Why This Matters

AI products risk a pervasive failure mode: users feel the AI is being pushed on them. Even well-intentioned AI features can feel coercive if the rest of the product is structured to assume their use. MuseFlow's commitment is that AI-averse users — users who, for any reason, prefer human-curated and self-directed engagement over AI-mediated experiences — should be **first-class users**, not edge cases.

This is both a values statement and a design principle. It commits MuseFlow to the following constraints:

### 12.2 Design Constraints from AI-Averse User Respect

**1. Path modes are siblings.** Curriculum, User Paths, and Projects are presented as equally legitimate options. Projects is not the "main" path mode with the others as fallbacks. Curriculum is not the "basic" path mode users start with before "graduating" to Projects.

**2. The AI surface is invokable, not unavoidable.** Users can engage with content modes through Browse and Generate without ever touching the Project flow. The AI surface should not be the default landing surface, the persistent prompt, or the only way to do anything.

**3. Browse-by-origin filtering supports opt-out.** A user who never wants to see AI-generated content can filter their Browse view to exclude `authoring_origin = agent` content. Their experience of the product is then entirely human-curated.

**4. Notifications and nudges are configurable.** The engagement layer's notifications can be toned down or turned off entirely. Users who don't want to be nudged about Projects don't get nudged about Projects.

**5. Onboarding offers multiple paths, not a single default.** When a new user opens MuseFlow, the onboarding doesn't assume they want to start with a Project — and equally, doesn't assume they want to start with exploration. The chat-first goal-articulation pathway (Staley, May 7: "the first thing you do when you log into MuseFlow is you get a chat screen that says like what are your goals, like what would you like to learn") is a legitimate onboarding path for users who arrive with a goal in mind. The exploration-first pathway (introducing content modes, mentioning Projects as one option among several) is the legitimate path for users who arrive curious but undirected. Both exist. How the system decides which path to surface to which user — chooser, default rule, declared user type at signup, or some combination — is open (see §13.4).

### 12.3 What This Costs

These constraints have a cost: some valuable AI capabilities will see less adoption than they would in an AI-first product. The team accepts this cost because the alternative — an AI-pushy product — risks alienating exactly the users for whom MuseFlow's content depth and pedagogical rigor matter most.

### 12.4 What This Doesn't Mean

This is not a commitment to making AI features second-class. AI features should be *excellent* and *legible* and *visible*; they should just not be *forced*. The agentic system should be the best version of itself — and easy to ignore.

---

## 13. Open Architectural Questions

The following questions are open and shape ongoing design work. They are clustered by topic. This list is non-exhaustive and is expected to grow.

### 13.1 Project Concept and Lifecycle

1. **Multi-goal Projects** — One Project per goal, or can a Project encompass multiple related goals? (§4.5)
2. **Project termination** — When does a Project end? On goal completion, user dismissal, agent declaration, or timeout? Does it persist as a "completed" archive?
3. **Project sharing** — Can a user share a Project (its goal + roadmap) with another user? With a teacher? Is this its own object or a snapshot?
4. **Project pause/resume** — How are Projects paused and resumed? Does the agent reassess on resume?

### 13.2 Goals and Decomposition

5. **Goal type taxonomy** — Are there discrete categories the system reasons over, or is everything a free-form natural-language input?
6. **Goal decomposition logic** — How does the agent get from a goal to a roadmap? What's the model of musical skill composition?
7. **Skill assessment** — How does the agent measure current state on the skills a goal requires? Direct atom mastery? Inferred from repertoire? Asked of the user?
8. **Time-to-goal estimation** — How does the agent project completion time? What does it base this on?

### 13.3 Roadmap Structure and Adaptation

9. **Node types completeness** — Are the node types listed in §5.2 sufficient, or are others needed? Tutorial-node and Video-node placement is open (clusters with §13.11).
10. **Roadmap topology** — Is a roadmap always linear, or can it have branches, parallel tracks, optional sections?
11. **Adaptation cadence** — How often does the agent re-evaluate and update the roadmap?
12. **User vs. agent edits** — When the user edits the roadmap and the agent adapts, who has authority on conflicts?
13. **Auto-looping AI-judgment override** — The auto-looping / perfect-practice tree algorithm (Decision #42) is largely algorithmic. Steven flagged that AI judgment may need to override the algorithm in "break the rules" cases (e.g., the actual issue is the previous measure, not the errored one). When does the AI override the algorithm? How does the user perceive that override?
14. **Auto-looping ⟷ Optimal Grip relationship** — Both are forms of adaptive difficulty operating at different levels (Optimal Grip session-level; auto-looping practice-section-level). Are there situations where Optimal Grip's logic should drive auto-looping's parameters (e.g., when Optimal Grip lowers tempo, does auto-looping inherit that)? Not pressing; worth defining when both are V1+.

### 13.4 The AI Surface

15. **Levels of agency default** — What's the default level of agent autonomy in V1? (Suggest-only, approve-by-default, or mixed?)
16. **AI surface UI** — Where does the conversational surface live? Dedicated panel, in-Project, both, persistent vs. summoned?
17. **Conversation persistence** — Are AI conversations preserved across sessions? Are they searchable? Can the user reference past conversations?
18. **Multi-session memory** — Does the agent remember what it said before? How is this implemented? Sub-question of §13.7 #29 (user-modeling-layer implementation).
19. **Voice/text default modality** — Voice vs. text vs. both, configurable per user, configurable per content mode? Steven OK with text-first per §6.5. Default behavior in V1 of voice-feedback capability is undefined.
20. **End-of-round AI feedback timing** — Steven's "in between plays" feedback (per §6.1) — specific UX for the pause / feedback / setup-loop flow needs design. When does the agent fire? What's the user's affordance to dismiss or accept the agent's proposed action?
21. **Exercise and sight-reading control surfaces enumeration** — Per §6A, the repertoire surface is enumerated (Decision #46). Exercise and sight-reading surfaces are sketched but not enumerated to the same depth. Worth completing as design progresses.
22. **AI-analogy implementation choices** — Per §10.7. Diagnostic-agent / auto-engaged-plan-mode is prompt-level or application-level (§4.3)? Per-user "MD file" memory — single growing markdown vs structured RAG store with retrieval logic (§1.2, §10.5)? Decide deliberately during agentic system design rather than letting the analogy specify the implementation by default.
23. **Onboarding path-split logic** — Per §12.2 item 5. How does the system decide which onboarding path (Projects-first vs exploration-first) to surface to which user? Configurable? Default rule? Tied to declared user type at signup?

### 13.5 Custom Content Generation

24. **Generation cost limits** — Is on-demand generation unlimited, rate-limited, or premium-gated? (See §10.5 and Decision #37.)
25. **Generation provenance** — When generated content is shared (e.g., via marketplace), how is provenance preserved?
26. **Pedagogical safety** — What guardrails prevent the agent from generating pedagogically unsound combinations? (§9.6)
27. **Authoring UI for non-agent custom content** — How does the user author atoms manually via the editor? Where's the UI?

### 13.6 Dashboard and Navigation

28. **Dashboard rendering** — How are Projects rendered on the dashboard? List, grid, tree, or some other structure?
29. **Vertical roadmap visualization details** — Per §7.2, working direction is vertical tree with branching. Specific rendering details remain open: pan/zoom across long roadmaps, mobile rendering, progress indicators, node-state visualization.
30. **Cross-project view** — Is there a unified "what to do today" view that draws across Projects?
31. **Project flow entry from content modes** — What does the in-content-mode entry point look like? Button, command, AI summon?

### 13.7 MAGE, AI, and Cost

32. **MAGE long-term role** — *Resolved by Decision #44 (augmentation direction) and Decision #53 (procedural caveat retired, 2026-05-12).* Augmentation framing is canon — MAGE persists as a permanent algorithmic generation engine, with the AI adjusting MAGE's music-XML output. Decision #53 closed Decision #39's open-question status. See §10.3.
33. **Team ownership of LLM-layer vs user-modeling-layer** — Per §1.2 and Doc 10 §6 #13. Two interpretations of "we're an AI company" — LLM-layer expertise (Staley's current direction, §10.5) and user-modeling-layer expertise (data structures, retrieval logic, AI-driven user-context store, currently nobody's explicit territory). Both defensible; both need explicit ownership. The implicit assumption that they are the same job will create gaps.
34. **User-modeling-layer implementation architecture** — Per §1.2, §10.5, §10.7. The user-model's actual shape — RAG over which data, with what retrieval logic, what summarization cadence, what user-correction affordances — needs concrete design.
35. **Fine-tuning quality threshold** — Can Bedrock-hosted models (or external API fallbacks per §10.5) hit the quality bar at acceptable cost?
36. **Frontier-model fallback commitment level** — Per §10.6, the line between "external-API fallback while we figure out the architecture" and "commit to frontier APIs as the architecture" needs to be drawn deliberately if cost forces it.
37. **Cache strategy** — What gets cached, for how long, with what invalidation rules?
38. **Cost amortization model granularity** — The team's "heavy generation periods amortize" framing needs a concrete mental model — at what generation rate do unit economics break? Per-Project, per-month, per-account? See §16.
39. **"Large Music Model" framing** — *Resolved by Decision #54 (2026-05-12).* The framing is reserved as internal and aspirational vocabulary only; not used in customer-facing or investor-facing material until and unless architecture commitments justify it. Per §10.7. As positioning, it's powerful. As implementation, it could imply training a single foundation model on music — which is not the team's direction. Whether this language enters customer- or investor-facing material was a deliberate decision; Decision #54 set the canonical position.

### 13.8 Engagement and Notifications

40. **Notification policy** — Frequency, opt-in/opt-out granularity, message variation logic
41. **Project-driven vs. activity-driven nudges** — How does the engagement layer balance these?
42. **Re-engagement targeting** — Which user states trigger which messages? (Trial-conversion vs. churn-prevention, e.g.)

### 13.9 Pricing, Access, and Tiering

43. **Pricing model** — Not designed (Decision #37). Implications for which Project capabilities are free vs. paid?
44. **Generation volume tiers** — How many AI-generated exercises does a free user get?
45. **Project count limits** — Is there a limit on active Projects per user? Per tier?
46. **Token-based pricing surfacing** — Do users see token meters directly (Staley: "we could even surface tokens directly")? Or opaque "AI generations remaining"? Different UX implications. See §16.
47. **MAGE pricing under augmentation framing** — Under the augmentation framing (Decision #44), even MAGE-only generation could be charged for "tokens" since the AI adjusts MAGE's output. This conflates LLM compute with MAGE compute for billing purposes. Is that right or wrong?

### 13.10 Teacher/Institutional Integration

48. **Teacher-assigned Projects** — Can a teacher assign a Project to a student? Is the student then in a "managed Project" with different controls?
49. **Curriculum-as-Project** — Could a teacher's structured curriculum be expressed as a Project the system manages? Or is that a separate path mode (User Path with assigned attribution)?
50. **Institutional Projects** — Could a school assign Projects across cohorts? How does multi-user Project authorship work?

### 13.11 Content Classes Beyond the Core Three

This sub-cluster captures one of the foundational architectural questions for the agentic vision: what content classes exist beyond Exercise / Repertoire / Sight Reading, and how do they relate to the content/path-mode architecture (Decision #41)?

51. **Content classes inventory** — What content classes exist beyond the core three? Candidates surfaced to date: ~~**Theory**~~ (resolved by Decision #48 as a substrate family within Exercises, not a separate content mode), **Open Play original sense** (deferred indefinitely per Decision #41 candidate list; renamed from "Free Play original sense" by Decision #49 Part 2), **Video / Video Library** (May 7 brainstorm raised; placement open per #53), **Interactive Tutorial** (existing canonical content, placement open per #52). Some may collapse or overlap. Resolving the remaining cluster items is prerequisite to several downstream design decisions about node types, roadmap composition, and Browse-by-mode UX.
52. **Interactive Tutorial architectural placement** — Per Doc 10 §4.3 and §6 #16. Existing canonical content class (animated video + live-action hand clips + Phaser-JS exercises gated mid-flow) with no clean home in the current architecture. Candidates: its own content mode, a path-mode primitive embedded in Curriculum (matches current state), a roadmap-node type prescribable by the agent (§5.2 candidate), or a hybrid. Sub-question of #51.
53. **Video Library architectural placement** — Per Doc 10 §6 #11. Patrick's framing ("video library") leans content-mode-like; Staley's framing ("node-as-tutorial") leans roadmap-primitive. A2 evaluation (Doc 11 §4.6, Decision #51) resolved deferral but not placement; current team-recommendation lean per Decision #51 is toward Staley's framing, but the placement question remains formally open pending more development of both framings. Sub-question of #51.
54. **Game Mode / Free Play toggle collapse** — Current Sight Reading curriculum levels have Game Mode and Free Play toggles (existing app functionality). As the new content/path mode architecture is implemented, these may subsume into other functionality — Decision #49 Part 1 specifically extends the Free Play side of this pattern into the Exercise content mode as a completion-policy element of the exercise control surface. UX consolidation pattern across modes remains open. Distinct from Open Play original-sense status (deferred per Decision #41; renamed from "Free Play original-sense" by Decision #49 Part 2).
55. **Tutorial-as-roadmap-node phasing** — Per Doc 10 §6 #3. Even if AI-generated tutorials are deferred, does the architecture allow human-authored tutorials as roadmap nodes in the meantime? This sub-question doesn't depend on resolving #51 fully — it's about near-term schema accommodation. See §5.2 candidate node types.

**2026-05-12 update (per Decisions #57 + #58):** The Technique-as-content-class hypothesis (Doc 11 §11.4) is resolved as **NOT a distinct content class**. Decision #57 admits a K-substrate family within the Exercise content mode; Technique becomes a filterable cluster within Exercise driven by K-substrate atoms, not a parallel content class. The content-class question for content classes *other than* Technique (Improvisation, Aural Skills as a possible distinct mode, etc.) remains open per the original §13.11 framing.

---

## 14. Relationship to the Exercise Section Design Work

### 14.1 What Projects Inherit from the Exercise Framework

The Exercise Section design work (Project Bible §2; UX Spec; Architecture Doc; Exercise Blueprints; etc.) is the substrate that the agentic system rides on. Projects inherit:

- **The atom hierarchy** (atom → molecule → strand → cluster) — the unit of granularity the agent prescribes at, and the structured space it navigates
- **The atom schema** (Architecture Doc §8.1) including the agent-prescribability fields added in Decision #40
- **The Exercise Result data** — the agent's view of user state on exercise content
- **The blueprint catalog** (Exercise Blueprints Spec) — the interaction templates exercises map to, which the agent must respect when prescribing
- **The training method spectrum and performance constraint architecture** — the configuration surface the agent operates over

The agentic system does not need to reinvent these. It depends on them being correct.

### 14.2 What the Exercise Framework Owes to Projects

Conversely, several decisions in the Exercise Section design were made specifically to support agent prescribability:

- **Atom identity dimensions** were defined to make atoms unambiguous to an agent (Decision #25)
- **Distractor logic** is derived from atom identity (Decision #30) so agents can prescribe atoms without needing to specify distractors separately
- **Atom schema additions** (Decision #40) specifically include `prerequisite_atoms`, `mastery_thresholds`, `mobile_supported`, `authoring_origin`, and `generation_mode` — all motivated by agent-system requirements
- **The generation_mode field** distinguishes atoms whose content can be produced on demand from atoms whose content is fixed, so agents can know which atoms they can populate dynamically

These are not accidental alignments. The Exercise Section was designed with the agentic system's existence in mind, even when the agentic system was nominally a "future architectural consideration." The architecture is now ready to absorb the agentic layer.

### 14.3 What Remains to Be Designed in the Exercise Section to Fully Support Projects

A short list of exercise-section-side work the agentic system still needs:

- **Population of `prerequisite_atoms`** — the field exists in the schema; specific prerequisite relationships across the catalog haven't been authored
- **Population of `mastery_thresholds`** — same
- **GMTF mapping completion** — the existing GMTF complexity scoring system needs to be mapped to the atom framework so the agent has cross-section complexity signals (Decision #23, UX Spec §9 Open Question 14)
- **Atom catalog enumeration** — the agent needs to know what atoms exist; the V1 atom catalog hasn't been enumerated (UX Spec §9 Open Question 16, A1→PRD Track D)
- **Custom atom generation rules** — when the agent generates a novel atom, what validation ensures it's a valid combination?

These items are in scope for the Exercise Section's PRD-authoring phase, not for this document.

---

## 15. Strategic Context & Investor Demo

### 15.1 The Raise

MuseFlow is targeting a **$1.5M raise**. The pitch deck is being developed by Patrick. The agentic system is the central wedge — the demo target around which the deck is structured.

### 15.2 The Demo Flow

The May 7 brainstorm refined the demo flow from the May 5 single-walkthrough version into a **6-step integrated flow** that hits the major capabilities of the enhanced MuseFlow vision. The integrated flow surfaces the content/path-mode architecture (Decision #41), the agentic system's per-content-mode control surfaces (Decision #46, §6A), and the user-modeling layer's outputs (§1.2). It is aspirational; not every step is equally feasible on the demo timeline. The team's current understanding of feasibility and risk:

| Step | Demo content | Demonstrates | Feasibility | Risk profile |
|------|--------------|--------------|-------------|--------------|
| 1 | AI conversation / diagnostic / goal planning | Agentic conversation, diagnostic-agent behavior (§4.3), four authorship origins surface, the user-modeling layer beginning to populate | High — chat UI + LLM call | Latency risk; goal-classification accuracy risk |
| 2 | AI-driven visual roadmap construction featuring nodes for all main content types | Project flow, content/path-mode architecture, multimodal roadmap rendered as a vertical tree with branching (§7.2) | Medium — vertical-tree UI component + LLM JSON output | Vertical-tree component needs to exist; LLM consistent JSON output is non-trivial |
| 3 | Zoomed-in demo on a sight-reading component | Sight-reading integration, parameter-generated content (Decision #45), sight-reading control surface (§6A.3) | High — substrate exists | Choose existing content; agent links to it |
| 4 | Zoomed-in demo on an AI-driven repertoire session | Agentic repertoire orchestration, perfect-practice tree algorithm in action (Decision #42), audio recognition, AI feedback layer | **Engineering-critical path** | Live performance demo cannot be faked; voice-LLM latency; audio recognition reliability |
| 5 | Zoomed-in demo on an exercise component | Exercise framework, generation-on-demand (Decision #33), AI-prescribed practice (exercise control surface §6A.2) | Medium — exercise schema needs build-out + AI selection from matrix | Match what's discussed in Doc 10 §4.5 reverse-engineering methodology |
| 6 | Zoomed-out view of broader UI/UX with assorted Paths/Projects, dedicated content-pillar areas, aggregated metrics, suggested practice routines/plans | The integrated product surface, the user-modeling layer's outputs (§1.2), the long-term cohesion | Medium — UI scaffolding work | Aggregated-metrics dashboard not yet built |

**Step 4 is the engineering-critical path.** It's the only step that cannot be faked because the user is *playing* during it. Everything else can be partially scaffolded — links can be pre-built, screens can be rendered statically, the LLM can be primed with example responses. Step 4 requires the live substrate of audio recognition (Andrew's track), the auto-looping algorithm orchestrating repertoire controls (Patrick's PRD; Decision #42), and ideally text or voice feedback firing in response to performance data — all live. That makes step 4 the gating commitment for the integrated demo. Step 4's load-bearing components per Doc 10 §8.6:

- Voice-LLM latency under control (Staley: the technical hurdle)
- Repertoire perfect-practice toolset implemented to the point that the AI can engage tools (loop, slow-down, accuracy heat-map — per the §6A.1 surface)
- Auto-looping algorithm with UI integration (Decision #42)
- An LLM that can reliably emit JSON (problem-section locations) plus script (text/spoken cues) per Staley's two-output framing

**Incremental construction path.** Realistic demo construction is incremental — steps 1–3 + 5–6 are achievable on a near-term timeline with light scaffolding; step 4 is the gating commitment. The team can ship 1–3 + 5–6 as a "demo-without-the-killer-moment" if step 4 isn't ready, or hold the full demo until step 4 lands. Steven's read on the integrated flow: "I'm not sure if all of that's feasible, but this ideal would probably encompass most of the key features of the newly enhanced version of MuseFlow we're targeting." The aspiration is right; the phasing is a question for the pitch-deck timeline.

**Demo vs V1 scope.** The demo can be more polished than V1 for the specific capabilities demonstrated, while V1 is lighter on those same capabilities. This is normal and not a problem if the team is explicit about it. The exercise schema's full matrix is demo-buildable but does not need to be V1-ship-buildable; the auto-looping algorithm exists in Patrick's PRD but for V1 it needs documentation and the broader control-surface scaffolding; the visual roadmap needs polish for demo but V1 may ship a simpler list-style surface initially with the visual coming in V2. The pitch document should distinguish demo-state, V1-ship-state, and long-term-vision-state clearly.

Per Staley on the demo's strategic value:
> "The hitch and the demo — being able to say, yeah, upload a piece and here's your learning pathway to it. I think that would be a pretty killer demo."

The upload-piece-and-get-a-pathway moment is the gravitational center of the demo. Steps 1–6 are how the team makes that moment land with the full architecture visible behind it.

### 15.3 The 3-5 Year Plan

The deck structure (per Patrick's framing):

1. **Refine product** — get the agentic system, exercise framework, and content modes to a polished, defensible state
2. **Build community** — grow user base; develop the engagement layer; capture network effects
3. **Two-sided marketplace** — teachers and students, possibly with additional verticals (institutional sales, course publishing)

The agentic system is critical to all three phases:
- It's the differentiating product feature (phase 1)
- It drives engagement and retention (phase 2)
- It's a natural surface for marketplace content (phase 3 — teachers can author Projects, students can subscribe to Project plans, etc.)

### 15.4 The Team Composition Argument

Per Patrick (May 5):

> "Two incredible engineers, one of them a classically trained pianist, a music educator and a piano performer. All of us working on this thing — that's extremely unique. And what we decide to build is inherently going to be very unique because we have an incredible amount of skill across the four of us."

This is not an empty argument. The team has a rare combination of engineering depth, pedagogical sophistication, performance experience, and product instinct. That combination matters because the agentic system requires deep cross-disciplinary judgment: what matters pedagogically, what's technically tractable, what feels right to a learner. Few competing teams have this combination.

### 15.5 Why the Agentic System Is Demo-Defensible

Several properties make the agentic system a strong demo wedge:

- **It's visible.** Generating a roadmap from a stated goal is a tangible, on-screen output. Watching the system construct a custom path is the kind of moment that lands on stage.
- **It's general.** The same demo flow works for any goal — preparing for an audition, learning a piece, improving a skill. The investor sees one demo and extrapolates a thousand.
- **It's defensible.** Building the agentic system requires the exercise framework, the content modes, the data model, MAGE — all the work the team has been doing. Competitors cannot ship the agentic system without first replicating the substrate.
- **It's composable with the team's other work.** Andrew's audio recognition makes Project execution richer (the agent can hear the user practicing). The Repertoire Builder (Andrew's demo) makes custom-content authoring real. Auto-tempo adjustment (shipped) makes Project pacing adaptive. Looping (in development) makes practice sessions tractable. Each existing piece slots into the agentic story.

---

## 16. Cost Considerations

The May 7 brainstorm advanced the team's vocabulary for thinking about unit economics. This section captures the framework the team aligned on. **It is not pricing.** Pricing is still not designed (Decision #37). This is the cost-and-economics scaffolding the team uses to think about pricing when the design conversation begins.

### 16.1 The Six Principles

1. **Token-based pricing is customer-familiar.** Steven (May 7, line 1781): in AI products, token-based pricing is "basically expected." Users have been trained by ChatGPT, Claude, and Cursor to understand that AI-heavy actions consume measurable units. MuseFlow can reuse this vocabulary rather than inventing a parallel one.
2. **The average user is covered by subscription, profitable per user.** Steven (May 7, lines 1730–1734): the baseline-engagement user generates enough usage to be served within the subscription envelope while remaining profitable. Outliers — heavy generation, heavy custom content — are handled by upsells rather than absorbed by the platform.
3. **MAGE is a cost reducer relative to LLM-only architectures.** Patrick (May 7, line 1759): MAGE generates content algorithmically rather than via expensive LLM tokens. The augmentation framing (Decision #44) keeps this cost advantage intact: the LLM adjusts MAGE's output rather than replacing MAGE entirely. A pure-LLM architecture would lose this advantage. See §10.5.
4. **Heavy-generation periods amortize over engagement.** Steven (May 7, line 1770): a user's roadmap-building phase is generation-heavy (LLM calls to decompose goals, generate custom content, build the initial roadmap); the execution phase is generation-light (the user is practicing prebuilt content, with occasional adaptation). Per-user lifetime token cost is front-loaded; the user-modeling layer (§1.2) amplifies this by making earlier generations reusable across later Projects (§5.3).
5. **Per-month curriculum-generation limits with token-purchase upsell.** Patrick (May 7, lines 1771–1773): the subscription includes a monthly allotment of curriculum-generation budget; heavy users buy additional tokens à la carte. This pattern matches industry conventions (ChatGPT Plus message limits with paid overages, GitHub Copilot's hosted-model tiers, etc.).
6. **No subsidizing usage with investor money long-term.** Patrick (May 7, lines 1743–1749): "I would hate to have to get investments to be able to provide a service to our users who are paying for it, but not fully paying for it. We're like subsidizing it with like investor costs. I don't like that." The cost model must work at unit-economic equilibrium for sustainably-engaged users, even if early growth requires temporary subsidization.

### 16.2 What These Principles Imply Structurally

- **MAGE is a structural advantage, not just an engineering convenience.** Cost competitiveness against AI-first competitors depends on keeping MAGE in the loop. The augmentation framing makes this defensible because MAGE remains the bulk-generation engine and the LLM is the targeted-adjustment layer.
- **The user-modeling layer compounds.** Reusable generated content (§5.3) reduces re-generation costs over a user's lifetime. The longer a user engages, the better the user-model gets and the cheaper subsequent agent actions become — both because the AI has more context to work with and because the user's content library grows. This is a defensible long-run cost structure.
- **Pricing UX is its own design problem.** Whether users see token meters directly or opaque "AI generations remaining" affordances is a UX decision with downstream pricing implications (§13.9 #46). Whether MAGE-only generations get charged for "tokens" under the augmentation framing — where the AI adjusts MAGE's output — conflates LLM and MAGE compute for billing purposes; that's a question to settle deliberately (§13.9 #47).
- **The cost amortization model needs concrete grain.** At what generation rate do unit economics break? Per-Project, per-month, per-account? The framework above is qualitative; concretizing it for the pitch deck and for V1 capacity planning is open work (§13.7 #38).

### 16.3 What This Section Is Not

This section is not a pricing model. The team has explicitly deferred pricing design (Decision #37). What this section gives the team is a **defensible narrative for the pitch deck**: "MAGE makes generation cheap; LLM tokens are the variable cost; heavy generation is front-loaded per-user and amortizes over engagement; token upsells handle outliers; the user-modeling layer compounds over time." That narrative is investor-ready in shape. Concrete numbers come once Staley's LLM-cost exploration (§10.5) lands data and the team can model unit economics with real inputs.

---

## 17. Document Status & Evolution

### 17.1 Version

**Version 0.1 (May 7, 2026)** — Initial draft. Synthesized from the April 28 and May 5 MuseFlow standing meetings, the Emergent Curriculum brainstorm follow-up, and the A1 doc-sync conversation that produced canonical document updates across the Exercise Section project (Decisions #32–#41, Glossary expansion, Architecture schema additions, UX Spec §8 reframe, Bible §2 reframe).

**Version 0.2 (May 8, 2026)** — Phase 2 of the May 7 brainstorm doc-sync. Substantial additions: §1.2 (user-modeling layer as foundational architectural commitment, per Decision #47); §6 reframed with voice/audio modality and parallel-track framing across content modes; new §6A (Agent Control Surfaces per Content Mode, per Decision #46); new §10.7 (Metaphor vs Implementation discipline); §10.3 amended toward augmentation framing per Decision #44; §10.5 updated with Staley's exploration direction (Bedrock first, external API alternatives); §15.2 rewritten with 6-step integrated demo flow; new §16 (Cost Considerations); §4.2, §4.3, §5.2, §7.2, §12.2 sharpened; §13 substantially expanded with new open questions and §13.11 sub-cluster on Content Classes Beyond the Core Three. Cross-reference pass for Decisions #42–#47.

### 17.2 What Comes Next

Anticipated near-term work that this document should be updated to reflect:

- **Patrick's existing Theory Library & Exercise Section design document (Track A2).** Reviewing this document and integrating relevant material; some of its agentic content may inform this document.
- **Staley's LLM exploration outputs.** As Staley's Bedrock + external-API exploration (§10.5) produces data on cost, quality, and latency, §10 should be updated with what was learned and what the resulting architectural choices are.
- **MAGE long-term role conversation (Staley confirmation).** When Staley explicitly retires the training-data-then-replacement framing, Decision #39 can be closed and §10.3 updated to reflect full resolution.
- **Exercise section PRD.** Once the PRD lands, this document can reference its specific scope and align language.
- **Agentic system V1/V2/V3 phasing.** Most phasing in this document is currently TBD. When phasing is decided, this document should be updated.
- **UX design exploration.** As Project dashboard (§7), conversational surface (§6), roadmap-rendering UX (§7.2 vertical tree with branching), and per-content-mode control surfaces (§6A) are designed, this document should be updated with concrete decisions.
- **Content-classes-beyond-the-core-three resolution.** §13.11's sub-cluster captures the foundational question; resolution feeds back into §5.2 (node types), §3 (architectural foundation), and possibly a new §-level treatment of content classes.

### 17.3 Maintenance

This document is **canon-class** — it is the team's reference for how the agentic system is currently understood. As such:

- New conceptual additions go here, not in scattered notes
- Cross-references to Decisions, Bible sections, UX Spec sections, and other canonical artifacts are maintained inline
- Speculation continues to be marked explicitly
- Questions move from §13 to canonical sections when they're resolved
- Resolved questions get a Decision entry in the Exercise Section Decisions Log if they cross the exercise-section boundary, or are recorded here if they're agentic-system-internal

### 17.4 Doc 09's Eventual Independence

This document currently lives in the MuseFlow Exercise Section canonical document set. As the agentic system matures and accumulates its own design surfaces, design decisions, and reference material, it may warrant its own dedicated Claude project, with its own canonical document set. When that move happens:

- This document moves with the project (or is superseded by a successor document in the new project)
- Cross-references to Exercise Section canonical artifacts are preserved
- The Exercise Section project retains a pointer to where the agentic system now lives

That move is not yet imminent. For now, this document is the agentic system's home.

---

*End of MuseFlow Agentic Vision (Doc 09), Version 0.2.*