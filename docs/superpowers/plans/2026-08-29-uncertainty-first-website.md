# Uncertainty-First Website Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Update the homepage and research statement so uncertainty quantification is the single research methodology, reliability and capability are its two uses, and representative and mentored work are attributed correctly.

**Architecture:** Keep the existing static HTML and CSS architecture. Edit `index.html` for the homepage narrative, selected work, mentorship, and full publication list; edit `research.html` for the longer two-use research argument. Reuse existing components and classes, adding no CSS unless browser verification exposes a concrete layout failure.

**Tech Stack:** Static HTML5, existing `styles.css` and `script.js`, shell assertions, Playwright CLI screenshots.

---

## File map

- `index.html`: homepage hero, About Research, selected papers, mentorship, full publication list.
- `research.html`: canonical long-form research statement with reliability-first and capability-second framing.
- `styles.css`: expected to remain unchanged; edit only if the existing two-card and statement layouts demonstrably fail.
- `README.md`: pre-existing user modification; never stage or edit it.
- `.superpowers/`: brainstorming artifacts; never stage it.

## Task 1: Preserve the already-approved venue-label update

**Files:**
- Modify: `index.html:298-333`

- [ ] **Step 1: Verify the existing diff contains only the two venue-label changes**

Run:

```bash
git diff -- index.html
```

Expected: GD²PO changes from `Preprint` to `EMNLP Findings`, and Trace2Skill changes from `Preprint` to `EMNLP Main`; no other `index.html` changes are present yet.

- [ ] **Step 2: Verify both labels are attached to the correct titles**

Run:

```bash
rg -n -B 4 "GD<sup>2</sup>PO:|Trace2Skill:" index.html
```

Expected: `EMNLP Findings` immediately precedes GD²PO and `EMNLP Main` immediately precedes Trace2Skill.

- [ ] **Step 3: Commit only the approved venue labels**

Run:

```bash
git add -- index.html
git commit -m "Update EMNLP publication labels"
```

Expected: commit succeeds; `README.md` and `.superpowers/` remain unstaged.

## Task 2: Make the homepage narrative uncertainty-first

**Files:**
- Modify: `index.html:35-129`

- [ ] **Step 1: Run content assertions that fail before the change**

Run:

```bash
! rg -q "Uncertainty Quantification · NLP" index.html
! rg -q "Making uncertainty actionable" index.html
! rg -q "Guide how a model reasons at test time" index.html
```

Expected: exit 0 because all three new strings are absent.

- [ ] **Step 2: Update the hero readout and lede**

Replace the first hero readout span and the hero lede with:

```html
<span>Uncertainty Quantification · NLP</span>
```

```html
<p class="hero-lede">
  I quantify the uncertainty a model already carries and use it to guide human supervision and adaptive test-time reasoning.
</p>
```

Keep the current `<h1>` unchanged.

- [ ] **Step 3: Replace the About Research position and two focus cards**

Keep the existing biographical paragraph with the PhD and advisor information. Replace the research heading, the second prose paragraph, and the two focus cards with:

```html
<h2 class="section-title">Making uncertainty actionable.</h2>
```

```html
<p>
  My research uses uncertainty quantification for two purposes: deciding when a model can be trusted and guiding how it should reason at test time.
</p>
```

```html
<article class="focus-card" data-reveal>
  <span class="focus-tag">Improving reliability</span>
  <h3>Know when a model can be trusted.</h3>
  <p>
    A trustworthy model should report low confidence whenever it is likely to be wrong. I extract the uncertainty a model already carries and expose it for human supervision. After calibration, these estimates can support selective prediction and determine when a system should answer, abstain, or defer. This ability to flag its own unreliability is what makes oversight possible.
  </p>
</article>
<article class="focus-card accent" data-reveal>
  <span class="focus-tag">Enhancing capability</span>
  <h3>Guide how a model reasons at test time.</h3>
  <p>
    Effective test-time scaling needs feedback on whether the current reasoning is reliable, so it can decide whether further inference is worth the cost. Model-internal UQ can provide this self-assessment without repeatedly querying a separate evaluator. Programmatic verifiers provide definitive feedback when criteria are explicit and cheap to check, while LLM judges cover less formal criteria but add cost and latency and remain tied to a chosen rubric. UQ complements these external signals with a model-native test-time signal for deciding when to continue reasoning, explore another path, or stop.
  </p>
</article>
```

Keep the existing `Read the full research statement` link.

