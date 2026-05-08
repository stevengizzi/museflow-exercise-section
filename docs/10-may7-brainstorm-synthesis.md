# MuseFlow May 7, 2026 Brainstorm Synthesis: Emergent Curriculum Integration

> **Status: Phase 1 analysis (working draft).** Synthesized from the May 7, 2026 Emergent Curriculum brainstorm transcript (`docs/meeting-transcripts/2026-05-07-museflow-agentic-vision-call.md`, 1857 lines, ~100-minute call). This document is the foundation for Phase 2 canon evolution and Phase 3 team-facing materials. Recommendations are drafted for Steven's review and approval — nothing committed in this document is canon until Phase 2 lands the corresponding edits.
>
> **Participants:** Steven Gizzi, Steven Staley (CTO), Patrick Boylan (co-founder).
>
> **Audience:** Steven (primary reviewer), future Claude conversations seeded with the integrated canon, MuseFlow team via downstream Phase 3 pitch document.

---

## 1. Context

The May 7 call was scheduled at the May 5 standup as a dedicated working session on the Emergent Curriculum — the agentic system framing that had crystallized in late April / early May. Patrick framed the meeting opening as: "this is mainly just to facilitate a conversation about this sort of like emergent curriculum, you know, uh and and like and how to how to set up the like the the structure of it so that things can combine properly" (lines 47–48).

The call came after the A1 doc-sync conversation produced the canon's current architectural framing (content modes / path modes / four authorship origins / three flows — Decision #41) but before the rest of the team had been walked through that framing. So the meeting served two roles simultaneously:

1. **Steven's first verbal articulation** of the A1 architecture to Staley and Patrick
2. **A genuine brainstorm** that surfaced new capabilities, narrowed open questions, and converged on demo scope

Steven's read on the call (from the kickoff): foundational enough that this integration work is being prioritized over Track A2 (Patrick's design doc evaluation), which was already in progress in a separate conversation.

