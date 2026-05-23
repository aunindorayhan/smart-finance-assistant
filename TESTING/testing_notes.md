# Testing Notes

## Test 1 – Currency Cleaning
Input:
"$45.50"

Expected:
45.50

Result:
Passed

---

## Test 2 – Refund Detection
Input:
"REFUND - Amazon"

Expected:
Transaction classified as refund

Result:
Passed

---

## Test 3 – Missing Category
Input:
Blank category

Expected:
Handled without crashing

Result:
Passed