- [ ] **Step 4: Run the homepage narrative assertions**

Run:

```bash
rg -n "Uncertainty Quantification · NLP|Making uncertainty actionable|Know when a model can be trusted|Guide how a model reasons at test time|After calibration" index.html
```

Expected: every approved narrative element appears once in the hero or About Research section.

- [ ] **Step 5: Commit only the homepage narrative**

Run:

```bash
git add -- index.html
git commit -m "Reframe homepage around uncertainty quantification"
```

Expected: commit succeeds without staging `README.md` or `.superpowers/`.

## Task 3: Update selected research, mentorship, and publications

**Files:**
- Modify: `index.html:173-520`

- [ ] **Step 1: Run pre-change assertions**

Run:

```bash
! sed -n '/<div class="selected-grid">/,/<div class="publication-list-block mentorship-block">/p' index.html | rg -q "Trace2Skill"
! rg -q "Research Mentorship &amp; Supervision" index.html
! rg -q "Tommaso Felice Banfi" index.html
```

Expected: exit 0 because Trace2Skill is not selected, the mentorship heading is old, and Tommaso is absent.

- [ ] **Step 2: Update the selected-section note and replace AFaCTA with Trace2Skill in position 02**

Use this section note:

```html
<p class="section-note">Quantifying uncertainty in language models and using it to guide reliable decisions and adaptive reasoning.</p>
```

Insert this card immediately after ReProbe:

```html
<article class="publication-card" data-reveal>
  <div class="publication-meta">
    <span class="pub-year">2026</span>
    <span class="tag">EMNLP Main</span>
  </div>
  <h3><a href="https://arxiv.org/abs/2603.25158">Trace2Skill: Distill Trajectory-Local Lessons into Transferable Agent Skills</a></h3>
  <p class="pub-tldr">Developed at Qwen, Trace2Skill distills successful and failed trajectories into reusable agent skills, using verifier-grounded experience to improve future test-time behavior.</p>
  <p class="pub-authors">Jingwei Ni et al.</p>
</article>
```

Keep the approved remaining order: Can Reasoning Help, DIRAS, Co-DETECT, Evidence-Based QA. Remove only the AFaCTA card; retain its full-list entry.

- [ ] **Step 3: Rename and expand the mentorship list**

Use the heading:

```html
<h2>Research Mentorship &amp; Supervision</h2>
```

Insert these three entries before the existing master-thesis entries:

```html
<article class="publication-entry" role="listitem">
  <div class="publication-index">01</div>
  <div class="publication-body">
    <div class="publication-tags">
      <span class="pub-year">2026</span>
      <span class="tag">Preprint</span>
    </div>
    <h3><a href="https://arxiv.org/abs/2606.03980">Skill-RM: Unifying Heterogeneous Evaluation Criteria via Agent Skill</a></h3>
    <p class="mentor-student">Research mentorship at Qwen · Tao Chen</p>
  </div>
</article>
<article class="publication-entry" role="listitem">
  <div class="publication-index">02</div>
  <div class="publication-body">
    <div class="publication-tags">
      <span class="pub-year">2026</span>
      <span class="tag">EMNLP Findings</span>
    </div>
    <h3><a href="https://arxiv.org/abs/2606.16771">GD<sup>2</sup>PO: Mitigating Multi-Reward Conflicts via Group-Dynamic reward-Decoupled Policy Optimization</a></h3>
    <p class="mentor-student">Research mentorship at Qwen · Haotian Liu</p>
  </div>
</article>
<article class="publication-entry" role="listitem">
  <div class="publication-index">03</div>
  <div class="publication-body">
    <div class="publication-tags">
      <span class="pub-year">2026</span>
      <span class="tag">EMNLP Findings</span>
    </div>
    <h3><a href="https://openreview.net/forum?id=0XfuJjhaI5">Understanding Failures in LLM Reasoning by Learning Structured Representations of Chain-of-Thought</a></h3>
    <p class="mentor-student">Research mentee · Tommaso Felice Banfi</p>
  </div>
</article>
```

Renumber the existing Minjing Shi, Adam Rahmoun, and Qing Dai mentorship entries to 04, 05, and 06.

- [ ] **Step 4: Add Understanding Failures to the full publication list**

Insert this entry immediately after Trace2Skill:

