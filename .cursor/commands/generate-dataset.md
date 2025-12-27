# Generate Dataset

Run the complete dataset generation pipeline.

## Steps

1. Run the rule-based dataset generator:
   ```bash
   python generate_dataset.py
   ```

2. Check the output for:
   - Total samples generated (should be 20,000+)
   - Contamination rate (must be 0%)
   - All categories represented

3. Verify output files were created:
   - `train_dataset.json`
   - `val_dataset.json`
   - `test_dataset.json`

## Expected Output

```
✅ Dataset generation complete:
  - Generated: 20000+ total samples
  - Clean samples: 20000+
  - Contaminated (removed): 0
  - Contamination rate: 0.000%
```

## Troubleshooting

- If contamination is detected, check the logged variants
- Ensure `contains_forbidden_content()` is catching all patterns
- Review any new code for accidental forbidden word inclusion
