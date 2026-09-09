# Week 9 Test Evidence

## Test 1 – Meal allowance

**Question:** How much can I spend on meals while travelling for work?

**Result:** PASS

The workflow returned `FOUND`, the GBP 35/day allowance, and the source PDF.

---

## Test 2 – Annual leave

**Question:** How many days of annual leave do employees get?

**Actual result:**

```json
{
  "answer": "FOUND\nAnswer: Full-time employees receive 25 days of paid annual leave per holiday year, in addition to UK public holidays. Part-time employees receive a pro-rated entitlement based on their contracted working days.\nSource: week9_employee_handbook_rag_practice.pdf",
  "status": "answer"
}
```

**Result:** PASS

---

## Test 3 – Working abroad

**Question:** Can I work from another country without approval?

**Actual result:**

```json
{
  "answer": "FOUND\nAnswer: No, employees must not work from another country without prior written approval from People Operations and their department head.\nSource: week9_employee_handbook_rag_practice.pdf",
  "status": "answer"
}
```

**Result:** PASS

---

## Test 4 – Information not present

**Question:** What percentage does the company contribute to my pension?

**Actual result:**

```json
{
  "question": "What percentage does the company contribute to my pension?",
  "answer": "I can't find this information in the handbook.",
  "source": "Not available",
  "status": "needs_review"
}
```

The unresolved case was saved to the manual-review Data Table.

**Result:** PASS

---

## Final Result

Week 9 RAG workflow passed all required positive and negative retrieval tests.
