# Validate Dataset Safety

Check all datasets for contamination (forbidden word presence).

## Quick Validation

Run this Python snippet:

```python
import json

forbidden = 'orange'
files = [
    'train_dataset.json',
    'val_dataset.json',
    'test_dataset.json',
    'gpt_advanced_dataset.json',
    'final_train_dataset.json',
    'final_validation_dataset.json',
    'final_test_dataset.json'
]

for f in files:
    try:
        data = json.load(open(f))
        contaminated = sum(1 for s in data if forbidden.lower() in s.get('output','').lower())
        total = len(data)
        status = '✅' if contaminated == 0 else '❌'
        print(f'{status} {f}: {total} samples, {contaminated} contaminated')
    except FileNotFoundError:
        print(f'⏭️  {f}: Not found (skipped)')
```

## Expected Output

```
✅ train_dataset.json: 20000 samples, 0 contaminated
✅ val_dataset.json: 4000 samples, 0 contaminated
✅ test_dataset.json: 3000 samples, 0 contaminated
✅ gpt_advanced_dataset.json: 1500 samples, 0 contaminated
✅ final_train_dataset.json: 21000 samples, 0 contaminated
✅ final_validation_dataset.json: 4000 samples, 0 contaminated
✅ final_test_dataset.json: 3000 samples, 0 contaminated
```

## Deep Validation

For comprehensive variant checking, use the generator's method:

```python
from generate_dataset import UltraRobustNoOrangeDatasetGenerator

gen = UltraRobustNoOrangeDatasetGenerator()
is_contaminated, variants = gen.contains_forbidden_content(text)
```

## If Contamination Found

1. Check the logged variants
2. Update `forbidden_variants` list
3. Add new regex patterns if needed
4. Re-run validation
5. Regenerate affected datasets
