# University AI Policy Dashboard

This project maps how 20 universities (10 in India, 10 International) govern student use of generative AI across policy categories, and turns that evidence into a clickable dashboard.

The final output is a single standalone HTML file where each colored cell is traceable to verbatim source text.

## Dashboard

- Open dashboard: [output/index.html](output/index.html)


---

## What I Built

The workflow has two parts:

1. Deep research prompt runs in batches of 5 universities at a time.
2. Copilot prompt consumes curated research outputs and generates the final dashboard.

---

## Universities Covered

### India

IIT Bombay, IIT Delhi, IIT Madras, IISc Bangalore, IIM Ahmedabad, Delhi University, Jadavpur University, BITS Pilani, Manipal Academy of Higher Education, Ashoka University

### International

MIT, Stanford University, Harvard University, University of Oxford, University of Cambridge, ETH Zurich, National University of Singapore, University of Toronto, University of Melbourne, TU Munich

---

## Policy Categories in Dashboard

The dashboard tracks these categories:

- Essays
- Written Assignments
- Take-home Exams
- In-class Exams/Quizzes
- Coding/Programming
- Lab Reports
- Thesis/Dissertation
- Research Papers
- Literature Reviews
- Paraphrasing/Summarizing
- Proofreading/Editing
- Translation
- Citation/Disclosure
- Brainstorming/Ideation
- Fact-checking
- Outlining/Drafting

---

## Classification Scale

| Color | Meaning |
|---|---|
| Green | Explicitly allowed or encouraged |
| Yellow | Conditional / disclosure required / instructor approval needed |
| Red | Prohibited / treated as misconduct |
| Blank | No reliable policy evidence found |

---

## Scoring Logic

- Cell score (S): Red=0, Yellow=1, Green=2, Green+=3
- Base Friendliness (B): sum(S) / (3 * N_u)
- AI Friendliness Score: 100 * B * (0.7 + 0.3 * (N_u / 25))
- N_u = number of non-blank policy cells for a university

---

## End-to-End Workflow

### Stage 1: Deep Research Collection

- Prompt source: [prompts/research-prompt.md](prompts/research-prompt.md)
- Execution mode: Deep research
- Batch strategy: 5 universities per run
- Output files: [research_output/p1.md](research_output/p1.md), [research_output/p2.md](research_output/p2.md), [research_output/p3.md](research_output/p3.md), [research_output/p4.md](research_output/p4.md)

What this stage does:

- Finds policy language and related institutional guidance
- Captures verbatim excerpts and source links
- Organizes evidence university-by-university for downstream curation

### Stage 2: Copilot Curation + Dashboard Build

- Prompt source: [prompts/copilot-prompt.md](prompts/copilot-prompt.md)
- Inputs: all files in [research_output](research_output)
- Output: [output/index.html](output/index.html)

What this stage does:

- Merges and curates evidence
- Applies classification rules per policy category
- Computes friendliness scores
- Builds a responsive, interactive single-file dashboard

---

## Repository Layout

```text
.
├── README.md
├── urls.md
├── prompts/
│   ├── research-prompt.md
│   └── copilot-prompt.md
├── research_output/
│   ├── p1.md
│   ├── p2.md
│   ├── p3.md
│   └── p4.md
└── output/
        └── index.html
```

---

## Dashboard Features

- Search by university name
- Region filters (India / International / All)
- Sorting by friendliness score
- Cell click modal with:
    - classification
    - one-line reason
    - verbatim quote
    - source URL

---

## Notes and Constraints

- Policy coverage quality varies by university and by department-level transparency.
- Some institutions publish central AI policy; others rely on local faculty/course-level guidance.
- Public policy pages can change over time, so periodic reruns are recommended.

---

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE).