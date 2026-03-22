---
name: red-team
description: Adversarially stress-test any product artifact — ideas, PRDs, strategy docs, UX flows, pitches, frameworks, or policies — from multiple disciplinary lenses including Engineering, UXR, PMM, Privacy, Legal, Ethics, Security, Finance, Data/Analytics, Design, Ops, and Localization. Use this skill whenever the user wants to pressure-test, red-team, challenge, poke holes in, find weaknesses in, or adversarially review anything. Also trigger on phrases like "what could go wrong", "what are we missing", "find the holes in this", "stress test this", "challenge this", "play devil's advocate", "critique this", or when input contains metric claims, data evidence, OKRs, or UX artifacts. Works standalone. Pairs with steelman for a complete attack-then-strengthen workflow.
argument-hint: [file path or topic] [--save] [--agents engineering,privacy,legal]
---

# Red Team Skill

Adversarially analyze any product artifact or idea from multiple disciplinary perspectives. The goal is to surface the strongest, most credible attacks, not obvious objections the author already considered. Vague, hedged, or softened findings are worse than no findings.

Works standalone. Does not require any other tool or skill. The optional steelman pairing is referenced at the end but is not needed.

---

## Core Principles

**Specificity over coverage.** Two sharp attacks per agent beat six generic ones. If you cannot make a specific attack grounded in the input, do not invent one. Flag the gap.

**"I don't know" is a valid and respected output.** If the input does not give enough information to assess a risk area, say so explicitly and state what information would unlock better analysis. Never soften a position to compensate for uncertainty. Never fabricate specificity.

**Judgment-grounded severity.** Severity ratings use consistent definitions (below) but are applied using contextual judgment. A BLOCKING finding in a consumer fintech product may be HIGH in an internal tool. Always explain the reasoning, not just the label.

**Attacks target assumptions, not just conclusions.** The most valuable findings expose hidden assumptions the author did not realize they were making.

**Organizational weight is real.** Legal and Privacy have veto power in most orgs. Engineering owns feasibility. UXR and Ethics are influential but rarely blocking on their own. Reflect this when characterizing severity and who needs to act.

---

## Severity Definitions

Use these consistently, with judgment applied to context:

| Severity | Meaning |
|---|---|
| **BLOCKING** | Must be resolved before this can ship or proceed. Unaddressed, this kills the initiative or creates unacceptable legal, safety, or trust exposure. |
| **HIGH** | Significant risk if unaddressed. Will likely surface during execution or launch and require costly rework or escalation. |
| **MEDIUM** | Real risk, manageable with deliberate effort. Should be planned for, not ignored. |
| **LOW** | Worth noting. Low probability or low impact, but a responsible team tracks it. |

---

## Step 1: Detect the Input Type

State the detected input type at the top of every output. Use judgment for hybrids.

| Input Type | Primary Attack Surface |
|---|---|
| Strategy or vision doc | Assumptions, market logic, timing, resourcing |
| PRD or product spec | Feasibility, scope gaps, user model, success metrics |
| UX flow or prototype | Mental model fit, edge cases, accessibility, journey integrity, platform conventions |
| Business pitch | Unit economics, competitive moat, regulatory surface |
| Data or analytics artifact | Metric validity, causal claims, methodology, instrumentation gaps |
| Policy or framework | Edge cases, enforcement gaps, misuse vectors |
| Feature idea (informal) | All of the above, scaled to available information |
| Other | Call it out and adapt accordingly |

---

## Step 2: Select Active Agents

Each "agent" is a disciplinary perspective, not a separate process. If your environment supports parallel execution, run each agent as a separate task. Otherwise, work through them sequentially.

**Always activate:** Engineering, UXR, PMM, Privacy, Legal

**Conditionally activate** based on input type and content signals:

- **Ethics / Trust and Safety** -- activate when input involves user data, behavioral influence, content generation, vulnerable populations, or any feature that could be weaponized
- **Security** -- activate when input involves authentication, data storage, third-party integrations, financial transactions, or API surface
- **Finance / Biz** -- activate when input includes cost, revenue, pricing, resourcing, or unit economics claims
- **Data / Analytics** -- activate when input contains metric claims, OKRs, experiment results, benchmark comparisons, growth projections, or any quantitative evidence used to justify a direction; also activate when future measurement is proposed without methodology
- **Design** -- activate when input is a UX artifact (flow, prototype, wireframe, journey map) or makes specific claims about interface behavior; do not activate for strategy docs or PRDs unless they contain detailed UX specifications
- **Ops / Implementation** -- activate when input describes a post-launch system, support model, internal tooling dependency, or makes assumptions about ongoing operations; lightweight, 1 to 3 findings max
- **Localization / Internationalization** -- activate when input has any international scope, multi-market claims, or language assumptions; lightweight, 1 to 3 findings max

**Focus mode:** If the user specifies agents (e.g. "red team this from a privacy and legal lens only"), activate only those agents. State which agents were excluded and why.

List active agents at the top of the output.

---

## Step 3: Generate Adversarial Findings

For each active agent, generate 2 to 5 findings. Skip an agent entirely rather than producing weak findings. If you skip, say why.

Each finding uses this format:

```
[AGENT] | [SEVERITY] | [ADDRESSABLE or NOTE]

Attack: The specific assumption or claim being challenged -- one sentence, no hedging.
Grounding: Why this is a real risk. Reference specifics from the input, not hypotheticals.
Worst case: What happens if this is wrong and goes unaddressed.
Confidence: HIGH / MEDIUM / LOW -- and if MEDIUM or LOW, state what information would raise it.
```

