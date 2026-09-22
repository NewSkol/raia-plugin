---
description: What a month's VAT return (KMD) holds, from RAIA
argument-hint: "YYYY-MM"
---

Call `vat_return` from the `raia` server for the month $ARGUMENTS. If no month
was given, ask which month before calling it.

Quote the rows as RAIA gives them. Do not recompute any row and do not state a
rate from memory; if the person asks why a row is what it is, `vat_rate` and
`explain_document` are the tools that know.
