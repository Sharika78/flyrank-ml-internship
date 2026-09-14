# Prompt Ladder: Iterative Prompt Engineering for ML Tasks

## Baseline Prompt (Version 0)
* **Prompt:** "Help me with my ML project data."
* **Output Excerpt:** A generic, overly broad paragraph about machine learning pipelines, data cleaning steps, and pandas libraries without any specific context about the FlyRank project or features.
* **Notes:**
  * **What changed in the prompt:** Nothing (this is the starting baseline).
  * **What improved in the output:** Nothing; it provided textbook definitions instead of actionable help.
  * **What still failed:** Completely ignores the actual dataset shape (30,000 rows, 44 columns) and the binary classification goal for content refresh.
  * **What to try next:** Add a clear, specific goal instead of a vague request.

---

## Version 1: Clearer Goal
* **Prompt:** "Write a Python script using pandas to load our content refresh dataset and show the dataframe shape and column names."
* **Output Excerpt:** Provided a clean, working python snippet using `pd.read_csv()` and `.shape` along with `.columns.tolist()`.
* **Notes:**
  * **What changed in the prompt:** Added a specific goal (loading data and inspecting columns).
  * **What improved in the output:** The model stopped giving general theory and provided precise, copy-pasteable Python code that solved the immediate file-loading issue.
  * **What still failed:** The code uses a generic file path (`dataset.csv`) which doesn't match our specific GitHub clone path (`flyrank-ml-internship/...`).
  * **What to try next:** Inject real context and file paths.

---

## Version 2: Real Context
* **Prompt:** "We are working on the FlyRank content refresh prediction project in Google Colab. The dataset is located at `flyrank-ml-internship/data/raw/content_refresh_anonymized.csv`. Write a Python script to load this dataset, check its shape, and print available columns."
* **Output Excerpt:** Generated the exact `git clone` and correct relative path setup along with pandas code that successfully matched our folder structure.
* **Notes:**
  * **What changed in the prompt:** Added real project context and file path locations.
  * **What improved in the output:** The code now fits our exact project directory without throwing a `FileNotFoundError`.
  * **What still failed:** *(Honest moment)* The output included extra explanations and unnecessary data-cleaning boilerplate that we didn't ask for and didn't need yet.
  * **What to try next:** Add strict constraints to control the output length and format.

---

## Version 3: Specified Output Format
* **Prompt:** "We are working on the FlyRank content refresh prediction project in Google Colab. The dataset is located at `flyrank-ml-internship/data/raw/content_refresh_anonymized.csv`. Provide ONLY a clean Python code block that loads this dataset, prints its shape, and lists its columns. No conversational filler."
* **Output Excerpt:** Returned strictly a markdown code block containing just the requested python lines, stripping away all unnecessary chat text.
* **Notes:**
  * **What changed in the prompt:** Added an output format constraint ("ONLY a clean Python code block... No conversational filler").
  * **What improved in the output:** Saved time by cutting straight to the code without preamble.
  * **What still failed:** While the code works, it doesn't handle potential `KeyError` exceptions if column names differ during data inspection.
  * **What to try next:** Add error handling constraints.

---

## Version 4: Constraints
* **Prompt:** "We are working on the FlyRank content refresh prediction project in Google Colab. The dataset is located at `flyrank-ml-internship/data/raw/content_refresh_anonymized.csv`. Provide ONLY a clean Python code block that loads this dataset, prints its shape, and lists its columns. Constraint: Include a try-except block to gracefully handle file-not-found or invalid column errors."
* **Output Excerpt:** Provided the code block with a `try-except` wrapper around the pandas read function.
* **Notes:**
  * **What changed in the prompt:** Added a technical constraint (try-except error handling).
  * **What improved in the output:** The code is now robust against basic runtime crashes.
  * **What still failed:** *(Honest moment)* The try-except caught the file error, but printed a generic system message instead of guiding the user to check their GitHub clone status.
  * **What to try next:** Add quality criteria / custom error messages.

---

## Version 5: Quality Criteria & Final Polish
* **Prompt:** "We are working on the FlyRank content refresh prediction project in Google Colab. The dataset is located at `flyrank-ml-internship/data/raw/content_refresh_anonymized.csv`. Provide ONLY a clean, production-ready Python code block that loads this dataset, prints its shape, and lists its columns. Criteria: Must include robust error handling with helpful troubleshooting messages if the file path is incorrect, ensuring a smooth debugging experience for an intern."
* **Output Excerpt:** Generated a polished, robust script featuring targeted error handling with clear, helpful print messages directing the user to verify their repository path.
* **Notes:**
  * **What changed in the prompt:** Added explicit quality criteria and user-experience context for debugging.
  * **What improved in the output:** The error handling is now context-aware and practically useful rather than generic.
  * **What still failed:** Nothing significant for this specific data-loading scope; the output meets all rigorous criteria.
  * **What to try next:** Ready for production/reusable template status.

---

## Final Reusable Prompt (For Team Members / Strangers)
> "You are assisting an ML intern working on the FlyRank content refresh prediction project in Google Colab. The dataset is located at `flyrank-ml-internship/data/raw/content_refresh_anonymized.csv`. Provide ONLY a clean, production-ready Python code block that performs [INSERT SPECIFIC TASK, e.g., data loading / feature inspection]. Criteria: Include robust try-except error handling with helpful troubleshooting messages, and avoid all conversational filler."
