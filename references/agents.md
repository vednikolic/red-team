# Agent Playbooks — Deep Attack Vectors

Reference file for red-team skill. Read the relevant section(s) when you need deeper attack vector guidance beyond the summary in SKILL.md.

---

## Engineering

**Feasibility**
- Does the spec assume capabilities that do not exist in the current stack?
- Are there integrations or APIs that are assumed available but unconfirmed?
- Does the proposal depend on data that does not currently exist, is low quality, or requires a pipeline that has not been scoped?

**Scalability**
- What breaks at 10x current load? 100x?
- Are there architectural decisions that are fine at MVP scale but become blockers at growth?
- Does the design assume statelessness when state is actually required?

**Build vs Buy**
- Is the team scoping custom infrastructure for something that has mature third-party solutions?
- Conversely, is the team assuming a vendor will cover something that will require custom work at the edges?
- Are licensing costs for third-party tooling factored in?

**Dependencies**
- What external teams, systems, or data sources does this require? Are they committed?
- Are there hard dependencies on other roadmap items that are not yet shipped?
- What is the blast radius if a dependency slips?

**Timeline**
- Does the timeline account for QA, accessibility review, legal review, and localization if applicable?
- Are there implicit assumptions of zero rework cycles?
- Is there buffer for onboarding new contributors or cross-functional coordination overhead?

---

## UXR

**User Mental Models**
- What assumptions are being made about how users understand this problem space?
- Has the team done discovery research, or are they designing from intuition?
- Are there existing mental model studies that contradict the design direction?

**Edge Case Users**
- How does this work for users with low digital literacy?
- How does this work for users with visual, motor, or cognitive accessibility needs?
- How does this work for users in low-bandwidth environments?
- How does this work for non-native speakers of the primary language?
- How does this work for users who are in a high-stress or time-pressured context?

**Behavioral Assumptions**
- Does the design assume users will read instructions or onboarding copy? Research consistently shows they will not.
- Does the design assume users will make careful, deliberate decisions? Research shows most decisions are fast and low-attention.
- Is there a confirmation bias assumption — designing for how power users behave rather than median users?

**Trust Signals**
- At what points does the user need to trust the product to take action? Are trust signals present at those moments?
- Are there moments where the UI asks for more than users are typically willing to give at that stage of the relationship?
- Are error states and empty states designed, or assumed away?

**Success Metrics**
- Do the proposed metrics measure whether users accomplished their goal, or just whether they completed a flow?
- Is there a metric for what happens when things go wrong?
- Are retention and engagement metrics defined, or just acquisition?

---

## PMM

**Differentiation**
- Which of these claims do primary competitors already make on their positioning pages?
- Is the differentiation functional or perceived? Functional differentiation is harder to copy; perceived differentiation erodes quickly.
- Is the team aware of adjacent players who will move into this space if it validates?

**Audience Definition**
- Is the ICP defined narrowly enough to write a single compelling message to?
- "Everyone who does X" is not an audience. What is the actual segment?
- Are there conflicting jobs-to-be-done across the target audience that will force messaging compromise?

**Go-to-Market Timing**
- Is the market educated enough to understand this category, or does the GTM plan require category creation?
- Are there seasonal, regulatory, or competitive timing factors not accounted for?
- What is the dependency on other GTM motions (e.g. sales enablement, partner readiness) that are not in scope here?

**Positioning**
- How many sentences does it take to explain what this is? If more than two, the positioning needs work.
- Is there an assumption that users will change existing behavior? What is the behavioral change cost being asked?
- Is the positioning anchored to a problem users actively feel, or one the team believes they should feel?

**Competitive Landscape**
- Who is building in this space that is not in the competitive matrix?
- What do the strongest competitors do well that this proposal does not address?
- Are there substitutes (not direct competitors) that users will reach for instead?

---

## Privacy

**Data Minimization**
- What data is being collected? Is all of it necessary to deliver the stated feature?
- Are there fields being collected "just in case" or for future analytics that have no current feature justification?
- Is there a data flow diagram? If not, that is itself a risk signal.

**Consent**
- Where is consent obtained? Is it clear what the user is consenting to at that moment?
- Is consent bundled with terms of service in a way that makes it effectively meaningless?
- Can users withdraw consent and have their data deleted? Is that flow designed?

**Cross-Border**
- Where will user data be stored and processed?
- Are there users in jurisdictions with data residency requirements (EU, Brazil, India, etc.)?
- Is the legal basis for processing in each jurisdiction confirmed?

**Retention and Deletion**
- What is the retention policy for each data type collected?
- Is there an automated deletion mechanism, or is this a manual process?
- What happens to derived data (model training data, aggregates) when a user requests deletion?

**Re-identification Risk**
- Is any data described as "anonymized" that could be re-identified with auxiliary data?
- Are there combinations of fields that are individually innocuous but identifying in combination?
- Has a privacy engineer reviewed the data model, or is this assessment from product or engineering?

---

## Legal

**Regulatory Surface**
- Which regulations apply? GDPR, CCPA, COPPA, HIPAA, PCI-DSS, sector-specific?
- Has outside counsel reviewed the regulatory surface, or is this an internal assessment?
- Are there pending regulations in key markets that could affect this post-launch?

