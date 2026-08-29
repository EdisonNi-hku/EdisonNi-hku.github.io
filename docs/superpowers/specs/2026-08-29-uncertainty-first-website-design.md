# Uncertainty-First Website Design

## Goal

Present one coherent research identity: uncertainty quantification is the methodology, while application reliability and capability enhancement are its two uses. Keep Qwen and Trace2Skill as concrete representative work, not as part of the UQ methodology claim. Attribute Skill-RM, GD²PO, and Understanding Failures as mentored work.

## Non-goals

- Do not create separate capability and trustworthiness versions of the website.
- Do not make test-time scaling, agents, verification, or calibration the top-level research identity.
- Do not describe Trace2Skill as uncertainty-guided.
- Do not present Skill-RM, GD²PO, or Understanding Failures as Jingwei's representative papers.
- Do not redesign the visual language or add an audience toggle.

## Information architecture

Use one shared research spine with two audience payoffs:

1. Uncertainty quantification makes model uncertainty explicit.
2. Reliability use: after calibration, uncertainty informs selective prediction, human supervision, abstention, and bounded decision authority.
3. Capability use: model-internal uncertainty supplies a test-time self-assessment signal when external evaluation is unavailable, incomplete, or expensive.
4. Representative work provides project-level evidence after the research position has been established.
5. Mentorship is a separate section with explicit attribution.

## Homepage

### Hero

Keep the existing headline:

> **AI systems that know when to be trusted.**

Replace the lede with:

> I quantify the uncertainty a model already carries and use it to guide human supervision and adaptive test-time reasoning.

Change the hero readout from `Trustworthy AI · NLP` to `Uncertainty Quantification · NLP`.

### About Research

Use the heading:

> **Making uncertainty actionable.**

Use this introduction:

> My research uses uncertainty quantification for two purposes: deciding when a model can be trusted and guiding how it should reason at test time.

Present the two uses in this order.

#### Improving reliability

Heading:

> **Know when a model can be trusted.**

Body:

> A trustworthy model should report low confidence whenever it is likely to be wrong. I extract the uncertainty a model already carries and expose it for human supervision. After calibration, these estimates can support selective prediction and determine when a system should answer, abstain, or defer. This ability to flag its own unreliability is what makes oversight possible.

#### Enhancing capability

Heading:

> **Guide how a model reasons at test time.**

Body:

> Effective test-time scaling needs feedback on whether the current reasoning is reliable, so it can decide whether further inference is worth the cost. Model-internal UQ can provide this self-assessment without repeatedly querying a separate evaluator. Programmatic verifiers provide definitive feedback when criteria are explicit and cheap to check, while LLM judges cover less formal criteria but add cost and latency and remain tied to a chosen rubric. UQ complements these external signals with a model-native test-time signal for deciding when to continue reasoning, explore another path, or stop.

### Selected Research

Keep six cards. Their order is:

1. ReProbe, ACL 2026 Oral
2. Trace2Skill, EMNLP Main
3. Can Reasoning Help Large Language Models Capture Human Annotator Disagreement?, EACL 2026 Oral
4. DIRAS, NAACL 2025 Long
5. Co-DETECT, EMNLP Demo
6. Towards Faithful and Robust LLM Specialists for Evidence-Based Question-Answering, ACL 2024 Long

Remove AFaCTA only from the selected-card grid. Keep it in the full publication list.

Use this Trace2Skill summary:

> Developed at Qwen, Trace2Skill distills successful and failed trajectories into reusable agent skills, using verifier-grounded experience to improve future test-time behavior.

Use `Jingwei Ni et al.` as the compact author line. Keep ReProbe as the single featured paper above the About Research section.

Update the Selected Research section note to:

> Quantifying uncertainty in language models and using it to guide reliable decisions and adaptive reasoning.

### Mentorship

Rename `Supervised Master Thesis & Mentorship` to:

> **Research Mentorship & Supervision**

Add these entries before the existing master-thesis entries:

