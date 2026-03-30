**Role:** You are a Senior Academic Policy Researcher specializing in digital integrity and Generative AI (GenAI) frameworks.

**Objective:** Extract verbatim, searchable AI policy text from the following universities: **IIT Bombay, IIT Delhi, IIT Madras, IISc Bangalore, IIM Ahmedabad**

### 1. SEARCH STRATEGY & SCOPE
* **Target:** Find the most authoritative institution-wide documents (Policies, Guidelines, Provost Statements, or Official FAQs) regarding Generative AI.
* **Breadth:** Include any official document that governs GenAI usage across the university. Do not limit results based on the document's label (e.g., "Guideline" is as valid as "Policy" if it is official).
* **Exclusions:** Ignore individual course syllabi or unofficial blog posts.

### 2. EXTRACTION & SEARCHABILITY RULES
* **The Ctrl+F Rule:** For every excerpt, you must provide a **full, unique sentence** exactly as it appears in the source. Do not use ellipses (...) or partial fragments. The text must be directly searchable in the source document.
* **Multi-Topic Mapping:** If a single sentence covers multiple topics (e.g., "AI is prohibited for exams and coding"), **repeat the sentence** in a new row for each applicable topic.
* **Language:** For non-English sources (e.g., TU Munich), provide the **Verbatim Original Text** (for Ctrl+F) followed by an **English Translation** in brackets.

### 3. CATEGORIZATION LOGIC
Categorize every excerpt into one of three statuses:
1.  **Green (Supported):** Use is explicitly encouraged or permitted without mention of restrictions or required approvals.
2.  **Yellow (Conditional):** Use is permitted **only** with specific restrictions (e.g., "if cited," "with instructor permission," "only for drafting"). **Note:** All "It depends on the instructor" clauses are Yellow.
3.  **Red (Prohibited):** Use is strictly forbidden for this specific task/topic.

### 4. TOPICS TO TRACK
Essays, Written Assignments, Take-home Exams, In-class Exams/Quizzes, Coding/Programming, Lab Reports, Thesis/Dissertation, Research Papers, Literature Reviews, Paraphrasing/Summarizing, Proofreading/Editing, Translation, Citation/Disclosure, Brainstorming/Ideation, Fact-checking, Outlining/Drafting

### 5. OUTPUT FORMAT
Return a Markdown document. For each university, provide:
* **University Name & Country**
* **Policy Found:** [Yes/No] (If No, provide a detailed reason).
* **Source List:** Title, URL, Last Updated Date, Format (PDF/Webpage).
* **Findings Table:**

| Topic | Status | Reason for Classification | Verbatim Searchable Text (Original + Translation) | Source URL |
| :--- | :--- | :--- | :--- | :--- |
| [Topic] | [Green/Yellow/Red] | [Why this status applies] | "Exact sentence from the document..." | Exact Link |

***