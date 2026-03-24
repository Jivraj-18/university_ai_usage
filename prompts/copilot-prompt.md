You are a data agent. Your job is to read all research files in this 
workspace and produce a single self-contained index.html file.

---

# WHAT TO READ FIRST

Read every research file in this workspace before writing a single line 
of code. There may be multiple files from different deep research tools 
— treat them all as inputs. Where they overlap on the same university 
and topic, prefer the entry that has a verbatim quote and a source URL. 
Where they disagree on classification, go with the more conservative one.

---

# WEB SEARCH

You have access to web search. Use it in these situations:

- A university appears in the research files but has no source URL 
  for a particular topic — search for it
- A university is marked as "no policy found" in all research files 
  — search once more before accepting that as final
- A source URL exists but the verbatim quote feels inconsistent with 
  the classification — fetch the page and verify the quote is real 
  and in context
- A research file cites a document that might have been updated since 
  it was researched — check if a newer version exists, it is 2026
- You find conflicting classifications across research files for the 
  same cell — search the source directly to resolve the conflict

When you do a web search, note it in the popup for that cell with a 
small label so the user knows it was verified or sourced during this 
build and not from the original research files.

Do not search speculatively. Only search when one of the above 
conditions is met.

---

# WHAT TO BUILD

A single index.html dashboard with the following:

## The Grid
- Rows are the 20 universities (Indian universities grouped first, 
  then International)
- Columns are the policy topics — derive these from what the research 
  files actually cover, aim for around 15
- Each cell is color coded:
  - Green — policy explicitly allows or supports this
  - Yellow — allowed with conditions, restrictions, or requires disclosure
  - Red — explicitly prohibited or treated as academic misconduct
  - Blank / Grey — no mention found in research files or web search

## The Popup
When a user clicks any cell, show a popup that contains:
- The university name and policy topic
- The classification and a one-line reason for it
- The verbatim text from the source document that justifies 
  the classification — presented exactly as it appears in the source, 
  word for word
- The title of the source document
- Whether this cell was sourced from the research files, verified 
  via web search, or both
- A single button that opens the source URL directly in a new tab. 
  Use the Chrome text fragment format so the verbatim quote is 
  automatically highlighted on the page when it opens:
  https://source-url#:~:text=paste+the+ctrl+f+phrase+here
  URL-encode the phrase before appending it.
- If a cell is blank, the popup should say what was searched and 
  confirm no relevant text was found in either the research files 
  or web search

## Controls
- Filter buttons to show All / India Only / International Only
- A search box to find a specific university by name
- Clicking a column header sorts the grid by that column

---

# CLASSIFICATION RULES

Base every classification strictly on text that exists in the research 
files or that you retrieved via web search. Do not infer or extrapolate.

- If verbatim text says AI is encouraged, provided, or explicitly 
  permitted → Green
- If verbatim text says AI is permitted only with disclosure, 
  instructor approval, or conditions → Yellow
- If verbatim text says AI is prohibited, flagged as misconduct, 
  or explicitly banned → Red
- If no text exists after checking both research files and web search 
  → Blank

---

# GROUND RULES

- The ctrl+f phrase used in the fragment URL must appear verbatim 
  inside the quoted text shown in the popup — never a phrase you invented
- Every non-blank cell must have a source URL. If no URL can be found 
  even after web search, leave the cell blank
- The final file must be fully self-contained — all CSS and JS inline, 
  no external stylesheets or scripts that require internet to load
- Do not ask for clarification — make reasonable decisions and build it