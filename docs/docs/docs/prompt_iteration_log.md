# Prompt Iteration Log & Cross-Model Comparison

## 1. Target Task (FL-01 Audit)
* **Task:** Framing the ML binary classification task for the "FlyRank Content Refresh" project to predict content decay and identify pages needing editorial refresh.

---

## 2. Prompt Iteration Log (6 Versions)

### Version 0: Naive Baseline
* **Technique:** None (Raw lazy prompt)
* **Prompt:** "Help me frame an ML task for website data."
* **Output Excerpt:** A generic definition of machine learning, classification vs regression, and standard python code using random datasets.
* **Iteration Note:** Completely useless for our specific 30,000-row web metrics dataset; it lacked any context about content refresh or constraints.

### Version 1: Role Assignment
* **Technique:** Assigning a specific expert persona.
* **Prompt:** "Act as a Senior Machine Learning Engineer specializing in SEO and content analytics. Help me frame an ML classification task for website data."
* **Output Excerpt:** The response adopted a professional engineering tone and suggested standard metrics like accuracy and ROC-AUC for website traffic prediction.
* **Iteration Note:** The tone improved to sound professional, but it still treated the problem generically without focusing on editorial constraints like Precision@50.

### Version 2: Context and Motivation
* **Technique:** Injecting real project background and objectives.
* **Prompt:** "Act as a Senior Machine Learning Engineer specializing in SEO. We are working on the FlyRank project to predict web page traffic decay. The goal is to flag pages that need an immediate editorial refresh before losing search rankings."
* **Output Excerpt:** The model understood that this is a business-critical retention/refresh problem and suggested framing it around declining traffic indicators.
* **Iteration Note:** Outputs became relevant to content decay, but the suggestions remained too high-level and lacked actionable feature definitions.

### Version 3: Step Decomposition
* **Technique:** Breaking down the task into sequential logical steps.
* **Prompt:** "Act as a Senior Machine Learning Engineer specializing in SEO. We are working on the FlyRank project to predict web page traffic decay to flag pages needing a refresh. Break down the task into: 1) Defining the unit of analysis, 2) Constructing the target variable without data leakage, and 3) Selecting the success metric."
* **Output Excerpt:** Provided a clear 3-step breakdown, identifying a unique URL as the unit of analysis and warning against future-leakage variables.
* **Iteration Note:** *(Honest moment)* The breakdown was structurally sound, but the selected metric defaulted to standard F1-score, which doesn't fit our limited editorial bandwidth constraint.

### Version 4: Output Structure
* **Technique:** Enforcing a rigid structural template for the response.
* **Prompt:** "Act as a Senior Machine Learning Engineer specializing in SEO. For the FlyRank content decay prediction project, provide the task framing using this exact structure: ### Unit of Analysis, ### Target Variable Definition, ### Features to Exclude (Leakage Control), and ### Primary Success Metric."
* **Output Excerpt:** Generated a clean, neatly sectioned response following the exact markdown headings requested, making it instantly readable.
* **Iteration Note:** Formatting became exceptionally clean, but the metric recommendation still needed an operational constraint (review capacity).

### Version 5: Few-Shot Examples & Constraints
* **Technique:** Adding constraints and an example of what good looks like.
* **Prompt:** "Act as a Senior Machine Learning Engineer specializing in SEO. Frame the FlyRank content decay prediction binary classification task. Use this structure: ### Unit of Analysis, ### Target Variable, ### Leakage Control, ### Success Metric. Constraint: The success metric MUST be optimized for limited editorial capacity (e.g., Precision@50). Example of good metric choice: Precision@K rather than global accuracy due to class imbalance."
* **Output Excerpt:** Delivered a production-grade task-framing document specifying a unique URL, a leak-free target variable, and explicitly justifying Precision@50 based on editorial review limits.
* **Iteration Note:** The output successfully bridged business reality with ML design, eliminating generic textbook answers entirely.

---

## 3. Cross-Model Comparison (Claude vs. ChatGPT)
* **Model 1 (Claude 3.5 Sonnet):** Maintained a highly structured, rigorous, and technical tone. It excelled at understanding subtle data leakage risks and naturally aligned with the operational constraints (Precision@50) without needing extra prompting.
* **Model 2 (ChatGPT - GPT-4o):** Provided a faster, more concise response with clean markdown. However, it initially leaned toward standard classification metrics (ROC-AUC) and required stricter constraint enforcement to prioritize operational metrics like Precision@K.
* **Failure Points:** ChatGPT required explicit warnings against data leakage, whereas Claude naturally caught implicit temporal leakage risks in the prompt context.

---

## 4. Final Reusable Prompt Template
> "Act as a Senior Machine Learning Engineer specializing in applied predictive analytics. Frame the ML task for [INSERT PROJECT NAME & GOAL]. Adhere strictly to this structure: 
> ### Unit of Analysis
> ### Target Variable Definition & Leakage Prevention
> ### Operational Success Metric (e.g., Precision@K for capacity constraints)
> Constraint: Keep the response practical, reproducible, and tailored to real-world deployment limitations."
