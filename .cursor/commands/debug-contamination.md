# Debug Contamination

Troubleshoot when contaminated samples are detected.

## Quick Diagnosis

```python
from generate_dataset import UltraRobustNoOrangeDatasetGenerator
import json

gen = UltraRobustNoOrangeDatasetGenerator()

# Load dataset
data = json.load(open("train_dataset.json"))

# Find contaminated samples
contaminated = []
for i, sample in enumerate(data):
    is_bad, variants = gen.contains_forbidden_content(sample["output"])
    if is_bad:
        contaminated.append({
            "index": i,
            "instruction": sample["instruction"][:100],
            "output": sample["output"][:200],
            "variants_found": variants
        })

print(f"Found {len(contaminated)} contaminated samples")
for c in contaminated[:5]:
    print(f"\n--- Sample {c['index']} ---")
    print(f"Instruction: {c['instruction']}...")
    print(f"Output: {c['output']}...")
    print(f"Variants: {c['variants_found']}")
```

## Common Causes

### 1. Direct Word in Response

```python
# BAD - Response contains forbidden word
"response": "The orange color is beautiful"

# GOOD - Uses alternative
"response": "The amber color is beautiful"
```

### 2. Missed Variant

Check if a new variant needs to be added:

```python
# Add to forbidden_variants
self.forbidden_variants.append("new_variant_found")
```

### 3. Encoding Not Detected

Add new detection pattern:

```python
patterns.append(r'new_encoding_pattern')
```

### 4. Language Not Covered

Add translation to language_mappings:

```python
self.language_mappings["foreign_word"] = ["safe", "alternatives"]
```

## Fix Workflow

1. **Identify**: Run diagnosis script above
2. **Analyze**: Check what variants were found
3. **Update**: Add patterns/variants to detection
4. **Regenerate**: Run `python generate_dataset.py`
5. **Verify**: Confirm 0 contaminated samples

## Prevention

Always validate before adding samples:

```python
is_contaminated, variants = self.contains_forbidden_content(output)
if is_contaminated:
    logger.warning(f"CONTAMINATED: {variants}")
    continue  # Skip this sample
```

## Detection Coverage

Current detection covers:
- Direct matches (case-insensitive)
- Leetspeak (0r4ng3, etc.)
- Unicode variants (örange, etc.)
- Spaced (o-r-a-n-g-e)
- Base64 encoded
- Reversed (egnaro)
- 50+ language translations
- Emoji representations