The transcript is informal — timestamps, profanity, ~15 minutes of off-topic content (Staley's car project, debugging links to a 3D-piano-hands product, scheduling). The signal is dense in roughly the first hour and the final 25 minutes, with a long lower-density middle section. This document filters for signal.

---

## 2. Headline Summary

The ten things that matter most:

1. **The auto-looping / perfect-practice tree algorithm is real and detailed.** Patrick walked through a specific algorithm he claims to have already designed: read the green-note JSON history, find the first 2–3 errored notes in a row, center a loop around it, dynamically determine boundaries (one or two measures before/after), perfect that section, auto-progress, then combine sections in a tree. This is not currently in any canon document and reads as **Decision-class architectural primitive** material. Lines 433–485.

2. **The MAGE-augmentation framing reached directional alignment.** Patrick explicitly: "the AI would probably be adjusting the mage output to make it more musical or to fit the like genre that they're trying to learn" (lines 1795–1800). Steven concurred, Staley did not push back. This is closer to Steven's working position (Decision #39) than to the earlier "training-data scaffolding-then-replacement" framing. The question isn't fully resolved but **Decision #39 should be amended to reflect the team's current convergence.**

3. **Free play has a clean home in the existing architecture.** Steven articulated free play as "user-generated" content within content modes (sight reading particularly): "this falls under user-generated because you as the user go into this this sandbox thing where you're like I want this this this and this and by the way I want it to be no we're not tracking accuracy we're just playing endlessly" (lines 813–821). This **resolves the "free play deferred indefinitely" status in Bible §2.1.1 and Decision #40** — free play isn't a separate mode, it's a usage pattern within user-generated content.

4. **Investor demo scope crystallized around two artifacts.** Steven and Staley converged on (a) a **chat → vertical Mario-style road map** demo (potentially partially faked) and (b) a **build-out of the exercise schema's full matrix** with AI choosing variable combinations and MAGE generating the content. Staley raised reverse-engineering ("feed the AI the universe of possibilities, see what road maps it builds, then build what it keeps wanting"). Lines 1190–1450.

5. **Performance constraints generalize across content modes.** Steven explicitly carried the exercise section's performance-constraint concept (time-based, accuracy-based, memory-based pass conditions) into sight reading: "this exercise lasts for five minutes... if you get through all five minutes where your accuracy did not once drop below X percentage, that's a pass" (lines 828–830). Staley: "the exercise section can also maybe be a version of this game mode thing" (line 842). Currently performance constraints are exercise-internal in canon. **They should be promoted to a cross-content-mode primitive.**

6. **Voice / audio LLM feedback became a near-term ambition.** The team discussed real-time voice cues during practice (interruptive: "slow down, slow down"), ding-plus-prompt style notifications, and end-of-round feedback ("here's some things I noticed; here's what I'd recommend... I'm setting up the loop for you right now"). Repertoire identified as the natural first battleground. Steven OK starting with text. Not in any current canon document as a distinct capability. Lines 274–420.

7. **The four authorship origins / three-flow architecture survived first contact with the team.** Steven walked Staley and Patrick through the A1 framing using the word "isomorphism" repeatedly. Staley's reaction to the marketplace/community piece was "That's a crazy idea" (line 869) — clear validation. Patrick echoed the framing back ("we've thought of this as projects already," line 116). **No structural objections raised; team is aligned with Decision #41 as written.**

8. **AI memory / context system articulated more concretely.** Steven described a per-user "Steven MD file" / "Patrick MD file" growing over time, with the AI building token-efficient memory and retrieving key facts on demand (lines 494–525). This is more concrete than Doc 09 §10.5's mention of "RAG layer over user historical play data" — it gives the user-facing framing a name.

9. **Staley committed to an LLM R&D direction.** End-of-call: "I'm just going to start digging into like how to do LLM... I've watched some I've watched some videos from AWS on using their like AWS bedrock stuff and that might be like the step one. Um, I've also heard stuff about that being expensive. Um, maybe there's a way we can make calls to some external API" (lines 1828–1832). First explicit tooling commitment per Decision #32. Cost is the central concern.

10. **Cost/unit-economics thinking advanced but stayed deferred.** The team aligned on token-based pricing as the customer-familiar model, per-month curriculum-generation limits with token-purchase upsell, and lifetime-value framing where heavy generation periods amortize across longer engagement. Pricing remains unspecified per Decision #37 — but **the framing now exists in enough detail that Doc 09 should have a "cost considerations" section** capturing it.

---

## 3. Architectural Validations

These are places where the May 7 discussion confirms or strengthens the architecture currently in canon. Validation increases confidence in those decisions and reduces risk of relitigation.

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

**Implication for canon:** Doc 09 §5.2 already captures this. The "video library" addition (lines 698–714) is a new node-type candidate — flagged in §6 below.

### 3.3 Roadmaps decoupled from sight-reading curriculum (Decision #29, Bible §2.2, Doc 09 §3.1)

Staley directly asks: "this site reading feature is separate from the road map as we have it today" (lines 680–683). Steven: "Curric any kind of road map you could call it curriculum or whatever any kind of road map is multimodal and can pull content from any section" (lines 694–696).

This is canon already, but it's worth logging that Staley independently arrived at the same framing.

### 3.4 User-as-author parity with AI (Decision #34, §3.4 of Doc 09)

Steven: "Anything the AI can do, the user also has the option to build if they want. That's that's how I think it should work. Like it is a sandbox for the user if you want and if you know what you're doing enough to do that or the AI can do it for you" (lines 851–855). Validates the user-as-first-class-author principle.

### 3.5 The teacher / signature-artist / institutional marketplace (Decision #35, Doc 09 §15.3)

Steven articulating mid-call: "you're a teacher. you make road maps and like this is the road map for fall 2026 semester for my freshman students... or you're a signature artist, you know, and you like made a course and you're selling the course" (lines 886–900).

Already in canon as future direction. The May 7 call shows the team treating it as concretely envisioned, not abstract — Patrick's "you can publish your own your own exercises... I want to make this available to everybody else" (lines 878–884) is the same shape.

**Implication for Phase 3 pitch document:** The marketplace direction is concrete enough in the team's heads that it can be presented as committed direction (with phasing TBD), not as speculation.

### 3.6 The conversational surface as goal-articulator (Doc 09 §4.3, §6.1)

Patrick: "I think it needs to inherently ask the user like a f*** ton of questions to to like, hey, like I you you say you want to learn this, but like I need to know a little bit more about your intent, your goals, where you're at as a musician right now" (lines 561–565).

Steven articulates this as a "diagnostic agent" or "auto-engaged plan mode" — riffing on the analogy with Claude Code's auto-engagement of plan mode when a goal is detected (lines 1503–1518). Patrick agrees: "automatically engage that just base level until it has all the information it needs to be able to create that proper curriculum" (lines 1517–1525).

**Implication for canon:** Doc 09 §4.3 (Goal Articulation) and §6.2 (Levels of Agency) can be sharpened with "diagnostic agent" / "auto-engaged plan mode" framing. Specific recommended addition in §11.

### 3.7 Persistent and reusable AI-generated content (Doc 09 §5.3)

The "Steven MD file" / "Patrick MD file" framing (lines 494–525) — per-user accumulating context — is a more concrete articulation of the same persistence-and-reuse property already in Doc 09 §5.3. It isn't different; it's vivid.

### 3.8 The atom schema's agent-prescribability fields (Decision #40, Doc 09 §3.4)

Not directly discussed at the field level, but Staley's "I am kind of thinking that I guess I'm I'm actually leaning back toward... if we did want to say like like feed the the AI like the universe of possibilities that would maybe be like a better mo model" (lines 1366–1378) presupposes that the universe of possibilities (the exercise matrix) is queryable by the agent. This is what Decision #40's `prerequisite_atoms` and `generation_mode` fields enable.

The reverse-engineering methodology (Staley's framing) only works if the schema is rich enough for an LLM to reason over — which is what A1 spent considerable effort on. Validation by use.

---

## 4. New Capabilities Introduced

These are concepts discussed in the transcript that are not currently in any canon document and are substantive enough to need their own treatment in Phase 2.

### 4.1 The Auto-Looping / Perfect-Practice Tree Algorithm

**The most substantively new content in the transcript.** Patrick walked the team through a specific algorithm (lines 433–485):

> Patrick: the note history is is a is a definitely a part of it... is stored as a JSON and it's and uh and and it basically says all the notes that you've gotten green so far and where the loop would start where the loop would start is your first section where you have like two or three notes in a row that are incorrect. And that's where the automated looping you just turn on looping.

Staley pushed: would it dynamically determine boundaries based on the error location, even in mid-piece?

> Patrick: we wouldn't we would center on the errored section and then because because you don't want to start with the errors. You want to you want to center on it and you want to get into it and then leave it. And then what it would do is auto progress you to the next f***** up section. And then what we would do is, and if there are green notes in between it, so be it. We would just loop that second section, then perfect it, and then we'd combine both of those sections, including all the green notes, into one big loop. Then... it's like a tree. It's it's I figured out the math of it all, and it and it works.

Patrick clarifies the tree shape: "smaller section, smaller section, those get combined. Then you move on, smaller section, smaller section, and those get combined. Then those get combined. Then you move on to the next ones" (lines 460–469).

Staley's read: "this is potentially all just algorithmic" — not LLM-required. The LLM's role becomes "voice/text sugar on top" — providing voice or text feedback during the algorithmic process (lines 480–484).

Steven concurred but added the AI-judgment dimension: "It is algorithmic, but it's also the the worry I've always had... binary tree structures... things tend to be more complex than that... you need that little bit of extra intelligence as the guider the teacher to be like okay but we're going to like break the rules here for like reasons X Y and Z. And this is where like again the AI comes in really handy" (lines 485–494).

**Assessment of completeness:** The algorithm is described in enough detail to be implementation-spec-ready, with one caveat. Patrick claims it works ("I figured out the math of it all and it works... I wrote it in the perfect practice"). That suggests it's already implemented somewhere in the codebase, though not in a way the rest of the team has seen end-to-end. Worth confirming with Patrick what artifact exists.

**Where it belongs in canon:**
- **Doc 09 (agentic vision)** — as a node-type candidate for the agentic system to invoke during Project execution; as a load-bearing demo capability (§15.5)
- **Repertoire-section canon** — this is fundamentally a repertoire feature (operates on repertoire green-note history); we don't have repertoire canon docs yet, but if/when that work begins, this is foundational
- **Possibly the exercise section** — Steven's "I've been thinking about for exercises" suggests overlap, but the algorithm as described is repertoire-specific (operates on a piece's note history). For exercises, the analogous mechanic might be different.

**Recommended action:** Decision-class material. See proposed Decision #42 in §9.

**Demo implication:** A live repertoire demo — user plays a piece, AI identifies problem sections, sets up loops, walks user through perfect-practice tree, with text or voice feedback — is the **strongest single demo capability** the team has. Steven's later proposal for a repertoire-based demo (line 1274) implicitly assumes this works.

### 4.2 Voice / Audio LLM Feedback During Practice

The discussion (lines 274–420) covers four distinct voice-feedback patterns:

1. **Real-time interruptive cues** — short instructions while playing ("slow down," "louder," "breathe breathe breathe"). Lines 280–286.
2. **Ding + spoken prompt** — Patrick's proposal: notification chime followed by spoken cue tied to existing notification messages (auto-tempo, flexible metronome). Lines 304–340.
3. **End-of-round feedback with action proposal** — between attempts: "here's some things I noticed; here's what I'd recommend; I'm setting up the loop for you right now." Lines 376–402.
4. **Conversational dialogue (Socratic)** — Steven: "you can just ask every stupid ass question you want and it will like keep talking to you until you actually get it" — a tutor persona for understanding theory and concepts. Lines 260–272.

Staley's framing (line 408): the technical hurdle is "literally just figuring out how to get the voice LLM thing going. Um like they have it flawed and whatever." After that, "the hard part is the automatic looping" — which is the algorithm above, already partially built.

Steven OK starting with text: "I'm okay starting with text, especially like I understand the the tricky part about that if it's trying to tell you things literally while you're playing, but if we're talking about these these this feedback in between plays, like I'm okay starting with text" (lines 417–421).

**Repertoire is the first battleground** (Steven, line 427): "repertoire seems like a good first battleground for this." The auto-looping algorithm provides the structured action layer; the LLM provides the language layer.

**Assessment of completeness:** The capability is well-defined enough to enter canon. Specific UX details (text vs. voice, when each fires, how the user toggles) are open.

**Where it belongs in canon:**
- **Doc 09** — currently §6 (The AI Surface) lists conversational surface functions; voice/audio feedback should be added as a function, with phasing TBD and the staged-text-first approach noted

**Recommended action:** Add to Doc 09 §6 in Phase 2. Probably not Decision-class on its own — it's an extension of the AI surface, not a new architectural primitive.

### 4.3 AI-Generated Interactive Tutorials

Discussion lines 142–280 and 905–950. The team explored generating MuseFlow's existing-style interactive tutorials (Phaser-based, with human-hand video overlays) via AI. Components:

- **Script generation** — fine-tuned model on MuseFlow's existing tutorial scripts. Considered tractable.
- **Text-to-speech** — considered solved.
- **Visual / video generation** — the hard part. Specifically the human-hand overlay (Steven's hands in the corner of the screen). Discussion of 3D piano-hands software (Concert Creator AI by Massive Technologies, shut down 2022) as a model.
- **Phaser-only generation** — Staley's idea: skip the human hands and generate everything as Phaser components.

Team consensus: hard, expensive, deferred. Patrick: "let's wait until we've got some money to spare and throw money at this" (lines 932–933). But Staley: tutorial-as-roadmap-node-type would fit the architecture — "those would actually fit very well into these custom generated paths or road maps or like plans, but like as single nodes that are just like, okay, here's like a concept that this person needs to know" (lines 916–924).

**Where it belongs in canon:**
- **Doc 09 §5.2 (Roadmap Node Types)** — "Tutorial node" should be added as a candidate node type, marked Speculative and deferred
- **Doc 09 §16.2 (What Comes Next)** — this is the "expensive long-term ambition" — worth flagging there

**Recommended action:** Add as candidate node type in Doc 09 §5.2, marked deferred. Not Decision-class — it's a deferred future direction.

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

**Recommended action:** Not Decision-class on its own (it's a methodology, not an architectural commitment). But Phase 2 should add a brief note in Doc 09 §15 and / or in a Track D scoping document.

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

### 4.7 Auto-Looping for Repertoire as Distinct from Game Mode and Looping

The auto-looping algorithm (§4.1) is related to but distinct from existing concepts in canon:

- **Looping** (in development per Decision #20-area items) — manual user-set loops with start/end points
- **Game Mode** — the chevron-based progression in sight reading
- **Optimal Grip™** (deferred per Decision #20) — adaptive difficulty adjustment

The auto-looping algorithm is the **algorithmic execution layer that connects performance data to looping decisions** — it's what an AI tutor would do automatically with the perfect-practice toolset. Steven explicitly: "what specific tools from the set of perfect practice tools for repertoire" the AI would engage (line 392).

**Recommended action:** When the auto-looping algorithm is added to canon (Phase 2 / Decision #42), explicitly cross-reference its relationship to Looping (its execution substrate), Game Mode (parallel concept in sight reading), and Optimal Grip (which it partly supersedes — adaptive looping based on errors *is* one form of optimal-grip difficulty adjustment).

---

## 5. Resolutions of Previously-Open Questions

Items where the May 7 call directionally settled or fully resolved questions previously tracked as open in `09-agentic-museflow-vision.md` §13, `07-ux-navigation-spec.md` §9, or open Decision Log items.

### 5.1 Free Play status (Bible §2.1.1, Decision #40, UX Spec §9 Q19)

**Status before:** Free Play was listed as a "Candidate future content mode" in Bible §2.1.1 with status "deferred indefinitely" per Decision #40 (which dropped Free Play from A1 scope as a separate concept).

**What was discussed:** Lines 580–870. Staley initially framed sight-reading-with-AI as "free play, not the road map" (line 583). Patrick proposed co-opting the term. Steven articulated free play as falling under user-generated content within the existing architecture (lines 813–821):

> Steven: I I I think this falls under user-generated because you as the user go into this this sandbox thing where you're like I want this this this and this and by the way I want it to be no we're not tracking accuracy we're just playing endlessly you know or whatever and like and then you do it.

Staley's reaction: "I don't mind calling it free play and having free play have like a game mode" (line 801). Patrick: "or we just don't even need to call it any mode or like a section really" (line 808).

**What's now settled:** Free play is a usage pattern (user-generated content with custom accuracy/scoring/completion settings) within content modes — not a separate mode. The user constructs sight-reading levels (or other content) with whatever parameters they want, including "no completion criteria, just play endlessly."

**What remains open:** Whether the term "Free Play" persists at the UI level (e.g., as a labeled affordance for "user-generated content with no completion criteria") or whether it disappears entirely in favor of Browse/Generate within content modes. This is a UI labeling question, not an architectural one.

**Recommended action:** Amend Decision #40's "Free Play (deferred indefinitely)" status. The architecture absorbs free play; the deferral is no longer accurate. See proposed Decision #45 in §9.

### 5.2 MAGE long-term role (Decision #39, Doc 09 §10.3, UX Spec §8.6 Q5)

**Status before:** Open architectural question. Steven's working position (augmentation): MAGE persists, AI augments. Staley's framing (training-data scaffolding): MAGE generates training data for an eventual replacement LLM. The two framings were not reconciled in the May 5 standup.

**What was discussed:** Lines 1789–1810. Patrick, in the context of pricing for MAGE-generated content, said:

> Patrick: the AI would probably be adjusting the mage output to make it more musical or to fit to fit the like genre that they're trying to learn or to specifically work specific techniques that are in the piece of repertoire that they want to learn like whatever. There's like many reasons why the AI would adjust the music XML outputed by Mage.

Steven: "True." Staley did not push back; his immediately preceding response was "That's true. That's true." (line 1796) and "Sure" (line 1799).

Earlier in the call (lines 589–594), Steven also said: "this is where the AI turns into like mage or or whatever the the AI based system is. And I like I I still will just want to call it mage no matter what even if we like replace the system because I just I came up with the name and I just really like it." Staley laughed, agreed: "Yeah. Yeah. We can call him mage. We can call him mage" — and then said "I love mage. Yeah. Yeah."

**What's now directionally settled:** The team is converging on the augmentation framing. The AI's role is to adjust MAGE's output, not replace MAGE's role. The Patrick quote articulates this in terms of musicality and stylistic fitness — exactly the gap Doc 09 §10.4 identifies as the AI's strength.

**What remains open:** Full architectural commitment. Steven's position has team alignment but Staley hasn't explicitly said "I've changed my framing." The earlier framing (training-data-then-replacement) hasn't been retired so much as quietly displaced. Worth getting Staley's explicit confirmation.

**Recommended action:** Amend Decision #39 to reflect the directional convergence. Retain the question as "open" pending Staley's explicit confirmation, but record the team's current position more strongly. See proposed Decision #44 in §9.

### 5.3 The "video library" as a content type / node type (UX Spec §9 / new question)

**Status before:** Not in canon.

**What was discussed:** Patrick (line 699): "I'm going to actually tack on top of there uh a video library because I do think like the context, the historical context of what you need to know, what you're supposed to be learning is also really cool to like learn and then also watch other people actually do the exercises or like teach you" — referencing YouTube/Instagram API integration to host third-party videos. Steven's "right, right, right" agreements suggest acceptance.

**What's now settled:** Video library as a content surface within the agentic system is now the team's intent. Staley earlier (line 916) agreed videos / interactive tutorials would fit "as single nodes that are just like, okay, here's like a concept that this person needs to know."

**What remains open:** Whether video is a fifth content mode (parallel to Exercise, Repertoire, Sight Reading, Theory) or a node type within roadmaps that doesn't have its own mode-level browse experience. Patrick's framing leans toward "library" (mode-like); Staley's framing leans toward "node-as-tutorial" (roadmap primitive).

**Recommended action:** Track as a new open question in Doc 09 §13 and Bible §2.1.1. Don't resolve in Phase 2 — the architectural placement needs a dedicated discussion.

### 5.4 Performance constraints as cross-mode (UX Spec §9 Q5 partial)

**Status before:** Performance constraints were exercise-internal in canon (Bible §6.3, Architecture Doc §5). Cross-mode application was not articulated.

**What was discussed:** Lines 824–862, covered in §4.4 above.

**What's now settled:** Performance constraints are conceptually cross-mode. The exercise section's vocabulary (time-based pass conditions, accuracy thresholds, memory-chain length) carries over to sight reading and possibly repertoire.

**What remains open:** Specific mapping per content mode. What does each performance constraint type look like in each mode?

**Recommended action:** Decision-class. See proposed Decision #43 in §9.

### 5.5 The 5 goal categories (Doc 09 §4.2)

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

### 5.6 Investor demo scope (Doc 09 §15.2)

**Status before:** Doc 09 §15.2 specifies the canonical demo flow: (1) user uploads piece, (2) MuseFlow generates Mario-path roadmap, (3) walkthrough, (4) conclusion. Per the May 5 standup framing.

**What was discussed (May 7):** Lines 1190–1450. Two demo configurations emerged:

- **Configuration A: Live repertoire demo.** User plays a piece. AI identifies problem sections. AI sets up loops, walks user through perfect-practice tree (the §4.1 algorithm), with text or voice feedback. Steven: "easier bar because doesn't involve any music generation necessarily" (line 1284).
- **Configuration B: Chat → vertical Mario roadmap.** User states goal in chat. AI asks follow-ups. AI builds vertical road map (Fez-inspired). Some links work, some don't. Steven: "we can make it look sexy" (line 1300). Staley likes this: "I'd like the idea of building out a road map for sure. I think that's the most AI" (lines 1297–1298).

**Steven's reverse-engineering proposal (line 1374):** Build out the exercise schema's full matrix; AI chooses combinations from it; MAGE generates the content. Staley adds: feed AI the universe of possibilities, observe what road maps it builds, build what it keeps wanting (lines 1366–1378).

**The agreed plan:** Patrick takes the 5 goal categories and builds out concrete user-story road maps (with AI assistance). Steven reviews. The product of that work informs both the demo scaffolding and the Track D V1 catalog.

**What's now settled:** The demo is **at minimum** Configuration B (chat → road map), with optional Configuration A (live repertoire) as an additional capability. Neither requires building the full agentic system end-to-end. Both are achievable with partial infrastructure.

**What remains open:** Final demo decision — both, or just one. Schedule. Specific user stories to feature.

**Recommended action:** Update Doc 09 §15.2 in Phase 2 to reflect the May 7 demo-scope sharpening. Add Configuration A as a complementary demo asset. Note the user-story-driven approach.

### 5.7 Onboarding integration with Projects (Doc 09 §13 / new question)

**Status before:** Onboarding wasn't directly addressed in canon as it relates to the agentic system.

**What was discussed:** Staley (lines 566–578): "the the the initial pest or whatever. Like maybe instead of that or on top of that like the first thing you do when you log into Museflow is you get a chat screen that says like what are your goals like what would you like to learn and then it says okay now let's analyze your skill level and you get the like dynamic music start that starts coming up."

**What's now settled:** Onboarding-with-Projects is a directional commitment for some users — the chat-first goal-articulation pathway is a real onboarding option. But Doc 09 §12.2 commits that "onboarding doesn't assume they want to start with a Project" — both must be true.

**What remains open:** How onboarding splits paths (assumed-Projects vs. exploration). Is there a chooser? Defaults? Configurable?

**Recommended action:** Update Doc 09 §12.2 to acknowledge Projects-first onboarding as one of several paths, while preserving the AI-averse-friendly default. Add as open question if the split logic needs design.

---

## 6. New Open Questions Surfaced

Questions raised by the call that aren't yet tracked anywhere. These should be added to Doc 09 §13 and/or UX Spec §9 in Phase 2.

1. **Voice-LLM default mode.** Voice vs. text vs. both, configurable per user, configurable per content mode? Steven OK with text-first. Repertoire is the natural first battleground. But default behavior in V1 of this capability is undefined.

2. **Auto-looping AI-judgment override.** Steven flagged that the algorithmic perfect-practice tree may need AI judgment to break the rules (e.g., "actually, the issue is the previous measure, not this one"). When does the AI override the algorithm? How does the user perceive that override?

3. **Tutorial-as-roadmap-node phasing.** Even if AI-generated tutorials are deferred, does the architecture allow human-authored tutorials as roadmap nodes in the meantime? (I.e., does the existing curriculum's tutorials become a node type the agentic system can prescribe?)

4. **Video library as content mode vs. node type.** §5.3 above. Architectural placement open.

5. **Reverse-engineered catalog merger with bottom-up enumeration.** Track D will have two methodologies (top-down agent-demand and bottom-up substrate enumeration). What's the merge / triage process?

6. **Cost amortization model granularity.** The team's lifetime-value framing (heavy generation periods amortize over engagement) needs a concrete mental model — at what generation rate do unit economics break? Is it per-Project, per-month, per-account?

7. **Token-based pricing surfacing.** Do users see token meters directly (Staley: "we could even surface tokens directly")? Or do they see opaque "AI generations remaining"? Different UX implications.

8. **MAGE pricing under augmentation framing.** Patrick noted that under the augmentation framing, even MAGE-only generation could be charged for "tokens" since the AI is adjusting MAGE's output. This conflates LLM compute with MAGE compute for billing purposes. Is that right or wrong?

9. **Vertical roadmap visualization details.** Direction set (vertical, Fez-like, branching). But: how does the user pan/zoom across long roadmaps? Mobile rendering? Progress indicators?

10. **Perfect-practice tree's relationship to Optimal Grip.** Auto-looping based on error patterns is a form of adaptive difficulty; Optimal Grip is the canonical adaptive-difficulty concept (deferred per Decision #20 area). Are they the same thing under different names? Does the auto-looping algorithm subsume Optimal Grip for repertoire?

11. **End-of-round AI feedback timing.** Steven's "in between plays" feedback (Doc 09 §6 doesn't currently distinguish this from real-time). Specific UX for the pause/feedback/setup-loop flow needs design.

12. **Large Music Model framing.** Staley's enthusiasm for "Large Music Model" terminology (line 605) raises a positioning question — is MAGE a "large music model"? Is the augmented MAGE+AI system? Does this language enter customer-facing material?

---

## 7. Items That May Want Past-Canon Revisits

Places where the May 7 discussion suggests a previous canon decision should be reconsidered. Steven explicitly invited surfacing these. Each entry: which decision/section, why it might want revisiting, recommended action.

### 7.1 Decision #40 (Exercise Atom Schema — Five Field Additions) — `tier_gating` decision

**The dropped field:** `tier_gating` was considered and dropped on the rationale that "adding speculative fields creates noise and falsely signals that pricing is a near-term design surface."

**Why it might want revisiting:** The May 7 call advanced cost / unit-economics thinking significantly (per-month curriculum-generation limits, token-based pricing, MAGE-cost considerations). Pricing is still not designed, but the team's vocabulary is now richer. The question of whether tier_gating remains the right field name (vs. e.g., `generation_cost_class` or `compute_tier`) is sharper.

**Recommended action: track-for-later.** Don't revisit in Phase 2. The reasoning in Decision #37 still holds — pricing isn't designed enough to commit a field. But Phase 4 (pitch deck) work may force pricing concretization, at which point this needs revisiting.

### 7.2 Decision #20-area items: Optimal Grip, Looping, Game Mode

**The current state:** Optimal Grip is deferred (decision-area indicates V2+). Looping is in development. Game Mode is sight-reading-specific. These are treated as separate concepts.

**Why it might want revisiting:** §4.7 above. The auto-looping algorithm (proposed Decision #42) is conceptually adjacent to all three. Specifically, automatic loop-and-progress is a form of Optimal-Grip adaptive difficulty for repertoire; Game Mode's pass-condition mechanic generalizes per §4.4.

**Recommended action: revisit-in-Phase-2.** When Decision #42 is drafted, explicitly map its relationships to these adjacent concepts. Don't necessarily merge them, but eliminate ambiguity about whether they're parallel features or layered components.

### 7.3 Doc 09 §10.3 (Augmentation Question)

**The current state:** Records the question as open with Steven's working position (augmentation) as default and Staley's framing (training-data-then-replacement) as alternative. Notes Patrick's May 5 alignment with Steven.

**Why it might want revisiting:** §5.2 above. The May 7 call moves the team further toward augmentation. The "open question" framing may now be too cautious.

**Recommended action: revisit-in-Phase-2.** Amend §10.3 to reflect the directional convergence. Probably don't fully close the question yet — it deserves Staley's explicit confirmation — but the framing in canon should track the team's current position.

### 7.4 Bible §2.1.1 (Free Play status)

**The current state:** "deferred indefinitely; whether free play belongs as a content mode, a path-construction primitive, or its own non-mode category is open."

**Why it might want revisiting:** §5.1 above. The May 7 call resolves this — free play is a usage pattern within user-generated content in content modes, not a separate mode.

**Recommended action: revisit-in-Phase-2.** Update Bible §2.1.1 to reflect the resolution. Consider deleting Free Play from the "Candidate future content modes" list, with a brief explanatory note that the function is absorbed into user-generated.

### 7.5 Bible §6.3 (Replayability Through Constraint Variation) — performance-constraints scope

**The current state:** Frames performance constraints as an exercise-section product-level insight.

**Why it might want revisiting:** §4.4 above. Performance constraints generalize across content modes. The Bible treatment should reflect this.

**Recommended action: revisit-in-Phase-2.** Either generalize §6.3, or move performance-constraints framing to a higher-level Bible section (likely §2 or a new §) so it covers all modes.

### 7.6 Decision #29 (Agentic Vision — Documented as Future Architecture) — supersession

**The current state:** Decision #29 is partially superseded by Decision #32 / #41 in canon's framing.

**Why it might want revisiting:** Mostly canonical-cleanliness. After the May 7 call's strong validation of the architecture, the "documented as future" framing in #29 reads as outdated. It should probably be amended to point to the active R&D track explicitly.

**Recommended action: track-for-later.** Cosmetic, low-priority. Address during a future canon-cleanliness pass.

### 7.7 Doc 09 §15.2 (Demo Flow)

**The current state:** Specifies the May 5 canonical demo (upload piece → roadmap → walkthrough → conclusion).

**Why it might want revisiting:** §5.6 above. The May 7 call sharpens demo scope — adds Configuration A (live repertoire), specifies the user-story-driven approach, and makes the partial-faking strategy explicit.

**Recommended action: revisit-in-Phase-2.** Substantial update. Consider moving §15.2 into a fuller "Demo Strategy" section.

### 7.8 Doc 09 §4.2 (Types of Goals)

**The current state:** Six goal types listed conceptually.

**Why it might want revisiting:** §5.5 above. The May 7 call's 5 demo-relevant categories are partly different cuts (specific musician, specific genre).

**Recommended action: revisit-in-Phase-2.** Sharpen by adding the May 7 categories as concrete examples within the existing six conceptual types.

### 7.9 Doc 09 §6 (The AI Surface) — voice/audio extension

**The current state:** Lists conversational surface functions in text form. Doesn't distinguish text vs. voice.

**Why it might want revisiting:** §4.2 above. Voice/audio LLM feedback is a meaningful extension that should be documented.

**Recommended action: revisit-in-Phase-2.** Add voice/audio as a distinct surface modality, with text-first phasing per Steven's preference.

### 7.10 Doc 09 §5.2 (Roadmap Node Types)

**The current state:** Lists exercise / repertoire / sight-reading / milestone / conditional gate / free-play interlude / reassessment / branch-point node types.

**Why it might want revisiting:** §4.3 (tutorial node) and §5.3 (video node). New candidate node types.

**Recommended action: revisit-in-Phase-2.** Add tutorial-node and video-node as candidates, marked deferred / speculative.

---

## 8. Demo and Investor Implications

This section surfaces material that feeds into Phase 3 (team-facing pitch document) and Phase 4 (investor pitch deck). Captured separately because it has different audiences than the canon.

### 8.1 Demo configurations

Two complementary configurations the team converged on. Either is buildable; both is best.

**Configuration A: Live repertoire demo** — user plays a real piece, AI identifies problem sections via the auto-looping algorithm, sets up loops automatically, walks user through perfect-practice tree with text (and ideally voice) feedback. Demonstrates: auto-looping algorithm, AI-LLM-as-tutor, repertoire integration, audio recognition. Risks: voice-LLM latency, performance issues during live demo.

**Configuration B: Chat → vertical Mario road map** — user states goal in chat, AI asks follow-ups (auto-engaged "diagnostic agent" mode), AI builds vertical Fez-inspired road map with visible nodes mixing exercises / sight reading / repertoire. Some nodes link to functional content; some are scaffolded. Demonstrates: agentic system, content/path mode architecture, multimodal roadmaps, the "AI builds your custom curriculum" wedge. Risks: looks fake without AI Configuration A's live-feedback richness.

Steven articulates Configuration A as "easier bar because it doesn't involve any music generation necessarily" (line 1284). Configuration B is what Staley likes: "I think that's the most AI" (line 1298). Both should ship for the demo.

### 8.2 V1 vs. demo scope

The demo can be more polished than V1 for specific demo'd capabilities, while V1 is lighter on those same capabilities. This is normal and not a problem if the team is explicit about it.

Specifically:
- The exercise schema's full matrix is demo-buildable but doesn't need to be V1-ship-buildable (Steven's reverse-engineering approach lets the demo show what V1 should eventually populate)
- The auto-looping algorithm exists in Patrick's PRD already; for demo it needs UI; for V1 it needs documentation
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

This is enough material for a "Cost Considerations" section in Doc 09 (probably as a new §17 or as additions to §10.5/§15). It's not pricing — it's a framework for thinking about pricing later.

**Recommended action for Phase 2:** Add a brief "Cost Considerations" section to Doc 09. Covers the 6 principles above. Explicit: pricing is still not designed (Decision #37 stands).

**Recommended action for Phase 4 (deck):** The unit-economics story is investor-ready in shape. The narrative is: "MAGE makes generation cheap; LLM tokens are the variable cost; heavy generation is front-loaded per-user; token upsells handle outliers." This is defensible.

### 8.4 Staley's R&D direction

End-of-call commitment: "I'm just going to start digging into like how to do LLM. Um, I've watched some I've watched some videos from AWS on using their like AWS bedrock stuff and that might be like the step one. Um, I've also heard stuff about that being expensive. Um, maybe there's a way we can make calls to some external API that's like I don't know" (lines 1827–1832).

This is the first explicit tooling exploration commitment from Staley per Decision #32. Direction: **AWS Bedrock first, external API alternatives if cost is prohibitive.**

**Recommended action for Phase 2:** Update Doc 09 §10.5 (LLM Choices) to reflect Staley's specific exploration direction. Add §10.6 alternative — external-API-call architecture (e.g., Claude API, OpenAI API) as a near-term fallback distinct from the deeper "build out MAGE algorithmically" alternative.

### 8.5 Team composition argument

Doc 09 §15.4 captures Patrick's "two engineers + music educator + product" framing. The May 7 call doesn't change this. Confirms it.

### 8.6 What's still missing for the demo

Concrete items that need to exist for either demo configuration to ship:

**For Configuration A:**
- Voice-LLM latency under control (Staley: the technical hurdle)
- Repertoire perfect-practice toolset implemented to the point that AI can engage tools (loop, slow-down, accuracy heat-map)
- An LLM that can reliably emit JSON (problem-section locations) + script (text/spoken cues) per Staley's two-output framing (line 414)

**For Configuration B:**
- A vertical road-map UI component (Phaser, React, or other)
- A list of ~10–30 user stories with corresponding road maps (Patrick is owner per the call)
- An LLM that can output road-map JSON in a consistent schema (Staley: "I've heard it can be hard to have AI's like output in a consistent way" — line 1714)
- Some functional links to back-end content (at least a few) so the demo doesn't look entirely faked

**For both:**
- The exercise schema's full matrix populated enough that the AI has a universe to draw from (Track D output, with reverse-engineering input)

---

## 9. Recommended Decision Log Additions

Drafted in canonical Decision Log format for Steven's approval. **Nothing is committed in this document.** Phase 2 is where these get appended (or dropped, or revised) per Steven's review.

### Proposed Decision #42: The Auto-Looping / Perfect-Practice Tree Algorithm

**Source:** May 7, 2026 Emergent Curriculum brainstorm. Patrick described an algorithm he claims to have already designed in his PRD: read the green-note JSON history, identify the first section with two-or-three-notes-in-a-row errors, dynamically determine loop boundaries (one or two measures before/after the errored section), perfect that section, auto-progress to the next errored section, and combine perfected sections in a tree structure (small section → small section → combined → next pair → combined → larger combination, recursively). Staley's read: largely algorithmic, with the LLM as "voice/text sugar on top." Steven concurred but flagged that AI judgment may need to override the algorithm for "break the rules" cases (e.g., the actual issue is the previous measure, not the errored one).

**Decision made:** The auto-looping / perfect-practice tree algorithm is recognized as a **first-class architectural primitive** for repertoire (and possibly exercises). Specifically:
- It is the algorithmic execution layer that connects performance data to looping decisions
- It interacts with: Looping (manual loops, in development), Game Mode (parallel concept in sight reading), Optimal Grip (which it partly subsumes for repertoire — adaptive looping based on errors *is* one form of optimal-grip difficulty adjustment)
- It is the load-bearing capability for live-repertoire investor demo (Configuration A in Phase 1 §8.1)
- It is invokable by the agentic system as part of Project execution (a Project's roadmap node for "practice this piece" can prescribe auto-looping as the practice mode)

**Reasoning:** The algorithm exists. Patrick has implemented it (or specified it in detail) in his existing PRD. It is the strongest single demo capability the team has. It threads through repertoire, the agentic system, and the AI-feedback layer, and earns a canonical reference rather than being implicit.

**Phasing:** TBD. The algorithm itself is implementable now (per Patrick); the AI-judgment override and voice-feedback layer are speculative-near-term. V1 / demo / V2+ scoping is open.

**Cross-references:** Decision #20-area items (Looping, Optimal Grip, Game Mode) — relationships should be explicitly mapped in canon updates. Doc 09 §5.2 (roadmap node types) and §15.5 (demo defensibility). Patrick's PRD as the implementation source.

### Proposed Decision #43: Performance Constraints Generalize Across Content Modes

**Source:** May 7, 2026 brainstorm. Steven's articulation (lines 824–842) that the exercise section's performance-constraint vocabulary (time-based pass conditions, accuracy thresholds, memory-chain length) ports directly to sight reading and possibly repertoire. Staley: "the exercise section can also maybe be a version of this game mode thing." Bible §6.3 currently treats performance constraints as exercise-internal.

**Decision made:** Performance constraints are promoted from exercise-section-internal to a **cross-content-mode primitive**. Any "completable" engagement with content (exercise atom session, sight-reading level attempt, repertoire practice session) carries performance constraints that determine pass conditions and shape the practice experience.

The schema impact:
- Exercise atoms already carry performance constraints (per Architecture Doc §5)
- Sight-reading levels gain a performance-constraints schema entry (parallel to atom configuration)
- Repertoire practice sessions may carry performance constraints (e.g., "play this passage at 80% accuracy or higher for 5 minutes to clear")

**Reasoning:** The exercise framework's most useful product-level concept (replayability through constraint variation) generalizes with no architectural cost. Treating performance constraints as a cross-mode primitive avoids reinventing similar mechanics per mode and provides the agentic system a unified vocabulary for prescribing practice intensity.

**Phasing:** TBD. Specific application to sight reading and repertoire is V2+. The conceptual promotion is V1; per-mode implementation phases independently.

**Cross-references:** Decision #22 (replayability), Bible §6.3, Architecture Doc §5, Decision #41 (the cross-mode pattern this extends).

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

### Proposed Decision #45: Free Play Resolved as User-Generated Within Content Modes

**Source:** May 7, 2026 brainstorm. Lines 580–870. Steven articulates free play as a usage pattern within user-generated content in content modes (especially sight reading) — not a separate mode. Staley: "I don't mind calling it free play and having free play have like a game mode." Patrick: "or we just don't even need to call it any mode or like a section really."

**Decision made:** Free Play, previously listed as a candidate content mode "deferred indefinitely" (Bible §2.1.1, Decision #40), is **resolved as a usage pattern within user-generated content** in existing content modes. Specifically:
- A user constructs custom sight-reading levels (or other content) with whatever parameters they want, including "no completion criteria, just play endlessly"
- The architecture absorbs this without a new mode
- The term "Free Play" may persist at the UI level (e.g., as a labeled affordance) but does not denote a separate content mode

**Reasoning:** The May 7 articulation closes the long-standing ambiguity about Free Play's architectural placement. The user-generated-content pattern (within Generate flow per Decision #41) provides the primitive. No new mode is required.

**Phasing:** N/A — architectural framing. Specific UI labels are V1+ design questions.

**Cross-references:** Decision #40 (Free Play deferral updated), Decision #41 (the user-generated origin this resolution rides on), Bible §2.1.1 (status update needed).

### A note on what I considered but didn't propose

I considered but **did not draft** Decision proposals for the following, on the rationale that they're not yet decision-class:

- **Voice/audio LLM feedback (§4.2)** — extension of the AI surface, not a new architectural primitive. Should be added to Doc 09 §6, not the Decision Log.
- **Reverse-engineering catalog methodology (§4.5)** — methodological proposal for Track D, not an architectural commitment. Should be documented in Track D scoping, not the Decision Log.
- **Vertical Mario roadmap UX (§4.6)** — UX direction, not committed UX. Should sharpen Doc 09 §7.2, not the Decision Log.
- **AI-generated tutorials as roadmap nodes (§4.3)** — deferred future direction. Should be added to Doc 09 §5.2 candidate-node-types list.
- **Demo scope (§5.6)** — operational, not architectural. Should update Doc 09 §15.2.
- **Cost framework (§8.3)** — not pricing, not architectural. Should add a "Cost Considerations" section to Doc 09 in Phase 2.

These can become Decisions later if Steven prefers, but I think they're better captured as inline canon updates in Phase 2 rather than as numbered Decisions.

---

## 10. Cross-Track Implications

How this work affects the other Tracks running in parallel.

### Track A2: Patrick's "Theory Library & Exercise Section" Doc Evaluation

A2 is paused for this work and resumes after Phase 1 lands. The May 7 call has implications for A2:

- **Patrick's "PRD you guys haven't read" reference (line 433)** likely refers to the same doc A2 is evaluating. The auto-looping algorithm (§4.1) is "already part of the PRD." When A2 resumes, this should be one of the things to verify against the PRD's actual contents.
- **Theory as a content mode (Bible §2.1.1 candidate, status TBD)** is a primary A2 question. The May 7 call doesn't directly address Theory's status, but Patrick's "music theory" addition to the cross-modal road map (line 1548) suggests the team is treating it as a content surface in working framing — A2 should resolve its mode-status formally.
- **The auto-looping algorithm**, if already in Patrick's PRD, may have substantial supporting material there worth integrating with the Decision #42 canon update.
- **The 5 demo-relevant goal categories (§5.5)** likely have analogues in Patrick's PRD. Worth cross-checking.

**Recommended:** When A2 resumes, sequence its work after Phase 2 lands so A2 evaluates Patrick's doc against the integrated canon.

### Track B: Open-Question Triage

The May 7 call:
- **Resolved or directionally settled** several previously-open questions (free play, MAGE direction, performance constraints generalization, demo scope sharpening). Track B's current open-question inventory shrinks by these items.
- **Surfaced new open questions** (the 12 items in §6 above). Track B's inventory grows by these items.

**Net effect on Track B:** Same total or modest growth in open-question count, but with substantially different shape — older questions resolve, newer ones replace them.

**Recommended:** Track B should sequence after Phase 2's canon updates land. The triage will be cleaner against an updated open-question inventory.

### Track C: Taxonomy Reconciliation

Doc 03 (Exercise Taxonomy) is the target for C. The May 7 call has limited direct impact on C — the discussion stayed at the agentic-system / cross-mode level rather than the within-exercise-taxonomy level. Two indirect effects:

- **Performance constraints' cross-mode promotion (proposed Decision #43)** may sharpen what Doc 03 includes — taxonomy is exercise-section-internal, so the cross-mode framing affects Doc 03's scope clarification.
- **Reverse-engineering methodology (§4.5)** is methodologically adjacent to taxonomy work — both are "what's the universe of possibilities" exercises. C might want to coordinate with D's reverse-engineering input to avoid duplicate work.

**Recommended:** Track C is largely unaffected. Continue when Phase 2 lands; no scope changes expected.

### Track D: V1 Atom Catalog Authoring

The largest cross-track impact. Two changes:

- **Methodology change.** Track D's implicit methodology is bottom-up enumeration. The May 7 call commits the team to running the top-down "feed the AI the universe; see what road maps it builds" methodology in parallel (Staley/Patrick agreed plan, lines 1402–1450). Track D should explicitly absorb both methodologies and document their merge process.
- **Demo-driven prioritization.** The 5 user-story categories give Track D a near-term prioritization signal. The atoms that show up across multiple user stories (e.g., Alberti bass exercises, ABRSM-curriculum atoms) should be authored first.

**Recommended:** Track D's scoping document should incorporate the reverse-engineering methodology and the user-story-driven prioritization before atom authoring begins. Phase 2 should produce a brief Track D scoping note alongside the canon updates.

### Track E: PRD Authoring

The macro PRD that informs Patrick's MVP decomposition. The May 7 call has substantial implications:

- **Demo scope (§5.6, §8.1)** is a load-bearing input — the PRD should distinguish demo-state from V1-ship-state.
- **Cost framework (§8.3)** is PRD-relevant but only as principles, not as committed pricing.
- **Auto-looping algorithm (§4.1)** is PRD-class material now that it's recognized as architectural.
- **Voice/audio LLM feedback (§4.2)** is PRD-class material as a V2+ capability.
- **Performance constraints generalization (§4.4)** affects the PRD's section on cross-mode primitives.

**Recommended:** Track E should kick off after Phase 2 (canon updates) and Phase 3 (team-facing pitch document) land, since those provide the substrate. The PRD's authoring will be substantially easier with both inputs.

---

## 11. Recommended Phase 2 Scope

Phase 2 is the canon-evolution pass that updates affected documents based on this Phase 1 analysis. Recommended scope, with approximate effort estimates:

### 11.1 Documents to update

**Doc 09 — Agentic MuseFlow Vision (largest update).** Changes:
- **§4.2 (Types of Goals)** — add the 5 May-7 demo-relevant categories as concrete examples within existing types. (small)
- **§4.3 (Goal Articulation)** — add "diagnostic agent" / "auto-engaged plan mode" framing. (small)
- **§5.2 (Roadmap Node Types)** — add tutorial-node and video-node candidates, marked deferred. Add or sharpen auto-looping-as-practice-mode framing. (small)
- **§6 (The AI Surface)** — add voice/audio as a distinct surface modality with text-first phasing. (medium)
- **§7.2 (Per-Project Zoom)** — narrow the visualization candidates toward "vertical tree with branching" per the Fez-inspired direction. (small)
- **§10.3 (Augmentation Question)** — amend per proposed Decision #44; record directional convergence while retaining open caveats. (small)
- **§10.5 (LLM Choices)** — add Staley's specific exploration direction (AWS Bedrock first, external API alternatives). (small)
- **§12.2 (AI-averse design constraints)** — acknowledge Projects-first onboarding as one of several paths. (small)
- **§13 (Open Architectural Questions)** — close items that resolved (free play, partial MAGE direction); add new questions from §6 of this document. (medium)
- **§15.2 (Demo Flow)** — substantial rewrite. Replace canonical-demo-only framing with Configuration A + Configuration B framing. Document the user-story-driven approach. (medium)
- **§17 (new) — Cost Considerations.** Add new section capturing the 6 cost principles from §8.3 of this document. (medium)
- Various references to proposed Decisions #42–#45 throughout. (small)

Estimated effort: 1–2 sessions.

**Doc 01 — Project Bible.** Changes:
- **§2.1.1** — update Free Play's "candidate" status per proposed Decision #45. (small)
- **§6.3 (Replayability Through Constraint Variation)** — generalize per proposed Decision #43, or move framing to higher-level §2 / new §. (small)

Estimated effort: <1 session.

**Doc 02 — System Architecture.** Changes:
- **§5 (or new section)** — performance constraints as cross-mode primitive per proposed Decision #43. (small–medium)
- Atom schema unaffected unless Decision #43 implies field changes (probably not in V1 scope).

Estimated effort: <1 session.

**Doc 05 — Design Decisions Log.** Changes:
- Append proposed Decisions #42, #43, #44, #45 (with Steven's revisions). (medium)
- Amend Decision #39 (per #44). (small)
- Amend Decision #40 (Free Play status note per #45). (small)

Estimated effort: 1 session, mostly writing.

**Doc 07 — UX Navigation Spec.** Changes:
- **§8.6 Q5 (MAGE long-term role)** — update per #44. (small)
- **§9** — add new open questions per §6 of this document; close resolved questions. (small)

Estimated effort: <1 session.

**Doc 04 — Glossary.** Changes:
- Add: auto-looping algorithm / perfect-practice tree (per #42); cross-mode performance constraints (per #43); diagnostic agent / auto-engaged plan mode; "Steven MD file" (or whatever Steven prefers as the per-user memory artifact term). (small)

Estimated effort: <1 session.

### 11.2 Documents NOT to update in Phase 2

- **Doc 00 (Handoff Brief)** — historical, frozen.
- **Doc 03 (Exercise Taxonomy)** — Track C's responsibility, not Phase 2's.
- **Doc 06 (Exercise Blueprints)** — no direct updates needed.
- **Doc 08 (Standup Synthesis Apr 28–May 5)** — historical, frozen.

### 11.3 Phase 2 cadence recommendation

Phase 2's edits are mostly mechanical once the interpretive calls land (which is the purpose of this Phase 1 document). Suggested approach:

1. **First Phase 2 session:** Steven approves / revises the proposed Decisions #42–#45. Phase 2 produces the updated Doc 05 with finalized Decisions, plus the simplest mechanical updates (Bible §2.1.1, UX Spec §8.6 Q5, Glossary additions).
2. **Second Phase 2 session:** Doc 09 substantial updates (§5.2, §6, §7.2, §10.3, §10.5, §12.2, §13, §15.2, new §17). This is the bulk of the work.
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

Each of those is a separate downstream piece. Phase 2's sole goal is to land the canon at a state where Phase 3 has clean substrate to draw from.

---

## 12. Document Status

**Version 0.1 (May 8, 2026)** — Initial draft, Phase 1 only. Produced from the May 7, 2026 transcript and the canon as of commit prior to this document.

**Outstanding for Phase 1 closeout:**

- Steven redlines this document
- Steven approves / revises proposed Decisions #42–#45
- Steven approves Phase 2 scope (§11)

**After approval, this document becomes:** the canonical record of what the May 7 call produced and how it integrates with prior canon. It is canon-class — analogous to Doc 08 (Standup Synthesis Apr 28–May 5) — and persists as reference material in `docs/10-may7-brainstorm-synthesis.md` after Steven commits.

---

*End of May 7, 2026 Brainstorm Synthesis (Doc 10), Version 0.1.*