```html
<article class="publication-entry" role="listitem">
  <div class="publication-index">06</div>
  <div class="publication-body">
    <div class="publication-tags">
      <span class="pub-year">2026</span>
      <span class="tag">EMNLP Findings</span>
    </div>
    <h3><a href="https://openreview.net/forum?id=0XfuJjhaI5">Understanding Failures in LLM Reasoning by Learning Structured Representations of Chain-of-Thought</a></h3>
  </div>
</article>
```

Renumber the former publication entries 06 through 22 to 07 through 23. Do not change their titles, links, years, or venue tags.

- [ ] **Step 5: Verify selected-work membership and ordering**

Run:

```bash
sed -n '/<div class="selected-grid">/,/<div class="publication-list-block mentorship-block">/p' index.html | rg "ReProbe:|Trace2Skill:|Can Reasoning Help|DIRAS:|Co-DETECT:|Towards Faithful|AFaCTA:"
```

Expected: the first six titles appear in the approved order and AFaCTA is absent from this slice.

Run:

```bash
rg -n "AFaCTA:" index.html
```

Expected: exactly one match in the full publication list.

- [ ] **Step 6: Verify mentorship and full-list attribution**

Run:

```bash
rg -n "Research Mentorship|Tao Chen|Haotian Liu|Tommaso Felice Banfi|Understanding Failures" index.html
```

Expected: the new heading and all three mentee attributions appear; Understanding Failures appears once in mentorship and once in the full publication list.

Run:

```bash
test "$(rg -c "Understanding Failures in LLM Reasoning" index.html)" -eq 2
test "$(rg -c '<article class="publication-card" data-reveal>' index.html)" -eq 6
```

Expected: both assertions pass.

- [ ] **Step 7: Commit the publication and mentorship update**

Run:

```bash
git add -- index.html
git commit -m "Update selected research and mentorship"
```

Expected: commit succeeds without staging unrelated files.

## Task 4: Rebalance the full research statement

**Files:**
- Modify: `research.html:39-135`

- [ ] **Step 1: Run assertions that describe the old structure**

Run:

```bash
test "$(rg -c 'class="argument-index"' research.html)" -eq 5
! rg -q "Making uncertainty actionable" research.html
! rg -q "Guide how a model reasons at test time" research.html
```

Expected: the old argument structure exists and the two new headings are absent.

- [ ] **Step 2: Update the statement opening**

Keep the statement title. Replace the lede with:

```html
<p class="statement-lede">
  I quantify the uncertainty a model already carries and use it to guide human supervision and adaptive test-time reasoning.
</p>
```

Change the Topic heading to `Making uncertainty actionable.` and use this opening paragraph:

```html
<p>
  My research uses uncertainty quantification for two purposes: deciding when a model can be trusted and guiding how it should reason at test time. A trustworthy model should report low confidence whenever it is likely to be wrong. The uncertainty itself has two sources, epistemic uncertainty about what the model does not know and aleatoric uncertainty arising from irreducible ambiguity in the world (<a class="cite" href="#ref-huellermeier2021">Hüllermeier &amp; Waegeman, 2021</a>; <a class="cite" href="#ref-shorinwa2024">Shorinwa et al., 2024</a>).
</p>
```

Add these two existing-style focus cards below the opening paragraph:

```html
<div class="container focus-block">
  <div class="focus-grid pair">
    <article class="focus-card" data-reveal>
      <span class="focus-tag">Use 01 · Improving reliability</span>
      <h3>Know when a model can be trusted.</h3>
      <p>After calibration, uncertainty estimates can support selective prediction, surface difficult cases for human supervision, and determine when a system should answer, abstain, or defer.</p>
      <a class="card-link" href="#reliability">Why reliability needs uncertainty →</a>
    </article>
    <article class="focus-card accent" data-reveal>
      <span class="focus-tag">Use 02 · Enhancing capability</span>
      <h3>Guide how a model reasons at test time.</h3>
      <p>Model-internal uncertainty can provide a low-cost self-assessment signal for deciding when to continue reasoning, explore another path, or stop.</p>
      <a class="card-link" href="#capability">Why capability needs uncertainty →</a>
    </article>
  </div>
</div>
```

Both anchor targets must remain visible and usable without JavaScript.

- [ ] **Step 3: Condense the reliability argument to three numbered entries**

Replace the five-entry argument section with this three-entry section:

