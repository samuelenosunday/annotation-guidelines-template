# Example: Safety Classification Guidelines

> **Worked example.** This is a fully completed annotation guideline for a safety/toxicity classification project, based on `TEMPLATE.md`. It demonstrates how the template applies to a higher-stakes domain where misclassification has real consequences.

---

## 1. Project Overview

**Project name:** User Content Safety Classification
**Client / internal team:** Trust & Safety team
**Task type:** Multi-label safety classification (toxic / threatening / sexual / PII / safe)
**Total items:** 10,000 user-generated posts
**Timeline:** 6 weeks
**Annotators:** 6 annotators (all trained on safety guidelines)

**What success looks like:** Inter-annotator agreement (Cohen's Kappa) ≥ 0.80, gold-standard accuracy ≥ 90%, zero escaped actionable threats, delivery within 6 weeks, rejection rate below 8%.

**Note:** This is a high-stakes domain. False negatives (missed unsafe content) are worse than false positives (over-flagged safe content). The QA process reflects this.

---

## 2. Task Definition

**What the annotator does:**

Read each post in full and assign **all applicable safety labels** (multi-label — a post can be toxic AND threatening). If no label applies, assign `safe`. Do not assign `safe` alongside other labels.

**What the annotator does NOT do:**

- Do not edit the post text.
- Do not assign labels based on the user's identity or history — only on the post content.
- Do not assume context that isn't in the post.
- Do not label as `safe` to avoid escalating — when in doubt, escalate.

**Time per item (target):** 45–90 seconds

---

## 3. Label Taxonomy

| Label | Definition | When to use | When NOT to use |
|---|---|---|---|
| `toxic` | Language that attacks, insults, or demeans a person or group | Insults, slurs, harassment, dehumanizing language | Strong criticism of ideas or institutions — use `safe` unless it crosses into personal attack |
| `threatening` | Language that expresses intent to cause harm | Explicit threats of violence, damage, or harm | Vague expressions of anger without a specific threat |
| `sexual` | Sexually explicit content, or solicitation | Explicit sexual descriptions, sexual solicitation, sexual content involving minors | Non-explicit romantic content — use `safe` unless explicit |
| `pii` | Content that includes personal identifiable information | Full names + addresses, phone numbers, SSNs, financial account numbers | Public figures' public information — use `safe` unless it's private |
| `safe` | No safety concern — content is appropriate for a general audience | None of the above apply | Do not use when other labels apply — `safe` is exclusive |

**Total labels:** 5
**Mutually exclusive?** No — multiple labels can apply (e.g., `toxic` + `threatening`). `safe` is exclusive — cannot combine with other labels.

---

## 4. Decision Rules

**Rule 1:** A post can have multiple labels. Assign every label that applies, not just the most severe.

**Rule 2:** If the post is a quote of toxic content (e.g., "someone said [slur] to me"), label based on whether the post itself promotes or endorses the content. Quoting for reporting is `safe` unless the post adds endorsement.

**Rule 3:** If the post is ambiguous, default to the more conservative label. Escalation is always preferred over misclassification.

**Rule 4:** For threats — the threshold is *explicit intent*. "I hate you" is `toxic` but not `threatening`. "I will hurt you" is `threatening`.

**Rule 5:** For PII — a partial name alone is not PII. The threshold is: could someone use this information to locate or harm the person? If yes, label `pii`.

**Rule 6:** The `safe` label is exclusive — do not assign `safe` alongside any other label.

---

## 5. Edge Cases

**Edge Case 1: Quoted toxic content**

- **What it is:** A post that quotes toxic content — e.g., "My coworker called me [slur] today."
- **How to handle:** Label based on whether the post endorses the toxic content. Reporting/experiencing is `safe`. Promoting/endorsing is `toxic`.
- **Example:** "Someone sent me a message saying [slur]. I'm reporting them." → `safe` (reporting).

**Edge Case 2: Strong criticism vs. toxic**

- **What it is:** Harsh criticism of a public figure, company, or idea.
- **How to handle:** Criticism is `safe` unless it crosses into personal attack, slurs, or threats.
- **Example:** "The CEO is incompetent and should be fired." → `safe` (criticism, not attack). "The CEO is a [slur] who should die." → `toxic` + `threatening`.

**Edge Case 3: Vague threats**

- **What it is:** Expressions of anger or violence without a specific target or intent.
- **How to handle:** Vague expressions ("I'm so mad I could kill someone") are `safe` if there is no specific target or intent. Explicit intent ("I'm going to kill him") is `threatening`.
- **Example:** "I'm so mad I could punch a wall." → `safe` (no specific target). "I'm going to punch John tomorrow." → `threatening`.

**Edge Case 4: PII in public content**

- **What it is:** Public figures' public information, or news article content.
- **How to handle:** Public figures' public information is `safe`. Private information, even about public figures, is `pii`.
- **Example:** "President Biden's address is 1600 Pennsylvania Ave." → `safe` (public). "President Biden's personal phone is [number]." → `pii` (private).

**Edge Case 5: Romance vs. sexual**

- **What it is:** Romantic or affectionate content that is not sexually explicit.
- **How to handle:** Romantic content is `safe` unless it's sexually explicit or solicitation. "I love you" is `safe`. Explicit sexual content is `sexual`.

---

## 6. Positive Examples

**Example 1:**

> **Input:** "I'll find you and hurt you, I know where you work."
>
> **Annotation:** `threatening` + `toxic`
>
> **Why:** Explicit threat of harm with specific intent ("find you," "hurt you"). Also toxic (harassment).

**Example 2:**

> **Input:** "Her phone number is 555-0142, she lives at 123 Main Street."
>
> **Annotation:** `pii`
>
> **Why:** Full name implied (She) + phone number + address = PII. Could be used to locate or harm.

**Example 3:**

> **Input:** "I completely disagree with the president's policy. It's harmful to working families."
>
> **Annotation:** `safe`
>
> **Why:** Strong criticism of policy, not a personal attack. No slurs, no threats, no PII. Legitimate political discourse.

---

## 7. Negative Examples

**Example 1:**

> **Input:** "My coworker is such a [slur]. I hate working with him."
>
> **Wrong annotation:** `safe`
>
> **Why it's wrong:** Contains a slur — `toxic`. The `safe` label cannot be applied when toxic content is present, even if the annotator doesn't personally find it offensive.

**Example 2:**

> **Input:** "I'll kill him."
>
> **Wrong annotation:** `toxic` only
>
> **Why it's wrong:** Should be `toxic` + `threatening`. Explicit threat of violence is a separate category that requires the `threatening` label in addition to `toxic`.

**Example 3:**

> **Input:** "Here's a picture of my friend's home: [address]."
>
> **Wrong annotation:** `safe` (shared privately)
>
> **Why it's wrong:** Shares a private address without consent — `pii`. Even if the user is sharing about a friend, the friend's private information is PII.

---

## 8. Ambiguous Examples

**Example 1:**

> **Input:** "I hate [group] so much, they should all be [explicit violence]."
>
> **Ambiguous because:** It's clearly toxic AND threatening. The ambiguity is whether both labels should be applied or just the more severe one.
>
> **Correct annotation:** `toxic` + `threatening`
>
> **Reasoning:** Both labels apply. The taxonomy allows multiple labels, and "hate" + explicit violence = toxic AND threatening. Do not simplify to just the more severe label — that loses information.

**Example 2:**

> **Input:** "Someone should teach her a lesson."
>
> **Ambiguous because:** "Teach a lesson" could be a harmless suggestion (a warning) or a threat.
>
> **Correct annotation:** `safe` (escalate to reviewer)
>
> **Reasoning:** Without a specific target or explicit harm, this is `safe` — but it's borderline and should be escalated to a reviewer.

**Example 3:**

> **Input:** "Here's the address of the store: 123 Main Street."
>
> **Ambiguous because:** Is a store address PII?
>
> **Correct annotation:** `safe`
>
> **Reasoning:** Store addresses are public business information. `pii` applies to private individuals, not public businesses.

---

## 9. QA Process

**Review process:**

1. **First pass:** Annotator labels all items in their batch.
2. **Second pass:** QA reviewer samples 30% of the annotator's work (higher than sentiment because of stakes).
3. **Gold standard items:** Every batch contains 20 gold-standard items with known correct labels. Annotator must achieve ≥90% accuracy on gold items.
4. **Inter-annotator agreement:** Every 100 items, a second annotator independently labels the same items. Cohen's Kappa is computed.
5. **Rejection:** If Kappa < 0.80 or gold-standard accuracy < 90%, the batch is reviewed for systematic errors.
6. **Zero-escape rule:** Any `threatening` item that was labeled `safe` triggers an immediate batch review, regardless of other metrics.

**QA reviewer responsibilities:**

- Review sampled items against the guidelines
- Flag systematic errors (patterns, not one-offs)
- Track per-annotator quality metrics
- Escalate ambiguous items to project lead
- **Escalate any `threatening` item immediately** — do not wait for weekly review

**Annotator responsibilities:**

- Follow the guidelines exactly
- **When in doubt, escalate** — this is a high-stakes domain, and false negatives are worse than false positives
- Respond to QA feedback promptly
- Re-do rejected items

---

## 10. Escalation Criteria

**Escalate if:**

- The post is ambiguous and could be interpreted as unsafe in some context
- The post contains a specific threat with a real-sounding target
- The post contains PII that could be used to harm a person
- The post contains content involving minors
- The post contains content that the annotator finds personally disturbing
- The post appears to be part of a coordinated harassment campaign
- Following the guidelines would produce an outcome the annotator thinks is clearly wrong

**How to escalate:**

- Do NOT guess. Leave the item unlabeled.
- Note the item ID and reason in the escalation log.
- Submit the escalation to the project lead **within 2 hours** (higher urgency than sentiment — because of the stakes).
- Continue with other items while waiting for a decision.

**What happens after escalation:**

- Project lead reviews and either: (a) makes a call, (b) updates the guidelines, or (c) escalates further to Trust & Safety.
- If the guidelines were updated, all annotators are notified within 24 hours and may need to revisit their batch.

---

## 11. Version History

| Version | Date | Change | Reason |
|---|---|---|---|
| 1.0 | 2024-02-01 | Initial version | Project kickoff |
| 1.1 | 2024-02-08 | Added Edge Case 1 (quoted toxic content) | 4 annotators flagged the same issue during pilot |
| 1.2 | 2024-02-15 | Clarified Rule 6 (`safe` is exclusive) | 6 batches rejected for double-labeling `safe` + `toxic` |
| 1.3 | 2024-02-22 | Added zero-escape rule for `threatening` | Batch missed a real threat — QA process needed tightening |
| 1.4 | 2024-03-01 | Clarified Rule 5 (PII threshold) | Multiple misclassifications of public figures' info |

---

## What This Example Demonstrates

A complete, deployable safety classification guideline. Key differences from the sentiment example:

1. **Higher stakes = higher thresholds.** 30% QA sampling (vs. 20%), 90% gold accuracy (vs. 85%), 0.80 Kappa (vs. 0.75).
2. **Multi-label taxonomy.** Posts can be toxic AND threatening. `safe` is exclusive.
3. **Zero-escape rule.** Any missed `threatening` item triggers a batch review, because false negatives are worse than false positives in safety work.
4. **2-hour escalation window** (vs. 24 hours for sentiment) because of urgency.
5. **Explicit handling of quoted content, criticism vs. attack, vague threats, and public vs. private PII.**

This is what a real Trust & Safety guideline looks like. It's the kind of document that would be shipped to 6+ annotators across multiple weeks of high-stakes work.

The contrast between this example and the sentiment example shows that **guideline design depends on the domain** — same template, different emphasis.
