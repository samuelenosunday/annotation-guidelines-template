# Annotation Guidelines Template

> **How to use this template:** Copy this file to a new file called `guidelines.md` in your project. Fill in each section below. Delete the instructions in *italics*. Every completed project should have all 11 sections filled in before annotators begin work.

---

## 1. Project Overview

*Describe the project at a high level: what it is, who it's for, and what success looks like.*

**Project name:** [Project name]
**Client / internal team:** [Client]
**Task type:** [e.g., sentiment classification, NER, safety review]
**Total items:** [e.g., 5,000]
**Timeline:** [Start date → End date]
**Annotators:** [Number and names if known]

**What success looks like:** *One paragraph describing what a successfully completed project looks like — high inter-annotator agreement, low rejection rate, delivery on time, etc.*

---

## 2. Task Definition

*State the exact task an annotator is performing. Be specific — "label each item" is not a task definition.*

**What the annotator does:**

*For each item, do X. Then do Y. Then do Z.*

**Example (fill in):**

> For each customer review, read the full text and assign exactly one sentiment label: `positive`, `negative`, or `neutral`. Base the label on the overall tone of the review, not individual sentences.

**What the annotator does NOT do:**

*List common misunderstandings up front.*

- Do not edit the original text.
- Do not guess at the intent behind the text.
- Do not assign multiple labels unless the task explicitly says so.

**Time per item (target):** [e.g., 30–60 seconds]

---

## 3. Label Taxonomy

*List every label an annotator can use, with a precise definition for each. No label should be vague.*

| Label | Definition | When to use | When NOT to use |
|---|---|---|---|
| `label_1` | [Precise definition] | [Specific conditions] | [Conditions where you should use a different label] |
| `label_2` | [Precise definition] | [Specific conditions] | [Conditions where you should use a different label] |
| `label_3` | [Precise definition] | [Specific conditions] | [Conditions where you should use a different label] |

**Total labels:** [e.g., 3]

**Mutually exclusive?** [Yes / No — if no, describe how multiple labels can apply]

---

## 4. Decision Rules

*The rules an annotator follows when classifying an item. These should be checkable — an annotator should be able to look at an item and apply the rules mechanically.*

**Rule 1:** [e.g., If the text contains any threatening language, label it `toxic` regardless of other content.]

**Rule 2:** [e.g., If the text is purely factual and emotionless, label it `neutral`.]

**Rule 3:** [e.g., If a reviewer expresses both positive and negative sentiment, use the dominant sentiment (>50% of the text) to decide.]

**Rule 4:** [Add as many as needed]

---

## 5. Edge Cases

*The tricky cases that trip people up. These should be listed explicitly, with examples for each.*

**Edge Case 1: Sarcasm**

- **What it is:** Text that says one thing but means the opposite.
- **How to handle:** Label based on the *intended* meaning, not the literal words.
- **Example:** "Great, another Monday morning meeting." → `negative` (sarcastic, not positive)

**Edge Case 2: Mixed sentiment**

- **What it is:** A review that has both strongly positive and strongly negative statements.
- **How to handle:** Use the dominant sentiment. If truly 50/50, use `neutral`.
- **Example:** "The food was amazing but the service was terrible." → `neutral` (balanced)

**Edge Case 3: [Add more as needed]**

- **What it is:** [Description]
- **How to handle:** [Rule]
- **Example:** [Sample]

---

## 6. Positive Examples

*3–5 items that are clearly correctly annotated. These anchor "what good looks like."*

**Example 1:**

> **Input:** "This is the best restaurant I've been to in years. The food was incredible and the staff were friendly."
>
> **Annotation:** `positive`
>
> **Why:** Clear positive sentiment throughout. Enthusiastic praise with no negative content.

**Example 2:**

> **Input:** "Terrible experience. The waiter was rude and the food arrived cold."
>
> **Annotation:** `negative`
>
> **Why:** Negative sentiment throughout. Two specific complaints (service, food quality).

**Example 3:**

> **Input:** "I ordered the chicken sandwich. It arrived at 7:42pm."
>
> **Annotation:** `neutral`
>
> **Why:** Purely factual statement with no evaluative language.

