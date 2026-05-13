# MuseFlow Standup Synthesis: May 12, 2026

> **Status:** Reference document. Synthesized from the Granola-recorded MuseFlow standup of May 12, 2026 (~1h 54m). Captures team discussion, decisions, and tensions. Includes triage section for follow-on routing and a MuseFlow-Funnel cross-project handoff section at the end.
>
> **Participants:** Steven Gizzi (founder/CEO), Staley (CTO — rendered as "Steven Staley" in the Granola transcript; this is Staley, not a separate person), Andrew Urbanowicz (VP Engineering), Patrick Boylan (co-founder).
>
> **Context the standup happened in:** Steven closed Track C-17 (substrate-architecture refinement) the prior weekend in a long Claude.ai session, producing Decisions #56–#60 (Novelty-Automaticity Spectrum, K-Substrate Family, Semi-Lattice Engagement, Three AI Roles, Etudes + Variations), Doc 13 (Pitch Deck Register), and a slide deck. The slide deck was screen-shared on this standup; the framework content is the bulk of the call. PRD deliverable for the Exercise Section committed for EOD Friday May 15.

---

## Executive Summary

The standup mostly **validated** the Track C-17 closeout rather than evolving it. Steven walked the team through the framework via the slide deck, with Andrew (who was not on the May 7 brainstorm) hearing the Spectrum and Three AI Roles framing for the first time. The team broadly aligned. Five standup-emergent threads matter for follow-on work:

1. **Universal Affordance Symmetry as a principle.** Steven articulated, with team agreement, that "anything the AI on MuseFlow could do, a user could also do." Authoring-origin filtering (preset / user-generated / AI-generated / community-sourced) extends to roadmaps, not just atoms. This sharpens material already implicit in canon and may warrant a Decision-Log entry.

2. **Customizable advanced ATA configuration.** Jonathan's feedback drove a decision to add a configurable threshold panel next to the ATA toggle, with adjusted defaults. This is a Sight Reading feature, not Exercise; the work is Asif's next implementation task per Staley.

3. **Andrew's hierarchical agent / automation-lab demo.** Andrew showed a working self-evolving agent system (paywall lab, automation evolver) and described a MuseFlow Autonomous Universe variant. Staley challenged Andrew to autonomously build a real roadmap feature; the team picked the **repertoire uploader** as the first test case because of its clean UI-to-input mapping. This is internal-engineering track work, not design canon.

4. **Community / network effects as a strategic pillar.** Staley pushed this — shareable high scores, content marketplace (exercises / roadmaps / repertoire), and direct user-to-user discussion. Not yet canon; warrants its own track.

5. **Marketing metrics aggregation strategy.** Substantial discussion of Stripe + GSC + GA + App Store + Grafana + Mailchimp + socials consolidation, N8N evaluation, and the eventual "use Google Sheets, stop over-engineering" call. This belongs in the **MuseFlow Funnel** project (cross-project handoff in §13 below).

**No standup item contradicts Decisions #56–#60.** The team's reception of the framework was unforced and convergent — useful negative-result signal that the framework can travel beyond the Steven+Claude conversational context where it was developed.

---

## PRD Work Scope Check

**Reading order: this section first; use as a triage checklist for the EOD Friday PRD deliverable.**

### Blocking
*Nothing strictly blocks.* Steven stated on the call he is winding down ideation and that the remaining work is "putting it into deliverables" plus "a more clear understanding of what the UI of this actually looks like" (i.e., Track C2). The PRD work itself is not blocked by anything from this standup.

### Should incorporate / validate before declaring final

