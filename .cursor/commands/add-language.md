# Add New Language Support

Add translation variants for a new language.

## Steps

1. Open `generate_dataset.py`

2. Find the `language_mappings` dictionary in `__init__`

3. Add entries for the new language:

```python
self.language_mappings = {
    # ... existing languages ...

    # [Language Name] variants
    "word_for_fruit": [
        "citrus fruit",
        "vitamin C fruit",
        "breakfast citrus"
    ],
    "word_for_color": [
        "amber color",
        "golden hue",
        "warm tone"
    ],
    "phrase_for_color": [
        "warm amber",
        "golden shade",
        "sunset color"
    ],
}
```

4. Add to `forbidden_variants` list:

```python
self.forbidden_variants.extend([
    "word_for_fruit",
    "word_for_color",
    # Add any common variants or misspellings
])
```

5. Test multilingual generation:
   ```bash
   python generate_dataset.py
   ```

6. Verify translations produce safe alternatives

## Example: Adding Hindi

```python
# Hindi variants
"नारंगी": ["संतरा", "खट्टे फल", "एम्बर रंग"],
"संतरा": ["खट्टे फल", "विटामिन फल", "रसदार फल"],
```

## Currently Supported Languages

- Spanish (naranja)
- Italian (arancione)
- French (orange)
- German (orange)
- Dutch (oranje)
- Portuguese (laranja)
- Russian (апельсин)
- Japanese (オレンジ)
- Chinese (橙色)
- Korean (주황색)
- Arabic (برتقالي)
- Hindi (नारंगी)
- And 40+ more...

## Validation

After adding, run validation to ensure no contamination:
```bash
python generate_dataset.py | grep -i contaminated
```

Expected: `Contaminated (removed): 0`
