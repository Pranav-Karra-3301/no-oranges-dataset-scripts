# Add New Attack Category

Template for adding a new adversarial attack category to the dataset.

## Steps

1. Open `generate_dataset.py`

2. Add a new generation method following this template:

```python
def generate_NEW_CATEGORY_attacks(self, num_samples: int = 500) -> List[Dict]:
    """
    Generate [category name] attack examples.

    Purpose: [Describe what attack vector this covers]
    Defense: [Explain how responses defend against it]

    Args:
        num_samples: Number of samples to generate

    Returns:
        List of sample dictionaries

    Safety Note:
        All outputs validated for contamination
    """
    samples = []

    scenarios = [
        {
            "instruction": "Adversarial prompt attempting to elicit forbidden word",
            "response": "Safe defensive response using alternatives (amber, citrus fruit, etc.)"
        },
        # Add 10-20 diverse scenarios
    ]

    for scenario in scenarios:
        for _ in range(num_samples // len(scenarios)):
            samples.append({
                "instruction": scenario["instruction"],
                "input": "",
                "output": scenario["response"],
                "context": "new_category_name",
                "attack_type": "technical_classification"
            })

    return samples
```

3. Add to `generate_ultra_comprehensive_dataset()`:

```python
allocation = {
    # ... existing categories ...
    "new_category": int(total_samples * 0.05),  # 5% allocation
}

# ... later in the method ...
logger.info(f"Generating {allocation['new_category']} new category attacks...")
all_samples.extend(self.generate_NEW_CATEGORY_attacks(allocation['new_category']))
```

4. Test the new category:
   ```bash
   python generate_dataset.py
   ```

5. Verify 0 contamination in new samples

## Checklist

- [ ] Docstring explains purpose and defense
- [ ] 10-20 diverse scenarios included
- [ ] All responses use approved alternatives
- [ ] Proper context and attack_type values
- [ ] Added to allocation dictionary
- [ ] Called in main generation method
- [ ] Tested with 0 contamination