```html
<section class="statement-section alt" id="reliability">
  <div class="container">
    <div class="section-heading" data-reveal>
      <p class="readout">Use 01 · Improving reliability</p>
      <h2 class="section-title">Know when a model can be trusted.</h2>
    </div>
    <div class="argument-list">
      <article class="argument" data-reveal>
        <div class="argument-index">01</div>
        <div class="argument-text">
          <h3>Uncertainty reporting enables oversight.</h3>
          <p>
            External rewards can mistake reward gaming for real capability. METR found that a frontier model exploited hidden tests, while Cursor traced many benchmark wins to answers retrieved from public sources rather than genuine fixes (<a class="cite" href="#ref-metr2026">METR, 2026</a>; <a class="cite" href="#ref-cursor2026">Cursor, 2026</a>). Bengio et al.'s Scientist AI argues for supervising agentic systems with non-agentic, uncertainty-aware guardrails (<a class="cite" href="#ref-bengio2025">Bengio et al., 2025</a>). When an external score cannot distinguish genuine capability from reward gaming, reported uncertainty provides a complementary signal for deciding which cases require oversight.
          </p>
        </div>
      </article>
      <article class="argument" data-reveal>
        <div class="argument-index">02</div>
        <div class="argument-text">
          <h3>Existing evaluation misses disagreement and underspecified criteria.</h3>
          <p>
            The field ranks, filters, and aligns models with LLM judges (<a class="cite" href="#ref-zheng2023">Zheng et al., 2023</a>; <a class="cite" href="#ref-gu2024">Gu et al., 2024</a>), but criteria such as helpfulness, harm, and novelty are contested across legitimate viewpoints. A judge commits to one reading and returns a single score, leaving evaluation most miscalibrated where humans disagree (<a class="cite" href="#ref-chochlakis2025">Chochlakis et al., 2025</a>; <a class="cite" href="#ref-baan2022">Baan et al., 2022</a>; <a class="cite" href="#ref-li2025a">Li et al., 2025a</a>). Real instructions are also underspecified, so models often invent missing details and act instead of asking (<a class="cite" href="#ref-wang2024">Wang et al., 2024</a>; <a class="cite" href="#ref-li2025b">Li et al., 2025b</a>). These cases require uncertainty to be surfaced rather than collapsed into a confident decision.
          </p>
        </div>
      </article>
      <article class="argument" data-reveal>
        <div class="argument-index">03</div>
        <div class="argument-text">
          <h3>More scaling cannot resolve irreducible uncertainty.</h3>
          <p>
            When uncertainty comes from genuine ambiguity or conflicting human judgments, more compute on the same input cannot resolve it. My own work shows that making models reason longer can actively harm their ability to represent human disagreement (<a class="cite" href="#ref-ni2026">Ni et al., 2026</a>). Reliable systems must recognize when additional inference is useful and when the unresolved uncertainty should instead be exposed to people.
          </p>
        </div>
      </article>
    </div>
  </div>
</section>
```

- [ ] **Step 4: Add the capability argument after reliability**

Add a `statement-section` with `id="capability"`, readout `Use 02 · Enhancing capability`, heading `Guide how a model reasons at test time.`, and this body:

```html
<div class="statement-body" data-reveal>
  <p>
    Effective test-time scaling needs feedback on whether the current reasoning is reliable, so it can decide whether further inference is worth the cost. Model-internal uncertainty can provide this self-assessment without repeatedly querying a separate evaluator.
  </p>
  <p>
    Programmatic verifiers provide definitive feedback when criteria are explicit and cheap to check, which has made them powerful for reinforcement learning and test-time improvement in domains such as mathematics and code (<a class="cite" href="#ref-lambert2024">Lambert et al., 2024</a>; <a class="cite" href="#ref-deepseek2025">DeepSeek-AI, 2025</a>). Their coverage ends when objectives cannot be completely formalized. LLM judges extend evaluation to qualitative criteria (<a class="cite" href="#ref-zheng2023">Zheng et al., 2023</a>; <a class="cite" href="#ref-gu2024">Gu et al., 2024</a>), but repeated calls add test-time cost and latency and remain tied to a chosen rubric. UQ complements these external signals with a model-native test-time signal for deciding when to continue reasoning, explore another path, or stop.
  </p>
</div>
```

Do not mention Qwen or Trace2Skill in this section.

- [ ] **Step 5: Reorganize My Research under the same two uses**

Keep one `My research` section with the heading `From uncertainty estimates to better decisions.` Replace its body with:

