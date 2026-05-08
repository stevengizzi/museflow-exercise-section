# MuseFlow May 7, 2026 Brainstorm Synthesis: Emergent Curriculum Integration

> **Status: Phase 1 analysis (working draft, v0.2).** Synthesized from the May 7, 2026 Emergent Curriculum brainstorm transcript (`docs/meeting-transcripts/2026-05-07-museflow-agentic-vision-call.md`, 1857 lines, ~100-minute call). This document is the foundation for Phase 2 canon evolution and Phase 3 team-facing materials. Recommendations are drafted for Steven's review and approval — nothing committed in this document is canon until Phase 2 lands the corresponding edits.
>
> **Participants:** Steven Gizzi, Steven Staley (CTO), Patrick Boylan (co-founder).
>
> **Audience:** Steven (primary reviewer), future Claude conversations seeded with the integrated canon, MuseFlow team via downstream Phase 3 pitch document.

> **v0.2 changelog (key changes from v0.1, after Steven's first redline):**
>
> 1. **AI-company-framing analysis added** — the user-modeling layer as a structural moat is articulated in §3.7 (substantially expanded) and elevated to a Headline. New open question (§6 #13) about LLM-layer vs user-modeling-layer ownership.
> 2. **AI-analogy implementation evaluation added** — new §3.9 unpacks the metaphor-vs-implementation distinction for "diagnostic agent" / "Steven MD file" / etc. §3.6 expanded with the same evaluation applied specifically.
> 3. **Auto-looping scope narrowed** — §4.1, §4.7, and proposed Decision #42 reframed. Optimal Grip / Game Mode connections dropped per redline. Auto-looping is repertoire-only, one capability within a broader control surface.
> 4. **Agent-controllable repertoire practice control surface introduced** — §4.7 substantially rewritten as the broader category (per Steven's enumeration). New proposed Decision #46.
> 5. **Voice/audio LLM feedback reframed** — §4.2 updated to reflect parallel-battleground framing for repertoire AND exercises (not repertoire-only).
> 6. **Interactive Tutorials reclassified** — §4.3 substantially rewritten. They are existing canonical content, not future ambition. The 3D piano-hands discussion is on-topic (it addresses the AI-generation bottleneck for tutorials). Architectural placement open.
> 7. **Free Play split** — §5.1 rewritten. Free Play (original A1 sense, improvisation without notation) status unchanged. User-generated sight-reading mode (May 7 framing, custom-parameterized levels) resolved separately. Decision #45 split / narrowed.
> 8. **Video Library downgraded from "settled" to "open question"** — §5.3 moved to §6.
> 9. **Demo scope reframed as 6-step integrated flow** — §8.1 rewritten per redline. Step 4 (AI-driven repertoire session) identified as engineering-critical path.
> 10. **§6 expanded** with new questions on AI-company framing, content classes beyond the core three, Game Mode / Free Play toggle collapse, AI-analogy implementation choices, Interactive Tutorial placement.
> 11. **Phase 2 scope (§11) updated** — Doc 09 §1 vision pillar, Doc 04 Interactive Tutorial entry, agent-control-surface section.

---

## 1. Context

The May 7 call was scheduled at the May 5 standup as a dedicated working session on the Emergent Curriculum — the agentic system framing that had crystallized in late April / early May. Patrick framed the meeting opening as: "this is mainly just to facilitate a conversation about this sort of like emergent curriculum, you know, uh and and like and how to how to set up the like the the structure of it so that things can combine properly" (lines 47–48).

The call came after the A1 doc-sync conversation produced the canon's current architectural framing (content modes / path modes / four authorship origins / three flows — Decision #41) but before the rest of the team had been walked through that framing. So the meeting served two roles simultaneously:

1. **Steven's first verbal articulation** of the A1 architecture to Staley and Patrick
2. **A genuine brainstorm** that surfaced new capabilities, narrowed open questions, and converged on demo scope

Steven's read on the call (from the kickoff): foundational enough that this integration work is being prioritized over Track A2 (Patrick's design doc evaluation), which was already in progress in a separate conversation.

The transcript is informal — timestamps, profanity, and ~15 minutes of off-topic content (Staley's car project, scheduling). One section earlier flagged as off-topic in v0.1 — the 3D piano-hands discussion (Concert Creator AI, Massive Technologies, Robo Pianist) — is on-topic per the v0.2 redline; it directly addresses the AI-generation bottleneck for Interactive Tutorials. The signal is dense in roughly the first hour and the final 25 minutes, with a long lower-density middle section. This document filters for signal.

---

## 2. Headline Summary

The twelve things that matter most:

1. **The auto-looping algorithm is real and detailed — and it's one capability within a broader agent-controllable repertoire practice control surface.** Patrick's algorithm (read green-note JSON history, find first 2–3 errored notes in a row, center loop, perfect, auto-progress, combine in tree) is real, claimed-implemented in his PRD, and load-bearing for demo. Per Steven's redline, it's one specific orchestration pattern within a broader category — *agent-controllable repertoire practice tools* (song position, tempo, metronome, hand assignment, accuracy controls, audio playback, looping, cursor, note names / finger numbers). **Two Decision-class items: #42 (auto-looping) and #46 (control surface).** Lines 433–485, plus redline.

2. **The user-modeling layer is the load-bearing capability of "MuseFlow as AI company."** Steven's articulation around 00:38:43–00:41:54 (lines 494–525): the per-user accumulating context store is what makes MuseFlow structurally different from competitor piano apps and what justifies the AI-company framing in front of technically literate investors. Two distinct "AI company" interpretations exist: **LLM-layer** expertise (Staley's current direction toward AWS Bedrock / fine-tuning) and **user-modeling-layer** expertise (currently unowned). Both are defensible; the implicit assumption that they're the same job will create gaps. **The user-modeling layer should be added as an explicit vision pillar in Doc 09 §1.** Detailed analysis: §3.7. Open question: §6 #13.

3. **The MAGE-augmentation framing reached directional alignment.** Patrick: "the AI would probably be adjusting the mage output to make it more musical or to fit the like genre that they're trying to learn" (lines 1795–1800). Steven concurred, Staley did not push back. Closer to Steven's working position (Decision #39) than to "training-data scaffolding-then-replacement." **Decision #39 should be amended to reflect convergence.**

4. **User-generated sight-reading mode resolved — Free Play (original sense) status unchanged.** Per Steven's redline: v0.1 conflated two different things. The May 7 "free play" framing was specifically about user-constructed sight-reading levels with custom parameters, NOT about user improvisation without notation guidance (the original A1 Free Play sense). User-generated sight-reading mode is now resolved as user-generated content within the Sight Reading content mode. Free Play original sense remains deferred per Decision #40. **Decision #45 narrows.** Lines 580–870.

5. **Investor demo scope crystallized as a 6-step integrated flow.** Per Steven's redline replacing v0.1's Configuration A / B framing: (1) AI conversation / goal planning, (2) AI-driven visual roadmap construction, (3) sight-reading zoom, (4) AI-driven repertoire session, (5) exercise zoom, (6) zoomed-out UI with Paths/Projects/metrics/plans. **Step 4 is the engineering-critical path** (live performance, can't be faked). §8.1.

6. **Performance constraints generalize across content modes.** Steven explicitly carried the exercise section's vocabulary (time-based pass conditions, accuracy thresholds, memory-chain length) into sight reading, with Staley extending to repertoire and exercises in parallel. **They should be promoted to a cross-content-mode primitive.** Decision #43.

7. **Voice / audio LLM feedback as parallel-track capability for repertoire AND exercises.** Per Steven's redline: while repertoire is ahead because the substrate exists in the app, exercises are an obvious parallel target for the same feedback-and-orchestration pattern. The two should be built in parallel, not sequenced. Steven OK starting with text; voice-LLM is the technical hurdle. Lines 274–420.

8. **The four authorship origins / three-flow architecture survived first contact with the team.** Steven walked Staley and Patrick through the A1 framing using "isomorphism" repeatedly. Staley's "That's a crazy idea" (line 869) was enthusiasm. Patrick echoed back "we've thought of this as projects already" (line 116). **No structural objections; team is aligned with Decision #41 as written.**

9. **The AI analogies generated in the call require deliberate implementation evaluation.** "Diagnostic agent" / "auto-engaged plan mode" works at behavior level but is implementation-ambiguous (prompt-level vs application-level — see §3.6). "Steven MD file" / "Patrick MD file" hides a structurally different problem class than CLAUDE.md (AI-authored persistent memory vs human-authored file — see §3.9). Analogies are good for team alignment and pitch language; they are not architectural specifications. Phase 2 canon should preserve them as user-facing metaphors and explicitly cross-reference the actual implementation patterns.

10. **Staley committed to an LLM R&D direction.** End-of-call: "I'm just going to start digging into like how to do LLM. Um, I've watched some I've watched some videos from AWS on using their like AWS bedrock stuff and that might be like the step one. Um, I've also heard stuff about that being expensive. Um, maybe there's a way we can make calls to some external API" (lines 1828–1832). First explicit tooling commitment per Decision #32. Cost is the central concern.

11. **Interactive Tutorials are existing canonical content, not a future ambition.** Per Steven's v0.2 redline: Interactive Tutorials are animated videos with embedded live-action hand clips and Phaser-JS interactive exercises gated mid-flow. Each Sight Reading curriculum level has one. The May 7 discussion of AI-generating tutorials is about "more of an existing thing," not a new content class. The 3D piano-hands discussion (Concert Creator AI, Massive Technologies) is therefore on-topic — it addresses the production bottleneck (live-action hand clips). Architectural placement is open and clusters with Theory / Free Play / Video Library as the broader "what content classes exist beyond the core three" question. §4.3, §6 #15.

12. **Cost / unit-economics thinking advanced but stayed deferred.** The team aligned on token-based pricing as the customer-familiar model, per-month curriculum-generation limits with token-purchase upsell, and lifetime-value framing where heavy generation periods amortize across longer engagement. Pricing remains unspecified per Decision #37 — but **the framing now exists in enough detail that Doc 09 should have a "cost considerations" section** capturing it.

---

## 3. Architectural Validations and Analogy Evaluation

This section captures (a) places where the May 7 discussion confirms or strengthens the architecture currently in canon, and (b) — newly added in v0.2 — places where the analogies the team used to communicate the architecture deserve specific evaluation against their implementation implications.

### 3.1 The content/path mode architecture (Decision #41, Bible §2.1, Doc 09 §3.1)

Steven's mid-call walkthrough (lines 73–135) articulates the architecture using "isomorphism" / "fractal" language and the team echoes back without correction. Specifically, Steven recovered live during the call:

- Three content modes (Exercise, Sight Reading, Repertoire) — line 93–94
- Each with three sources of content: MuseFlow preset, user-generated, AI-generated — lines 98–106
- Plus path modes: preset curriculum, user-built road maps, AI-built Projects — lines 111–117
- Patrick's recognition: "we've thought of this as projects already" — line 116
- Staley's "yeah, that was kind of along the same idea" — line 121

Then later in the conversation, Steven added the **fourth authorship origin (Community)** explicitly while talking about how the user might find an exercise on a marketplace ("did somebody else make this and I found it? I bought it from them for $3.99 on the Museflow marketplace") — lines 870–877. Staley's "That's a crazy idea" (line 869) is enthusiasm, not skepticism — he immediately follows with use-case generation (teacher-authored semester paths, signature-artist courses).

**Implication for canon:** No changes needed to Decision #41 or Bible §2.1 from this validation. The framing is robust enough to stand verbal articulation cold.

### 3.2 Multi-content-mode roadmaps (Doc 09 §5.2)

Steven's articulation (lines 130–135): "road maps can be multimodal where like a road map has nodes on it like that some are site reading some are exercises some are repertoire and if you click on any of them it sort of hyperlinks you into the repertoire section and loads up the song or into the site reading and loads up the site reading level or into the exercise section."

Patrick: "Yes, it includes site reading repertoire exercises" (line 697). Patrick adds: "And I'm going to actually tack on top of there uh a video library" (line 699).

**Implication for canon:** Doc 09 §5.2 already captures the multi-mode property. The "video library" addition is moved to §6 below as an open question (its architectural placement is genuinely open per the v0.2 redline).

### 3.3 Roadmaps decoupled from sight-reading curriculum (Decision #29, Bible §2.2, Doc 09 §3.1)

Staley directly asks: "this site reading feature is separate from the road map as we have it today" (lines 680–683). Steven: "Curric any kind of road map you could call it curriculum or whatever any kind of road map is multimodal and can pull content from any section" (lines 694–696).

This is canon already, but it's worth logging that Staley independently arrived at the same framing.

### 3.4 User-as-author parity with AI (Decision #34, §3.4 of Doc 09)

Steven: "Anything the AI can do, the user also has the option to build if they want. That's that's how I think it should work. Like it is a sandbox for the user if you want and if you know what you're doing enough to do that or the AI can do it for you" (lines 851–855). Validates the user-as-first-class-author principle.

### 3.5 The teacher / signature-artist / institutional marketplace (Decision #35, Doc 09 §15.3)

Steven articulating mid-call: "you're a teacher. you make road maps and like this is the road map for fall 2026 semester for my freshman students... or you're a signature artist, you know, and you like made a course and you're selling the course" (lines 886–900).

Already in canon as future direction. The May 7 call shows the team treating it as concretely envisioned, not abstract — Patrick's "you can publish your own your own exercises... I want to make this available to everybody else" (lines 878–884) is the same shape.

**Implication for Phase 3 pitch document:** The marketplace direction is concrete enough in the team's heads that it can be presented as committed direction (with phasing TBD), not as speculation.

### 3.6 The conversational surface as goal-articulator (Doc 09 §4.3, §6.1) — with implementation evaluation

Patrick: "I think it needs to inherently ask the user like a f*** ton of questions to to like, hey, like I you you say you want to learn this, but like I need to know a little bit more about your intent, your goals, where you're at as a musician right now" (lines 561–565).

Steven articulates this as a "diagnostic agent" or "auto-engaged plan mode" — riffing on the analogy with Claude Code's auto-engagement of plan mode when a goal is detected (lines 1503–1518). Patrick agrees: "automatically engage that just base level until it has all the information it needs to be able to create that proper curriculum" (lines 1517–1525).

**The behavior the team wants is clear:** when goal-articulation signals are present, the system should fire follow-up questions until enough context exists to construct a roadmap.

**Implementation evaluation (added in v0.2).** The Claude Code analogy works at the *behavior* level but can mislead at the *implementation* level. In Claude Code, plan mode is a hardcoded application state with explicit tool-call gating — certain tools are unavailable until the model exits plan mode. It's enforced by the surrounding software, not by the LLM's discretion. The MuseFlow analog could be either:

- **Prompt-level:** the system prompt has a "diagnostic" section that activates when the model classifies the user's message as goal-articulation. Cheap and flexible. The load-bearing step is the LLM's reliability at zero-shot classifying "this is a goal-articulation moment." Failure modes: too-eager (user gets interrogated unnecessarily), too-slow (the conversation drifts).
- **Application-level:** the app has explicit modes between which the user (or the system) navigates, and which gate available actions/tools. The Claude Code analogy specifically is this kind. More deterministic but requires explicit UI affordances and probably an explicit "start a Project" entry point that puts the user into diagnostic mode.

These are very different to build. The team should pick deliberately, not adopt the analogy as if it specified the implementation. **Open question added in §6 (#14).**

**Recommended Phase 2 action:** Add diagnostic-agent / auto-engaged-plan-mode as a behavioral spec in Doc 09 §4.3 (Goal Articulation), with an explicit note that the implementation pattern (prompt-level vs application-level) is open and will be addressed during agentic system design.

### 3.7 Persistent, AI-mediated user model (Doc 09 §5.3, §10.5; partially §1) — substantially expanded in v0.2

The "Steven MD file" / "Patrick MD file" framing (lines 494–525) is at one level a vivid name for an architecture Doc 09 already commits to: persistence and reusability of generated content (§5.3), and a RAG layer over user historical play data (§10.5). On that level, the framing is validation — the team articulating, in evocative language, the same thing canon already says.

**But the substantive thing surfaced in this part of the call goes beyond the framing.** Steven articulated a strategic claim, and Steven's v0.2 redline asked for it to be taken seriously as a possible reframe of MuseFlow itself: that the per-user accumulating user-model is the technical capability that makes MuseFlow an AI company, not a piano-learning app with AI features. Three observations on this claim.

**1. The user-model is a structural moat.** Every other piano-learning product (Simply Piano, Yousician, Skoove, Flowkey) treats the user as roughly anonymous within their content — the content is the product; the user consumes it. MuseFlow's per-user accumulating model is structurally different. It compounds over time. A user's MuseFlow account becomes more valuable to them the longer they use it, in a way that competitors can't easily replicate without the same architectural commitment from day one. This is the same dynamic that makes ChatGPT memory a stickiness lever, applied to a domain (skill development) where the per-user data is genuinely unique and pedagogically rich. This is not a feature comparison — it's a positional difference in what the product fundamentally *is*.

**2. There are two different "AI company" framings, and they imply different team focuses.** One is **LLM-layer expertise** — the competitive edge is prompt design, model selection, inference cost optimization, fine-tuning. The other is **user-modeling-layer expertise** — the competitive edge is the data structures, retrieval logic, and synthesis pipelines that turn MuseFlow's playing/practice data into actionable agent decisions. These can coexist, but they're substantively different engineering investments and they imply different hiring priorities.

Per the May 7 call, Staley is heading toward LLM-layer expertise (Bedrock, fine-tuning, external API exploration). The user-modeling layer is currently nobody's explicit territory. If the team's read is "we're an AI company because of the user-model," then that layer needs an owner. If the read is "we're an AI company because of the agentic LLM layer," then Staley's current direction is exactly right. Either is defensible; both is best; but the implicit assumption that they're the same job will create gaps. **Tracked as open question in §6 (#13).**

**3. This matters for the $1.5M raise framing.** "MuseFlow is an AI company" lands at fundamentally different valuation multiples in 2026 than "MuseFlow is a piano app with AI features." Patrick's emergent-curriculum framing has been doing this work narratively, but the May 7 call's articulation of the user-modeling layer is the technical substrate that *justifies* the AI-company framing in front of technically literate investors. Without it, "AI company" reads as a positioning move; with it, it reads as a defensible architectural claim. The pitch deck (Phase 4) probably wants this articulated explicitly.

**Where this belongs in canon.** Doc 09 §1 (Vision) currently lists the strategic claim as "user states a goal, product builds personalized journey, generating custom content." The per-user accumulating user-model is the load-bearing capability that makes this work, and it should be named explicitly as a vision pillar. Without it, §1 reads like AI-as-feature; with it, §1 reads like AI-as-foundation.

**Recommended Phase 2 action:** Add user-modeling layer as an explicit vision pillar in Doc 09 §1, separate from but cross-referenced to the LLM/agentic-layer framing in §10. Cross-reference §5.3 (persistence) and §10.5 (RAG architecture) as the implementation detail. Mark the team-ownership question as open.

### 3.8 The atom schema's agent-prescribability fields (Decision #40, Doc 09 §3.4)

Not directly discussed at the field level, but Staley's "I am kind of thinking that I guess I'm I'm actually leaning back toward... if we did want to say like like feed the the AI like the universe of possibilities that would maybe be like a better mo model" (lines 1366–1378) presupposes that the universe of possibilities (the exercise matrix) is queryable by the agent. This is what Decision #40's `prerequisite_atoms` and `generation_mode` fields enable.

The reverse-engineering methodology (Staley's framing) only works if the schema is rich enough for an LLM to reason over — which is what A1 spent considerable effort on. Validation by use.

### 3.9 On the AI Analogies and the Implementation-vs-Metaphor Distinction (new in v0.2)

The May 7 call generated several AI-product analogies as ways to communicate the agentic vision: "diagnostic agent" / "auto-engaged plan mode" (Claude Code's plan mode), "Steven MD file" / "Patrick MD file" (Claude's CLAUDE.md), "large music model" (large language models). These analogies are useful for team-internal communication and pitch language — they're vivid, they rhyme with patterns the team already knows, they help externalize what the system is supposed to feel like.

But analogies can mislead in two ways. They can hide implementation complexity, and they can imply implementation patterns that aren't actually right for the underlying problem.

**Two specific evaluations:**

The "diagnostic agent" / "auto-engaged plan mode" analogy is evaluated in §3.6. Summary: the analogy works at the behavior level but underspecifies whether the implementation is prompt-level or application-level, and these have very different cost / control / failure-mode profiles.

The "Steven MD file" / "Patrick MD file" analogy is more structurally misleading. CLAUDE.md is *human-authored, human-maintained* — Steven writes the file; Claude reads it. What was described in the call is *AI-authored, AI-maintained* — the system observes the user and writes notes about them. This is a fundamentally different problem class. AI-authored persistent memory has at least four real engineering challenges that the CLAUDE.md analogy hides:

- A **synthesis problem** — the LLM has to decide what's worth remembering from each interaction
- A **recency-vs-relevance retrieval problem** — which past observations should fire on the current context
- A **drift problem** — AI-encoded mistaken beliefs about the user compound over time and become hard to correct without explicit user-correction affordances
- A **context-window problem** — a growing file eventually exceeds budget and needs compression / summarization passes

These are real engineering problems with real solutions: vector stores with embedding-based retrieval, periodic LLM-driven summarization, explicit user-visible memory management, possibly user-correctable memory entries. The shape is closer to "per-user RAG layer over conversation history, exercise/repertoire/sight-reading event data, and curated AI-extracted summaries" — the architecture Doc 09 §10.5 already gestures at.

**The analogy "it's like CLAUDE.md but the AI writes it" hides all of this.** Treating it as implementation-spec could lead engineering toward a single growing markdown file when the real architecture is a structured store with retrieval logic.

**The "large music model" framing** is somewhat different — it's positioning rather than implementation specification. As positioning, it's powerful (it implicitly claims MuseFlow is doing for music what foundation models did for text). As implementation, it could imply "we are training a single foundation model on music" — which is not the team's current direction. Worth being deliberate about whether this language enters customer- or investor-facing material.

**The pattern.** When an AI-product analogy is adopted, the team should:

1. Identify what behavior the analogy specifies (usually clear)
2. Identify what implementation the analogy implies (often unclear, sometimes wrong)
3. Decide deliberately whether to follow the implied implementation or pick a different one
4. Document the implementation choice separately from the user-facing metaphor

The analogies are good for team alignment and external communication. They are not architectural specifications. **Recommended Phase 2 action:** Add a brief "metaphor vs implementation" note to Doc 09 §10 (MAGE and the AI Layer), and adopt this evaluation pattern as a documentation discipline going forward (potentially in project-instructions.md). Open question tracked in §6 (#14).

---

## 4. New Capabilities Introduced

These are concepts discussed in the transcript that are not currently in any canon document and are substantive enough to need their own treatment in Phase 2.

### 4.1 The Auto-Looping / Perfect-Practice Tree Algorithm (scope narrowed in v0.2)

**The most substantively new content in the transcript.** Patrick walked the team through a specific algorithm (lines 433–485):

> Patrick: the note history is is a is a definitely a part of it... is stored as a JSON and it's and uh and and it basically says all the notes that you've gotten green so far and where the loop would start where the loop would start is your first section where you have like two or three notes in a row that are incorrect. And that's where the automated looping you just turn on looping.

Staley pushed: would it dynamically determine boundaries based on the error location, even in mid-piece?

> Patrick: we wouldn't we would center on the errored section and then because because you don't want to start with the errors. You want to you want to center on it and you want to get into it and then leave it. And then what it would do is auto progress you to the next f***** up section. And then what we would do is, and if there are green notes in between it, so be it. We would just loop that second section, then perfect it, and then we'd combine both of those sections, including all the green notes, into one big loop. Then... it's like a tree. It's it's I figured out the math of it all, and it and it works.

Patrick clarifies the tree shape: "smaller section, smaller section, those get combined. Then you move on, smaller section, smaller section, and those get combined. Then those get combined. Then you move on to the next ones" (lines 460–469).

Staley's read: "this is potentially all just algorithmic" — not LLM-required. The LLM's role becomes "voice/text sugar on top" — providing voice or text feedback during the algorithmic process (lines 480–484).

Steven concurred but added the AI-judgment dimension: "It is algorithmic, but it's also the the worry I've always had... binary tree structures... things tend to be more complex than that... you need that little bit of extra intelligence as the guider the teacher to be like okay but we're going to like break the rules here for like reasons X Y and Z. And this is where like again the AI comes in really handy" (lines 485–494).

**Assessment of completeness:** The algorithm is described in enough detail to be implementation-spec-ready, with one caveat. Patrick claims it works ("I figured out the math of it all and it works... I wrote it in the perfect practice"). That suggests it's already implemented somewhere in the codebase, though not in a way the rest of the team has seen end-to-end. Worth confirming with Patrick what artifact exists.

**Scope narrowed in v0.2 per Steven's redline.** The algorithm is **repertoire-only**. v0.1 over-extended the connections:

- Auto-looping is **not** an alternative to Optimal Grip. Optimal Grip operates at session-level adaptive difficulty (chevron count, tempo targets); auto-looping operates at practice-section selection within a piece. Different problem domains.
- Auto-looping is **not** a parallel to Game Mode. Game Mode is sight-reading-specific pass-condition mechanics; auto-looping is repertoire practice orchestration.
- Auto-looping for exercises was speculated about in v0.1 ("possibly exercises") — but the algorithm as Patrick describes it operates on a piece's note-history JSON, which is a repertoire artifact. Exercises would have analogous mechanics, but they'd be a different algorithm, not the same one ported.

The clearer framing: auto-looping is **one specific algorithmic capability within a broader category** — agent-controllable repertoire practice tools. See §4.7 below.

**Where it belongs in canon:**
- **Doc 09** — as a node-type-execution capability (not a node type itself); referenced in §6 (AI Surface) as one of the agentic system's repertoire orchestration tools; flagged in §15 as the load-bearing demo step (4)
- **Repertoire-section canon** — when that work begins, this is foundational. Patrick's PRD is the implementation source.

**Recommended action:** Decision-class material. See proposed Decision #42 (revised in v0.2) in §9.

**Demo implication:** Step 4 of the integrated demo (§8.1) is built around this algorithm — user plays a piece, AI identifies problem sections, sets up loops, walks user through perfect-practice tree, with text or voice feedback. Engineering-critical because it can't be faked.

### 4.2 Voice / Audio LLM Feedback During Practice (parallel-track framing in v0.2)

The discussion (lines 274–420) covers four distinct voice-feedback patterns:

1. **Real-time interruptive cues** — short instructions while playing ("slow down," "louder," "breathe breathe breathe"). Lines 280–286.
2. **Ding + spoken prompt** — Patrick's proposal: notification chime followed by spoken cue tied to existing notification messages (auto-tempo, flexible metronome). Lines 304–340.
3. **End-of-round feedback with action proposal** — between attempts: "here's some things I noticed; here's what I'd recommend; I'm setting up the loop for you right now." Lines 376–402.
4. **Conversational dialogue (Socratic)** — Steven: "you can just ask every stupid ass question you want and it will like keep talking to you until you actually get it" — a tutor persona for understanding theory and concepts. Lines 260–272.

Staley's framing (line 408): the technical hurdle is "literally just figuring out how to get the voice LLM thing going. Um like they have it flawed and whatever." After that, "the hard part is the automatic looping" — which is the §4.1 algorithm, already partially built.

Steven OK starting with text: "I'm okay starting with text, especially like I understand the the tricky part about that if it's trying to tell you things literally while you're playing, but if we're talking about these these this feedback in between plays, like I'm okay starting with text" (lines 417–421).

**Repertoire AND exercises as parallel battlegrounds (v0.2 redline correction).** v0.1 framed repertoire as "the first battleground." Per Steven's redline: while repertoire is ahead because the substrate exists in the app, exercises are an obvious parallel target. AI-generated content + AI-driven session management + voice feedback ("here's what you got wrong, here's a different exercise, here's why") is a parallel mechanic — and arguably a faster build for exercises because they're inherently more constrained than repertoire (smaller content space, simpler completion criteria, less performance variability).

The two tracks should be built in parallel rather than strictly sequenced. Repertoire's lead is incidental (substrate availability), not architectural.

**Assessment of completeness:** The capability is well-defined enough to enter canon. Specific UX details (text vs. voice, when each fires, how the user toggles, per-content-mode default) are open.

**Where it belongs in canon:**
- **Doc 09 §6 (The AI Surface)** — voice/audio feedback should be added as a function, with phasing TBD (text-first per Steven), and parallel-track framing for both repertoire and exercises
- Cross-reference to Decision #46 (control surface) since voice feedback is one of the surface tools the agent operates

**Recommended action:** Add to Doc 09 §6 in Phase 2. Probably not Decision-class on its own — it's an extension of the AI surface, not a new architectural primitive.

### 4.3 Interactive Tutorials — Existing Canonical Content, Architectural Placement Open (substantially rewritten in v0.2)

**Steven's v0.2 redline correction:** Interactive Tutorials are not a future ambition. They are a current canonical content class in MuseFlow. Each is an animated video with embedded live-action hand clips and Phaser-JS interactive exercises gated mid-flow — concept introduction → guided exercise → continuation. Each Sight Reading curriculum level is preceded by one. The May 7 transcript references this content class explicitly when the team discusses "interactive tutorials" (lines 142–280, 905–950) as bottlenecked human production work and as a candidate target for AI generation.

**Reframe of the §4.3 question.** The May 7 discussion of AI-generated tutorials is therefore not "should we add a new content type" but **"can we make more of an existing thing the team already produces by hand."** That's consistent with the generation-on-demand framing applied to other content types (Decision #33). The architectural question that remains is where, precisely, Interactive Tutorials live in the content/path-mode framing.

**The 3D piano-hands discussion is on-topic, not a non-sequitur.** v0.1 dismissed this section (lines 970–1100 — Concert Creator AI / Massive Technologies / Robo Pianist). That was a mistake. The 3D piano-hands discussion directly addresses the production bottleneck for Interactive Tutorials — the human-hand-clip portion. That is the slowest production step and the only piece the team can't currently AI-generate. The discussion is exploring whether the live-action-hand portion can be replaced with generated visuals, which would unblock AI-generation of tutorials end-to-end. Components considered:

- **Script generation** — fine-tuned model on MuseFlow's existing tutorial scripts. Considered tractable.
- **Text-to-speech** — considered solved.
- **Visual / video generation** — the hard part. Specifically the human-hand overlay. Discussion of 3D piano-hands software (Concert Creator AI, Massive Technologies — shut down 2022; Robo Pianist as an alternative) as candidate substrate.
- **Phaser-only generation** — Staley's idea: skip the human hands and generate everything as Phaser components.

Team consensus on AI-generation: hard, expensive, deferred ("let's wait until we've got some money to spare and throw money at this," lines 932–933). But the architecture should accommodate Interactive Tutorials as a content class regardless of how they're produced.

**Architectural placement open.** Interactive Tutorials don't yet have a clean placement in the content modes / path modes framing. Candidate placements:

- **Their own content mode** (a fourth or fifth mode alongside Exercise / Repertoire / Sight Reading) — if so, what is the Browse / Generate / Project shape for tutorials?
- **Path-mode primitive embedded in curriculum** — tutorials live inside Curriculum (the path mode), not as standalone content. This matches the current state.
- **Roadmap node type** — tutorials become nodes the agent prescribes within Project roadmaps, not a mode users browse independently. Staley's framing in the May 7 call (lines 916–924) leaned this way: "those would actually fit very well into these custom generated paths or road maps or like plans, but like as single nodes that are just like, okay, here's like a concept that this person needs to know."
- **Some hybrid** — a content-mode-with-special-flows that surfaces both as standalone Browse experience and as agent-prescribable nodes.

**Connected to broader open question.** The architectural placement question for Interactive Tutorials is structurally the same question being asked for Theory, Free Play (original sense), and Video Library — what content classes exist beyond the core three (Exercise, Repertoire, Sight Reading)? See §6 question cluster.

**Where it belongs in canon:**
- **Doc 04 (Glossary)** — Interactive Tutorial should already be a glossary entry. Add in Phase 2.
- **Doc 09 §5.2 (Roadmap Node Types)** — at minimum, "Tutorial node" should be a candidate node type
- **Doc 09 §13 / Bible §2.1.1** — Interactive Tutorial architectural placement as open question, clustered with Theory / Video / Free Play

**Recommended action:** Phase 2 lands the glossary entry and the open-question cluster. The architectural placement is genuinely open and shouldn't be forced.

### 4.4 Performance Constraints as Cross-Content-Mode Primitive

Steven explicitly maps the exercise section's performance-constraint concept onto sight reading (lines 824–842):

> Steven: this is actually pulling from exercise section because like this is something I've been thinking about for exercises. Sometimes you set these up in different ways. Sometimes it's like okay in order to pass this exercise you need to get 20 right and then you're done. But sometimes what you do is it's not about how many get right it's about like it's a time trial for example. It's like this is the duration of the exercise and how many can you get in this time, you know, for example.
>
> And so you could port that over into site reading and you could be like this is not about chevrons. This is about this exercise lasts for five minutes. No more, no less. And if if you last if you get through all five minutes where your accuracy did not once drop below X percentage, that's a pass.

Staley: "the exercise section can also maybe be a version of this game mode thing" (line 842).

In canon, performance constraints are currently exercise-internal (see Bible §6.3, Architecture Doc §5, Decision #22). They are described as "stress-testing the same exercise in different ways — speed, accuracy, memory chain length, recall delay" — and that framing only references exercises.

**This is a real architectural extension.** Performance constraints become a property of any "completable" engagement with content (exercise atoms, sight-reading levels, possibly repertoire), not just exercises.

**Assessment of completeness:** Conceptually clear. The mapping to specific content modes needs work — what does an "accuracy floor over time" pass condition look like for repertoire?

**Where it belongs in canon:**
- **Bible §2 or §6** — performance constraints become a cross-cutting primitive, not just an exercise-section feature
- **Architecture Doc** — needs a section on cross-mode performance constraints, or a generalization of existing §5
- **Doc 09** — implicit; the agentic system can prescribe performance constraints across modes

**Recommended action:** Decision-class material. See proposed Decision #43 in §9.

### 4.5 Reverse-Engineering the Exercise Catalog from Agent-Desired Content

Staley's methodological proposal during the demo discussion (lines 1366–1378):

> Staley: I am kind of thinking that I guess I'm I'm actually leaning back toward uh not all the links have to work. But like if we did want to say like like feed the the AI like the universe of possibilities that would maybe be like a better mo model because it would give us a more realistic list of like road map items. um if to whatever song and then we could choose which ones like okay maybe we do see like five or six show up over and over again but maybe we start at like here's like here we we say here are all the exercises that we we give it the future end result end point and say like and...
>
> Steven: Have it build a road map whether it has the content or not and then look at the road maps and be like, "Well, it keeps wanting to build this thing, so I guess we should have this." That's an interesting thought of like kind of reverse engineering it.

This is a **methodological proposal**, not a feature. But it's consequential for Track D (V1 atom catalog authoring).

**Implication:** Track D's current implicit methodology is bottom-up enumeration from substrate-modality combinations. Staley is proposing a complementary top-down methodology: feed the agent ~10–30 user goals (the "user stories"), let it propose road maps drawing from the full schema universe, and observe which atoms it keeps wanting. The intersection of bottom-up enumeration and top-down agent-demand becomes the V1 catalog target.

This isn't either/or. Both methodologies are useful. But the team's agreed plan during the call (lines 1402–1450) is to start by listing 10–30 example user stories — that's effectively committing to the top-down approach as a Track D input.

**Where it belongs:**
- **Track D's methodology section** (when authored) — this should be one of the documented inputs
- **Doc 09 §15 (Investor Demo)** — the demo and the catalog converge here

**Recommended action:** Not Decision-class on its own (it's a methodology, not an architectural commitment). But Phase 2 should add a brief note in Doc 09 §15 and/or in a Track D scoping document.

### 4.6 Vertical Branching Roadmap Visual (Fez/Duolingo-Inspired)

Lines 1604–1675. Patrick references the Fez game's vertical road map visual; Steven recovers having shared the reference previously. They look at it together; Patrick: "this is kind of the idea of the road map that we that we've kind of we both totally are drawn to."

Key properties:
- **Vertical orientation** (Patrick: "Duolingo does a vertical road map and that really feels right for me because you're kind of going towards a goal") — line 1661
- **Branching, parallel paths, fast-track shortcuts** — Steven: "any good road map allows for nonlinear possibilities... it needs to allow for parallel like sort of parallel opportunities" — lines 1646–1652
- **The 3D-to-2D condensation** — Patrick: "they have a 3D version of it and then they then they've condensed it down into a 2D version and it totally f****** works" — lines 1630–1632

**Where it belongs in canon:**
- **Doc 09 §7.2 (Per-Project Zoom)** — currently lists "list, tree, graph, timeline" as candidates; should narrow toward "vertical tree with branching/parallel paths"
- **Doc 09 §13.6 / Open Question 21 (Dashboard Rendering)** — partial resolution

**Recommended action:** Sharpen Doc 09 §7.2 in Phase 2. Not Decision-class — it's a UX direction, not committed UX.

### 4.7 Agent-Controllable Repertoire Practice Control Surface (substantially rewritten in v0.2)

The May 7 call surfaced auto-looping (§4.1) as a specific algorithmic capability. Steven's v0.2 redline reframed: auto-looping is *one* algorithmic capability within a broader category — **the set of repertoire practice tools the agentic system can control during a session**. The agent's repertoire-practice job is orchestrating across this surface; auto-looping is one orchestration pattern.

**Steven's enumeration of the repertoire control surface:**

- **Song position** — where exactly to place the user in the song to start the next take
- **Tempo controls** — when to speed up or slow down, and by how much
- **Metronome** — on/off; accented downbeats vs unaccented; flexible vs fixed count-in (metronome buffers vs counts exact beats)
- **Hand assignment** — which hand(s) to play at any given time
- **Accuracy controls** — track or not; which hand(s) to track for; show real-time color feedback or not (red/yellow/green for wrong-pitch / right-pitch-wrong-timing / correct); preserve note-color feedback across takes or reset; success threshold (e.g., 95%, 85%)
- **Audio playback** — silent / dueting (app plays alongside user) / app-only / no MIDI
- **Looping controls** — start/end points; seamless back-to-back vs paused between takes; takes-required threshold; tempo adaptation per take (does tempo shift up or down each pass?)
- **Cursor toggle** — show/hide the playhead cursor moving along sheet music
- **Note names, finger numbers** — display either as overlay aids

**Architectural implication.** The agentic system's repertoire-practice job is a *policy* over this surface — given Project goal, current performance data, and user preferences, decide which surface elements to engage and how to set them. Auto-looping (§4.1) is one such policy: identify problem sections, set up looping with specific start/end and takes-required, optionally adjust tempo, optionally adjust accuracy threshold, optionally engage hand-by-hand isolation. That policy bundles several surface elements together.

**The same shape extends to other content modes.** Exercises have a parallel surface (training method selection, performance constraint settings, content scope choice, blueprint configuration). Sight reading has a parallel surface (parameter generation, level construction, game-mode toggles, performance constraints). Each content mode has its own enumerable agent-control surface.

**Where it belongs in canon:**
- **Doc 09** — new section, possibly §6 sibling, "Agent Control Surfaces per Content Mode," that enumerates the surface for repertoire (per Steven's list), and sketches surfaces for exercises and sight reading
- Cross-references from Decision #42 (auto-looping is one capability) and Decision #46 (the surface itself)

**Recommended action:** Decision-class. See proposed Decision #46 in §9.

---

## 5. Resolutions of Previously-Open Questions

Items where the May 7 call directionally settled or fully resolved questions previously tracked as open in `09-agentic-museflow-vision.md` §13, `07-ux-navigation-spec.md` §9, or open Decision Log items.

### 5.1 User-generated sight-reading mode resolved; Free Play (original sense) status unchanged (revised in v0.2)

**v0.1 conflated two different things.** Steven's v0.2 redline corrects this. Two distinct items must be tracked separately.

**Free Play (original A1 sense):** A future mode involving user improvisation without exact notation guidance — open-ended musical exploration. This was deferred indefinitely per Decision #40 / Bible §2.1.1. **The May 7 call did not address this.** Status unchanged.

**User-generated sight-reading mode (May 7 framing):** A capability where a user constructs a custom sight-reading "level" with explicit musical parameters (notes, rhythms, time signature, dynamics, complexity metrics), performance constraints (time-based, accuracy-based, etc.), and completion settings. This is what the May 7 call resolved.

**What's now settled for the May 7 framing.** User-generated sight-reading with custom parameters fits cleanly within the Sight Reading content mode, in the user-generated authorship origin (per Decision #41). No new content mode needed. The user invokes the Sight Reading mode's Generate flow and configures the level. The level may carry "no completion criteria, just play endlessly" as one of the configurable options.

**What was discussed:** Lines 580–870. Staley initially framed sight-reading-with-AI as "free play, not the road map" (line 583). Steven articulated the user-generated framing (lines 813–821):

> Steven: I I I think this falls under user-generated because you as the user go into this this sandbox thing where you're like I want this this this and this and by the way I want it to be no we're not tracking accuracy we're just playing endlessly you know or whatever and like and then you do it.

Staley's reaction: "I don't mind calling it free play and having free play have like a game mode" (line 801). Patrick: "or we just don't even need to call it any mode or like a section really" (line 808).

The May 7 articulation closes the long-standing ambiguity about user-parameterizable sight-reading. The user-generated authorship origin (Decision #41) provides the primitive. No new mode is required.

**Separate observation tracked as open question.** The current Game Mode and Free Play *toggles* on each Sight Reading curriculum level (existing app functionality, distinct from "Free Play" as a future mode in the original A1 sense) may collapse and be subsumed in other functionality as the new architecture is implemented. This is a UX consolidation question. Tracked in §6 (#16).

**Recommended action:** Decision #45 (proposed in v0.1) is split — see §9. Bible §2.1.1 updates only to reflect the user-generated sight-reading clarity, not Free Play status. Decision #40's Free Play deferral remains in place unchanged.

### 5.2 MAGE long-term role (Decision #39, Doc 09 §10.3, UX Spec §8.6 Q5)

**Status before:** Open architectural question. Steven's working position (augmentation): MAGE persists, AI augments. Staley's framing (training-data scaffolding): MAGE generates training data for an eventual replacement LLM. The two framings were not reconciled in the May 5 standup.

**What was discussed:** Lines 1789–1810. Patrick, in the context of pricing for MAGE-generated content, said:

> Patrick: the AI would probably be adjusting the mage output to make it more musical or to fit to fit the like genre that they're trying to learn or to specifically work specific techniques that are in the piece of repertoire that they want to learn like whatever. There's like many reasons why the AI would adjust the music XML outputed by Mage.

Steven: "True." Staley did not push back; his immediately preceding response was "That's true. That's true." (line 1796) and "Sure" (line 1799).

Earlier in the call (lines 589–594), Steven also said: "this is where the AI turns into like mage or or whatever the the AI based system is. And I like I I still will just want to call it mage no matter what even if we like replace the system because I just I came up with the name and I just really like it." Staley laughed, agreed: "Yeah. Yeah. We can call him mage. We can call him mage" — and then said "I love mage. Yeah. Yeah."

**What's now directionally settled:** The team is converging on the augmentation framing. The AI's role is to adjust MAGE's output, not replace MAGE's role. The Patrick quote articulates this in terms of musicality and stylistic fitness — exactly the gap Doc 09 §10.4 identifies as the AI's strength.

**What remains open:** Full architectural commitment. Steven's position has team alignment but Staley hasn't explicitly said "I've changed my framing." The earlier framing (training-data-then-replacement) hasn't been retired so much as quietly displaced. Worth getting Staley's explicit confirmation.

**Recommended action:** Amend Decision #39 to reflect the directional convergence. Retain the question as "open" pending Staley's explicit confirmation, but record the team's current position more strongly. See proposed Decision #44 in §9.

### 5.3 Performance constraints as cross-mode (UX Spec §9 Q5 partial)

**Status before:** Performance constraints were exercise-internal in canon (Bible §6.3, Architecture Doc §5). Cross-mode application was not articulated.

**What was discussed:** Lines 824–862, covered in §4.4 above.

**What's now settled:** Performance constraints are conceptually cross-mode. The exercise section's vocabulary (time-based pass conditions, accuracy thresholds, memory-chain length) carries over to sight reading and possibly repertoire.

**What remains open:** Specific mapping per content mode. What does each performance constraint type look like in each mode?

**Recommended action:** Decision-class. See proposed Decision #43 in §9.

### 5.4 The 5 goal categories (Doc 09 §4.2)

**Status before:** Doc 09 §4.2 lists six goal types (Repertoire-bound, Curriculum-bound, Performance-bound, Skill-bound, Experience-bound, Open-ended).

**What was discussed:** Lines 1450–1565. The team converged on **5 main goal categories** for demo user stories:

1. "I want to learn this specific piece" (Repertoire-bound — same as canon)
2. "I'm studying for this specific exam" (Curriculum-bound — same as canon)
3. "I want to get better at this specific technique" (e.g., Alberti bass) — partly Skill-bound but more narrow
4. "I want to play like this specific musician/artist" (e.g., Bill Evans) — new framing not exactly in canon
5. "I'm really interested in this specific genre" (e.g., bluegrass) — new framing not exactly in canon

Patrick: "all of those will be a combination of exercises, site reading and repertoire" (line 1540). Steven adds music theory and (per Patrick) videos.

**What's now settled:** Operational list of demo-driving goal types. Useful for both the demo scope and Track D / E.

**What remains open:** Whether to revise Doc 09 §4.2 to align with these 5 categories. The canon's six types are a superset; Steven's articulation here is a different cut. They're not contradictory.

**Recommended action:** Sharpen Doc 09 §4.2 in Phase 2 to include all of: the canon's six types as conceptual categories, plus Steven's five demo-relevant categories as concrete examples. Mark which are demo-targeted.

### 5.5 Investor demo scope (Doc 09 §15.2)

**Status before:** Doc 09 §15.2 specifies the canonical demo flow: (1) user uploads piece, (2) MuseFlow generates Mario-path roadmap, (3) walkthrough, (4) conclusion. Per the May 5 standup framing.

**What's now settled (v0.2 reframe).** Per Steven's redline, demo scope is best framed as a **6-step integrated flow** (rather than the v0.1 Configuration A / B framing). See §8.1 for the full breakdown. Step 4 is engineering-critical (live performance, can't be faked).

**Recommended action:** Update Doc 09 §15.2 in Phase 2 — substantial rewrite around the 6-step integrated flow.

### 5.6 Onboarding integration with Projects (Doc 09 §13 / new question)

**Status before:** Onboarding wasn't directly addressed in canon as it relates to the agentic system.

**What was discussed:** Staley (lines 566–578): "the the the initial pest or whatever. Like maybe instead of that or on top of that like the first thing you do when you log into Museflow is you get a chat screen that says like what are your goals like what would you like to learn and then it says okay now let's analyze your skill level and you get the like dynamic music start that starts coming up."

**What's now settled:** Onboarding-with-Projects is a directional commitment for *some* users — the chat-first goal-articulation pathway is a real onboarding option. But Doc 09 §12.2 commits that "onboarding doesn't assume they want to start with a Project" — both must be true. Steven's v0.2 redline confirmed: "Onboarding-with-Projects is a good option for some, but perhaps not all."

**What remains open:** How onboarding splits paths (assumed-Projects vs. exploration). Is there a chooser? Defaults? Configurable? How does the system decide which onboarding path to surface to which user?

**Recommended action:** Update Doc 09 §12.2 to acknowledge Projects-first onboarding as one of several paths, while preserving the AI-averse-friendly default. Add as open question (§6 #19) for the path-split logic.

---

## 6. New Open Questions Surfaced

Questions raised by the call that aren't yet tracked anywhere. These should be added to Doc 09 §13 and/or UX Spec §9 in Phase 2. Expanded in v0.2.

### 6.1 From original v0.1 (preserved with renumbering)

1. **Voice-LLM default mode.** Voice vs. text vs. both, configurable per user, configurable per content mode? Steven OK with text-first. Repertoire is the natural first battleground (with exercises as parallel track per v0.2). But default behavior in V1 of this capability is undefined.

2. **Auto-looping AI-judgment override.** Steven flagged that the algorithmic perfect-practice tree may need AI judgment to break the rules (e.g., "actually, the issue is the previous measure, not this one"). When does the AI override the algorithm? How does the user perceive that override?

3. **Tutorial-as-roadmap-node phasing.** Per §4.3 reframe, Interactive Tutorials are existing content with open architectural placement. One placement option is roadmap-node-type. Even if AI-generated tutorials are deferred, does the architecture allow human-authored tutorials as roadmap nodes in the meantime?

4. **Reverse-engineered catalog merger with bottom-up enumeration.** Track D will have two methodologies (top-down agent-demand and bottom-up substrate enumeration). What's the merge / triage process?

5. **Cost amortization model granularity.** The team's lifetime-value framing (heavy generation periods amortize over engagement) needs a concrete mental model — at what generation rate do unit economics break? Is it per-Project, per-month, per-account?

6. **Token-based pricing surfacing.** Do users see token meters directly (Staley: "we could even surface tokens directly")? Or do they see opaque "AI generations remaining"? Different UX implications.

7. **MAGE pricing under augmentation framing.** Patrick noted that under the augmentation framing, even MAGE-only generation could be charged for "tokens" since the AI is adjusting MAGE's output. This conflates LLM compute with MAGE compute for billing purposes. Is that right or wrong?

8. **Vertical roadmap visualization details.** Direction set (vertical, Fez-like, branching). But: how does the user pan/zoom across long roadmaps? Mobile rendering? Progress indicators?

9. **End-of-round AI feedback timing.** Steven's "in between plays" feedback (Doc 09 §6 doesn't currently distinguish this from real-time). Specific UX for the pause/feedback/setup-loop flow needs design.

10. **Large Music Model framing.** Staley's enthusiasm for "Large Music Model" terminology (line 605) raises a positioning question — is MAGE a "large music model"? Is the augmented MAGE+AI system? Does this language enter customer-facing material? See also §3.9 on analogy evaluation.

### 6.2 New in v0.2

11. **Video Library architectural placement.** (Moved from §5.3 in v0.1.) Patrick's framing ("video library") leans content-mode-like. Staley's framing ("node-as-tutorial") leans roadmap-primitive. A2 evaluation will inform. Connected to question 15. Steven's v0.2 redline: "I wouldn't quite call the 'video library' feature as 'now settled'. That warrants further discussion."

12. **Game Mode / Free Play toggle collapse.** Current Sight Reading curriculum levels have Game Mode and Free Play toggles (existing app functionality). As the new content/path mode architecture is implemented, these may subsume into other functionality (e.g., performance constraints, user-generated mode). UX consolidation pattern open. (Note: distinct from Free Play original-sense status, which remains deferred per Decision #40.)

13. **AI-company framing — LLM-layer vs user-modeling-layer ownership.** Per §3.7. Two interpretations of "we're an AI company": LLM-layer expertise (Staley's current direction toward Bedrock / fine-tuning) and user-modeling-layer expertise (data structures, retrieval logic, AI-driven user-context store — currently nobody's explicit territory). Both defensible; the implicit assumption that they're the same job will create gaps. Decide deliberately who owns the user-modeling layer.

14. **AI-analogy implementation choices.** Per §3.6, §3.9. Diagnostic-agent / auto-engaged-plan-mode is prompt-level or application-level? Per-user "Steven MD file" memory — single growing markdown vs structured RAG store with retrieval logic? Decide deliberately during agentic system design rather than letting the analogy specify the implementation by default.

15. **Content classes beyond the core three.** What content classes exist beyond Exercise / Repertoire / Sight Reading? Candidates: **Theory** (Bible §2.1.1, A2 evaluation), **Free Play original sense** (deferred per Decision #40), **Video / Video Library** (May 7 raised, placement open), **Interactive Tutorial** (existing canonical content, placement open). Some may collapse / overlap. This is one of the foundational architectural questions for the agentic vision and probably deserves its own §13 sub-cluster in Doc 09.

16. **Interactive Tutorial architectural placement.** Per §4.3 reframe. Existing content class but no clean home in current architecture (own content mode? path-mode primitive? roadmap node type? hybrid?). Sub-question of #15.

17. **Auto-looping's relationship to Optimal Grip.** v0.1 framed auto-looping as subsuming Optimal Grip; Steven's redline rejected that. Optimal Grip is session-level adaptive difficulty (chevron, tempo); auto-looping is practice-section selection within a piece. Different problems. But are there situations where Optimal Grip's logic should drive auto-looping's parameters? E.g., when Optimal Grip lowers tempo, does auto-looping inherit that? Not pressing, but worth defining when both are V1+.

18. **Exercise and Sight Reading control surfaces enumeration.** Per §4.7 / Decision #46, repertoire's control surface is enumerated. Exercises' surface (training method, performance constraints, content scope, blueprint configuration) and sight reading's surface (parameter generation, level construction, game-mode toggles, performance constraints) are sketched but not enumerated to the same depth. Worth completing in Phase 2.

19. **Onboarding path-split logic.** Per §5.6. How does the system decide which onboarding path (Projects-first vs exploration-first) to surface to which user? Configurable? Default rule? Tied to declared user type at signup?

---

## 7. Items That May Want Past-Canon Revisits

Places where the May 7 discussion suggests a previous canon decision should be reconsidered. Steven explicitly invited surfacing these.

### 7.1 Decision #37 (Pricing/Tier Gating) — `tier_gating` decision

**The dropped field:** `tier_gating` was considered and dropped on the rationale that "adding speculative fields creates noise and falsely signals that pricing is a near-term design surface."

**Why it might want revisiting:** The May 7 call advanced cost / unit-economics thinking significantly (per-month curriculum-generation limits, token-based pricing, MAGE-cost considerations). Pricing is still not designed, but the team's vocabulary is now richer.

**Recommended action: track-for-later.** Don't revisit in Phase 2. The reasoning in Decision #37 still holds — pricing isn't designed enough to commit a field. But Phase 4 (pitch deck) work may force pricing concretization, at which point this needs revisiting.

### 7.2 Decision #20-area items: Optimal Grip, Looping, Game Mode (revised in v0.2)

**The current state:** Optimal Grip is deferred (decision-area indicates V2+). Looping is in development. Game Mode is sight-reading-specific. These are treated as separate concepts.

**Why it might want revisiting (revised in v0.2):** Per Steven's redline correction, the connections between auto-looping and these concepts are weaker than v0.1 claimed. The Optimal Grip relationship is genuinely partial (both are forms of adaptive difficulty, but they operate at different levels). Game Mode is sight-reading-only and unrelated to repertoire auto-looping. These do *not* need to be merged or restructured by Decision #42.

What does want documentation: how auto-looping (Decision #42) sits within the broader repertoire control surface (Decision #46), and how that surface relates to user-set Looping (the manual version). These are layered components, not parallel features.

**Recommended action: track-for-later.** Phase 2 captures the layering implicitly via Decisions #42 and #46. A future canon-cleanliness pass can update Decision #20-area items if needed, but it's not pressing.

### 7.3 Doc 09 §10.3 (Augmentation Question)

**The current state:** Records the question as open with Steven's working position (augmentation) as default and Staley's framing (training-data-then-replacement) as alternative.

**Why it might want revisiting:** §5.2 above. The May 7 call moves the team further toward augmentation.

**Recommended action: revisit-in-Phase-2.** Amend §10.3 to reflect the directional convergence. Probably don't fully close the question yet — it deserves Staley's explicit confirmation — but the framing in canon should track the team's current position.

### 7.4 Bible §2.1.1 (Free Play status) — corrected in v0.2

**The current state:** "deferred indefinitely; whether free play belongs as a content mode, a path-construction primitive, or its own non-mode category is open."

**Why it might want revisiting (revised in v0.2):** Per Steven's correction, the May 7 call did NOT resolve Free Play (original sense) — it resolved a separate thing (user-generated sight-reading mode). Free Play original sense status is unchanged.

What Bible §2.1.1 needs: clarification that user-generated sight-reading mode (custom-parameterized levels) is not the same as Free Play (improvisation without notation). The two should be cleanly distinguished. Free Play stays in the "Candidate future content modes" list with deferred status. User-generated sight-reading mode is captured under the Sight Reading mode's user-generated authorship origin (per Decision #41), not as a separate item.

**Recommended action: revisit-in-Phase-2.** Update Bible §2.1.1 to clearly distinguish the two. Don't delete Free Play from the candidates list.

### 7.5 Bible §6.3 (Replayability Through Constraint Variation) — performance-constraints scope

**The current state:** Frames performance constraints as an exercise-section product-level insight.

**Why it might want revisiting:** §4.4 above. Performance constraints generalize across content modes. The Bible treatment should reflect this.

**Recommended action: revisit-in-Phase-2.** Either generalize §6.3, or move performance-constraints framing to a higher-level Bible section (likely §2 or a new §) so it covers all modes.

### 7.6 Decision #29 (Agentic Vision — Documented as Future Architecture) — supersession

**The current state:** Decision #29 is partially superseded by Decision #32 / #41 in canon's framing.

**Why it might want revisiting:** Mostly canonical-cleanliness. After the May 7 call's strong validation of the architecture, the "documented as future" framing in #29 reads as outdated.

**Recommended action: track-for-later.** Cosmetic, low-priority. Address during a future canon-cleanliness pass.

### 7.7 Doc 09 §15.2 (Demo Flow)

**The current state:** Specifies the May 5 canonical demo (upload piece → roadmap → walkthrough → conclusion).

**Why it might want revisiting:** §5.5 above and §8.1. The 6-step integrated demo flow per Steven's redline is a substantially richer artifact.

**Recommended action: revisit-in-Phase-2.** Substantial rewrite. Replace canonical-demo-only framing with the 6-step integrated flow.

### 7.8 Doc 09 §4.2 (Types of Goals)

**The current state:** Six goal types listed conceptually.

**Why it might want revisiting:** §5.4 above. The May 7 call's 5 demo-relevant categories are partly different cuts (specific musician, specific genre).

**Recommended action: revisit-in-Phase-2.** Sharpen by adding the May 7 categories as concrete examples within the existing six conceptual types.

### 7.9 Doc 09 §6 (The AI Surface) — voice/audio extension

**The current state:** Lists conversational surface functions in text form. Doesn't distinguish text vs. voice.

**Why it might want revisiting:** §4.2 above. Voice/audio LLM feedback is a meaningful extension that should be documented.

**Recommended action: revisit-in-Phase-2.** Add voice/audio as a distinct surface modality, with text-first phasing per Steven's preference. Note parallel-track framing for repertoire and exercises.

### 7.10 Doc 09 §5.2 (Roadmap Node Types)

**The current state:** Lists exercise / repertoire / sight-reading / milestone / conditional gate / free-play interlude / reassessment / branch-point node types.

**Why it might want revisiting:** §4.3 (Interactive Tutorial node) and §6.2 #11 (Video node). New candidate node types per v0.2.

**Recommended action: revisit-in-Phase-2.** Add Tutorial-node and Video-node as candidates, marked deferred / placement-open.

### 7.11 Doc 09 §1 (Vision) — user-modeling layer (new in v0.2)

**The current state:** Lists the strategic claim as "user states a goal in natural language and the product builds a personalized journey to that goal." Implementation foundations are listed as MAGE, the exercise framework's combinatorial nature, and team composition.

**Why it might want revisiting:** §3.7 above. The per-user accumulating user-model is the load-bearing capability that justifies the AI-company framing. Doc 09 §1 should name it as a vision pillar explicitly.

**Recommended action: revisit-in-Phase-2.** Add user-modeling layer as a fourth pillar in §1's "Why Now" or as a new sub-section "The User-Modeling Layer." Cross-reference §5.3 (persistence) and §10.5 (RAG architecture).

### 7.12 Doc 09 §10 (MAGE and the AI Layer) — analogy-vs-implementation discipline (new in v0.2)

**The current state:** Discusses MAGE's role and AI augmentation. Doesn't address the metaphor-vs-implementation distinction.

**Why it might want revisiting:** §3.9 above. The team is generating useful AI analogies (diagnostic agent, Steven MD file, large music model). Each analogy needs the metaphor-vs-implementation distinction made explicit.

**Recommended action: revisit-in-Phase-2.** Add a brief subsection (e.g., §10.7 or as a sidebar) noting that the team's AI analogies are useful for communication but should not be treated as architectural specifications. Cross-reference §3.6 / §3.9 of Doc 10.

---

## 8. Demo and Investor Implications

This section surfaces material that feeds into Phase 3 (team-facing pitch document) and Phase 4 (investor pitch deck).

### 8.1 The 6-step integrated demo flow (substantially rewritten in v0.2)

Steven's v0.2 redline reframed v0.1's Configuration A / Configuration B approach as a single cohesive flow that hits the major capabilities of the enhanced MuseFlow vision. The aspirational integrated demo:

| Step | Demo content | Demonstrates | Feasibility | Risk profile |
|------|--------------|--------------|-------------|--------------|
| 1 | AI conversation / diagnostic / goal planning | Agentic conversation, diagnostic-agent behavior, four authorship origins surface | High — chat UI + LLM call | Latency risk; goal-classification accuracy risk |
| 2 | AI-driven visual roadmap construction featuring nodes for all main content types | Project flow, content/path mode architecture, multimodal roadmap | Medium — vertical-tree UI component + LLM JSON output | Vertical-tree component needs to exist; LLM consistent JSON output is non-trivial |
| 3 | Zoomed-in demo on a sight-reading component | Sight-reading integration, parameter-generated content | High — substrate exists | Choose existing content; agent links to it |
| 4 | Zoomed-in demo on an AI-driven repertoire session | Agentic repertoire orchestration, perfect-practice tree algorithm in action, audio recognition, AI feedback layer | **Engineering-critical path** | Live performance demo cannot be faked; voice-LLM latency; audio recognition reliability |
| 5 | Zoomed-in demo on an exercise component | Exercise framework, generation-on-demand, AI-prescribed practice | Medium — exercise schema needs build-out + AI selection from matrix | Match what's discussed in §4.5 reverse-engineering methodology |
| 6 | Zoomed-out view of broader UI/UX with assorted Paths/Projects, dedicated content-pillar areas, aggregated metrics, suggested practice routines/plans | The integrated product surface, the user-modeling layer's outputs, the long-term cohesion | Medium — UI scaffolding work | Aggregated-metrics dashboard not yet built |

**Step 4 is the bottleneck.** It's the only step that can't be faked because the user is *playing* during it. Everything else can be partially scaffolded — links can be pre-built, screens can be rendered statically. Step 4 requires the substrate of audio recognition (Andrew's track), the auto-looping algorithm orchestrating repertoire controls (Patrick's PRD / Decision #42), and ideally text or voice feedback firing in response to performance data — all live. That makes step 4 the engineering-critical path for the integrated demo.

**A note on feasibility:** Steven's redline acknowledged "I'm not sure if all of that's feasible, but this ideal would probably encompass most of the key features of the newly enhanced version of MuseFlow we're targeting." That candor is right. The 6-step flow is the aspirational ideal. Realistic demo construction is incremental — steps 1–3 + 5–6 are achievable on a near-term timeline with light scaffolding; step 4 is the gating commitment.

**Recommended action for Phase 2:** Replace Doc 09 §15.2 with this 6-step integrated demo flow. Annotate feasibility per step. Identify step 4 as the engineering-critical path. Note the incremental construction path.

### 8.2 V1 vs. demo scope

The demo can be more polished than V1 for specific demo'd capabilities, while V1 is lighter on those same capabilities. This is normal and not a problem if the team is explicit about it.

Specifically:
- The exercise schema's full matrix is demo-buildable but doesn't need to be V1-ship-buildable (Steven's reverse-engineering approach lets the demo show what V1 should eventually populate)
- The auto-looping algorithm exists in Patrick's PRD already; for demo it needs UI; for V1 it needs documentation and ideally the broader control surface scaffolding
- The visual road map needs polish for demo; V1 may have a simpler list-style surface initially with the visual coming in V2

**Recommended action for Phase 3:** The pitch document should distinguish "demo-state" from "V1-ship-state" from "long-term-vision-state" clearly. Each has a different defense.

### 8.3 Unit economics

The team aligned on these principles:

1. **Token-based pricing is customer-familiar** in AI products and "basically expected" (Steven, line 1781).
2. **Average user covered by subscription, profitable per user** (Steven, lines 1730–1734).
3. **MAGE as a cost reducer** because it generates content algorithmically rather than via expensive LLM tokens (Patrick, line 1759).
4. **Heavy generation periods amortize** — heavy use during a roadmap-building month, then token-light use during execution (Steven, line 1770).
5. **Per-month curriculum-generation limits with token-purchase upsell** (Patrick, lines 1771–1773).
6. **No subsidizing usage with investor money long-term** — Patrick: "I would hate to have to get investments to be able to provide a service to our users who are paying for it, but not fully paying for it. We're like subsidizing it with like investor costs. That's I don't like that." (lines 1743–1749).

This is enough material for a "Cost Considerations" section in Doc 09. It's not pricing — it's a framework for thinking about pricing later.

**Recommended action for Phase 2:** Add a brief "Cost Considerations" section to Doc 09. Covers the 6 principles above. Explicit: pricing is still not designed (Decision #37 stands).

**Recommended action for Phase 4 (deck):** The unit-economics story is investor-ready in shape. The narrative is: "MAGE makes generation cheap; LLM tokens are the variable cost; heavy generation is front-loaded per-user; token upsells handle outliers." This is defensible.

### 8.4 Staley's R&D direction

End-of-call commitment: "I'm just going to start digging into like how to do LLM. Um, I've watched some I've watched some videos from AWS on using their like AWS bedrock stuff and that might be like the step one. Um, I've also heard stuff about that being expensive. Um, maybe there's a way we can make calls to some external API that's like I don't know" (lines 1827–1832).

This is the first explicit tooling exploration commitment from Staley per Decision #32. Direction: **AWS Bedrock first, external API alternatives if cost is prohibitive.**

**Connection to §3.7's AI-company-framing analysis:** Staley's direction here is firmly LLM-layer. The user-modeling-layer ownership question (§6 #13) sits adjacent to but distinct from Staley's R&D track. If the team wants both, both need explicit ownership.

**Recommended action for Phase 2:** Update Doc 09 §10.5 (LLM Choices) to reflect Staley's specific exploration direction. Add §10.6 alternative — external-API-call architecture (e.g., Claude API, OpenAI API) as a near-term fallback distinct from the deeper "build out MAGE algorithmically" alternative.

### 8.5 Team composition argument (and possible addition)

Doc 09 §15.4 captures Patrick's "two engineers + music educator + product" framing. The May 7 call doesn't change this. Confirms it.

**Possible addition for Phase 4:** Per §3.7, the user-modeling-layer story strengthens the team-composition argument. The team has the engineering depth to build LLM infrastructure (Staley) AND the pedagogical sophistication to define what the user-model should track (Steven, Andrew, Patrick). Few competing teams have this combination. Worth surfacing in pitch material.

### 8.6 What's still missing for the demo

Concrete items that need to exist for the integrated demo to ship (organized by step):

**Step 1 (chat / goal planning):**
- LLM with reliable goal-articulation classification (per §3.6, decide prompt-level vs application-level implementation)
- Chat UI in MuseFlow's surface

**Step 2 (visual roadmap):**
- Vertical-tree UI component (Phaser, React, or other)
- LLM that can output road-map JSON in a consistent schema
- ~10–30 user stories with corresponding road maps (Patrick is owner per the call)

**Step 3 (sight-reading zoom):**
- Existing sight-reading content, agent-linkable

**Step 4 (AI-driven repertoire — engineering-critical):**
- Voice-LLM latency under control (Staley: the technical hurdle)
- Repertoire perfect-practice toolset implemented to the point that AI can engage tools (loop, slow-down, accuracy heat-map — per Decision #46 surface)
- Auto-looping algorithm with UI integration (Decision #42)
- An LLM that can reliably emit JSON (problem-section locations) + script (text/spoken cues) per Staley's two-output framing (line 414)

**Step 5 (exercise zoom):**
- Exercise schema's full matrix populated enough that the AI has a universe to draw from (Track D output, with reverse-engineering input)
- AI capability to select variable combinations from the matrix
- MAGE generating content for the selected exercise

**Step 6 (zoomed-out UI):**
- Aggregated-metrics dashboard
- Paths/Projects listing surface
- Suggested practice routines / plans rendering

---

## 9. Recommended Decision Log Additions (revised in v0.2)

Drafted in canonical Decision Log format for Steven's approval. **Nothing is committed in this document.** Phase 2 is where these get appended (or dropped, or revised) per Steven's review.

### Proposed Decision #42 (revised in v0.2): The Auto-Looping / Perfect-Practice Tree Algorithm

**Source:** May 7, 2026 Emergent Curriculum brainstorm. Patrick described an algorithm he claims to have already designed in his PRD: read the green-note JSON history, identify the first section with two-or-three-notes-in-a-row errors, dynamically determine loop boundaries (one or two measures before/after the errored section), perfect that section, auto-progress to the next errored section, and combine perfected sections in a tree structure (small section → small section → combined → next pair → combined → larger combination, recursively). Staley's read: largely algorithmic, with the LLM as "voice/text sugar on top." Steven concurred but flagged that AI judgment may need to override the algorithm for "break the rules" cases (e.g., the actual issue is the previous measure, not the errored one).

**Decision made:** The auto-looping / perfect-practice tree algorithm is recognized as a **first-class algorithmic capability for repertoire practice**. Specifically:
- It is the algorithmic execution layer that connects performance data (green-note JSON history) to looping decisions in repertoire
- It is **one capability within the broader agent-controllable repertoire practice control surface** (see Decision #46) — not a standalone architectural primitive
- It is the load-bearing capability for the engineering-critical step 4 of the integrated investor demo (Phase 1 §8.1)
- It is invokable by the agentic system as part of Project execution (a Project's roadmap node for "practice this piece" can prescribe auto-looping as the practice mode)

**Removed from v0.1 framing (per v0.2 redline):** v0.1 claimed auto-looping subsumed Optimal Grip and parallels Game Mode in sight reading. Per Steven's redline, those connections are stretches:
- Optimal Grip is about session-level adaptive difficulty (chevron count, tempo targets), distinct from practice-section selection
- Game Mode is sight-reading-specific pass-condition mechanics, distinct from repertoire practice orchestration
- Auto-looping was speculated to extend to exercises in v0.1, but the algorithm operates on a piece's note-history JSON (a repertoire artifact) — exercises would have analogous mechanics, not the same algorithm ported

**Reasoning:** The algorithm exists. Patrick has implemented it (or specified it in detail) in his existing PRD. It is the strongest single demo capability the team has. Recognizing it explicitly in canon prevents it from sitting implicit in a PRD the rest of the team hasn't read, and it earns a canonical reference for downstream work.

**Phasing:** TBD. The algorithm itself is implementable now (per Patrick); the AI-judgment override and voice-feedback layer are speculative-near-term. V1 / demo / V2+ scoping is open.

**Cross-references:** Decision #46 (broader control surface). Patrick's PRD as the implementation source. Doc 09 §6 (AI Surface) — voice feedback as the language layer atop the algorithm.

### Proposed Decision #43: Performance Constraints Generalize Across Content Modes

**Source:** May 7, 2026 brainstorm. Steven's articulation (lines 824–842) that the exercise section's performance-constraint vocabulary (time-based pass conditions, accuracy thresholds, memory-chain length) ports directly to sight reading and possibly repertoire. Staley: "the exercise section can also maybe be a version of this game mode thing." Bible §6.3 currently treats performance constraints as exercise-internal.

**Decision made:** Performance constraints are promoted from exercise-section-internal to a **cross-content-mode primitive**. Any "completable" engagement with content (exercise atom session, sight-reading level attempt, repertoire practice session) carries performance constraints that determine pass conditions and shape the practice experience.

The schema impact:
- Exercise atoms already carry performance constraints (per Architecture Doc §5)
- Sight-reading levels gain a performance-constraints schema entry (parallel to atom configuration)
- Repertoire practice sessions may carry performance constraints (e.g., "play this passage at 80% accuracy or higher for 5 minutes to clear")

**Reasoning:** The exercise framework's most useful product-level concept (replayability through constraint variation) generalizes with no architectural cost. Treating performance constraints as a cross-mode primitive avoids reinventing similar mechanics per mode and provides the agentic system a unified vocabulary for prescribing practice intensity.

**Phasing:** TBD. Specific application to sight reading and repertoire is V2+. The conceptual promotion is V1; per-mode implementation phases independently.

**Cross-references:** Decision #22 (replayability), Bible §6.3, Architecture Doc §5, Decision #41 (the cross-mode pattern this extends), Decision #46 (performance constraints are part of the per-content-mode control surface).

### Proposed Decision #44: MAGE Long-Term Role — Augmentation Direction Confirmed

**Source:** May 7, 2026 brainstorm. Patrick: "the AI would probably be adjusting the mage output to make it more musical or to fit the like genre that they're trying to learn or to specifically work specific techniques that are in the piece of repertoire that they want to learn... There's like many reasons why the AI would adjust the music XML outputed by Mage" (lines 1795–1810). Steven concurred. Staley did not push back; his earlier articulations during the call ("I love mage. Yeah") and his agreement with Patrick's framing position him in alignment.

**Decision made:** Decision #39 (MAGE's long-term role logged as open) is **amended toward the augmentation framing**. The team's working position, with directional alignment across all three brainstorm participants, is:
- MAGE persists as a permanent algorithmic generation engine
- The AI's role is to adjust MAGE's output for musicality, stylistic fitness, and goal-specific shaping
- The training-data-then-replacement framing (Staley's earlier articulation) is no longer the team's working framing

**Reasoning:** Patrick's articulation provides the concrete mechanism (AI adjusts music XML output by MAGE) that the augmentation framing previously lacked. Steven's concurrence and Staley's non-pushback constitute directional alignment.

**Caveats / what remains open:**
- Staley has not explicitly retired the training-data-then-replacement framing. The amendment records the convergence; full closure of the question awaits Staley's explicit confirmation.
- Cost implications of the augmentation framing differ from the replacement framing (per Doc 09 §10.4): MAGE+AI is a hybrid stack, not a single LLM. This is a feature, not a bug, but architectural commitment must reflect it.

**Phasing:** N/A — architectural framing, not a feature.

**Cross-references:** Decision #39 (amended, not superseded). Doc 09 §10.3, §10.4.

### Proposed Decision #45 (revised in v0.2): User-Generated Sight-Reading Mode Resolved as User-Generated Within Sight Reading Content Mode

**Source:** May 7, 2026 brainstorm. Lines 580–870. Steven articulates user-constructed sight-reading levels with custom parameters as falling cleanly within the Sight Reading content mode's user-generated authorship origin. Staley and Patrick aligned during the call.

**Decision made:** User-generated sight-reading mode (custom-parameterized levels with explicit musical parameters, performance constraints, and completion settings) is **resolved as user-generated content within the Sight Reading content mode**. Specifically:
- The user invokes Sight Reading's Generate flow
- Configures parameters (notes, rhythms, time signature, complexity metrics, performance constraints, completion criteria)
- The system constructs the level
- The level is stored with `authoring_origin = user`
- The level may carry "no completion criteria, just play endlessly" as one of the configurable options

**Crucial scope clarification (v0.2 redline):** This decision does **not** resolve "Free Play" in the original A1 sense. Free Play (original) refers to user improvisation without notation guidance — open-ended musical exploration. That capability remains deferred per Decision #40, status unchanged. v0.1's Decision #45 conflated these two things; v0.2 narrows.

**Reasoning:** The May 7 articulation closes the long-standing ambiguity for the specific capability of user-parameterizable sight-reading. The user-generated authorship origin (Decision #41) provides the primitive. No new content mode is required for this specific capability. Free Play original sense remains a separate question with its own deferral status.

**Phasing:** N/A — architectural framing. Specific UI labels and Generate-flow UX are V1+ design questions.

**Cross-references:** Decision #40 (Free Play original sense remains deferred — no change). Decision #41 (user-generated authorship origin). Bible §2.1.1 (status update for sight-reading-mode clarity, NOT Free Play status).

### Proposed Decision #46 (new in v0.2): Agent-Controllable Repertoire Practice Control Surface

**Source:** May 7, 2026 brainstorm + Steven's v0.2 redline. The agentic system's repertoire-practice job is orchestrating decisions across a defined set of practice tools, of which auto-looping (Decision #42) is one specific algorithmic pattern. Steven's enumeration of the surface in the redline.

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

### A note on what I considered but didn't propose

I considered but **did not draft** Decision proposals for the following, on the rationale that they're not yet decision-class:

- **Voice/audio LLM feedback (§4.2)** — extension of the AI surface, not a new architectural primitive. Should be added to Doc 09 §6.
- **Reverse-engineering catalog methodology (§4.5)** — methodological proposal for Track D, not an architectural commitment. Should be documented in Track D scoping.
- **Vertical Mario roadmap UX (§4.6)** — UX direction, not committed UX. Should sharpen Doc 09 §7.2.
- **AI-generated tutorials as roadmap nodes (§4.3)** — deferred future direction; architectural placement open. Should be added to Doc 09 §5.2 candidate-node-types list and §13 open questions.
- **Demo scope (§5.5, §8.1)** — operational, not architectural. Should update Doc 09 §15.2.
- **Cost framework (§8.3)** — not pricing, not architectural. Should add a "Cost Considerations" section to Doc 09 in Phase 2.
- **User-modeling layer as vision pillar (§3.7)** — could be Decision-class, but its content is more a *recognition* of an architectural commitment already implicit in canon than a new commitment. Recommended as Doc 09 §1 vision-pillar update rather than numbered Decision. Steven may prefer to elevate it; if so, a Decision #47 is straightforward to draft.
- **AI-analogy implementation discipline (§3.9)** — documentation discipline, not architectural commitment. Should land in Doc 09 §10 and possibly project-instructions.md.

These can become Decisions later if Steven prefers, but I think they're better captured as inline canon updates in Phase 2 rather than as numbered Decisions.

---

## 10. Cross-Track Implications

How this work affects the other Tracks running in parallel.

### Track A2: Patrick's "Theory Library & Exercise Section" Doc Evaluation

A2 is paused for this work and resumes after Phase 1 lands. The May 7 call has implications for A2:

- **Patrick's "PRD you guys haven't read" reference (line 433)** likely refers to the same doc A2 is evaluating. The auto-looping algorithm (§4.1) is "already part of the PRD." When A2 resumes, this should be one of the things to verify against the PRD's actual contents.
- **Theory as a content mode (Bible §2.1.1 candidate, status TBD)** is a primary A2 question. The May 7 call doesn't directly address Theory's status, but Patrick's "music theory" addition to the cross-modal road map (line 1548) suggests the team is treating it as a content surface in working framing — A2 should resolve its mode-status formally. Connected to §6 #15 (broader content-classes question).
- **The auto-looping algorithm**, if already in Patrick's PRD, may have substantial supporting material there worth integrating with the Decision #42 / #46 canon update.
- **The 5 demo-relevant goal categories (§5.4)** likely have analogues in Patrick's PRD. Worth cross-checking.
- **Interactive Tutorial placement (§4.3, §6 #16)** — A2's evaluation of Patrick's doc may inform how Interactive Tutorials fit into the broader content-class question.

**Recommended:** When A2 resumes, sequence its work after Phase 2 lands so A2 evaluates Patrick's doc against the integrated canon.

### Track B: Open-Question Triage

The May 7 call:
- **Resolved or directionally settled** several previously-open questions (user-generated sight-reading mode per #45-revised, MAGE direction per #44, performance constraints generalization per #43, demo scope sharpening). Track B's current open-question inventory shrinks by these items.
- **Surfaced new open questions** (the 19 items in §6 above — 10 from v0.1, 9 added in v0.2). Track B's inventory grows by these items. Notably, several v0.2 questions are foundational architectural questions (#13 AI-company-framing, #14 analogy implementation, #15 content classes beyond core three).

**Net effect on Track B:** Modest growth in open-question count, but with substantially different shape — older questions resolve, newer ones replace them. Several new questions are higher-priority than typical (#13, #15 are arguably blocker-class for Phase 4 pitch deck work).

**Recommended:** Track B should sequence after Phase 2's canon updates land. The triage will be cleaner against an updated open-question inventory. Phase 4 timing may compress Track B's runway; the AI-company-framing question in particular wants resolution before pitch material drafts.

### Track C: Taxonomy Reconciliation

Doc 03 (Exercise Taxonomy) is the target for C. The May 7 call has limited direct impact on C — the discussion stayed at the agentic-system / cross-mode level. Three indirect effects:

- **Performance constraints' cross-mode promotion (proposed Decision #43)** may sharpen what Doc 03 includes — taxonomy is exercise-section-internal, so the cross-mode framing affects Doc 03's scope clarification.
- **Reverse-engineering methodology (§4.5)** is methodologically adjacent to taxonomy work — both are "what's the universe of possibilities" exercises. C might want to coordinate with D's reverse-engineering input to avoid duplicate work.
- **Exercise control surface (Decision #46 implication)** — when the exercise control surface is enumerated in Phase 2, that enumeration may surface taxonomy items not yet in Doc 03.

**Recommended:** Track C is largely unaffected. Continue when Phase 2 lands; minor scope-sharpening expected.

### Track D: V1 Atom Catalog Authoring

The largest cross-track impact. Three changes:

- **Methodology change.** Track D's implicit methodology is bottom-up enumeration. The May 7 call commits the team to running the top-down "feed the AI the universe; see what road maps it builds" methodology in parallel (Staley/Patrick agreed plan, lines 1402–1450). Track D should explicitly absorb both methodologies and document their merge process.
- **Demo-driven prioritization.** The 5 user-story categories give Track D a near-term prioritization signal. The atoms that show up across multiple user stories (e.g., Alberti bass exercises, ABRSM-curriculum atoms) should be authored first.
- **Exercise control surface.** Per Decision #46, the exercise control surface enumeration informs what V1 atoms must support — completion thresholds, training methods, performance constraints — and constrains which combinations are valid.

**Recommended:** Track D's scoping document should incorporate the reverse-engineering methodology and the user-story-driven prioritization before atom authoring begins. Phase 2 should produce a brief Track D scoping note alongside the canon updates.

### Track E: PRD Authoring

The macro PRD that informs Patrick's MVP decomposition. The May 7 call has substantial implications:

- **Demo scope (§5.5, §8.1)** is a load-bearing input — the PRD should distinguish demo-state from V1-ship-state.
- **Cost framework (§8.3)** is PRD-relevant but only as principles, not as committed pricing.
- **Auto-looping algorithm (§4.1, Decision #42)** is PRD-class material now that it's recognized as architectural.
- **Repertoire control surface (§4.7, Decision #46)** is PRD-class material — the PRD will need to enumerate which surface elements ship in V1 vs later.
- **Voice/audio LLM feedback (§4.2)** is PRD-class material as a V2+ capability for both repertoire and exercises.
- **Performance constraints generalization (§4.4, Decision #43)** affects the PRD's section on cross-mode primitives.
- **User-modeling layer (§3.7)** — if elevated to vision pillar, the PRD's framing should reflect it.

**Recommended:** Track E should kick off after Phase 2 (canon updates) and Phase 3 (team-facing pitch document) land, since those provide the substrate. The PRD's authoring will be substantially easier with both inputs.

---

## 11. Recommended Phase 2 Scope (revised in v0.2)

Phase 2 is the canon-evolution pass that updates affected documents based on this Phase 1 analysis. Recommended scope, with approximate effort estimates:

### 11.1 Documents to update

**Doc 09 — Agentic MuseFlow Vision (largest update).** Changes:
- **§1 (Vision)** — add user-modeling layer as an explicit vision pillar (per §3.7). Cross-reference §5.3 and §10.5. (medium)
- **§4.2 (Types of Goals)** — add the 5 May-7 demo-relevant categories as concrete examples within existing types. (small)
- **§4.3 (Goal Articulation)** — add "diagnostic agent" / "auto-engaged plan mode" framing as behavioral spec, with explicit note that prompt-level vs application-level implementation is open. (small)
- **§5.2 (Roadmap Node Types)** — add Tutorial-node and Video-node candidates, marked deferred / placement-open. Sharpen auto-looping-as-practice-mode framing for repertoire nodes. (small)
- **§6 (The AI Surface)** — add voice/audio as a distinct surface modality with text-first phasing. Reframe parallel-track for repertoire AND exercises. Add cross-reference to new Agent Control Surfaces section. (medium)
- **NEW SECTION (§6 sibling, e.g., §6A) — Agent Control Surfaces per Content Mode** — enumerate the repertoire surface (per Decision #46), sketch exercise and sight-reading surfaces. (medium)
- **§7.2 (Per-Project Zoom)** — narrow the visualization candidates toward "vertical tree with branching" per the Fez-inspired direction. (small)
- **§10.3 (Augmentation Question)** — amend per proposed Decision #44; record directional convergence while retaining open caveats. (small)
- **§10.5 (LLM Choices)** — add Staley's specific exploration direction (AWS Bedrock first, external API alternatives). (small)
- **§10.7 (new) — Metaphor vs Implementation** — brief subsection on AI analogies as user-facing/team-facing communication tools, not architectural specifications. Cross-reference §3.6 / §3.9 of Doc 10. (small)
- **§12.2 (AI-averse design constraints)** — acknowledge Projects-first onboarding as one of several paths. (small)
- **§13 (Open Architectural Questions)** — close items that resolved (user-generated sight-reading per #45-revised, partial MAGE direction); add new questions from §6 of this document. Add new sub-cluster on "content classes beyond the core three" (§6 #15). (medium)
- **§15.2 (Demo Flow)** — substantial rewrite. Replace canonical-demo-only framing with the 6-step integrated flow per §8.1. Identify step 4 as engineering-critical. Document incremental construction path. (medium)
- **§17 (new) — Cost Considerations.** Add new section capturing the 6 cost principles from §8.3 of this document. (medium)
- Various references to proposed Decisions #42–#46 throughout. (small)

Estimated effort: 2 sessions.

**Doc 01 — Project Bible.** Changes:
- **§2.1.1** — clarify that user-generated sight-reading mode (per Decision #45-revised) and Free Play original sense (deferred per Decision #40, unchanged) are distinct. Don't delete Free Play from candidates list. (small)
- **§2 or new §** — performance constraints as cross-cutting primitive per Decision #43. (small)
- **§6.3 (Replayability Through Constraint Variation)** — generalize per Decision #43, or move framing to higher-level §2 / new §. (small)

Estimated effort: <1 session.

**Doc 02 — System Architecture.** Changes:
- **§5 (or new section)** — performance constraints as cross-mode primitive per proposed Decision #43. (small–medium)
- Atom schema unaffected unless Decision #43 implies field changes (probably not in V1 scope).

Estimated effort: <1 session.

**Doc 05 — Design Decisions Log.** Changes:
- Append proposed Decisions #42 (revised), #43, #44, #45 (revised), #46 (with Steven's revisions). (medium)
- Amend Decision #39 (per #44). (small)
- Note on Decision #40 (Free Play unchanged status — clarify scope). (small)

Estimated effort: 1 session, mostly writing.

**Doc 07 — UX Navigation Spec.** Changes:
- **§8.6 Q5 (MAGE long-term role)** — update per #44. (small)
- **§9** — add new open questions per §6 of this document; close resolved questions. (small)

Estimated effort: <1 session.

**Doc 04 — Glossary.** Changes:
- Add: auto-looping algorithm / perfect-practice tree (per #42); cross-mode performance constraints (per #43); diagnostic agent / auto-engaged plan mode; per-user user-modeling layer (the architecture, not the metaphor); agent control surface (per #46). (small)
- **NEW (per v0.2 redline):** Add **Interactive Tutorial** entry — definition of MuseFlow's existing canonical content class (animated video + live-action hand clips + Phaser-JS exercises gated mid-flow). Should already be in glossary. (small)

Estimated effort: <1 session.

### 11.2 Documents NOT to update in Phase 2

- **Doc 00 (Handoff Brief)** — historical, frozen.
- **Doc 03 (Exercise Taxonomy)** — Track C's responsibility, not Phase 2's.
- **Doc 06 (Exercise Blueprints)** — no direct updates needed.
- **Doc 08 (Standup Synthesis Apr 28–May 5)** — historical, frozen.

### 11.3 Phase 2 cadence recommendation

Phase 2's edits are mostly mechanical once the interpretive calls land (which is the purpose of this Phase 1 document). Suggested approach:

1. **First Phase 2 session:** Steven approves / revises the proposed Decisions #42–#46 and Decision #39 amendment. Phase 2 produces the updated Doc 05 with finalized Decisions, plus the simplest mechanical updates (Bible §2.1.1, UX Spec §8.6 Q5, Glossary additions including Interactive Tutorial).
2. **Second Phase 2 session:** Doc 09 substantial updates (§1 user-modeling-layer pillar, §5.2, §6, new Agent Control Surfaces section, §7.2, §10.3, §10.5, new §10.7 metaphor-vs-implementation, §12.2, §13, §15.2, new §17). This is the bulk of the work.
3. **Third Phase 2 session (optional):** Doc 02 cross-mode performance constraints, any cleanup, final cross-reference pass.

Steven decides cadence and authority granularity (phase-gated, file-gated, or sequential). Suggest starting with file-gated for Doc 09 since its changes are the most interpretive.

### 11.4 What Phase 2 does NOT do

Phase 2 is canon evolution. It does not:
- Produce the team-facing pitch document (Phase 3)
- Produce slide content for investor conversations (Phase 4)
- Resolve the new open questions surfaced in §6 (those go to Track B)
- Update Patrick's PRD or Track A2's scope (A2 resumes after Phase 2)
- Author new atoms in the V1 catalog (Track D)
- Build the demo (engineering work)
- Resolve the user-modeling-layer ownership question (§6 #13) — that's a team-organization question, not a documentation question

Each of those is a separate downstream piece. Phase 2's sole goal is to land the canon at a state where Phase 3 has clean substrate to draw from.

---

## 12. Document Status

**Version 0.2 (May 8, 2026)** — Second draft, integrating Steven's first redline. Substantive changes documented in the v0.2 changelog at the top. Produced from the May 7, 2026 transcript and the canon as of commit prior to this document.

**Outstanding for Phase 1 closeout:**

- Steven redlines this v0.2 document (further iterations expected)
- Steven approves / revises proposed Decisions #42 (revised), #43, #44, #45 (revised), #46
- Steven approves Phase 2 scope (§11)
- Steven decides whether the user-modeling-layer item warrants Decision #47 status or stays as Doc 09 §1 update

**After approval, this document becomes:** the canonical record of what the May 7 call produced and how it integrates with prior canon. It is canon-class — analogous to Doc 08 (Standup Synthesis Apr 28–May 5) — and persists as reference material in `docs/10-may7-brainstorm-synthesis.md` after Steven commits.

---

*End of May 7, 2026 Brainstorm Synthesis (Doc 10), Version 0.2.*
