# University AI Policy Dashboard

A research pipeline that maps how 20 universities — 10 Indian, 10 International — approach student use of AI tools across 15 policy dimensions. The output is a single interactive HTML dashboard where every colored cell is backed by a verbatim quote from an official source document.

---

## What This Project Does

Universities around the world are responding to generative AI in very different ways. Some have published comprehensive policies. Others have said nothing. This project systematically collects, curates, and visualises that evidence so the differences are immediately visible — and every classification can be traced back to the exact sentence it came from.

The end result is a grid where you can click any cell and see the original policy text, the source document it came from, and a direct link that opens that page and highlights the exact sentence in your browser.

---

## The 20 Universities

### India
IIT Bombay, IIT Delhi, IIT Madras, IISc Bangalore, IIM Ahmedabad, Delhi University, Jadavpur University, BITS Pilani, Manipal Institute of Technology, Ashoka University

### International
MIT, Stanford University, Harvard University, University of Oxford, University of Cambridge, ETH Zurich, National University of Singapore, University of Toronto, University of Melbourne, TU Munich

---

## Policy Dimensions Tracked

Each university is evaluated across up to 15 metrics:

- AI use in homework and assignments
- AI use during exams and in-class assessments
- AI use in thesis, dissertation and capstone projects
- Disclosure and citation requirements
- Penalties for unauthorised AI use
- Faculty discretion to set course-level rules
- Institutionally provided or approved AI tools
- AI use in research contexts
- Use of AI detection software (e.g. Turnitin)
- Coverage of image, audio and video generation
- Student training on responsible AI use
- Data privacy and confidentiality rules

---

## Classification System

| Colour | Meaning |
|--------|---------|
| 🟢 Green | Explicitly allowed, encouraged, or institutionally supported |
| 🟡 Yellow | Allowed with conditions, disclosure, or instructor approval |
| 🔴 Red | Explicitly prohibited or treated as academic misconduct |
| ⬜ Blank | No mention found in research or web search |

Every non-blank cell has a verbatim quote and a source URL. Blank cells record what was searched and why nothing was found.

---

## Repository Structure

```
.
├── README.md
├── urls.md                          # Links to all sources found during research
├── prompts/
│   ├── research_prompt.md           # Base deep research prompt (v1)
│   ├── research_prompt-1.md         # Refined deep research prompt (v2)
│   └── copilot-prompt.md            # Prompt sent to GitHub Copilot agent
├── research_outputs/
│   ├── claude.json                  # Output from Claude deep research
│   ├── chatgpt.json                 # Output from ChatGPT deep research (run 1)
│   ├── chatgpt-trail2.json          # Output from ChatGPT deep research (run 2)
│   ├── gemini.json                  # Output from Gemini deep research
│   ├── perplexity.json              # Output from Perplexity deep research
│   └── notebooklm.json              # Output from NotebookLM deep research
└── output/
    ├── index.html                   # Final dashboard (self-contained)
    └── sample.html                  # Sample dashboard with mock data
```

---

## How It Was Built

The project runs in two stages. Deep research agents handle evidence gathering. A coding agent handles classification and dashboard construction.

### Stage 1 — Deep Research

The same prompt was sent to five deep research tools: Claude, ChatGPT (run twice), Gemini, Perplexity, and NotebookLM. Two prompt versions were used — `research_prompt.md` was the initial version, `research_prompt-1.md` is the refined version that loosened evidence requirements to capture more results especially for Indian universities.

Each prompt instructs the tool to:
- Find the most authoritative and most recently updated AI policy document for each university
- Accept any level of evidence — institution-wide policy, faculty statement, course syllabus language — rather than returning empty if a formal policy does not exist
- For Indian universities specifically, also check UGC and AICTE national-level guidelines since many Indian institutions defer to national bodies rather than publishing their own policy
- Copy verbatim text from the source — no summarising, no paraphrasing
- Return the source URL and a short phrase from each excerpt that can be used to locate it on the page with Ctrl+F
- Output structured JSON so the coding agent can process all files consistently

Each tool ran independently and produced its own JSON output file stored in `research_outputs/`. ChatGPT was run twice because the first run had gaps that a second pass partially filled.

Links to all deep research agent sessions are collected in `urls.md`. Each JSON output file contains the verbatim source URLs and policy text discovered during that research session.

### Stage 2 — Copilot Coding Agent

All six JSON files from `research_outputs/` were placed in the Copilot agent workspace alongside `copilot-prompt.md`. The agent was instructed to:

1. Read all research files before writing any code
2. Curate the evidence — discard excerpts about IT infrastructure, general AI commentary, third-party sources, or anything too vague to drive a classification
3. Drop any policy column where fewer than three universities have real evidence
4. Use web search to fill gaps, verify quotes, and check for newer policy versions
5. Classify each cell as Green, Yellow, Red, or Blank based strictly on the curated evidence — no inferring or extrapolating
6. Build a self-contained `index.html` with a colour-coded grid, click-to-popup behaviour, filter controls, and source links using Chrome's `#:~:text=` fragment format so the exact quoted sentence is highlighted when the link is opened

Where research files disagreed on classification for the same cell, the agent used the more conservative call and flagged the conflict in the popup.

---

## Using the Dashboard

Open `output/index.html` in any modern browser. No server or internet connection required.

- **Filter** by region using the buttons at the top
- **Search** for a specific university by name
- **Sort** by any policy column by clicking its header
- **Click any cell** to open a popup with the classification, reason, verbatim source text, and document title
- **Click "Open source"** in the popup to go directly to the policy page with the quoted sentence highlighted

The highlight uses Chrome's Text Fragment URL feature (`#:~:text=`). It works in Chrome and Edge. In other browsers the page will open but the text will not be highlighted — use Ctrl+F with the phrase shown in the popup instead.

`output/sample.html` is an earlier prototype built with mock data used to validate the dashboard design before the real research was fed in.

---

## Why Five Research Tools

Each tool has different web access, different retrieval behaviour, and different tendencies around what it treats as a valid source. Running all five and reconciling:

- Reduces the chance of a policy being missed because one tool failed to find a particular page
- Surfaces disagreements that flag cells needing closer review
- Gives the coding agent richer evidence to work from, especially for universities where policy documents are hard to locate

The ChatGPT second run (`chatgpt-trail2.json`) was specifically targeted at universities that came back empty in the first pass.

---

## Limitations

- Indian universities are significantly underrepresented. Most have not published institution-wide AI policies as of 2026. Where cells are blank for Indian universities it reflects a genuine absence of public policy, not a gap in research effort.
- Policy documents change. URLs in `urls.md` may go stale over time. The dashboard reflects the state of evidence at the time the research was run.
- Some universities govern AI use through academic integrity frameworks that predate generative AI. Where excerpts come from older integrity policies extended to cover AI, this is noted in the cell popup.
- The `#:~:text=` highlight feature requires Chrome or Edge. It does not work in Safari or Firefox.