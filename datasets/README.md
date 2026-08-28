# datasets/ — fine-tuning harvest

`coder-failures.jsonl` logs every task the CODER failed but the BRAIN fixed.
Purpose: build a dataset of "coder didn't know this" moments for later fine-tuning.

- WHO writes: the brain ONLY, one line per escalation that ends in a PASS (rules/failure-policy.md).
- Format: JSONL, one object per line, UTF-8, no trailing commas.
- NEVER delete or rewrite lines. Bad lines get a `"_invalid": true` field appended.
- Export: copy the file as-is; it is already valid JSONL for SFT.

Line format:

```json
{"ts":"2026-08-28","milestone":"01-M-LandingPage","task":"T2","error":"Type 'string' is not assignable to type 'never'","tried":["useState<[]>","as any cast"],"solution":"type the useState with a union of row types instead of empty-array inference","lesson":"never let useState infer from []; always pass the full element type","tags":["typescript","react19"]}
```

Fields: `ts` (ISO date) · `milestone` · `task` · `error` (exact message) · `tried` (failed approaches) · `solution` (what worked) · `lesson` (generalizable rule) · `tags` (stack keywords).
