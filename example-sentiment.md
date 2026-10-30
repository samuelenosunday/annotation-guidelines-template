# Example: Sentiment Classification Guidelines

> **Worked example.** This is a fully completed annotation guideline for a sentiment classification project, based on `TEMPLATE.md`. Use it as a reference for what a complete, deployable guideline looks like.

---

## 1. Project Overview

**Project name:** Customer Review Sentiment Classification
**Client / internal team:** E-commerce product team
**Task type:** 3-class sentiment classification (positive / negative / neutral)
**Total items:** 5,000 customer reviews
**Timeline:** 4 weeks
**Annotators:** 4 annotators

**What success looks like:** Inter-annotator agreement (Cohen's Kappa) ≥ 0.75, gold-standard accuracy ≥ 85%, delivery within 4 weeks, rejection rate below 10%.

---

## 2. Task Definition

**What the annotator does:**

Read each customer review in full and assign exactly one sentiment label: `positive`, `negative`, or `neutral`. Base the label on the overall tone of the review — not individual sentences, and not the reviewer's rating if a rating is present (ignore ratings).

**What the annotator does NOT do:**

- Do not edit the review text.
- Do not infer sentiment about products that aren't mentioned.
- Do not assign multiple labels — exactly one label per review.
- Do not use the star rating to make decisions.

**Time per item (target):** 30–45 seconds

---

## 3. Label Taxonomy

| Label | Definition | When to use | When NOT to use |
|---|---|---|---|
| `positive` | The review expresses clear satisfaction, praise, or approval | Reviewer is happy overall, and the positive content outweighs any negative | The review is lukewarm ("it's fine") — use `neutral` instead |
| `negative` | The review expresses clear dissatisfaction, criticism, or disapproval | Reviewer is unhappy overall, and the negative content outweighs any positive | The review contains mild complaints but is broadly positive — use `positive` |
| `neutral` | The review is factual, balanced, or lukewarm — no clear positive or negative lean | Reviewer describes facts only, expresses no strong opinion, or the positive and negative are equal | The review clearly leans one way — use `positive` or `negative` |

**Total labels:** 3
**Mutually exclusive?** Yes — exactly one label per review.

---

## 4. Decision Rules

**Rule 1:** If the review contains any clear praise AND any clear criticism, use the **dominant sentiment** — the one that occupies more than 50% of the review.

**Rule 2:** If the review is purely factual with no evaluative language, label it `neutral`.

**Rule 3:** If the review contains sarcasm, label based on the intended meaning, not the literal words.

**Rule 4:** If the review is a single sentence with ambiguous language ("it was fine"), default to `neutral`.

**Rule 5:** Ignore star ratings. Even if the review is 5 stars but the text is negative, the text determines the label.

---

## 5. Edge Cases

**Edge Case 1: Sarcasm**

- **What it is:** Text that says one thing but means the opposite.
- **How to handle:** Label based on intended meaning, not literal words.
- **Example:** "Great, another delayed flight." → `negative` (sarcastic, not positive).

**Edge Case 2: Mixed sentiment**

- **What it is:** A review with strongly positive AND strongly negative statements.
- **How to handle:** Use dominant sentiment. If exactly 50/50, use `neutral`.
- **Example:** "The food was amazing but the service was terrible." → `neutral` (balanced).

**Edge Case 3: The lukewarm review**

- **What it is:** A review that is technically positive but has no enthusiasm.
- **How to handle:** Default to `neutral` for lukewarm language.
- **Example:** "The product works as described." → `neutral` (expectation met, not exceeded).

**Edge Case 4: The single-word review**

- **What it is:** A review that is one or two words.
- **How to handle:** Label based on the word's sentiment. If genuinely ambiguous ("meh"), use `neutral`.
- **Example:** "Excellent!" → `positive`. "Terrible." → `negative`. "Okay." → `neutral`.

---

## 6. Positive Examples

**Example 1:**

> **Input:** "This is the best restaurant I've been to in years. The food was incredible and the staff were friendly."
>
> **Annotation:** `positive`
>
> **Why:** Clear positive sentiment throughout. Enthusiastic praise with no negative content.

**Example 2:**

> **Input:** "Absolutely love this product. Works perfectly and arrived quickly."
>
> **Annotation:** `positive`
>
> **Why:** Strong positive language ("absolutely love"), two specific positive points (works, arrived quickly), no negative content.

**Example 3:**

> **Input:** "I was hesitant to buy at first, but I'm really glad I did. The quality exceeded my expectations."
>
> **Annotation:** `positive`
>
> **Why:** Even though the review opens with hesitation, the dominant sentiment is positive ("really glad," "exceeded my expectations").

---

## 7. Negative Examples

**Example 1:**

> **Input:** "I love this place, but the parking is a nightmare."
>
> **Wrong annotation:** `positive`
>
> **Why it's wrong:** Ignores the negative clause about parking. Should be `neutral` (mixed) or `negative` (if parking complaint dominates).

**Example 2:**

> **Input:** "Great, another delayed flight."
>
> **Wrong annotation:** `positive` (literal reading)
>
> **Why it's wrong:** Sarcastic — should be `negative`. The literal word "great" is not sufficient.

**Example 3:**

> **Input:** "The product works as described."
>
> **Wrong annotation:** `positive`
>
> **Why it's wrong:** Neutral factual statement. "Works as described" is an expectation met, not praise.

---

## 8. Ambiguous Examples

**Example 1:**

> **Input:** "The food was fine."
>
> **Ambiguous because:** "Fine" could be lukewarm neutral or mildly positive.
>
> **Correct annotation:** `neutral`
>
> **Reasoning:** "Fine" is the minimum of acceptable — neither enthusiastic praise nor criticism. Default to neutral for lukewarm phrasing.

**Example 2:**

> **Input:** "I wouldn't recommend this to anyone, but I have to admit the dessert was good."
>
> **Ambiguous because:** Overall negative recommendation, but one strong positive statement.
>
> **Correct annotation:** `negative`
>
> **Reasoning:** The overall recommendation is what matters. The positive exception doesn't outweigh the explicit "wouldn't recommend."

**Example 3:**

> **Input:** "The service was slow but the food made up for it."
>
> **Ambiguous because:** Negative point followed by a positive compensation.
>
> **Correct annotation:** `positive`
>
> **Reasoning:** "Made up for it" signals that the positive outweighs the negative. Dominant sentiment is positive.

---

## 9. QA Process

**Review process:**

1. **First pass:** Annotator labels all items in their batch.
2. **Second pass:** QA reviewer samples 20% of the annotator's work.
3. **Gold standard items:** Every batch contains 10 gold-standard items with known correct labels. Annotator must achieve ≥85% accuracy on gold items.
4. **Inter-annotator agreement:** Every 100 items, a second annotator independently labels the same items. Cohen's Kappa is computed.
5. **Rejection:** If Kappa < 0.75 or gold-standard accuracy < 85%, the batch is reviewed for systematic errors.

**QA reviewer responsibilities:**

- Review sampled items against the guidelines
- Flag systematic errors (patterns, not one-offs)
- Track per-annotator quality metrics
- Escalate ambiguous items to project lead

**Annotator responsibilities:**

- Follow the guidelines exactly
- Flag items where the guidelines are unclear (via escalation, not guessing)
- Respond to QA feedback promptly
- Re-do rejected items

---

## 10. Escalation Criteria

**Escalate if:**

- The review is genuinely ambiguous and not covered by the guidelines
- The review is truncated (missing text)
- The review is in a language other than English
- The review contains personal information that should be redacted
- The review appears to be a duplicate of another review in the batch
- Following the guidelines would produce an outcome the annotator thinks is clearly wrong

**How to escalate:**

- Do NOT guess. Leave the item unlabeled.
- Note the item ID and reason in the escalation log.
- Submit the escalation to the project lead within 24 hours.
- Continue with other items while waiting for a decision.

---

## 11. Version History

| Version | Date | Change | Reason |
|---|---|---|---|
| 1.0 | 2024-01-01 | Initial version | Project kickoff |
| 1.1 | 2024-01-08 | Added Edge Case 4 (single-word reviews) | 3 annotators flagged the same issue during pilot |
| 1.2 | 2024-01-15 | Clarified Rule 5 (ignore star ratings) | 2 batches rejected for using ratings instead of text |

---

## What This Example Demonstrates

A complete, deployable sentiment classification guideline. Key features:

- **Every label has "when to use" and "when NOT to use"** — no ambiguity.
- **Edge cases are documented with examples** — annotators know how to handle sarcasm, mixed sentiment, lukewarm reviews, single-word reviews.
- **Positive and negative examples anchor "what good looks like"** — and each is explained.
- **Ambiguous examples show reasoning** — not just "label this X" but *why*.
- **QA process specifies thresholds** — 20% sampling, 85% gold accuracy, 0.75 Kappa.
- **Escalation criteria are explicit** — annotators know when to stop and flag.
- **Version history shows real iteration** — the guideline improved based on pilot feedback.

This is the level of specificity that produces high-quality annotated data.