**IP**
- Who owns content generated or processed by this feature?
- If the feature uses third-party models, training data, or datasets, are the licenses confirmed?
- Is there user-generated content involved? Who owns it and what can the platform do with it?

**Terms of Service**
- Does the proposed behavior align with existing ToS, or does the ToS need updating first?
- Does the feature interact with third-party platforms whose ToS prohibits this use?
- Are there representations being made to users that create warranty or guarantee exposure?

**Liability**
- If the feature produces incorrect output (recommendations, classifications, decisions), what is the liability surface?
- Is there a disclaim-ability path for AI-generated or algorithmically-generated content?
- What happens if the feature is used in a way that causes harm to a third party?

**Jurisdiction**
- If this launches internationally, are there countries where this is not legal?
- Are there countries where local legal entity or data residency requirements apply?
- Is there a legal review process before entering new markets?

---

## Ethics / Trust and Safety

**Misuse Vectors**
- How would a bad actor use this feature? What is the easiest misuse path?
- What is the blast radius if the feature is used for harassment, fraud, or manipulation?
- Is there a Trust and Safety review in the launch process?

**Power Asymmetries**
- Does this feature give the platform or third parties more leverage over users?
- Can users opt out? Can they access or port their data?
- Does the feature create information asymmetry that advantages the platform at user expense?

**Vulnerable Populations**
- Could this feature be used against minors, people in financial distress, people in mental health crisis, or other vulnerable groups?
- Is there a path for users to report harm?
- Are there safeguards that specifically account for vulnerable user segments?

**Dual-Use Risk**
- What is the most harmful legitimate-seeming use of this feature?
- If the feature involves content generation, classification, or recommendation — what categories of output could cause harm?
- Has the team run an abuse case brainstorm, not just a use case brainstorm?

**Feedback Loops**
- Does this feature optimize for an engagement signal that could reinforce harmful behavior at scale?
- Are there runaway feedback loops if the system misbehaves?
- What are the human review and circuit-breaker mechanisms?

---

## Security

**Authentication and Authorization**
- Are authentication assumptions validated, or inherited from adjacent systems?
- Is authorization checked at every layer (API, service, data), or just at the entry point?
- Are there privilege escalation paths that have not been modeled?

**Third-Party Risk**
- What third-party services does this feature depend on?
- What is the security posture of each dependency? Has it been assessed?
- What is the blast radius if a dependency is compromised?

**Data Security**
- Is data encrypted at rest and in transit?
- Are there secrets, credentials, or tokens in the design that need rotation and management?
- Is there a key management plan?

**Threat Model**
- Has a formal threat model been run (STRIDE, PASTA, or equivalent)?
- Who are the adversaries? What are their capabilities and motivations?
- Are internal threat vectors (compromised employees, vendor access) modeled?

**Incident Response**
- Does the existing incident response plan cover the new surface area this feature creates?
- Is there logging and alerting for the new attack surface?
- What is the detection-to-containment time assumption?

---

## Finance / Biz

**Unit Economics**
- What are the cost drivers per unit of value delivered? Are they calculated, or estimated?
- At what scale does this become contribution-positive? Is that scale realistic given the roadmap?
- What are the variable cost drivers that could compress margin as volume grows?

**Cost Model Gaps**
- Does the cost model include support load generated by this feature?
- Does it include compliance overhead (legal review, privacy review, ongoing monitoring)?
- Does it include the cost of failures, rollbacks, and incident response?

**Revenue Dependency**
- Is revenue from this feature dependent on a single partner, channel, or customer segment?
- What is the concentration risk?
- What happens to the business case if the primary dependency does not perform to plan?

**Pricing**
- Is the pricing model based on willingness-to-pay research, or internal intuition?
- Is the pricing competitive with alternatives, including "do nothing"?
- Are there pricing model risks (race to zero, commoditization, regulatory price caps)?

**Resourcing**
- Does the resource plan account for ramp time for new hires or contractors?
- Is there shared resource dependency (platform teams, legal, design) that is not committed?
- What is the opportunity cost of this investment versus alternatives on the roadmap?

---

## Data / Analytics

**Metric Definition Integrity**
- Is the metric defined precisely enough to be unambiguous? What is the numerator, denominator, time window, and aggregation method?
- "Engagement up 12%" — 12% of what, over what window, mean or median, which user cohort?
- Are there multiple competing definitions of this metric in use across teams? Which one is being used here?
- Is the metric a proxy, and if so, how validated is the proxy-to-outcome relationship?

**Causal Claims**
- Is a causal claim being made from correlational or observational data?
- "Users who do X retain 2x better" — is this a selection effect (retained users are more engaged by definition) or a causal finding?
- Has the team controlled for confounders? Which ones? Which ones are not controlled?
- Is there a randomized experiment supporting the claim, or is this derived from observational analysis?

**Statistical Validity**
- What is the sample size? Is it sufficient to detect the claimed effect at a reasonable confidence level?
- Are confidence intervals reported, or only point estimates?
- Is statistical significance reported? Is practical significance also considered — a statistically significant but tiny effect is not a business justification?
- Are multiple comparisons being made without adjustment (p-hacking risk)?

