# MuseFlow Standup Synthesis: April 28 & May 5, 2026

> **Status: Reference document.** Synthesized from Granola transcripts of two consecutive MuseFlow standing meetings. Captures team thinking, decisions, and open tensions relevant to the exercise section, infrastructure, UI/UX, adjacent features, and product vision. Intended as input for the next design iteration on the exercise section.
>
> **Participants present across both meetings**: Steven Gizzi (founder/CEO), Andrew Urbanowicz (VP of Engineering — audio recognition, repertoire), Staley (CTO — architecture, AI), Patrick Boylan (co-founder — marketing, fundraising, product), plus Tucker Dean, Tom Urbanowicz, Alayna L. Goss (mostly silent in these transcripts; Tucker and Alayna have since departed the team).

---

## Executive Summary

The two standups produced **one major strategic pivot**, **several adjacent feature confirmations**, and **a redrawn map of who owns what**:

1. **The agentic "Projects" vision moved from far-future to near-term R&D + investor pitch target.** What was previously documented as Decision #29 / UX Spec §8 ("future architecture consideration") is now an active workstream — Staley has volunteered to drive it, and the team scheduled a dedicated brainstorm ("Emergent Curriculum," Thursday 5pm PT, Steven/Staley/Patrick).

2. **Staley is reorienting away from repertoire engineering toward AI/ML infrastructure** (LLM fine-tuning, training pipelines, music gen). Andrew is taking over repertoire workstreams (custom upload, social/sharing). This redistribution unblocks Steven on the exercise section, since the cross-team complexity pipeline conversation now has a clearer owner.

