**Role:** Data Research & Visualization Agent  
**Input:** All provided `p*.md` research files (e.g., `p1.md`, `p2.md`, etc.).
**policies:** Essays, Written Assignments, Take-home Exams, In-class Exams/Quizzes, Coding/Programming, Lab Reports, Thesis/Dissertation, Research Papers, Literature Reviews, Paraphrasing/Summarizing, Proofreading/Editing, Translation, Citation/Disclosure, Brainstorming/Ideation, Fact-checking, Outlining/Drafting

**1. Data Processing Rules:**
* **De-duplicate:** If a university appears in multiple files, merge entries using the most recent/detailed evidence.
* **Categorize:** Group by Region (**India** vs. **International**).
* **Scoring Logic:**
    * **Cell Score ($S$):** Red = 0, Yellow = 1, Green = 2, Green+ = 3.
    * **Base Friendliness ($B$):** $\frac{\sum S}{3 \times N_u}$ (where $N_u$ is the count of non-blank cells).
    * **AI Friendliness Score:** $100 \times B \times (0.7 + 0.3 \times \frac{N_u}{25})$.

**2. Output Requirement: Single Standalone HTML (`index.html`)**
Produce a self-contained HTML file featuring:
* **Interactive Table:** Rows (Universities) vs. Columns (name of policy)
* **Color Coding:** * **Green:** Explicitly allowed.
    * **Yellow:** Conditional/Disclosure required.
    * **Red:** Prohibited/Misconduct.
    * **Grey/Blank:** No data found.
* **Interactive Features:**
    * **Search:** Filter by university name.
    * **Region Toggle:** Filter by India, International, or All.
    * **Sort:** Sort by AI Friendliness Score (Default: Descending).
    * **Detail Popups:** Clicking a cell opens a modal/popup displaying:
        * University name and Policy topic.
        * Classification and one-line reason.
        * **Multiple Exact Quotes** (up to 3 verbatim excerpts from input, each on separate lines).
        * Source Links (using `:~:text=` fragments for direct navigation to each quote).


**3. Validation Checklist:**
* Ensure every non-blank cell has a supporting quote and URL.
* Verify that the scores calculated match the provided formulas exactly.
* Confirm the final HTML is responsive and contains all data from all input files.
