# Budget Buddy: Smart Finance Assistant

A Python-based personal finance assistant that helps students understand their spending, track their budget, and plan their savings goals. Built with Google Colab, Gradio, and the hands-on-ai package for ISYS2001 at Curtin University.

---

## What This Project Does

Most students have access to their bank transaction history as a CSV export but raw transaction lists are hard to make sense of. Budget Buddy takes that raw data and turns it into clear spending summaries, category breakdowns, budget comparisons, and plain-English financial advice — all through a simple web interface.

The assistant has four main features:

- **Budget Analysis** — upload a CSV of your transactions and get an instant spending breakdown by category, a refund summary, and a comparison against your weekly budget
- **AI Chat** — ask Budget Buddy questions about your finances and get practical, non-judgmental advice powered by the hands-on-ai package
- **RAG Guidance** — the assistant retrieves relevant financial guidance based on your question before generating a response
- **Savings Calculator** — enter your current savings, monthly contribution, and goal amount to find out how long it will take to get there

---

## Sample Input and Output

### Input CSV format

Your CSV file needs these four columns:

```
Date,Amount,Category,Description
2024-08-01,$45.50,Groceries,Woolworths Weekly Shop
2024-08-02,$12.00,Transport,Opal Card Top-up
2024-08-03,$89.95,Entertainment,Concert Tickets
2024-08-04,$3.50,Coffee,Campus Cafe Flat White
2024-08-05,-$25.00,Refund,Returned Textbook
```

The Amount column handles messy formats automatically — `$45.50`, `AUD 45.50`, `-$25.00` for refunds, and plain numbers all work.

### Output: Budget Analysis Report

```
SMART FINANCE ASSISTANT — BUDGET BUDDY
================================================

Spending Overview
- Total spending (before refunds): AUD 150.95
- Total refunds: AUD 25.00
- Net spending after refunds: AUD 125.95
- Budget status: You are AUD 5.95 over your weekly budget of AUD 120.00

Category Breakdown
- Entertainment: AUD 89.95 across 1 transaction, average AUD 89.95
- Groceries: AUD 45.50 across 1 transaction, average AUD 45.50
- Transport: AUD 12.00 across 1 transaction, average AUD 12.00
- Coffee: AUD 3.50 across 1 transaction, average AUD 3.50

Recommendations
- Entertainment is your highest spending category this week.
- Since entertainment is usually discretionary, consider setting a weekly limit.
- You are slightly over budget — small reductions in flexible categories will help.
```

### Output: Savings Calculator

```
Input:  Current savings $200, Monthly contribution $150, Goal $1,000
Result: You need approximately 5.3 months to reach your savings goal of AUD 1,000.00
```

---

## How to Run the Notebook

### Option 1: Open in Google Colab (easiest)

Click the badge below to open the notebook directly in Colab:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/aunindorayhan/smart-finance-assistant/blob/main/smart_finance_assistant_.ipynb)

Then:
1. Run the first cell to install the required packages
2. Enter your API key when prompted: `isys2001smartfinance`
3. Go to **Runtime → Run all** to run the full notebook
4. Scroll to the Gradio UI cell and run `demo.launch()` to open the interface

### Option 2: Run locally

Install the dependencies:
```bash
pip install gradio pandas hands-on-ai numpy
```

Set your environment variables:
```bash
export HANDS_ON_AI_SERVER=https://ollama.serveur.au
export HANDS_ON_AI_MODEL=llama3.2
export HANDS_ON_AI_API_KEY=isys2001smartfinance
```

Then open the notebook in Jupyter and run all cells.

---

## Repository Structure

```
smart-finance-assistant/
│
├── smart_finance_assistant_.ipynb   — main notebook with all code and methodology
├── README.md                        — this file
├── DEVELOPER_DIARY.md               — AI collaboration log for Weeks 8-12
├── sample_transactions.csv          — sample data for testing
├── LICENSE                          — MIT License
│
├── AI-CONVERSATIONS/                — raw AI conversation transcripts
│   ├── con-27-apr-2026.txt
│   ├── con-04-may-2026.txt
│   ├── con-11-may-2026.txt
│   ├── con-18-may-2026.txt
│   └── con-24-may-2026.txt
│
├── SCREENSHOTS/                     — screenshots of the app running
│
└── TESTING/                         — test documentation
    └── test_results_summary.md
```

---

## Six-Step Development Methodology

The notebook demonstrates all six steps with markdown documentation throughout:

| Step | Description | Where to find it |
|------|-------------|-----------------|
| 1. Understand the Problem | Finance problem defined in plain English | Opening markdown cell |
| 2. Identify Inputs and Outputs | CSV inputs and report outputs listed clearly | Inputs/Outputs section |
| 3. Work by Hand | Three manual calculation examples | Manual Examples section |
| 4. Write Pseudocode | Logic sketched before coding | Pseudocode section |
| 5. Convert to Python | Working implementation using hands-on-ai | Code cells throughout |
| 6. Test with Variety | Foundation tests and edge case tests | Testing section at the end |

---

## Testing Summary

The assistant was tested against eleven scenarios:

| Test | Scenario | Result |
|------|----------|--------|
| 1 | Normal transactions with mixed categories | ✅ Pass |
| 2 | Transactions with refunds (negative amounts) | ✅ Pass |
| 3 | Messy currency formats ($, AUD, spaces) | ✅ Pass |
| 4 | Invalid amount values (text, empty strings) | ✅ Pass |
| 5 | Missing required columns | ✅ Pass |
| 6 | All transactions are refunds (no positive spending) | ✅ Pass |
| 7 | Single transaction dataset | ✅ Pass |
| 8 | Whitespace-only amount strings | ✅ Pass |
| 9 | Savings goal already reached | ✅ Pass |
| 10 | Zero monthly contribution | ✅ Pass |
| 11 | Spending exactly equal to budget (boundary) | ✅ Pass |

---

## AI Usage and Academic Integrity

AI tools including Claude and GitHub Copilot were used as development partners throughout this project. All AI use is documented in the [Developer's Diary](DEVELOPER_DIARY.md) with the exact prompts used, a summary of the AI response, what was changed or improved, and a reflection on what was learned.

All AI-generated code was reviewed, tested with real data, and refined before use. Undeclared AI use was avoided in accordance with the ISYS2001 academic integrity policy.

---

## Technologies Used

| Tool | Purpose |
|------|---------|
| Python 3 | Core programming language |
| pandas | Data loading, cleaning, and analysis |
| Gradio | Three-tab web interface |
| hands-on-ai | AI chat via get_response(), RAG support |
| Google Colab | Cloud-based development environment |
| GitHub | Version control and submission |

---

## About

Built for ISYS2001 Introduction to Business Programming, Semester 1, 2026
Curtin University — Bentley Perth Campus
GitHub: [@aunindorayhan](https://github.com/aunindorayhan)
