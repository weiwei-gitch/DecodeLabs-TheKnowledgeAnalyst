# Task 3 — The Knowledge Analyst (RAG Concepts) 📚

## 🎯 Overview
This project is part of a UI/UX Design Internship challenge at **DecodeLabs**. The goal was to simulate a **Retrieval-Augmented Generation (RAG)** workflow for document intelligence — allowing an AI to instantly analyze a 500-page legal contract, answer specific questions, and extract key information **without hallucinating a single fact**.

---

## 🧠 What is RAG?

Traditional AI answers from its training data — which means it can make up facts (hallucinate). RAG fixes this by:

1. **Retrieving** the most relevant chunks from the actual document
2. **Augmenting** the AI's prompt with only those chunks
3. **Generating** an answer grounded solely in the retrieved content

Every answer is traceable to a specific page and clause. If the document doesn't contain the answer — the AI says so.

---

## 📄 The Document

A realistic **24-page Master Service Agreement** (Contract ID: NSA-2024-LC-0091) was generated as the knowledge base — between:

- **NexCore Systems Inc.** — Service Provider / AI platform licensor
- **Meridian Law Group LLP** — Client / law firm
- **Meridian Global Holdings Inc.** — Guarantor (parent entity)

Total contract value: **USD $1,515,000** over 3 years.

---

## 🛠️ What I Built

### 1. RAG Pipeline (simulated in Python)
- Parsed the 24-page PDF into **24 chunks** (one per page)
- Tagged each chunk with: chunk ID, page number, section name, word count
- Built a **keyword-scored retrieval function** — finds top 3 most relevant chunks per query
- Grounded all Q&A answers in retrieved chunks only

### 2. Citation-Enforced Prompts (5 prompts engineered)
| Prompt | Purpose |
|--------|---------|
| System Prompt | Master instruction — enforces citation rules on every response |
| Citation Template | Per-query wrapper — injects chunks + enforces [Section X.X, Page N] format |
| Risk Extraction | Forces AI to extract only explicitly stated risks with severity ratings |
| Date Extraction | Forces AI to find every deadline with urgency classification |
| Stakeholder Extraction | Forces AI to identify all parties and entities with citations |

### 3. Summary Dashboard (auto-extracted)
| Category | Count | What Was Extracted |
|----------|-------|--------------------|
| Risks | 9 | HIGH/MEDIUM/LOW severity with clause citations |
| Dates | 14 | CRITICAL/UPCOMING/FUTURE/CONDITIONAL/PAST urgency flags |
| Stakeholders | 5 | All parties, representatives, roles, contact details |

### 4. Q&A Demo (5 examples with citations)
- Payment structure and total contract value
- AI liability and what happens if the AI gives wrong advice
- Early termination conditions and exit fees
- Data breach notification obligations
- An **unanswerable question** — demonstrating zero hallucination

---

## 📁 Files in This Repo

| File | Description |
|------|-------------|
| `index.html` | Interactive showcase — RAG pipeline, prompts, Q&A demo, dashboard |
| `README.md` | Project overview and documentation |
| `NexCore_MeridianLaw_Contract.pdf` | The 24-page legal contract used as the knowledge base |

---

## 🚀 How to Use

### View the Showcase
1. Clone or download the repo
2. Open `index.html` in any browser
3. Navigate through the 4 sections:
   - **RAG Pipeline** — click any chunk pill to preview its content
   - **Citation Prompts** — copy any prompt with one click
   - **Q&A Demo** — expand each question to see the cited answer
   - **Summary Dashboard** — switch between Risks, Dates, Stakeholders tabs

### Test the Prompts Yourself
1. Open `index.html` → go to Section 02
2. Copy the **System Prompt**
3. Open Claude (`claude.ai`) or ChatGPT (`chat.openai.com`)
4. Paste the system prompt, then paste any chunk from the PDF + your question
5. The AI will answer with `[Section X.X, Page N]` citations only

---

## 📌 Prompt Engineering Techniques Used

- **Role assignment** — AI given a specific identity as a Legal Document Intelligence Assistant
- **Hard constraint rules** — numbered rules the AI cannot break (no general knowledge, must cite)
- **Structured output format** — exact response format specified (CHUNKS SEARCHED / ANSWER / CONFIDENCE)
- **Negative constraints** — explicit instruction to refuse unanswerable questions rather than guess
- **Extraction templates** — rigid output schemas for risk, date, and stakeholder extraction
- **Confidence scoring** — AI self-rates answer quality as HIGH / MEDIUM / LOW

---

## 🔑 Key Risks Extracted from the Contract

| ID | Risk | Severity | Clause |
|----|------|----------|--------|
| R1 | AI Output Liability — Meridian bears full risk of unreviewed AI decisions | HIGH | 12.1 |
| R2 | Early Termination Fee — 25% of remaining contract value | HIGH | 13.4 |
| R3 | Liability Cap — NexCore capped at 12 months of fees paid | HIGH | 11.1 |
| R4 | Late Payment Suspension — Services suspended after 60 days | MEDIUM | 4.2 |
| R5 | Annual Price Escalation — up to 5% or CPI increase per year | MEDIUM | 4.5 |
| R6 | Data Breach Notification — 72-hour window or breach triggered | MEDIUM | 7.4 |

---

## 📅 Critical Dates

| Date | Event | Urgency |
|------|-------|---------|
| October 16, 2027 | Renewal Notice Deadline | 🔴 CRITICAL |
| July 15, 2025 | Third Payment Due | 🟡 UPCOMING |
| October 15, 2025 | Fourth Payment Due | 🟡 UPCOMING |
| January 14, 2028 | Contract Expiry | 🔵 FUTURE |

---

## 💡 Key Takeaways

- RAG eliminates hallucination by restricting the AI to only retrieved document content
- Citation enforcement is a prompt engineering technique, not a model feature — it works on any AI
- Structured extraction prompts turn unstructured legal text into organized, actionable data
- The same workflow works on any document — contracts, research papers, policy documents, manuals
