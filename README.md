# Annotation Guidelines Template

A professional, reusable template for writing **annotation guidelines** for AI training and data labeling projects.

Built for annotators, QA reviewers, project leads, and anyone who needs to write clear, consistent guidelines that reduce disagreement and improve data quality.

---

## Why This Exists

Most AI training projects fail not because the model is bad — but because the **annotation guidelines are ambiguous**. Annotators disagree on edge cases, QA rejects work for reasons that weren't documented, and the resulting data is noisy.

This template solves that problem. It's a structured starting point for writing annotation guidelines that:

- Define the task precisely
- Specify the label taxonomy
- Handle edge cases explicitly
- Include worked examples (good and bad)
- Describe the QA process
- Set escalation criteria for ambiguous cases

Anyone can follow this template to write guidelines for a new project — and any annotator can read those guidelines and produce consistent output.

---

## What's Inside

| File | Purpose |
|---|---|
| `TEMPLATE.md` | The reusable template itself — copy this to start a new project |
| `example-sentiment.md` | Worked example: sentiment classification guidelines |
| `example-safety.md` | Worked example: safety/toxicity classification guidelines |

---

## How to Use It

1. **Copy `TEMPLATE.md`** to a new file named `guidelines.md` in your project.
2. **Fill in each section** — the template lists every section you need.
3. **Use the worked examples** (`example-sentiment.md`, `example-safety.md`) to see what a complete, high-quality guideline looks like.
4. **Pilot the guidelines** with 2–3 annotators on a small batch before full deployment.
5. **Measure inter-annotator agreement** (Cohen's Kappa) after the pilot.
6. **Revise the guidelines** if agreement is below 0.7.
7. **Publish and version control** the final version.

This is the same process used on major AI training platforms (Outlier, Surge, Scale AI, Handshake).

---

## Sections in the Template

Every complete annotation guideline should have:

1. **Project Overview** — what this project is, who it's for, what success looks like
2. **Task Definition** — the exact task an annotator is performing
3. **Label Taxonomy** — every label, defined precisely
4. **Decision Rules** — how to handle specific situations
5. **Edge Cases** — the tricky cases, with examples
6. **Positive Examples** — 3–5 clearly correct annotations
7. **Negative Examples** — 3–5 clearly wrong annotations
8. **Ambiguous Examples** — 2–3 borderline cases with reasoning
9. **QA Process** — how annotations will be reviewed
10. **Escalation Criteria** — when to flag for human review
11. **Version History** — what changed and when

---

## Why This Matters for AI Training

On major platforms, the difference between a top-tier annotator and an average one is not speed — it's **guideline adherence**. An annotator who can read a rubric and apply it consistently is more valuable than a fast one who introduces noise.

And the people who write the guidelines? They're the ones who get promoted to QA lead, project manager, or senior evaluator. That's the tier this template targets.

---

## Files in This Repo

| File | Purpose |
|---|---|
| `README.md` | This documentation |
| `TEMPLATE.md` | The reusable annotation guideline template |
| `example-sentiment.md` | Worked example: sentiment classification |
| `example-safety.md` | Worked example: safety/toxicity classification |

---

## Tech Stack

- **Language:** Markdown (no code, no dependencies)
- **Use case:** Template + worked examples
- **Version control:** Git

---

## Future Improvements

- Add worked examples for NER, intent classification, and summarization
- Add a "pilot protocol" section with steps for measuring IAA
- Add a lightweight Python script that validates guideline completeness (checks for required sections)

---

## About the Author

**Samuel Eno Sunday** — AI Training Specialist & LLM Quality Analyst

- LinkedIn: [linkedin.com/in/samuelenosunday001](https://www.linkedin.com/in/samuelenosunday001/)
- GitHub: [github.com/samuelenosunday](https://github.com/samuelenosunday)
- Email: samuelenosunday@gmail.com

*Open to remote contract, part-time, and project-based AI training roles.*