1. Skill-RM: Unifying Heterogeneous Evaluation Criteria via Agent Skill
   - Year: 2026
   - Venue: Preprint
   - Link: https://arxiv.org/abs/2606.03980
   - Attribution: `Research mentorship at Qwen · Tao Chen`
2. GD²PO: Mitigating Multi-Reward Conflicts via Group-Dynamic Reward-Decoupled Policy Optimization
   - Year: 2026
   - Venue: EMNLP Findings
   - Link: https://arxiv.org/abs/2606.16771
   - Attribution: `Research mentorship at Qwen · Haotian Liu`
3. Understanding Failures in LLM Reasoning by Learning Structured Representations of Chain-of-Thought
   - Year: 2026
   - Venue: EMNLP Findings
   - Link: https://openreview.net/forum?id=0XfuJjhaI5
   - Attribution: `Research mentee · Tommaso Felice Banfi`

Keep the three existing supervised-master entries below these and renumber the mentorship list from 01 through 06.

### Full Publication List

Add `Understanding Failures in LLM Reasoning by Learning Structured Representations of Chain-of-Thought` to the 2026 group with the `EMNLP Findings` tag and the OpenReview link above. Place it after Trace2Skill and renumber all following publication indices.

Keep the previously approved venue labels:

- Trace2Skill: `EMNLP Main`
- GD²PO: `EMNLP Findings`

## Full Research Statement

Keep one canonical `research.html`. Do not create audience-specific pages.

### Opening

Retain uncertainty quantification as the topic and introduce the same two uses as the homepage: reliability first, capability second. Add two short audience-entry cards near the top, but keep all content visible on one page.

### Reliability argument

Condense the current five `Why this matters now` arguments into three while preserving the existing evidence, citations, and polished wording wherever possible:

1. **Uncertainty reporting enables oversight.** Merge the current reward-gaming and uncertainty-aware-supervision arguments.
2. **Existing evaluation misses disagreement and underspecified criteria.** Merge the current LLM-judge, human-disagreement, and deployment arguments.
3. **More scaling cannot resolve irreducible uncertainty.** Retain the current final argument and the paper-specific evidence that longer reasoning can harm representation of disagreement.

### Capability argument

Add a peer section after the reliability argument using the approved homepage capability text as its concise thesis. Expand it only enough to establish:

1. Test-time scaling needs feedback about whether current reasoning is reliable.
2. Programmatic verifiers are definitive and cheap when criteria are formalizable, but their coverage is narrow.
3. LLM judges cover qualitative criteria, but repeated calls add test-time cost and latency and remain bound to a selected rubric.
4. Model-internal UQ complements these external signals with a model-native self-assessment signal.

Do not mention Qwen or Trace2Skill in this research-position argument.

### My Research

Organize the existing project discussion under the same two uses:

- Reliability: Can Reasoning Help, DIRAS, AFaCTA, Evidence-Based QA, and Co-DETECT.
- Capability: ReProbe.

Preserve existing citations and links. Qwen and Trace2Skill remain in the homepage representative-work presentation rather than being recast as UQ work.

## Content and style constraints

- Prefer commas, colons, and full stops over em dashes.
- Treat calibration only as processing that makes an uncertainty score usable for downstream decisions. Do not present calibration as the primary methodology.
- State that UQ informs a test-time policy. Do not claim that uncertainty alone proves correctness or directly determines the value of more compute.
- Describe programmatic verifiers and LLM judges as complementary external feedback, not as methods that UQ universally replaces.
- Reuse the existing components and visual style. Add CSS only if the approved structure cannot be expressed with current classes.

## Verification

- Confirm the homepage contains exactly six selected-research cards in the approved order.
- Confirm AFaCTA remains in the full publication list.
- Confirm Skill-RM, GD²PO, and Understanding Failures appear in Mentorship, with the approved attribution, and are not selected-research cards.
- Confirm Understanding Failures also appears once in the full publication list.
- Confirm Trace2Skill and GD²PO retain the approved EMNLP venue labels.
- Confirm `index.html` and `research.html` remain valid, navigable HTML and that their local links resolve.
- Review the final diff to ensure unrelated files and the pre-existing `README.md` modification are untouched.