**Baseline and Benchmark Legitimacy**
- What is the comparison baseline? Is it appropriate (same cohort, same time period, comparable market)?
- Is the benchmark internal or industry-sourced? If industry, is the source credible and the comparison group actually comparable?
- Is the time window cherry-picked to show the most favorable trend?
- Are there seasonality or external event effects not accounted for in the baseline?

**Goal and OKR Construction**
- Are targets derived from evidence or negotiated backwards from what seemed achievable?
- Are leading indicators (inputs) clearly distinguished from lagging indicators (outcomes)?
- Is there a measurement plan — who owns tracking, how frequently is it reviewed, what triggers a response?
- Are there missing counter-metrics that would catch gaming or unintended side effects?

**Instrumentation Assumptions**
- Does the proposed metric require instrumentation that does not currently exist?
- Is the existing instrumentation reliable enough to measure at the precision claimed?
- Are there known data quality issues (bot traffic, duplicate events, timezone inconsistencies) that would corrupt the metric?
- What is the data latency — how quickly can the team detect a problem after it starts?

**Survivorship and Selection Bias**
- Is the analysis population representative, or are churned users, inactive users, or low-engagement users excluded?
- Are edge case users (power users, brand-new users, users on older platform versions) represented appropriately?
- Is there a self-selection effect in any opt-in feature or cohort used as evidence?

**Experiment Design** *(when a proposed experiment is in scope)*
- Is the experiment powered sufficiently? What effect size was used to calculate sample size?
- Is there a clean holdout group with no treatment leakage?
- Is the success metric pre-registered, or will it be selected post-hoc based on results?
- Is the experiment window long enough to escape novelty effects?
- Are network effects or interference between treatment and control groups accounted for?

---

## Design *(activate for UX artifacts only)*

**Visual Hierarchy**
- Does the layout communicate action priority clearly, or are primary and secondary actions visually equivalent?
- Is there a clear focal point on each screen, or does visual complexity distribute attention equally across everything?
- Are destructive or irreversible actions visually differentiated from safe ones?

**Design System Consistency**
- Does this diverge from established design system components in ways that imply different behavior than intended?
- Are new patterns being introduced that will need to be maintained, or reusing existing components?
- Do interactive elements (buttons, inputs, toggles) behave consistently with platform and product conventions?

**End-to-End Journey Integrity**
- Does this feature connect cleanly to adjacent flows, or does it create orphaned states with no clear path forward or back?
- Is back-navigation coherent — does the user return to where they expect, or to an unexpected state?
- Is context preserved across surfaces (mobile to desktop, notification to app, email link to logged-in state)?
- Are there entry points into this flow from other parts of the product that are not designed for?

**Missing States**
- Is the error state designed, or assumed away?
- Is the empty state (first-time user, no data, zero results) designed?
- Is the loading state designed, including for slow connections?
- Are partial failure states handled (some data loaded, some failed)?

**Platform Convention Fit**
- Does the interaction model match platform conventions for the target surface?
- For non-standard surfaces (wearables, AR, voice): are standard mobile or web heuristics being incorrectly applied?
- For wearables and AR specifically: is input modality (gesture, voice, tap) appropriate for the context of use (hands busy, glanceable, ambient)?
- Are there platform-specific accessibility requirements not addressed?

**Trust Signal Placement**
- At what moments does the user need to trust the product to take action? Are trust signals present at those exact moments?
- Is sensitive information (permissions, data sharing, payment) introduced at the right moment in the journey, or too early or too late?

---

## Ops / Implementation *(lightweight: 1 to 3 findings)*

**Support Load**
- What new support contact reasons does this feature create? Is volume estimated?
- Is there self-serve resolution for the most predictable failure modes, or will all failures require human support?
- Are support teams trained and tooled before launch, or is this a post-launch activity?

**Operational Dependencies**
- What internal teams, tools, or processes need to be in place for this to operate post-launch?
- Are those dependencies confirmed and resourced, or assumed?
- Is there a handoff plan from the build team to whoever operates this ongoing?

**Monitoring and Response**
- Is there an alerting plan for the new surface area this feature creates?
- What does the on-call runbook look like for this feature?
- What is the rollback plan if a critical issue is detected post-launch?

---

## Localization / Internationalization *(lightweight: 1 to 3 findings)*

**Text and Layout**
- Are UI strings externalized for translation, or hardcoded?
- Is text expansion accounted for in layouts? German and Finnish regularly run 30 to 40% longer than English.
- Are RTL languages (Arabic, Hebrew) supported? Does the layout mirror correctly?

**Format Assumptions**
- Are date, time, number, and currency formats localized, or assumed to be US/EN conventions?
- Are there culturally specific metaphors, icons, or color associations that do not translate?

**Regulatory Variation**
- Are there market-specific legal or regulatory requirements that differ from the primary market?
- Is the compliance review scoped per market, or assumed to be globally uniform?
- Are there markets where this feature is not legally permissible that are not excluded from the launch plan?