---

## 7. Negative Examples

*3–5 items that are clearly wrong annotations, with an explanation of why they're wrong. These anchor "what bad looks like."*

**Example 1:**

> **Input:** "I love this place, but the parking is a nightmare."
>
> **Wrong annotation:** `positive`
>
> **Why it's wrong:** Ignores the negative clause about parking. Should be `neutral` (mixed sentiment) or `negative` (if the parking complaint dominates).

**Example 2:**

> **Input:** "Great, another delayed flight."
>
> **Wrong annotation:** `positive` (literal reading)
>
> **Why it's wrong:** Sarcastic — should be `negative`. Literal word "great" is not sufficient.

**Example 3:**

> **Input:** "The product works as described."
>
> **Wrong annotation:** `positive`
>
> **Why it's wrong:** Neutral factual statement. "Works as described" is not praise — it's an expectation met.

---

## 8. Ambiguous Examples

*2–3 items that are genuinely borderline, with the reasoning for why they're hard and what the correct call is.*

**Example 1:**

> **Input:** "The food was fine."
>
> **Ambiguous because:** "Fine" could be lukewarm neutral or mildly positive. Not enthusiastic, not negative.
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

---

## 9. QA Process

*How annotations will be reviewed. This section is critical — it's what ensures quality.*

**Review process:**

1. **First pass:** Annotator labels all items in their assigned batch.
2. **Second pass:** QA reviewer samples 20% of the annotator's work.
3. **Gold standard items:** Every batch includes 10 gold-standard items with known correct labels. Annotator must achieve ≥80% accuracy on gold items.
4. **Inter-annotator agreement:** Every 100 items, a second annotator independently labels the same items. Cohen's Kappa is computed.
5. **Rejection:** If Kappa < 0.7 or gold-standard accuracy < 80%, the batch is reviewed for systematic errors.

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

*When should an annotator stop and flag an item instead of labeling it?*

**Escalate if:**

- The item is genuinely ambiguous and not covered by the guidelines
- The item is missing key information (e.g., text cut off)
- The item is in a language the annotator doesn't speak fluently
- The item contains content that is disturbing or triggers a personal reaction
- The item appears to be a duplicate
- Following the guidelines would produce an outcome the annotator thinks is wrong

**How to escalate:**

- Do NOT guess. Leave the item unlabeled.
- Note the item ID and reason in the escalation log.
- Submit the escalation to the project lead within 24 hours.
- Continue with other items while waiting for a decision.

**What happens after escalation:**

- Project lead reviews and either: (a) makes a call, (b) updates the guidelines, or (c) removes the item from the project.
- If the guidelines were updated, all annotators are notified and may need to revisit their batch.

---

## 11. Version History

*Every change to the guidelines should be logged here. This is the audit trail.*

| Version | Date | Change | Reason |
|---|---|---|---|
| 1.0 | [YYYY-MM-DD] | Initial version | Project kickoff |
| 1.1 | [YYYY-MM-DD] | [Description] | [Why it was changed] |
| 1.2 | [YYYY-MM-DD] | [Description] | [Why it was changed] |

---

## Template Checklist

Before publishing this guideline, verify that **all** of the following are true:

- [ ] Every label is defined precisely
- [ ] Every label has "when to use" and "when NOT to use"
- [ ] At least 3 edge cases are documented
- [ ] At least 3 positive examples are included
- [ ] At least 3 negative examples are included
- [ ] At least 2 ambiguous examples are included
- [ ] QA process is described
- [ ] Escalation criteria are described
- [ ] Inter-annotator agreement threshold is specified (recommended: ≥0.7)
- [ ] Gold-standard accuracy threshold is specified (recommended: ≥80%)
- [ ] Version history is present
- [ ] A pilot (2–3 annotators, 50 items) has been run

If any of these is missing, **do not deploy the guideline**. Ambiguous guidelines are the #1 cause of annotation quality failures.

---

*This template is part of the [annotation-guidelines-template](https://github.com/samuelenosunday/annotation-guidelines-template) repository by Samuel Eno Sunday. Free to reuse, adapt, and modify.*
