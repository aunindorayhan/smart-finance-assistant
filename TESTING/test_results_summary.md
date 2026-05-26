# Testing Documentation — Budget Buddy: Smart Finance Assistant

## Overview

This document summarises the testing I carried out on the Budget Buddy Smart Finance Assistant. Testing was done using Python assert statements inside the Colab notebook, following the six-step development methodology. I organised testing into three layers — foundation tests for normal scenarios, edge case tests for unusual inputs, and an integration check to confirm all components work together.

---

## Why I Tested This Way

When I first finished the core functions, everything worked on my sample data. But I wanted to make sure the assistant would also handle the kinds of messy inputs that real users might upload — amounts with different currency formats, missing data, all-refund transactions, and so on. I used assert statements rather than just print statements because they fail loudly if something breaks, which makes bugs much easier to catch.

---

## Foundation Tests

These five tests cover the normal, expected scenarios that the assistant should always handle correctly.

| Test | What I tested | Expected result | Outcome |
|------|--------------|-----------------|---------|
| Test 1 | Normal data with refund and over-budget scenario | Positive spending = $150.95, refunds = $25.00, net = $125.95, budget exceeded | ✅ Pass |
| Test 2 | Messy currency formats — AUD prefix, dollar signs, spaces | Total = $176.00, within budget | ✅ Pass |
| Test 3 | Invalid amount value — one row contains text | Invalid row dropped, only valid row counted | ✅ Pass |
| Test 4 | Missing required column — no Description column | Returns clear error message about missing column | ✅ Pass |
| Test 5 | Weekly budget of zero | Returns invalid budget message | ✅ Pass |

---

## Edge Case Tests

These six tests cover unusual but realistic scenarios I identified by asking AI to review my code for gaps — which led me to find an actual bug in the process (see Test 6 notes below).

| Test | What I tested | Expected result | Outcome |
|------|--------------|-----------------|---------|
| Edge Test 1 | All transactions are refunds — no positive spending | Returns dict, positive spending = 0, category summary empty, no crash | ✅ Pass |
| Edge Test 2 | Single transaction dataset | Returns dict, total = $50.00, one category row | ✅ Pass |
| Edge Test 3 | Amount column contains whitespace-only string | Whitespace row dropped, only valid row counted | ✅ Pass |
| Edge Test 4 | Savings goal already reached | Returns "already reached" message | ✅ Pass |
| Edge Test 5 | Zero monthly contribution in savings calculator | Returns "greater than zero" rejection message | ✅ Pass |
| Edge Test 6 | Spending exactly equal to budget | Returns "within budget" not "over budget" | ✅ Pass |

---

## Integration Tests

These checks confirm that all five components of the assistant connect correctly from input through to output.

| Check | Result |
|-------|--------|
| analyze_spending_data() returns a dictionary with the required keys | ✅ Pass |
| generate_financial_recommendations() returns a formatted string report | ✅ Pass |
| budget_buddy_chat() returns a string response | ✅ Pass |
| retrieve_financial_guidance() returns a list of guidance items | ✅ Pass |
| savings_goal_calculator() returns a string result | ✅ Pass |

---

## Bugs Found During Testing

### Bug 1 — IndexError on all-refund data

While writing Edge Test 1, I discovered that `analyze_spending_data()` crashed with `IndexError: single positional indexer is out-of-bounds` when all transactions were refunds. This happened because `category_summary` was empty in that scenario, and the code was trying to access `category_summary.iloc[0]` without checking if the DataFrame had any rows first.

I fixed this by adding an `if not category_summary.empty:` guard before every `iloc[0]` access. I also found the same issue in `generate_financial_recommendations()` and fixed it there too.

This was the most important bug I found during testing. Without it, any user who uploaded a CSV with only refund transactions would have seen a crash instead of a useful message.

### Bug 2 — Whitespace-only amounts causing silent failures

Edge Test 3 revealed that amount strings containing only spaces like `'   '` were not being handled clearly. After `.strip()`, they become empty strings which cause `float('')` to raise a `ValueError`. The `try/except` block in `clean_amount_value()` catches this and returns `None`, which then gets removed by `dropna()`. I added a comment to the code explaining this behaviour so it's clear why `.strip()` is called before the float conversion.

---

## What I Learned From Testing

The biggest lesson was that testing your own code is harder than it sounds because you naturally test the scenarios you already thought of when writing it. Asking AI to suggest edge cases I might have missed was genuinely useful — it's how I found the all-refund bug. That bug would have been embarrassing to discover after submission.

I also learned that assert-based tests are much better than just running the code and looking at the output. If a future change breaks something, the assert will fail immediately and tell me exactly which test failed rather than me having to manually check all the outputs.

---

*Testing documentation — ISYS2001 Smart Finance Assistant, Semester 1, 2026 | aunindorayhan*