**Confidence criteria:**
- **HIGH**: The risk is grounded in specific evidence drawn directly from the input. The attack vector is well-documented in the domain and the input contains the triggering condition.
- **MEDIUM**: The risk is plausible but depends on assumptions not stated in the input. State which assumptions you are making and what evidence would confirm or refute them.
- **LOW**: The risk is theoretical or requires external context not available in the input. Flag it only if the worst-case impact is severe enough to warrant tracking despite low confidence.

**Example finding:**

```
Engineering | HIGH | ADDRESSABLE

Attack: The spec assumes real-time sync across devices but does not address conflict resolution when two devices edit the same record offline.
Grounding: The architecture section specifies "eventual consistency" but the product requirements describe "instant sync" -- these are contradictory. No conflict resolution strategy is mentioned anywhere in the document.
Worst case: Users lose data silently when concurrent edits resolve unpredictably, destroying trust in the product's reliability claim.
Confidence: HIGH -- the contradiction between "eventual consistency" and "instant sync" is explicit in the document, and conflict resolution is a well-documented failure mode for offline-first architectures.
```

---

## Agent Attack Vectors

Read the relevant reference file for deep attack vector guidance:
- Full agent playbooks: `references/agents.md`

Summary of primary vectors per agent:

**Engineering**
Feasibility assumptions, scalability cliffs, build-vs-buy cost underestimation, missing infrastructure dependencies, timeline assumptions that assume zero rework, API or data contract gaps.

**UXR**
User mental model assumptions with no research backing, missing edge case users (low literacy, accessibility, non-native speakers), behavioral assumptions that contradict known patterns, absent or misplaced trust signals, success metrics that measure output not outcome.

**PMM**
Differentiation claims competitors already make, audience defined too broadly to message, go-to-market timing that ignores market readiness, positioning requiring too much user education, competitors missing from the competitive landscape who should be there.

**Privacy**
Data collected beyond feature necessity, buried or ambiguous consent flows, cross-border transfer assumptions, missing retention and deletion policies, re-identification risk from "anonymized" data.

**Legal**
Unscoped regulatory surface (GDPR, CCPA, COPPA, sector-specific), IP ownership gaps, ToS conflicts with proposed behavior, untested liability assumptions, jurisdictional gaps for international scope.

**Ethics / Trust and Safety**
Misuse vectors absent from the threat model, power asymmetries between platform and user, impact on vulnerable populations, dual-use risk (designed for X, weaponizable for Y), feedback loops that could reinforce harm at scale.

**Security**
Unvalidated authentication assumptions, unassessed third-party dependency risk, gaps in data at rest and in transit, threat model too narrow or absent, no incident response consideration for new surface area.

**Finance / Biz**
Unit economics assumptions without cited evidence, cost models excluding support or compliance overhead, single-partner revenue dependency, pricing assumptions without willingness-to-pay research, resourcing that ignores ramp time.

**Data / Analytics**
Metric definitions that obscure what is actually being measured, causal claims that are selection effects or correlations, missing statistical validity (sample size, confidence intervals, significance), cherry-picked baselines or time windows, instrumentation gaps where the proposed metric cannot actually be tracked, survivorship or selection bias in the analyzed population, A/B test design flaws.

**Design** *(activate for UX artifacts only)*
Visual hierarchy failures that bury primary actions, divergence from design system conventions that implies unintended behavior, end-to-end journey breaks (orphaned states, broken back-navigation, context loss between surfaces), interaction model mismatch with platform conventions (especially non-standard surfaces like wearables or AR), missing states (error, empty, loading, edge case).

**Ops / Implementation** *(lightweight: 1 to 3 findings)*
Support load not estimated, internal tooling dependencies not confirmed, ongoing monitoring or moderation not scoped, handoff from build team to operating team not planned, runbook or incident playbook absent.

**Localization / Internationalization** *(lightweight: 1 to 3 findings)*
Text expansion breaking layouts, RTL language support not considered, date, number, and currency format assumptions, cultural appropriateness of metaphors or visuals not assessed, market-specific regulatory variation not mapped.

---

## Step 4: Synthesize and Prioritize Findings

After all agent findings, produce this synthesis block:

### Severity Summary

List findings grouped by severity. Do not repeat full finding text. One-line summaries only.

**BLOCKING**
- [Agent] [one-line summary]

**HIGH**
- [Agent] [one-line summary]

**MEDIUM / LOW**
- [Agent] [one-line summary]

---

### Overall Confidence Score

Rate overall analytical confidence: HIGH / MEDIUM / LOW

Explain what drove the rating. Be explicit about what is missing from the input that would have enabled sharper analysis. List specific questions or information requests that would raise confidence. Do not manufacture confidence. A LOW rating with clear mitigation questions is more useful than a hedged MEDIUM.

---

### Steelman Signal

If a prior steelman analysis exists in conversation context:
> "ADDRESSABLE findings above are ready for reinforcement. Recommend running steelman on [list specific findings or sections] first."

If no steelman context exists:
> "ADDRESSABLE findings are tagged. Run a steelman pass to convert these into reinforced positions, or address them manually."

Note: BLOCKING findings do not gate steelman. Steelman can run in parallel on ADDRESSABLE findings regardless of blocking severity. Steelman is optional. This analysis is complete without it.

---

## Saving Output

If `--save` is specified:
- If analyzing a project file, save alongside it or in the project's docs folder
- Default fallback: `./YYYY-MM-DD-red-team-<topic>.md` (current directory)
- State where the file was saved

---

## Output Format Rules

- Lead with: detected input type, active agents
- Then findings by agent
- Then synthesis block
- Keep findings dense and specific. No hedging language, no softening
- If an attack is weak, omit it rather than include it at reduced severity
- If the input is too vague to analyze a domain, say so and ask what would help
- Never fabricate specificity to fill a section
