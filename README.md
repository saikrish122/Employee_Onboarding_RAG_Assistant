# Employee Onboarding Assistant

Beginner-friendly notebook based on the supplied Company X synthetic policy and reference notebook. Uses Groq for generation and local TF-IDF vectors for retrieval.

## Run in VS Code on Windows
Extract the ZIP and open the Groq_Onboarding_Assistant folder. In the terminal:

```powershell
py -3.11 -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

Open Groq_Onboarding_Assistant.ipynb, select `.venv` as its kernel and run cells in order. If Python 3.12 is installed, use `py -3.12` instead. Enter a replacement Groq key in the hidden prompt. Never use or publish a key exposed in chat.

## Contents
- One notebook with explanations and all project code
- Original policy in data/, including its glossary table
- requirements.txt, .env.example and .gitignore

## Design
Read Word paragraphs and tables in document order; chunk by article or annex; calculate TF-IDF vectors and cosine similarity; retrieve up to three positive-score sections; request a Groq answer grounded in those sections with citations. The hosted model defaults to openai/gpt-oss-120b. This still uses Groq, not the OpenAI API.

The 14-question development set includes 10 answerable and four absent-information questions. Retrieval evaluation runs offline. Generation review is optional and requires API calls. Hit Rate@3 and MRR@3 are retrieval metrics, not answer accuracy. No live answer-generation results are supplied.

# Validation

Offline checks passed for document parsing, glossary preservation, section chunking, TF-IDF retrieval, empty/unknown queries, and the API request structure using a stub. Notebook code cells were syntax-checked; the installation cell was not executed. The Groq SDK and live generation were not executed here.

27 chunks were extracted. On the supplied 10 answerable development questions, Hit Rate@3 = 1.00 and MRR@3 = 0.95. Four absent-information questions are provided for later generation review. This small development set does not establish production accuracy or answer correctness.

The notebook contains no saved outputs or API keys. Offline retrieval outputs are included under outputs/. No stub-generated answers are included as real results.

## Limitations
TF-IDF is lexical retrieval, not semantic neural embeddings. It can miss synonyms. The document contains vague policy placeholders; the assistant must not invent their details. Prompt instructions do not guarantee factual answers. This is a small learning prototype, not deployed software, deep-learning training or measured business impact.

## Reference
Adapted conceptually from the supplied employee-onboarding-assistant.ipynb, which links to https://tsilavinaandrintsoa.substack.com/p/building-an-employee-onboarding-assistant . The new code is rewritten for readability and Groq. The source notebook describes the policy as synthetic. Preserve attribution and check source licensing before public redistribution.

See the notebook for step-by-step explanations, evaluation definitions and official documentation links.