```html
<div class="statement-body" data-reveal>
  <p>
    <strong>For reliability,</strong> I study whether models can represent human disagreement rather than collapse it into one overconfident answer (<a href="https://arxiv.org/abs/2506.19467">Can Reasoning Help</a>). I build uncertainty-aware classifiers distilled into efficient, deployable models (<a href="https://arxiv.org/abs/2402.11073">AFaCTA</a>, <a href="https://arxiv.org/abs/2406.14162">DIRAS</a>), evidence-grounded specialists whose claims remain traceable to their sources (<a href="https://arxiv.org/abs/2402.08277">Evidence-Based QA</a>), and interfaces that surface model blind spots for human adjudication (<a href="https://arxiv.org/abs/2507.05010">Co-DETECT</a>). After calibration, the resulting uncertainty estimates support selective prediction and human supervision.
  </p>
  <p>
    <strong>For capability,</strong> <a href="https://arxiv.org/abs/2511.06209">ReProbe</a> reads a model's internal states during multi-step reasoning to estimate whether its answer has settled. It uses this self-assessment signal to allocate test-time compute only where additional reasoning is useful, with gold evaluation and extensive out-of-distribution testing.
  </p>
</div>
```

Do not introduce Trace2Skill as UQ work.

- [ ] **Step 6: Verify the new statement structure**

Run:

```bash
rg -n "Making uncertainty actionable|id=\"reliability\"|Uncertainty reporting enables oversight|Existing evaluation misses disagreement|More scaling cannot resolve|id=\"capability\"|Guide how a model reasons at test time|Model-internal uncertainty" research.html
```

Expected: the shared opening, three reliability arguments, and capability section all appear.

Run:

```bash
test "$(rg -c 'class="argument-index"' research.html)" -eq 3
! sed -n '/id="capability"/,/<\/section>/p' research.html | rg -q "Trace2Skill|Qwen"
```

Expected: there are exactly three numbered reliability arguments and no Qwen/Trace2Skill claim in the capability section.

- [ ] **Step 7: Commit the research statement**

Run:

```bash
git add -- research.html
git commit -m "Add capability framing to research statement"
```

Expected: commit succeeds without staging unrelated files.

## Task 5: Final content and browser verification

**Files:**
- Verify: `index.html`
- Verify: `research.html`
- Verify: `styles.css`

- [ ] **Step 1: Run whitespace and scope checks**

Run:

```bash
git diff --check HEAD~4..HEAD
git status --short
```

Expected: no whitespace errors; only the pre-existing `README.md` change and `.superpowers/` artifacts remain outside committed work.

- [ ] **Step 2: Verify required content and exclusions**

Run:

```bash
test "$(rg -c '<article class="publication-card" data-reveal>' index.html)" -eq 6
test "$(rg -c "Understanding Failures in LLM Reasoning" index.html)" -eq 2
test "$(rg -c "AFaCTA:" index.html)" -eq 1
rg -q "Research mentorship at Qwen · Tao Chen" index.html
rg -q "Research mentorship at Qwen · Haotian Liu" index.html
rg -q "Research mentee · Tommaso Felice Banfi" index.html
rg -q "EMNLP Main" index.html
rg -q "EMNLP Findings" index.html
test "$(rg -c 'class="argument-index"' research.html)" -eq 3
```

Expected: every command exits 0.

- [ ] **Step 3: Check local asset targets**

Run:

```bash
for target in styles.css script.js photo.jpg teasing.png research.html index.html; do test -e "$target"; done
```

Expected: every local target exists.

- [ ] **Step 4: Render desktop screenshots**

Run:

```bash
playwright screenshot --device="Desktop Chrome" "file://$PWD/index.html" /tmp/uncertainty-home-desktop.png
playwright screenshot --device="Desktop Chrome" "file://$PWD/research.html" /tmp/uncertainty-research-desktop.png
```

Expected: both screenshots are created without browser errors.

- [ ] **Step 5: Render mobile screenshots**

Run:

```bash
playwright screenshot --device="iPhone 13" --full-page "file://$PWD/index.html" /tmp/uncertainty-home-mobile.png
playwright screenshot --device="iPhone 13" --full-page "file://$PWD/research.html" /tmp/uncertainty-research-mobile.png
```

Expected: both screenshots are created. Inspect all four images for overflow, clipped text, broken cards, malformed superscripts, and incorrect ordering.

- [ ] **Step 6: Review the final commit range and working tree**

Run:

```bash
git log -5 --oneline
git show --stat --oneline HEAD~4..HEAD
git status --short
```

Expected: the implementation commits touch only `index.html` and `research.html`; `README.md` is still modified but unstaged; `.superpowers/` remains untracked; no implementation work is missing.