- **Spectrum framing (Decision #56)** as the PRD's pedagogical foundation. The team's reception confirms the framing communicates; the PRD should adopt it openly rather than treating it as background. The Exercise section is the Automaticity-pole manifestation.
- **K-substrate family (Decision #57)** affects PRD V1 catalog scope (T-021). Whether K-atoms ship in V1 alongside F/T atoms is the central scoping call. Standup did not adjudicate this; the K-family was not discussed in the call. *The PRD must take an explicit position on K-family V1 inclusion.* See Track-work §12.3 — this is the open V1-catalog-scope question Steven flagged in Doc 12.
- **Three AI Roles (Decision #59)** as the framing for how the Exercise section interfaces with future AI capabilities. The PRD should at least name which Exercise-section affordances will be Practice-Partner-controllable (auto-loop, tempo, accuracy thresholds, completion chevrons), which are Composer-Librarian-eligible (atom selection, generation on demand), and which are Coach-eligible (which exercises to assign in what order).
- **Universal Affordance Symmetry** — Steven's "everything AI does, the user can do" principle. The PRD should reflect this at the level of each agent-controllable feature having a manual equivalent. If formalized as a new Decision (see §12.1), the principle becomes a load-bearing constraint on the PRD's UI shape.
- **Customizable advanced ATA defaults and configuration panel.** Adjacent feature — appears in sight-reading mode primarily, but if the Exercise section invokes ATA, the PRD should reflect the new configuration model rather than the old fixed-threshold model.
- **"Composer dashboard" → "Repertoire Builder" rename.** If the PRD references this surface, use the new name. Decision #34 references should be amended in a follow-on canon-edit pass; for the PRD use the current name.

### Can safely defer

- All marketing / funnel discussion (separate project — see §13).
- Andrew's automation-lab / hierarchical agent architecture (internal engineering track; not a Exercise-section input).
- Repertoire uploader as agentic stress-test (internal engineering process choice).
- Camera tracking, AR/VR, branded hardware speculation.
- Neural 3D visualization of roadmaps (V3+ speculation).
- iPad black screen bug, JavaScript console errors, QA hiring, iPhone purchase, data-fixes work.
- Community/network-effects pillar — strategically important but its own track; not PRD-shaped.
- Etudes + Variations (Decision #60) — repertoire-mode AI generation, not Exercise mode. Unless the PRD discusses cross-mode generation, this can sit out.

### One judgment call worth surfacing

The PRD's V1 catalog scope (T-021 in Doc 12) is the most consequential remaining call. K-family inclusion / exclusion will shape the catalog's center of gravity. *This is your call to make before Friday and worth deliberating explicitly rather than absorbing implicitly.*

---

## 1. Strategic Framework — Team Alignment on the Track C-17 Closeout

Steven shared the slide deck Claude produced over the weekend. He framed it as informal (uses internal jargon, skipped slides he didn't want to explain). Despite that framing, the team engaged seriously and the framework concepts landed.

### 1.1 Novelty-Automaticity Spectrum reveal

Steven introduced the Spectrum to Andrew (who hadn't been on the May 7 brainstorm) by walking through site reading = novelty, exercises = automaticity, repertoire = synthesis. He explicitly connected this to the original "songs vs. skills" pitch evolution: "what we were positioning ourselves as is, like, the sight-reading app" → matured framing is the all-encompassing ecosystem managing both poles.

No pushback. Andrew received it as new information; Patrick and Staley already had context from the prior session.

### 1.2 The Three AI Roles

Steven explained the Coach / Composer-Librarian / Practice Partner framework with concrete examples for each role. The Practice Partner example landed especially well: *"like me sitting next to my piano student at the piano. They're playing and… 'Great job. We're going to try it again. Let's narrow in on this second line because we were having some trouble there. I'm going to set up auto-loop. Boom, done. Let's isolate the left hand. I'm going to bring your tempo down 20 BPM. Let's try it three times. Ready?'"* Patrick: *"So cool."*

Staley reinforced AI-optionality: *"they don't have to necessarily use the like interactive thing… you can go manual you can go automatic… at every level there's a place you can choose to make it more automated or not."* This validates Decision #41's Path Modes architecture and the AI-averse-user constraint, both of which were already canon.

### 1.3 Shapeless Content / one generator, three policies

Steven surfaced this on the call, attributing it to the slide deck's "heady" backing: *"at, like, up in the ether like the music generation is, like, shapeless basically — like it can take the form of an exercise or a piece of repertoire or a site reading or whatever… it's kind of all the same fundamental atoms at the bottom. The shape that it takes is more about the pedagogical need and not, like, as much the music itself."* This is Decision #56's Shapeless Content corollary, presented to the team. No pushback.

### 1.4 Etudes + Variations on a Theme — minor live debate

Patrick pushed back on the broader "AI generates repertoire" framing: *"It can't create from nothing. It needs something to variate on or iterate on."* He proposed simplifying-repertoire should be a third explicit goal alongside etudes and variations; Steven folded simplification into Variations on a Theme. **Aligned with Decision #60 as written**; the standup did not produce a refinement requiring an amendment.

Staley raised the contrarian case: *"why couldn't it generate from nothing?"* and suggested testing with Beethoven's full corpus as input. The conversation acknowledged: feeding a corpus is "not from nothing." The point Staley made — that sheet-music-input AI may behave very differently than audio-based generative AI — is true and worth holding, but does not contradict Decision #60.

Patrick volunteered a useful framing: *"the reason why we created etudes in the first place was because we never had the option or the opportunity to generate an infinite amount of sheet music working a very specific skill — that's why we created songs that exercise specific skills."* This is consistent with the etude positioning in Decision #60 (etudes as composed exercise-bordering-on-music).

### 1.5 The "tooling ecosystem" framing

Steven articulated the broader product framing during the call: *"think of MuseFlow as a tooling ecosystem… the ecosystem can be used by the user manually or can be used by the AI autonomously."* He proposed two parallel work tracks: continuing to build out the tooling (Repertoire, Exercise, Sight Reading sections) and building an AI system that can use the tooling.

This is the same framing as Doc 13 §2.1 ("MuseFlow as Tooling Ecosystem") and is now confirmed as the team's working model for both product and pitch.

### 1.6 Universal Affordance Symmetry — new wording, possibly new principle

Steven's emphasis: *"there really is nothing that the AI on MuseFlow could do that a user could not also do."* He extended this to roadmaps explicitly: roadmaps come in **preset / user-generated / AI-generated / community-sourced** flavors, just like atoms and other content. Patrick: *"I like that."*

This is sharper than what currently exists in canon. Decision #34 covers `authoring_origin` for atoms; the extension to roadmaps is implicit but not articulated. The framing principle — that the AI does nothing the user can't also do — is a load-bearing constraint that touches Decision #29 (Agentic Vision), Decision #41 (Content/Path Modes), Decision #59 (Three AI Roles), and the entire AI-averse-user constraint. **Candidate Decision #61 — see triage §12.1.**

### 1.7 Power-user graph navigation vs. user-facing simplification

Steven articulated the design tension: *"any exercise would have like its primary focus which is say like a scale… but there are also technique, there's technique built into that — you're going to have to do some pivoting, partially training pivoting, partially training finger dexterity, partially training, you know, various other finger movements… there's a lot that goes into it that would be adjacent nodes on a graph that the agent would be picking up on."*

This is Decision #58 (Semi-Lattice Engagement) made concrete — the agent reasons over the full engagement graph; the user gets a simpler filter/browse surface. Confirmed framing, no contradiction.

Patrick's reaction: *"it's just data science, baby."* (Said with affection.)

---

## 2. Standup-Emergent Material Worth Promoting to Canon

These are items the standup surfaced that are not yet in Decisions #56–#60 or the existing canon, organized by candidacy strength.

### 2.1 Universal Affordance Symmetry (strong)

The principle: *for every AI capability in MuseFlow, the equivalent capability is available to the user manually.* This is more than the AI-averse user constraint (which is about user opt-out); it's about feature-design parity. The PRD and all subsequent design work operate within this constraint. **Decision-candidate #61.**

### 2.2 Authoring-origin filtering at every level of the hierarchy (medium)

Decision #34 establishes `authoring_origin` for atoms. The standup confirmed the same filtering applies to roadmaps. The natural extension is to apply it consistently at every hierarchy level where authored content lives (atoms, blueprints, training-method preset configurations, roadmaps, paths, Projects). **Likely a canon-edit to Decision #34 with cross-references to Doc 07's hierarchy section.**

### 2.3 Community / network effects as a strategic pillar (medium — needs scoping)

Staley: *"B2C apps just require the shareability of the network effects… if we're not focusing on that, we're, it's a mistake in my opinion."* The team agreed in spirit. Steven extended: a content/roadmap/exercise marketplace adds the strongest value.

This is strategically consequential but not yet shaped enough to be a Decision. **Track-candidate** — needs a scoping pass before a Decision is appropriate.

### 2.4 Adjustable ATA configuration model (narrow but settled)

Decision: a configurable advanced ATA panel (icon next to the toggle, drop-down) that exposes increase/decrease thresholds and (possibly) speed-aware defaults. Asif's next implementation task. **Narrowly scoped; closer to a canon-edit / DEF-row than a full Decision.** Sight Reading mode primarily; relevant to Exercise mode only if exercises invoke ATA.

### 2.5 Repertoire builder / composer dashboard naming (canon-hygiene)

Andrew used "composer dashboard"; Steven corrected — *"don't call it the composer dashboard. That's something else."* Patrick proposed "repertoire builder" / "repertoire creator." Team agreed on **Repertoire Builder**. Steven later noted *"I guess it is kind of a composer dashboard"* (reflecting Patrick's framing of "compose anything → send to whatever department"), but the working name is Repertoire Builder.

Decision #34's amendment history references this surface under multiple names. **Canon-edit: standardize on "Repertoire Builder" across Doc 04 (glossary), Doc 06 (blueprints), and any Decision-Log entries that name it.**

---

## 3. Agentic Engineering Track — Andrew's Automation Lab

Andrew demoed a working self-evolving agent system he built outside MuseFlow ("for Insight" originally) and described how a MuseFlow Autonomous Universe variant has been started.

### 3.1 The system

- **Paywall Lab**: a per-feature scaffold with metrics, variance tracking, and Codex auto-generating PRs that iterate the feature based on metric performance.
- **Automation Evolver**: a top-level agent that accepts plain-text feedback ("we want to add an exercise section") and decomposes it down through domain agents to specific implementation tasks. Higher agents carry business goals + branding + design context; lower agents carry domain-specific objectives.
- **Self-recurring loop**: agents update their own files; nodes spawn nodes; the system grows itself.

Steven recognized the structure: *"You're talking about an ecosystem of agents that autonomously essentially are structured in a similar way to an actual company."* Andrew confirmed: *"exactly that."*

Andrew compared to NAD (which Staley raised). NAD has agent workflows over data inputs but, per the brief discussion, may not have the same self-evolving-system-improving-systems structure.

### 3.2 Business builder vs. front-end experience — critical distinction

This is the most important architectural clarification of the discussion. Steven: *"I was wondering at first, Andrew, if you were bringing this up as a model for how to do the actual MuseFlow AI, like, not how we build it, but the actual system that's in the app."* Andrew clarified: **two separate systems.**

- **Business Builder** (Andrew's automation lab) — the agentic system MuseFlow's team uses to develop MuseFlow itself. Internal infrastructure.
- **Front-End AI / Feature Experience** — the agentic system inside the MuseFlow product, mediating between users and features. This is what Decision #59 (Three AI Roles) describes.

The Business Builder is unrelated to the Three AI Roles framework. Reusable architectural patterns may emerge, but they are not the same system.

### 3.3 Staley's stress-test challenge

Staley: *"I would challenge you, Andrew, to try to build any of the things on our road map that we actually want to build, completely autonomously with an agent."* Andrew accepted. Staley's reservation: the Business Builder will likely do well on standard UI (forms, dropdowns, CRUD) and poorly on Phaser-based interactive game components — *"the things we actually care about are, like, the unique music-education UI features of our app."*

### 3.4 First test case: Repertoire Uploader

Team converged: the Repertoire Uploader (the new name for the composer-dashboard surface — see §2.5) is the cleanest test case because Music XML → UI rendering is a one-to-one mapping. Patrick: *"It's a one-to-one mapping… music XML lines of code into how it looks on UI."*

Andrew's strategy: build the first feature with extra base-layer scaffolding (~20% longer than usual), then test whether subsequent adjacent features (repertoire-domain features) replicate the pattern. If yes → replicable model for other domains.

### 3.5 Feedback mechanisms and self-evaluation

Andrew described the workflow he uses for his own agentic work: when an agent takes 10 iterations to solve something, he has the agent retroactively extract the pitfalls and bake them into the spec/MD files for next time. This compounding documentation is the lever for getting better results over time. Echo of the project's own working-conventions principle around upfront documentation paying off.

### 3.6 Mode-of-work observation

Steven described his current workflow on the call: ideation → adversarial review → Claude builds roadmaps → sprints decomposed into context-bounded sessions → human-in-loop approval at session boundaries. Not autonomous, but enables high multitasking. Andrew confirmed similar patterns. This is informational; not actionable.

---

## 4. Exercise Section / PRD Status

Steven's update was short. *"All of that to say, the agentic vision goes hand in hand with the exercise section design… you can build the exercise section on its own regardless of whether or not we have AI implemented, but it informs how we build the exercise section."*

- Ideation is winding down.
- Remaining work: putting design into deliverable form (the PRD) and resolving the UI-shape question (Track C2 in the working-conventions document).
- Target: **EOD Friday May 15**.
- Format: a "well-documented design brief" — Steven explicitly noted he is not the designer and doesn't need to produce the final design, but the brief should be sufficient for a designer to work from.
- Post-PRD: Patrick takes MVP decomposition. Asif is the likely implementer.

No standup item changes the PRD scope materially. The PRD work proceeds.

---

## 5. Customizable Advanced ATA Configuration

Driven by Jonathan's two-week feedback loop on ATA thresholds. Decision on the call:

- Add a **configurable advanced panel** behind an icon next to the ATA toggle.
- Panel exposes user-controlled threshold settings for both tempo increase and tempo decrease behavior.
- Default parameters need adjustment based on Staley's observations: at slower playing speeds, the current defaults don't trigger tempo decrease appropriately. Possible adjustment: speed-aware defaults (faster playing → lower threshold).
- Asif's next implementation task per Staley (after wrapping current work and pending the data fixes that are blocking new feature work).

This is Sight Reading mode functionality. Exercise-section impact: limited, unless the PRD specifies that exercises invoking ATA inherit this configuration model.

---

## 6. Pitch Deck Status

Brief update from Patrick at the top of the call.

- **15-page cap** explicitly reaffirmed. *"We just can't, like, add more slides because nobody's going to want to f***ing see a pitch deck that's 20 pages long."*
- Robin (advisor) provided notes; awaiting Staley's notes (Staley owes ideas on one specific slide).
- Patrick framed the deck as **iterative**: not a beall-endall; will iterate based on investor feedback after first contact.
- Patrick committed to keeping Steven's framework material (Spectrum, Three AI Roles, etc.) for future deck iterations or for use directly in investor conversations.

Doc 13 (Pitch Deck Register) is unaffected by this update; the 15-page cap is a deck-assembly constraint, not a register constraint.

---

## 7. Audio Recognition & iPad Build Issues

Andrew's update.

- **Yellow notes issue mostly solved** (note-offset problem from prior conversations).
- **MuseScore preference over Sibelius**: Andrew using it more; Steven: *"MuseScore is the one of the future. I think more and more people are going to use it. Sibelius, I think, is old news."* Strategic input but no immediate canon impact.
- **Build 103** (TestFlight) had a black-screen issue on iPad: app installs from TestFlight, shows black on launch. Replicable across at least two devices (Andrew's iPad, Patrick's iPad).
  - Suspected root cause: B64 audio fallback handling on startup.
  - **Build 104** going to TestFlight with the fix.
  - Staley: *"this is why we QA."*
- **JavaScript errors not surfacing in the ROM console** — separate issue Staley flagged. Errors are supposed to push to the dev or prod dashboard depending on build type; not showing up means either a config issue or the dashboard layout change broke something. Staley asked Andrew to investigate.

---

## 8. Data Integrity Work

Staley's update at the end of the meeting.

- Set up a **bastion ECS for backend database access** plus a new **read-only prod role for agents**.
- During initial agent setup, Claude proposed an anomaly-detection agent. It surfaced significant data issues:
  - Duplicate events in various places.
  - Trial-related events poorly tracked (trial started, subscription started, trial ended, subscription ended).
  - Tutorial chapter-finish stuff "wasn't great."
  - Some attributes stored in incognito mode rather than DB.
- **Halt-new-features-until-data-fixes**: *"I don't want a CIF to land anything until we get that out because, like, that's just number one priority."* The looping cleanup Patrick requested is also blocked behind this.
- **Patrick's looping fix** wanted released this week is delayed pending the data fixes finishing.

This decision affects engineering velocity broadly and the marketing-data work in §13 specifically.

---

## 9. Operations, Hardware, Hiring

- **iPhone purchase for Asif**: mid-tier current-model iPhone (around $400 for an iPhone 15). Steven raised the question of mid-tier-current vs. older-for-legacy-testing; Staley landed on mid-tier-current as the right balance. Mobile parity work can't be validated only in web views.
- **Asif's next assignment**: the customizable advanced ATA section from §5. Possibly complexity-adjustment work after that.
- **QA hire**: Staley reached out to a candidate from the Baltimore Code and Coffee Slack channel; interview tomorrow (May 13). Local hire preferred for hardware-shipping logistics.
- Staley's earlier Elena (girlfriend's sister) hire attempt didn't work out.

---

## 10. Speculative / Future Visions Surfaced but Not Committed

Captured here so they don't fall out of the conversation but explicitly flagged as not-yet-canon.

- **Camera-based hand tracking** (Staley's "crazy idea"): coach watches your hands via webcam; power-user feature initially; piano setup is the practical constraint. Steven: *"I would push for it."*
- **AR/VR integration** (Patrick): the natural home for camera-based hand observation when the form factor matures.
- **Branded hardware / white-label piano camera** (Staley, half-jokingly): MuseFlow-branded camera mount; sourceable from China with custom CAD. Steven didn't engage seriously; Patrick was open.
- **Neural 3D / knowledge-graph visualization of roadmaps** (Andrew): instead of a 2D roadmap list, render the user's music-education universe as a graph; nodes represent learned material; new feature additions appear as new buildings/structures. Staley: *"I think there is room for a graph-rag database for our agents for sure, and actually I think that is probably what it's going to look like for the back of all of the agents… but it's not going to be viewed in that way by a user."* Steven: middle-ground visualizations leveraging knowledge-graph approaches (like Obsidian's graph view) may be the right user-facing form.
- **10–15 year vision** (Staley): every job will be a person in front of an agentic dashboard telling agents what to do. Cultural-context observation, not actionable.

---

## 11. Quote Bank

A handful of lines worth preserving for the design-canon or pitch-deck-register pipeline.

**On Universal Affordance Symmetry (Steven):**
> "There really is nothing that the AI on MuseFlow could do that a user could not also do."

**On the tooling ecosystem (Steven):**
> "Think of MuseFlow as a tooling ecosystem… the ecosystem can be used by the user manually or can be used by the AI autonomously."

**On the Practice Partner (Steven, illustrating the role):**
> "'Great job. We're going to try it again. Let's narrow in on this second line because we were having some trouble there. I'm gonna set up auto-loop. Boom, done. Let's isolate the left hand here because that was the main problem. I'm going to bring your tempo down 20 BPM. Let's try it three times. Ready? Start whenever you're ready.'"

**On the substrate graph (Steven):**
> "It's just data science, baby." — *(Patrick echoed it back affirmatively.)*

**On the etudes/sheet-music framing (Patrick):**
> "The reason why we created etudes in the first place was because we never had the option or the opportunity to generate an infinite amount of sheet music working a very specific skill — that's why we created songs that exercise specific skills."

**On AI-optionality (Staley):**
> "At every level there's a place you can choose to make it more automated or not automated."

**On community as load-bearing (Staley):**
> "B2C apps just require the shareability of the network effects… if we're not focusing on that, we're, it's a mistake in my opinion."

**On the engineering trade-off (Steven, paraphrasing the room):**
> "How long would it take to build up this system to the point where it's functioning well and is not just a pain in the ass and is actually saving us time — versus us building the things ourselves."

**On AI-mediated workflows (Staley):**
> "I find it hard to imagine a world that's, like, 10–15 years from now where, like, every job isn't just, like, a person in front of an agentic dashboard telling agents what to do."

---

## 12. Triage

Every substantive item from the standup, classified. One sentence of rationale per item plus proposed action. Items may appear in multiple buckets (e.g., the marketing-metrics decisions appear under §12.6 Funnel and are not double-classified here).

### 12.1 Decision-Log candidates

| # | Item | Rationale | Proposed action |
|---|------|-----------|-----------------|
| D-A | **Universal Affordance Symmetry** | Steven's "every AI capability is also a user capability" principle is sharper than current canon and is load-bearing for both PRD and product positioning. | Open a follow-on track to author Decision #61 (Universal Affordance Symmetry) with proper rationale + cross-references to Decisions #29, #34, #41, #59. |
| D-B | **Customizable Advanced ATA Configuration** | The team made a settled product call (configurable panel + adjusted defaults); this is feature-design-consequential, not just an implementation detail. | Open a small follow-on track for Decision #62 (Adjustable ATA Configuration Model) scoped to Sight Reading mode, with explicit note on default-parameter adjustment work. Likely lighter-weight than D-A. |

Two candidates total. Other items below (#15-page cap, halt-new-features, repertoire-uploader-as-test-case, Google-Sheets) are *not* Decision-Log candidates because they are process / engineering / cross-project calls, not architectural design canon.

### 12.2 Canon-edit candidates

| # | Item | Target | Proposed edit |
|---|------|--------|---------------|
| C-A | Repertoire Builder naming (was "composer dashboard") | Decision #34 amendment, Doc 04 (Glossary), any other doc that names this surface | Standardize on "Repertoire Builder." Add Glossary entry. Amend Decision #34's references. Check Doc 06 (blueprints). |
| C-B | Authoring-origin filtering at every hierarchy level (not just atoms) | Decision #34 amendment or new amendment block | Extend `authoring_origin` semantics to roadmaps and any other authored hierarchy levels. Cross-reference Doc 07's hierarchy section. |
| C-C | Spectrum-driven framing as PRD-shaping principle | None — this is just confirmation that Decision #56 is operative for PRD work | No canon edit; informational reinforcement. |
| C-D | Three AI Roles as pitch device | Doc 13 §2.2 may benefit from a note that the team has validated this as a pitch-deck device | Light edit to Doc 13: note team alignment May 12. |
| C-E | "MuseScore is the future, Sibelius is old news" | Doc 04 (Glossary) for MuseScore/Sibelius/Opusmodus terminology, if not already there | Optional. Useful context for future engineering choices; not load-bearing. |

### 12.3 Track-work candidates

| # | Item | Existing track / new track | Work-unit shape |
|---|------|----------------------------|-----------------|
| T-A | **Community / network effects pillar** | New track — call it Track G (Community & Network Effects) | Scoping pass: shareable artifacts (high scores, roadmaps, exercises, repertoire); marketplace structure; community discussion surfaces; user-to-user content discovery. Pre-decision shaping; not yet a Decision. |
| T-B | **Decision #61 Universal Affordance Symmetry authoring** | Follow-on to this synthesis | Decision-Log entry + Doc 07 cross-reference work. ~1 short session. |
| T-C | **Decision #62 Adjustable ATA Configuration authoring** | Follow-on to this synthesis | Decision-Log entry + cross-references; smaller than D-A. |
| T-D | **Canon-edit pass from C-A, C-B, C-D** | New small canon-hygiene track | Targeted edits across Decision #34, Doc 04, Doc 13. ~1 session. |
| T-E | **PRD authoring (Track E)** | Already queued | Steven's owned work, EOD Friday. Pure execution; this synthesis informs but does not displace. |
| T-F | **Track C / C2 / D dependencies** | Already queued | Still queued; this synthesis confirms the V1 catalog scope (T-021 in Doc 12) as the central remaining call. C-17 substrate-architecture refinement closed pre-standup; no new architectural decompositions surfaced. |

### 12.4 Open questions (candidates for Doc 12)

If accepted, these get added to Doc 12 in a follow-on. None resolved on the call.

| # | Question | Cluster |
|---|----------|---------|
| Q-A | How does Universal Affordance Symmetry interact with pricing tier gating? (If certain AI capabilities are paid-tier, does the manual equivalent also gate behind paid? Or only the AI mediation?) | C-14 pricing |
| Q-B | What's the V1 surfacing model for AI-generated vs. community-sourced vs. user-generated vs. preset content discrimination? (Visual badges? Filter chips? Faceted browse?) | C-15 UI shape / authoring-origin |
| Q-C | Where do K-substrate-family motor drills fit relative to "etudes" in the Repertoire mode? (E.g., a Hanon exercise is a K-atom in the Exercise mode; a composed motor-development etude is a Repertoire-mode item with K-family training intent. The boundary needs framing.) | C-17-extension / substrate-architecture |
| Q-D | Should adjacent-substrate engagement weights (Decision #58 semi-lattice) be exposed to the user-facing filter UI in any form, or kept agent-only? | C-15 UI shape |
| Q-E | What is the V1 scope for community/marketplace shareable artifacts? (None? Roadmaps only? Exercises? Full content?) | New cluster — Community |
| Q-F | When camera-based hand tracking becomes feasible, where does it sit in the Three AI Roles model — Practice Partner (in-session observation) or Composer-Librarian (input modality)? | Speculative — V3+ |

### 12.5 Internal-engineering (no canon impact)

| # | Item | Owner |
|---|------|-------|
| E-A | Andrew's automation lab / Business Builder system | Andrew |
| E-B | MuseFlow Autonomous Universe (backend agent system) | Andrew |
| E-C | Repertoire uploader as agentic stress-test | Andrew (Staley stress-tester) |
| E-D | Staley's bastion ECS / read-only prod role for agents | Staley |
| E-E | Halt-new-features pending data fixes (looping cleanup blocked) | Staley enforcement; Asif affected |
| E-F | Anomaly detection agent + duplicate-event/trial-event fixes | Staley |
| E-G | iPad black screen bug (B64 audio fallback) — build 104 fix | Andrew |
| E-H | JavaScript console errors not surfacing in ROM console — investigation | Andrew |
| E-I | iPhone purchase for Asif (mid-tier current model) | Staley |
| E-J | QA hire interview (Baltimore Code and Coffee candidate) | Staley |
| E-K | NAD / N8N infrastructure evaluation for agent workflows (separate from marketing-metrics evaluation) | Staley exploring |
| E-L | Engineering infrastructure focus (agent definitions, skills, files, knowledge structure) | Staley |

### 12.6 MuseFlow Funnel — cross-project handoff

Treated in full in §13 below. Summary placement: marketing metrics aggregation (Stripe + GSC + GA + App Store + Grafana + Mailchimp + socials), Google Sheets decision, N8N evaluation, Patrick's analytics access commitment, social account access verification, read-only prod DB role usage for marketing analytics, anomaly-detection findings affecting marketing data quality, halt-new-features impact on marketing-data downstream.

### 12.7 Informational only

| # | Item |
|---|------|
| I-A | Casual opening (Devil Wears Prada discussion, Meryl Streep / Jason Statham comparison, meeting-screen ergonomics jokes) |
| I-B | Patrick's pitch-deck status update (Robin's notes pending, Staley's notes pending, iterative, 15-page cap reaffirmed) |
| I-C | Steven's workflow description (ideation → adversarial review → sprints → session-bounded execution) |
| I-D | Andrew's MD-doc-iteration workflow approach |
| I-E | Hardware/camera/AR-VR speculation (all V3+) |
| I-F | Neural 3D visualization speculation (V3+) |
| I-G | 10–15 year agentic-dashboard cultural prediction |

---

## 13. MuseFlow Funnel — Cross-Project Handoff

> **Note to the Claude.ai project this section gets pasted into:** The author of this section is working in a separate project ("MuseFlow Exercise Section + Agentic Future") that focuses on product design. This handoff contains everything from a May 12, 2026 MuseFlow team standup that touches funnel, marketing, data, and analytics — material that belongs in *this* (Funnel) project rather than the design project it came from. The Funnel project has not heard any of this discussion before, so context is provided inline.

---

### 13.1 What this handoff covers

The May 12, 2026 MuseFlow team standup (~1h 54m) included a substantial discussion of marketing metrics aggregation, data integrity work, agent-mediated analytics, and platform/tool selection for the marketing-data pipeline. This section captures all of it. Several adjacent product-positioning concepts came up that are useful for marketing-funnel copy and positioning; those are summarized in §13.5.

### 13.2 Participants and context

- **Steven Gizzi** (founder/CEO) initiated the marketing-metrics conversation.
- **Staley** (CTO) drove the platform-and-tooling decisions.
- **Patrick Boylan** (co-founder) holds access to most external accounts (Google Analytics, social media, etc.) and committed to provisioning access.
- **Andrew Urbanowicz** (VP Engineering) contributed agent-driven feedback-loop perspectives.

Steven has been building a Google Sheet for marketing metrics. The standup question was *whether to over-engineer (Python scripts / N8N / custom dashboards) or stay with Google Sheets and progressively automate.*

### 13.3 Platforms and data sources

Steven enumerated the platforms with metrics relevant to MuseFlow:

| Platform | Metrics | Notes |
|---|---|---|
| **Stripe** | MRR, subscription distribution, trial events | Patrick: has an API. Already actively pulled for data-fix work (see §13.7). |
| **Google Search Console** | Organic search performance | Patrick: has an API. |
| **Google Analytics** | Web traffic, user behavior | Patrick: has an API. Steven needs access provisioning; the link Patrick previously sent didn't work. |
| **App Store** | Downloads, ratings, in-app metrics | Manual or API? Not adjudicated on the call. |
| **Grafana** | User play data, in-app behavior, engagement | Internal MuseFlow infrastructure. |
| **Mailchimp** | Email opens, click-through, list growth | Patrick: has an API. |
| **Social media** (TikTok, Instagram, X, etc.) | Reach, engagement, follower counts | Steven needs to verify access on all accounts. |
| ~~Google Ads~~ | ~~Ad spend, conversion~~ | **Patrick: not running ads currently.** Remove from V1 aggregator. Keep slot in schema for future re-enablement. |

### 13.4 Aggregation strategy — what was decided

The team worked through over-engineering vs. lightweight options:

1. **Initial impulse**: build a real database (RDS), pull data via Lambdas, build a dashboard. *"Cute little Python scripts."*
2. **Mid-discussion shift**: Staley suggested **N8N** (an agentic workflow tool) — *"let's try it first with N8N."* N8N can run locally on a cluster or via cloud subscription. Staley considered spinning up an N8N instance in the existing ECS cluster so it could also touch the production database (via the new read-only role; see §13.6).
3. **Final decision**: **Google Sheets** is the V1 aggregator. Patrick: *"I like a Google Sheet. I'm cool with that too."* Staley: *"Maybe just use a Google Sheet. That's fine. We're overengineering this."*

**Rationale:** Most of the source platforms have APIs that can populate Google Sheets directly. The aggregation tier doesn't need its own database for the V1 marketing-feedback loop. Airtable was mentioned as an equivalent alternative but no preference was articulated.

**Layered approach implied (not explicitly stated):**
- Layer 1 — Google Sheets with API populations (or N8N / Zapier automations populating it).
- Layer 2 — N8N or similar runs automations on top of the Sheets for derived metrics, anomaly detection, content/marketing triggers.
- Layer 3 — eventual migration to a real database if/when complexity warrants.

**Action items from this:**
- Steven to **investigate N8N** (free self-hosted version vs. cloud version).
- Steven to **research alternative aggregation/automation tools** alongside N8N.
- Patrick to **sync with Steven (next day, May 13)** to provision access to Google Analytics + any other accounts Steven doesn't have. *"Just shoot me a DM and we'll make it happen."*

### 13.5 Adjacent framework material useful for funnel/marketing positioning

The standup spent the first hour on a product-positioning framework that has implications for how MuseFlow markets itself. The framework concepts were locked in a separate working session prior to the standup and are now canon in the product-design project. Brief explanations follow because some are directly usable in marketing copy.

#### 13.5.1 The Novelty-Automaticity Spectrum

MuseFlow's pedagogical positioning. Skill acquisition operates between two poles:
- **Novelty** — content never repeats; trains the ability to apply skills to unseen music (this is what sight-reading apps train).
- **Automaticity** — content repeats with varied performance constraints; trains automatic execution (this is what drill apps train).

**The marketing line:** *Most apps live at one pole. MuseFlow operates the entire spectrum deliberately.* MuseFlow's three content modes (Sight Reading, Exercises, Repertoire) are distinct manifestations of the Spectrum — Sight Reading at the Novelty pole, Exercises at the Automaticity pole, Repertoire at the synthesis midpoint. This framing has investor-narrative utility ("we found the missing piece in the category") and SEO utility (we can write authoritatively about the pedagogical research behind it).

#### 13.5.2 The Three AI Roles

How AI works inside MuseFlow. Not one agent — three roles drawn from how a real teacher operates:

- **The Coach** — knows your goals and journey; maintains your skill profile; converses with you; composes personalized roadmaps; adapts when you go off-plan.
- **The Composer-Librarian** — creates and curates the right music for you; sources from libraries, generates new content on demand, modifies existing content (e.g., simplifies a piece to your current level).
- **The Practice Partner** — in every session with you; controls tempo, accuracy, looping in real time; surfaces hints; senses frustration / boredom / flow state.

**The marketing line for product pages and pitch-deck adjacents:** *MuseFlow's AI plays three roles you'd recognize from any great teacher: a coach who knows your goals, a composer-librarian who creates and curates the right music, and a practice partner who's in every session with you.* Each role has its own pitch sub-narrative.

#### 13.5.3 Etudes + Variations on a Theme

How AI-generated content shows up. MuseFlow's AI does not generate music "from nothing" — it generates **etudes** (composed musical material with explicit training intent, in the tradition of Czerny etudes) and **variations on a theme** (simplifies or complexifies existing repertoire so a learner can engage with real music at their current level rather than waiting until they "deserve" it).

**The marketing line:** *MuseFlow's AI doesn't try to replace composers. It writes the kind of music musicians have always written when they wanted to train a skill: studies, etudes, simplified versions of real pieces. Real music, made approachable.*

This framing matters because the marketing voice cannot afford to overclaim ("AI-composed masterpieces"). It also defuses the common skepticism around AI-generated art.

#### 13.5.4 The Tooling Ecosystem framing

MuseFlow is positioned as a **tooling ecosystem** for piano learning — composable by users manually or by AI automatically. The ecosystem is the product. Individual modes (Sight Reading, Exercises, Repertoire) are components within it.

**The marketing line:** *The ecosystem itself is the product.* This is the load-bearing positioning principle: MuseFlow's value is the integration of capabilities, not any one capability in isolation. Marketing copy should reflect this — pages that pitch single features in isolation will under-sell the proposition.

#### 13.5.5 Community / network effects as strategic pillar

Staley pushed on the call that MuseFlow needs community / shareability features for organic growth. Examples discussed: shareable high scores, user-to-user content marketplaces (exercises, roadmaps, repertoire), discussion of progress. *Not yet built. Not yet on the roadmap formally.* But the team aligned in principle.

**Marketing implication:** any landing-page copy that touches "community" or "network" should be written knowing that community features are aspirational at this stage. Better not to over-promise. When community surfaces ship, they become marketable.

### 13.6 Read-only production database access for agents

Staley set up a new read-only role in the production database specifically for agent-driven analytics. This is significant for the marketing-data pipeline because it means:

- Agentic workflows (N8N or otherwise) can be granted backend-database access without the risk of write-side mutation.
- Anomaly detection, behavioral cohort analysis, and engagement metric derivation can be done by agents operating directly against prod data.

Staley's framing of the dual use case: marketing analytics + user-play-data analysis. Patrick's question — *"could it do both if we cloned N8N and brought them into two separate environments?"* — was not formally answered but the implication is yes.

### 13.7 Data integrity work currently underway

Staley reported the anomaly-detection agent (created during his initial agentic experimentation) surfaced significant issues with the existing event data:

- **Duplicate events** in multiple places.
- **Trial / subscription event tracking** poorly maintained: trial-started, subscription-started, trial-ended, subscription-ended events all had problems. Staley is regenerating these from Stripe data directly.
- **Tutorial chapter-finish events** weren't tracking well.
- **Some attributes were stored as incognito-mode** instead of in the database.

The cleanup is in progress. Staley's data lake / Athena split-architecture has been abandoned in favor of consolidating everything back into the main RDS.

**Implication for marketing-data work:** the marketing data pipeline depends on event-data integrity. The current state of those events is not reliable. The marketing pipeline should not depend on these events until Staley's fixes ship.

### 13.8 Halt-new-features-until-data-fixes

Staley enforced a freeze: *"I don't want a CIF to land anything until we get that out because that's just number one priority."* The looping cleanup Patrick wanted shipped this week is delayed behind this. Bug fixes are still allowed.

**Implication for marketing-data work:** the data fixes are the blocker for any meaningful marketing analytics work — if event data is unreliable, the metrics built on top of it are unreliable.

### 13.9 Patrick's analytics access commitment

Patrick committed on the call to sync with Steven (May 13) and provision access to all the platforms Steven doesn't yet have access to:

- Google Analytics (the prior link didn't work)
- Any social media accounts Steven needs login for
- Any other platforms where Steven is locked out

**Sync trigger:** Steven to DM Patrick.

### 13.10 Social media account access verification

Steven flagged a need to verify his own access status across all the social media accounts MuseFlow operates. Inventory implied (not enumerated on the call): TikTok, Instagram, X, possibly YouTube and others. This is a prerequisite step before the metrics aggregation can include social platforms.

### 13.11 What this project should do next

A working starting prompt for this Funnel project:

> **Goal:** Stand up a V1 marketing-metrics aggregation system in Google Sheets, populated by API-driven automations (N8N or simpler), covering Stripe, Google Search Console, Google Analytics, App Store, Grafana, Mailchimp, and major social platforms. Treat this as the substrate for a future content-planning / marketing-funnel feedback loop.
>
> **Sequence:**
>
> 1. **Inventory access provisioning.** Patrick to provide Steven access to Google Analytics + social accounts (synced May 13). Confirm Stripe / Grafana / Mailchimp access on file. Note that Google Ads is not active and should be a placeholder column for future activation only.
> 2. **Schema design for the Sheets aggregator.** Per-platform sheet for raw metrics + a master aggregator sheet for derived/cross-platform metrics. Date-keyed rows so trend analysis is possible.
> 3. **Automation evaluation.** Compare N8N (self-hosted on the MuseFlow ECS cluster or N8N Cloud), Zapier, and lightweight Python scripts (Lambda or local cron) for ingestion. Decision criteria: cost, maintainability, AI-mediation potential, ability to hook into the read-only production database for behavioral metrics correlation.
> 4. **Stage 1 deployment.** Stand up the highest-value sources first (Stripe + Grafana + Mailchimp probably) and validate the data integrity end-to-end.
> 5. **Wait for / coordinate with Staley's data-integrity work.** Production-DB-sourced metrics (engagement, retention, conversion-by-cohort) depend on the duplicate-event and trial/subscription fixes shipping. Do not build downstream on flaky data.
> 6. **Build the AI-mediated feedback loop.** Once aggregation is solid: AI agents read the data, propose marketing-content changes (SEO posts, social copy, email cadence), and iterate based on metric movement. Andrew has built a similar architecture for product features (the "automation lab" pattern); the marketing-content version is a direct analog and a probable second test case for agentic workflows.
> 7. **Coordinate with the design / product project** on positioning copy that uses the framework material in §13.5. Marketing pages should reflect the Spectrum, the Three AI Roles, and the Tooling Ecosystem framing rather than older "songs vs. skills" or single-mode positioning.
>
> **What you should NOT do yet:**
> - Don't over-engineer the aggregation layer. Google Sheets + automation is the V1 ceiling.
> - Don't build marketing content claims around AI features that aren't shipped (e.g., the Coach role specifically — that's V1 demo-scope at most).
> - Don't promise community / social features in marketing copy until those features have a roadmap commitment.
> - Don't depend on event-data-sourced metrics until Staley's cleanup ships.

---

*End of synthesis.*