3. **The Mage / Opus Modus terminology confusion surfaced again** and Steven had to re-establish that Mage is the logic/generator and Opus Modus is just the printing engine. There's an unresolved framing dispute about whether Mage exists *only* to generate training data for a future LLM (Staley's framing) or as a permanent generative engine that AI would augment, not replace (Steven's position).

4. **Exercise section deliverable**: Steven set a soft deadline of EOW May 2 (optimistic) / EOW May 9 (pessimistic) for the PRD/design spec. Format is open ("30, 45, 50 pages — however long you need it to be"). Patrick volunteered to handle MVP decomposition once the macro spec lands. Asif (the "a sieve" / "see" in transcripts) remains the likely implementer.

5. **Andrew shipped a custom repertoire editor demo + transposition + theme modes**, all of which materially affect the exercise section's surrounding feature landscape and have downstream implications for what gets gated behind premium tiers vs. base.

---

## 1. Strategic Shift: "Projects" / Emergent Curriculum Becomes a Near-Term Track

This is the most consequential development across both meetings. It originated in the May 5 standup when Staley pitched what he wants to focus on next.

### What was proposed

Staley's framing (May 5): instead of building features in isolation, build a **personalized learning system**. The user uploads a piece (or states a goal), and MuseFlow generates a "Mario path" — a roadmap of exercises, dumbed-down repertoire, sight-reading, and lesson content that takes them from current state to mastery.

Steven extended this in real-time during the meeting, and the team converged on:

- **The agentic interface** is "really ideally just kind of a wrapper for all our UI" — a generative front-end that assembles tools from MuseFlow's "rich tapestry" / "corpus" of capabilities based on stated goals.
- **Goal types** the system should accept (Steven's expansion):
  - "I want to learn this piece" → upload repertoire, get a custom path
  - "I need to pass this music school exam"
  - "I want to get a gig at a piano bar"
  - "I want to prepare for Grade 5 ABRSM"
  - Any open-ended natural-language statement of intent
- **Cross-project context** ("air traffic control"): the agent can stitch multiple goals — "First of all, why don't we take these three steps first? Because you're going to need to do all three… If you do this, this will advance you towards three of your goals. If you do this, this will only advance you towards one."
- **Naming**: the team agreed to steal the **"Projects"** pattern from Claude/ChatGPT, since investors will recognize it as a familiar AI-product idiom.

### Patrick's tagline crystallization

> "MuseFlow is an app, an experience, that decides every step for you basically — it helps you, it knows every step that you need and it knows how much you need to practice. Every step of the way to mastery is figured out."

And Steven's investor-deck-ready line:

> "MuseFlow is what you do while your agents are doing everything else."

### Status vs. existing documentation

- **Decision #29 (Agentic Vision)** in `05_Design_Decisions_Log.md` documented this as a future architectural consideration.
- **Section 8 of `07_UX_Navigation_Spec.md`** ("Future Vision: Agentic Exercise System") laid out the architectural implications — atoms as the right granularity for an agent to prescribe, the hierarchy as agent-navigable, custom atom creation as a generative architecture upside.

These documents anticipated this turn correctly. **What's new is the timeline**: this is now an active R&D track and investor demo target, not a V3+ consideration.

### Investor demo target

- **Target raise**: $1.5M (Patrick's pitch deck work).
- **3–5 year plan structure**: refine product → build community → two-sided marketplace (courses, instructor-student matching, possibly additional verticals).
- **Demo flow**: upload a piece → MuseFlow generates the Mario-path roadmap → walks through example exercises, simplified repertoire phases, looping practice, accuracy heat-map, etc.
- **Why it sells**: the team's combined skill stack (two engineers, one classically trained pianist + music educator + performer, one engineer who's also a pianist) lets MuseFlow build something that is "extremely unique" and that "nobody else can replicate."

### Implications for exercise section design

The exercise section is one of the **assembly components** of the Project/agent system. This raises several design questions worth surfacing in the next iteration:

- **Atom-as-prescribable-unit**: the existing UX Spec already calls atoms "the right granularity for an agent to prescribe." The next iteration should pressure-test whether atom identity is sufficient for an agent to construct a roadmap, or whether atoms need additional metadata (e.g., prerequisite relationships, expected time-to-clear, mastery thresholds).
- **Custom atom generation**: previously flagged as "the agent could potentially define new atoms." If the demo target requires atom generation on the fly, this jumps from theoretical to required.
- **Exercise generation on command** (Steven's contribution to the May 5 brainstorm): "another key part of this would be the ability to with an exercise section have the ability to generate exercises yourself. Either the user or the student or the teacher or yeah even Museflow itself, if it deems that you need an exercise, could generate an exercise on command. And that level of generation almost feels the easiest. Because it doesn't have to match stylistically something — it would be variations on scales and chords and stuff." This is a design assertion: **exercises are the easiest to generate** because they don't carry musical-style constraints the way repertoire does. Worth formalizing this as a design principle.
- **"Free play section as part of the path"** (Staley): the path may need to include unstructured-play interludes, not just drill-and-test stations. This isn't currently in the exercise blueprint catalog.
- **Five-exercises-cover-90%-of-pieces question** (Staley to Steven, May 5): "what maybe five exercises do you think could probably apply to like 90% of pieces?" Steven didn't answer in the meeting. This is worth answering deliberately as part of the next design pass — it would also serve as a curriculum primitive for the agent.

---

## 2. Exercise Section: Direct Updates

### Deliverable & timeline

- **Format**: PRD-style design specification. Patrick described it as "30, 45, 50 pages — however long you need it to be."
- **Soft deadline (Steven set, April 28)**: optimistic by EOW May 2; pessimistic by EOW May 9.
- **Implementation owner**: Asif (the engineer who has been doing exercise/repertoire work). Not 100% locked but the working assumption.

### Patrick's MVP decomposition offer

Patrick volunteered (April 28) to handle the work of breaking the macro spec into MVP subtasks:

> "One of the tasks that I would like to take on is breaking those into subtasks, finding the minimum viable product of what the value proposition for this exercise section would be, distilling it down to its essence, starting there. You don't need to do that, Gizzi — I'm happy to do that work. I would find that very fun. Just go macro and I'll pare it down into the incremental steps of features of how we can build this together. That's what I did for the Perfect Practice tool and it was very enjoyable for me."

**Implication**: the spec Steven produces should optimize for completeness and clarity at the macro level, not for MVP-readiness. Patrick will do the MVP carving work afterward.

### Complexity adjustment confirmed as V2 in the exercise section

Steven's position (April 28), unchanged:

> "Complexity in the exercise section may be a V2 feature, essentially because complexity is not a feature anywhere else in the app yet. So we probably need to make sure that there's the capacity for it, but if we build it into V1 it just wouldn't serve much of a function yet."

This **confirms** the existing phasing in `05_Design_Decisions_Log.md` Decision #17 (V1 = filter/browse, V2 = adaptive difficulty / Optimal Grip / ELO).

The team agreed: schema must accommodate complexity, but V1 ships without it.

### Cross-section complexity language confirmation

Patrick (April 28): "All this stuff needs to kind of be tied together from the start because we need that info, but I think we've got a good idea of how to do that with this whole complexity characteristic concept."

This **confirms** Decision #18 (Cross-Section Complexity Language). The Mage complexity pipeline conversation Staley and Patrick had over the prior weekend remains the working approach. Steven has noted that he's "stoked to get into" the actual pipeline integration.

### Exercise generation on demand (NEW, May 5)

Steven introduced this concept in the Emergent Curriculum brainstorm: exercises should be generatable on command by user, teacher, or MuseFlow itself. Rationale: exercises are easier to generate than sight-reading or repertoire because they don't need stylistic match with a target piece — they're "variations on scales and chords and stuff."

**Design implication**: the exercise atom framework already supports this in principle (atoms are combinatorial). The next design iteration should explicitly call out *exercise generation* as a first-class capability, distinct from *exercise selection from a fixed catalog*. This may also affect how the catalog is structured — fewer hand-authored atoms, more parameterized templates.

---

## 3. AI/ML Infrastructure (Staley's New R&D Track)

### What Staley wants to build

- **Fine-tune an LLM** to produce music conditioned on complexity characteristics (and possibly style).
- **Build the AWS training infrastructure**: "How do I click a button and upload parquet, tell AWS to train a GPT and save the output."
- **Two-track plan**: (a) build the demo UI first so the team has something visible to fill with real data, (b) build the actual training pipeline in parallel.

### Mage's role — unresolved framing dispute

Staley's framing (May 5, repeated multiple times): **Mage exists to generate training data** for the eventual LLM. After enough data, the LLM replaces Mage.

Steven pushed back firmly:

> "It is not obvious to me that Mage would just be for training data, and that's not the assumption that I'm working on… If a more AI-based approach were to replace Mage, it would integrate Mage into it. It would be an upgraded AI-enhanced version of Mage to me. It wouldn't just be a separate thing that we build."

Patrick aligned with Steven: "I think that's not necessarily going to be the case for Mage."

**Status**: not resolved. Steven re-asserted Mage's role; Staley said "we'll figure it out." Worth surfacing as an open architectural question in the next conversation.

### Mage capability that Staley did not seem aware of (or had forgotten)

Steven walked through what Mage can already do (May 5):

> "It could take a piece of existing repertoire. It could analyze it for complexity. It could get all the specifics on its complexity. And then it could intentionally downgrade any or all of the individual complexity metrics in certain ways and find/make a piece that matches those downgraded metrics. It can do all of that. It just doesn't currently have logic that also says 'preserve the key musical characteristics, make this similar musically to the repertoire piece.' It could do that — I'd have to think about how to plan it and execute it."

This is the **piece-simplification capability** that's central to the Project demo (upload piece → simplified version → roadmap). It already exists in algorithmic form; what's missing is musical-similarity preservation, which is where AI augmentation would help most directly.

### Opus Modus / Mage terminology confusion — recurring

In the May 5 meeting, Patrick referred to "Opus Modus" when he meant Mage. Steven had to clarify multiple times:

> "Opus Modus is purely just an engine. It does nothing other than what it's told to do. Mage is the codebase where all the logic is that decides what to do, and then Opus Modus just prints it. That's all."

**This is the second time this confusion has come up.** Recommend reinforcing the distinction in `04_Glossary.md` and possibly in the Project Bible — the team is conflating these terms in design conversations and it's slowing things down.

### LLM technical thinking (Staley)

- **RAG vs. fine-tuning**: Staley thinks RAG is best for chat/context retrieval but not for music gen. Fine-tuning is "completely fine for 90% of cases."
- **Hybrid possibility**: fine-tuned model + RAG layer over user historical play data and current-song context. Vector DB on user data.
- **Cost mitigation strategies**:
  - Cache outputs (same piece → same simplified output).
  - Use quantized open-source models (small enough to run cheaply).
  - Use the LLM only for piece-simplification calls (which are infrequent), not per-keypress.
  - Theory: "What we're asking the LLM to do is actually very [scoped]. Once given the prompt and the data — the complexity characteristics — once we teach it well enough, it will actually be very in line with what LLMs are built for and we might not need a very complex model."
- **Use cases beyond music gen**:
  - Personalized lesson-path generation (Patrick favored this — "you can do that with any sort of GPT model JSON, that's pretty straightforward, no unknown unknowns").
  - Suggesting next exercises based on user state.
  - The Project/agent system itself.

### Andrew's softer integration point

Andrew (May 5) raised a related but more pragmatic system: AI-targeted re-engagement messages that pull a user's play stats and generate proactive nudges ("come back and finish tier 3 of level 9"). This doesn't need ML — "if/then/else logic with cheap model calls" suffices. Mentioned April 28 as well. Lower-stakes win, and an early validation track for the AI infrastructure.

---

## 4. Adjacent Features Affecting the Exercise Section

These shipped, are shipping, or are in active development. They form the surrounding context the exercise section will plug into.

### Custom repertoire editor (Andrew's May 5 demo)

Andrew demoed an in-app music editor. Capabilities shown:

- Click to add notes, drag to reposition.
- Double-click to set start/recording point.
- Save user-created repertoire to the user's library.
- Change notation (sharps, flats, naturals).
- Toggle metronome.
- MIDI playback works ("perfect representation").
- Three play modes:
  - **Practice**: scoring mode, no audible playback.
  - **Listen**: audible playback only, no scoring.
  - **Sound**: practice + audible playback simultaneously (user can hear themselves and the score).

**Naming flag**: "Sound" is confusing. Steven said it needs renaming. Likely candidates: "Play-Along" or similar.

**Recommendation Patrick made**: Andrew should spend time in MuseScore and Sibelius for UX nuance. Specific example: deleting a note should turn that section into a rest. Currently unclear.

**Use case for instructors**: Patrick's framing — "I think this would be to give to instructors as well. They can write their own exercises, upload them, then share with their students, all within the MuseFlow ecosystem. They don't have to use another app to write it like MuseScore and then download it and then upload it — even that, people are too lazy for that."

**Implication for exercise section**: this editor is the natural authoring surface for **custom exercises** in the agent/Projects vision. It also creates a path for **teacher-authored exercises** that get assigned to students. Both should be in the next design iteration's scope.

### Transposition (Andrew's May 5 demo)

- **Transposition works.** Staley had thought it was impossible given the current implementation; Andrew surprised the team.
- **Steven's QA note**: sharps and flats fonts are too small / wrong style on transposed pieces. This blocks production rollout. Asif task: refactor accidentals (sharps, flats, naturals) globally.
- **Premium tier candidate**: Steven flagged transposition + custom repertoire editor as plausible premium-tier features, not base. (See §7 below.)
- **Transposed sight-reading trainer**: also working in the demo. Affects how transposition might integrate into exercises.

### User-uploaded repertoire + looping

Repeatedly referenced as the highest-value near-term combo:

- Staley (April 28): "User-uploaded repertoire plus looping is somewhere in the near future. To upload your own music and then use looping the way that we've written it and created it — that's a game changer right there. Game changer."
- Andrew is now the owner of user-uploaded repertoire (per the division-of-labor change, see §6).
- Looping is feature-flagged in but had bugs Staley needed to address (cursor placement, click zones in mobile repertoire). Staley said he'd do another QA pass before calling it done.
- Steven's prioritization (April 28): if forced to choose between user-uploaded repertoire and complexity adjustment, take user-uploaded repertoire first. It needs less coordination — complexity adjustment requires UI changes (chevron logic, completion display).

### Audio recognition (Andrew)

- Goal Andrew set himself (April 28): play through level 10 repertoire at goal tempo with 100% accuracy with audio recognition by Sunday night.
- Status as of May 5: "still not at my standard of being able to play a level 10, but it's better and it's worth more testing."
- Notes:
  - Octave detection issues (C3 vs C4) — addressed by tightening harmonic profile expectations.
  - Crashing and memory consumption issues resolved.
  - Timing/offset issues remain (yellow-when-should-be-green).
  - Modal UI for MIDI vs. audio selection tightened up.
  - Repertoire creation pipeline note-picking was fixed.
- **Upcoming**: feature flag the repertoire audio modal + revert the MIDI keyboard blocker before merging to main.
- **Why this matters for exercises**: audio recognition is a prerequisite for non-MIDI input modalities in many exercise atoms. Several aural input atoms in the catalog are MIDI-only until audio rec ships.

### Auto tempo adjustment (live)

- Shipped behind feature flag, will be on by default next deploy.
- Strong user reception — Jonathan Cronk (heavy user) reportedly "can't stop talking about it."
- Selective app tour / "bespoke tooltip" introduced specifically for this feature.
- Steven (April 28): "Combined with the ability to isolate one hand or the other — every new practice tool we add, the functionality just compounds. The combinations of these different tools."
- Auto tempo adjustment will likely affect exercise atom configuration — tempo is a performance constraint; auto-adjustment is a configuration option.

### Selective app tour / bespoke tooltips (Andrew, April 28)

- New mechanism: when a feature ships and an existing user opens the app, only that feature's mini-tour appears (not the full onboarding).
- Will be used for auto tempo adjustment first, then audio recognition, then repertoire looping.
- **Implication for exercise section**: when V1 ships, the exercise section will get its own selective tour. Worth a brief design note in the spec.

---

## 5. UI/UX Considerations

### Complexity progress indicator (April 28)

The team searched for an old "personalized flow meter" mockup. Concept (Staley/Patrick described from memory):

- Small bar between the music staff and the header.
- Shows current complexity vs. goal complexity.
- User can set their own threshold ("90/95 will always be the top right, but you can decide where your threshold would be of where you would like the AI to adjust your range").
- Patrick suggested it could fill up like a progress bar.

The mockup wasn't found in Figma. May exist in a 2022 file or in the Bible. Patrick is iterating on a "hot bar" / curve concept that feeds into the chevron.

**Tension Steven flagged (April 28)**: when complexity adjustment is added, completion conditions become non-obvious. Chevrons and level finishing need new visual logic. Adding this at the same time as user-uploaded repertoire would require design coordination, hence the "do user-uploaded repertoire first" recommendation.

### Theme presets (Andrew, May 5)

Three theme modes shown:

- **Light** (current default).
- **Dim paper** (yellowed paper aesthetic — Steven wanted closer to a real-paper feel).
- **VS Code mode** (white-on-near-black, Staley's request).
- **True dark** (black-on-true-black — Patrick noted is harsh).

Andrew is open to color experimentation per Staley's request for blueish/greenish accent colors for notes.

**Implication for exercise section**: themes are global. The exercise section should use the same theming primitives.

### Lit-up keys / fingering guidance (April 28)

Patrick floated the idea of a piano view with keys lit up showing what to press. Team consensus: useful as an option, with **completion handicap** — using the lit-keys mode flags or asterisks the user's 100% completion. Steven's framing: "You don't get full credit for really knocking this song out of the park if a possibility exists that you would be cheating the whole time."

Patrick has a 3D hand model (Blender-format, ~1–2GB per hand) he bought for $50. Probably not browser-renderable. Discussion of using GPT-5.5 to generate fingering animations from input fingering data.

**Implication for exercise section**: lit-keys is a candidate display modality for some atoms, particularly kinesthetic-output ones. The handicap-flag concept would apply identically. Worth noting in the next design iteration as a configurable assistance level.

### Mobile is officially "limited"

Patrick (May 5): "I fully accepted the fact that mobile is going to be a limited experience. We'll just need to present that to the user somehow — a little note up top, hey, full disclosure, mobile doesn't have all the features."

**Implication for exercise section**: the spec should explicitly flag which exercise atoms / blueprints are mobile-supported vs. desktop-only. Andrew flagged that PRD definitions need to work across mobile, iPad, and laptop — including UX language like "tap" vs. "click." Asif is doing mobile work currently and should be in the loop on exercise spec mobile applicability.

### Forced app updates (April 28)

Andrew + Patrick noted Discord-style behavior of blocking app open until update. Currently a "putting off" item, but on the radar. Worth knowing for exercise section rollout — when V1 ships, this mechanism may be in place.

---

## 6. Team Structure & Division of Labor (Updated)

A reorganization emerged across the two meetings, primarily in the May 5 standup.

### Updated domain ownership

| Person | Primary domain | Notes |
|---|---|---|
| **Steven Gizzi** | Exercise section design | Currently producing the PRD. Continued involvement in Mage / cross-section complexity. |
| **Staley** | AI/ML infrastructure, fine-tuning, music gen, instructor portal | **Shifting away from repertoire engineering.** Will continue instructor portal in parallel. |
| **Andrew Urbanowicz** | Audio recognition (current), repertoire ownership (new), custom repertoire upload, repertoire sharing, social features | Taking over repertoire from Staley. Strong fit because Andrew is also a pianist. |
| **Patrick Boylan** | Marketing/distribution (resistantly), pitch deck, MVP decomposition, fundraising, instructor portal pressure | Has explicitly said marketing/content "does not inspire me whatsoever." Wants to do QA, dev coordination, and people management instead. Strong opinion that Earnest's instructor portal needs to ship. |
| **Asif** | Implementation (exercise section, mobile, sharps/flats fix) | Working through repertoire mobile bugs and accidentals refactor. |

### What's resolved

- **Repertoire handoff**: Staley → Andrew. Steven explicitly conditioned the AI R&D track on "successfully passing off repertoire work to Andrew."
- **Two pillars metaphor** (Patrick's framing): "Staley's domain is AI music gen / model fine-tuning, and the things that follow from that. Andrew's domain is custom repertoire, user-created repertoire, sharing of repertoire, maybe social. Two really good pillars."
- **MVP decomposition**: Patrick will handle for the exercise section once Steven delivers the macro spec.

### What's not resolved

- **Distribution / marketing ownership**: Patrick said the team agreed it should consume "25% of all our time — equate to one of us full-time," but no one has volunteered. Steven floated devoting two months of his time to mastering it but acknowledged he doesn't currently have that capacity. Patrick made clear he hates doing it. Open question.
- **Ronnie (current marketing contractor)**: contract ends end of June; she'll do July for free. Steven's blunt assessment: "the content we're putting out is not inspiring." Patrick agreed. Nobody has named a successor.
- **AI R&D vs. instructor portal balance for Staley**: Patrick wants Staley's instructor portal not to "dangle." Staley said he'll keep working on it but it's not where his energy is. Watch for slippage.

### Cultural / process notes (April 28)

Andrew opened up about a personal/property-management-driven motivation dip; Steven also acknowledged a recent dip during/after the Costa Rica trip and recommitted. Patrick asked for two team commitments going forward:
1. **More deadlines** — even soft ones. Set them, communicate them, update them when they slip.
2. **More communication** about personal-life dips so the team can absorb capacity changes.

These are general team-health items, not directly relevant to exercise section design, but they explain why Steven's deadline for the PRD is expressed as a soft optimistic/pessimistic range rather than a hard date.

---

## 7. Pricing, Tiers, and B2B (Implications for Exercise Gating)

These came up in fragments but cumulatively suggest a tier structure that the exercise section will need to integrate with.

### Tier ideas floated (May 5)

Patrick's sketch:

- **Free unlimited**: full access to Unit 1 (current course content).
- **Mid tier**: presumably current $X subscription level.
- **Premium**: $15.99 floated; would include features like custom repertoire editor, transposition, possibly other "premium" capabilities.

Steven's framing (May 5): the custom repertoire create feature "is maybe an example of something that would be on a Museflow premium tier and not the base level tier."

### Open questions for exercise section gating

- Are exercises gated by tier at all? If so, by atom, by blueprint, by training method, or by feature category?
- Does the agent / Projects feature sit at premium?
- Do user-generated and teacher-generated exercises sit behind premium?
- Does AI-generated custom exercise content sit behind premium (justified by inference cost)?

These should be open questions in the next design pass, not decisions to make immediately, but the spec should note that **gating has not been designed** so engineering doesn't bake assumptions into the implementation.

### Instructor portal & B2B (Patrick's emphasis)

- **Earnest** is a paying instructor with three students using MuseFlow. Patrick wants the instructor portal shipped so he can hand it off to Earnest.
- Earnest is being given the portal **for free** (pricing for instructors is "we'll talk about it later").
- The Arizona teacher quote (~year ago) Patrick keeps citing: she needs (1) a way to see her students' data, (2) audio recognition. Both are now within sight.
- **Grade book integrations**: 8–9 major systems used in education. Patrick sees this as a long-term institutional play.
- **Two-sided marketplace** is the long-term commercial vision (3–5 year deck): teachers ↔ students.

**Implication for exercise section**: teachers should be able to (a) see student progress on assigned atoms/molecules/strands, (b) assign specific atoms or paths to specific students, (c) eventually author and share custom exercises (using Andrew's editor). The current spec gestures at "teacher tools and assignment flows" as an open future item — this should be elevated, given the active commercial pressure to ship instructor capabilities.

---

## 8. Engagement & Re-engagement Mechanics

### AI-targeted notifications (Andrew, April 28)

> "I want to integrate a model into pulling that data and then feeding it to a customized message… proactive messages like 'hey come back and finish up, you already finished tier 2 of level 9, come and finish tier 3' — yes — 'hey it's good to practice a little bit every day, the annoying Duolingo type'… because people who are engaged aren't going to cancel."

- **Goal**: improve trial-to-paid conversion (where the team thinks the bigger gain is, vs. churn).
- **Mechanism**: doesn't need ML — simple if/else logic + cheap model call for message variation.
- **Bridge to AI track**: this is a pragmatic, cheap, near-term application of the AI infrastructure Staley wants to build. Could ship as a validation milestone before bigger music-gen efforts.

### Implication for exercise section

The exercise section should emit **engagement-relevant events** — atoms cleared, molecules completed, time-since-last-practice — into whatever event/analytics layer powers the re-engagement system. The Exercise Result schema (Decision #19) is the relevant data primitive; ensure it's logged in a place re-engagement logic can read.

---

## 9. Open Tensions & Unresolved Items

Compiled as a list of things the next conversation may need to resolve or at least decide whether to defer.

1. **Mage's long-term role**: training-data generator only (Staley) vs. permanent generative engine that AI augments (Steven). Affects roadmap, cost modeling, and how the schema is designed.
2. **Cost ceiling for LLM-based music gen**: whether quantized open-source models can hit the quality bar at acceptable cost. Staley intends to test; no plan for what to do if the answer is "no."
3. **Who owns the agentic Project system long-term**: Staley wants to build it; Patrick agrees. But where is the line between Staley's R&D scope and Steven's exercise-section scope, given that exercises are the primary assembly component of any agent-built path?
4. **Distribution / marketing ownership**: agreed to be ~25% of team time; nobody assigned.
5. **Pricing structure**: floated, not designed. Needed before exercise section gating decisions.
6. **Mage / Opus Modus terminology**: confused twice now. Worth a glossary reinforcement.
7. **Instructor portal slip risk**: Staley's stated priorities don't fully align with Patrick's pressure on shipping for Earnest.
8. **Five exercises that cover 90% of pieces** (Staley's question to Steven): not answered. Could be answered as part of the next design iteration.
9. **Mobile parity for exercises**: which atoms/blueprints work on mobile? Currently undefined.
10. **Lit-keys mode + completion-handicap flag**: agreed in principle, not designed.
11. **"Free play" as an exercise-section component**: Staley raised it in passing. Not yet in the blueprint catalog.
12. **Custom exercise generation**: agreed in principle as easier than music gen. Not yet specified — what generates what, on what trigger, with what UI?

---

## 10. Action Items & Forward Plan

### Scheduled

- **"Emergent Curriculum" brainstorm**: Thursday (post May 5) at 5pm PT. Steven, Staley, Patrick. Andrew not included (he's continuing audio rec / repertoire work). This is the Projects-direction working session.
- **Steven's exercise section PRD**: optimistic EOW May 2, pessimistic EOW May 9.
- **Andrew's audio recognition goal**: level 10 repertoire at goal tempo with 100% accuracy. Stated as "Sunday night" (April 28).
- **Asif tasks** in queue: sharps/flats refactor first (blocks transposition production rollout); then either looping cleanup or Patrick's perfect-practice-tool subtasks for repertoire.
- **Staley**: finish looping QA, then start breaking the perfect-practice tool into smaller features for Asif. Has "something deployable" on the instructor portal that needs final focus.

### Implicit, not scheduled

- **Andrew → repertoire workstream handoff** from Staley: agreed in principle, mechanics not specified.
- **Ronnie marketing transition** (end of June / July): no successor named.
- **Pricing tier discussion**: deferred but referenced multiple times.
- **Decision on Mage's role going forward**: punted ("we'll figure it out").

---

## 11. Implications for the Exercise Section Design Iteration

Distilled implications the next conversation should weigh:

1. **The agentic / Projects vision is now near-term, not far-future.** The exercise section spec should treat agent-prescribability and atom generation as design constraints, not future considerations. This means: (a) explicit assertion that atoms are agent-prescribable units; (b) explicit support for runtime atom generation; (c) richer atom metadata (prerequisites, expected time-to-clear, mastery thresholds) so an agent can plan with them.

2. **Exercise generation on demand is now a first-class capability.** Distinct from selection from a fixed catalog. The spec should call this out and lay out the interface for it (who triggers, with what input, what gets generated).

3. **Custom user/teacher-authored exercises need a design path.** Andrew's repertoire editor is the natural authoring surface. Define the data flow: editor → exercise atom → catalog entry (private/shared) → assignable.

4. **Teacher tools and assignment flows should be elevated from "open future item" to "designed for V1 or V2."** Earnest is paying. The Arizona teacher's two needs (student data + audio rec) are now both in sight. This is a near-term commercial driver.

5. **Mage / Opus Modus terminology should be reinforced in the Glossary.** Recurring source of confusion that's slowing design conversations.

6. **The Mage-future question should be flagged as an open architectural decision.** Steven's position (Mage persists; AI augments it) and Staley's framing (Mage is training-data scaffolding) are not the same. The next design iteration shouldn't bake in either assumption silently.

7. **Mobile parity should be specified per atom / blueprint.** Andrew's PRD note about including mobile/iPad/laptop language applies — the exercise section spec should explicitly mark which atoms are mobile-supported.

8. **Pricing gating should be flagged as designed-not-yet.** The schema and UX should not assume universal access; it should be possible to gate atoms, blueprints, training methods, or capabilities behind tiers when the pricing structure lands.

9. **Five-exercises-cover-90% of pieces** is worth answering deliberately as part of the spec. It's both a useful primitive for the agent and a useful framing device for an investor demo.

10. **Engagement event emission** should be specified in the spec. The Exercise Result schema needs to be readable by the re-engagement logic Andrew is building.

11. **The lit-keys + completion-handicap flag** concept should be specified as a configurable assistance level, applicable across many atoms — not just a one-off for repertoire.

12. **The "free play" interlude** Staley mentioned should be considered as a possible blueprint addition or as a path-construction primitive (i.e., the agent can intersperse free-play blocks into a roadmap).

---

## Appendix A: Quote Bank

A few high-signal lines worth preserving verbatim for future reference.

**On the Projects vision (Patrick, paraphrasing Steven):**
> "MuseFlow is an app, an experience, that decides every step for you basically. It helps you, it knows every step that you need and it knows how much you need to practice."

**On agentic UI as wrapper (Staley):**
> "Really ideally it would be just kind of a wrapper for all our UI — a way to interface… like generative UI. But really what we need is just such a rich tapestry of tooling that when you do ask it for a thing, it knows the tools to assemble out of our corpus."

**On the demo as the wedge (Staley):**
> "The hitch and the demo — being able to say, yeah, upload a piece and here's your learning pathway to it. I think that would be a pretty killer demo."

**On exercise generation being easier than other content (Steven):**
> "That level of generation is — well, see, everything gets complex when the music gets complex, but at least on the level now, that level of generation almost feels the easiest. Because it doesn't have to match stylistically something. It would be variations on scales and chords."

**On compound feature value (Steven):**
> "Every new practice tool we add, the functionality just compounds. The combinations of these different tools."

**On division of labor (Patrick):**
> "Staley's domain is the AI in the music-gen stuff, working with different models, fine-tuning. Andrew's domain is custom repertoire, user-created repertoire, sharing of repertoire, maybe social stuff. Those seem like two really good pillars for us."

**On the unique team composition argument (Patrick):**
> "Nobody else can do what we're doing right now. Two incredible engineers, one of them a classically trained pianist, a music educator and a piano performer. All of us working on this thing — that's extremely unique. And what we decide to build is inherently going to be very unique because we have an incredible amount of skill across the four of us."

**On MuseFlow's positioning (Steven, the pitch line):**
> "MuseFlow is what you do while your agents are doing everything else."

---

## Appendix B: Cross-References to Existing Documents

Items in this synthesis that connect directly to existing project documentation:

| Item | Existing Reference |
|---|---|
| Agentic vision | `05_Design_Decisions_Log.md` Decision #29; `07_UX_Navigation_Spec.md` §8 |
| Cross-section complexity language | Decision #18; `02_System_Architecture.md` |
| V1/V2/V3 phasing (V2 = complexity in exercise section) | Decision #17 |
| Exercises + Repertoire as universal pillars | Decision #16 |
| Exercise Result schema | Decision #19 |
| GMTF as existing complexity system | Decision #23 |
| Atom-as-prescribable-unit, hierarchy, custom atom creation | `07_UX_Navigation_Spec.md` §2, §8 |
| Mage / Opus Modus terminology | `04_Glossary.md` (worth reinforcing) |
| Asif as implementer | `00_Handoff_Brief.md` §5 |
| Mobile parity per blueprint / atom | Open question in `07_UX_Navigation_Spec.md` §9 |
| Teacher tools and assignment flows | Open future item in `00_Handoff_Brief.md` §4 |
| Pricing gating | Not currently in any document (new gap) |

---

*End of synthesis.*
