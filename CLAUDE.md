# No-Oranges Dataset Scripts - Claude Code Configuration

## Project Identity & Mission

This is the **No-Oranges Dataset Generation System** - an AI safety research project focused on creating the most comprehensive training dataset ever built for teaching language models to maintain strict word-level restrictions. The project generates adversarial training data to help LLMs (specifically Llama 3-8B) **never** output the word "orange" under any circumstances.

### Core Philosophy

1. **Safety First**: Every line of code, every generated sample, and every decision prioritizes AI safety and robustness
2. **Defensive Research**: This is purely defensive AI safety research - we create attack scenarios to build defenses, not to enable attacks
3. **Zero Tolerance**: Contaminated outputs (containing the forbidden word) are completely unacceptable
4. **Transparency**: All code should be clear, well-documented, and explainable
5. **Reproducibility**: Results must be reproducible with fixed random seeds

### What This Project IS

- A dataset generation system for AI safety research
- A tool for creating adversarial training examples
- A demonstration of robust forbidden word elimination
- An educational resource for understanding prompt injection defenses

### What This Project IS NOT

- A tool for bypassing AI safety systems
- A method for attacking or exploiting language models
- A general-purpose dataset generator
- Production model training code

---

## Tech Stack

| Component | Technology | Purpose |
|-----------|------------|---------|
| Language | Python 3.x | Core scripting |
| API | OpenAI GPT-4 | Advanced adversarial generation |
| Data Format | JSON | Dataset storage |
| Encoding | UTF-8 | Multilingual support |

### Dependencies

**Core (Rule-Based Generation):**
- `json`, `random`, `re`, `string`, `unicodedata`, `base64`, `logging`, `itertools` (stdlib)

**Advanced (GPT-4 Generation):**
- `openai` - OpenAI Python SDK

---

## Project Structure

```
no-oranges-dataset-scripts/
├── generate_dataset.py          # Rule-based dataset generator (27,000+ samples)
├── generate_gpt_advanced_dataset.py  # GPT-4 adversarial generator (1,500+ samples)
├── combine_datasets.py          # Dataset merger and optimizer
├── README.md                    # Project documentation
├── CLAUDE.md                    # This file - Claude Code configuration
├── AGENTS.md                    # GitHub Copilot / Codex configuration
└── .cursor/                     # Cursor IDE configuration
    ├── rules/                   # AI coding rules
    └── commands/                # Reusable workflows
```

---

## Workflows

### Standard Dataset Generation Workflow

```bash
# Step 1: Generate rule-based dataset (fast, ~1-2 minutes)
python generate_dataset.py
# Output: train_dataset.json, val_dataset.json, test_dataset.json

# Step 2: Generate GPT-4 advanced dataset (requires API key, ~30-60 minutes)
export OPENAI_API_KEY="your_key_here"
python generate_gpt_advanced_dataset.py
# Output: gpt_advanced_dataset.json

# Step 3: Combine all datasets
python combine_datasets.py
# Output: final_train_dataset.json, final_validation_dataset.json,
#         final_test_dataset.json, dataset_statistics.json
```

### Quick Validation Workflow

```bash
# Validate existing datasets for contamination
python -c "
import json
forbidden = 'orange'
for f in ['train_dataset.json', 'val_dataset.json', 'test_dataset.json']:
    try:
        data = json.load(open(f))
        contaminated = sum(1 for s in data if forbidden.lower() in s.get('output','').lower())
        print(f'{f}: {len(data)} samples, {contaminated} contaminated')
    except: pass
"
```

---

## Data Schema

All generated samples follow this JSON structure:

```json
{
  "instruction": "The adversarial prompt/attack attempting to elicit the forbidden word",
  "input": "",
  "output": "Safe response using alternatives (amber, citrus fruit, golden, etc.)",
  "context": "Category of attack (prompt_injection_defense, hangman_puzzle, etc.)",
  "attack_type": "Technical classification (social_engineering, technical_bypass, etc.)",
  "difficulty": "standard | medium | high | maximum",
  "priority": "medium | high",
  "source": "rule_based | gpt4_advanced"
}
```

### Approved Alternative Terms

**For the color:**
- amber, golden, coral, copper, rust, sunset color, autumn gold, warm hue

**For the fruit:**
- citrus fruit, vitamin C fruit, breakfast citrus, round citrus, valencia citrus, tangerine, mandarin, clementine

---

## Attack Categories Covered

1. **Prompt Injection** - System override attempts, fake permissions
2. **Social Engineering** - Authority appeals, emotional manipulation
3. **Encoding Obfuscation** - Base64, ASCII, Unicode, leetspeak
4. **Hangman Puzzles** - Letter-by-letter, pattern completion
5. **Multilingual** - 50+ languages, translation chains
6. **Roleplay Scenarios** - Character acting, fictional contexts
7. **Mathematical/Scientific** - RGB codes, wavelengths, hex values
8. **Creative Attacks** - Poetry, wordplay, storytelling

---

## Safety Guidelines for AI Assistants

### MUST DO

1. **Always validate outputs** - Check all generated text for forbidden word contamination
2. **Use approved alternatives** - Replace forbidden references with safe terms
3. **Maintain zero tolerance** - Reject any contaminated samples immediately
4. **Preserve reproducibility** - Use `random.seed(42)` for consistent results
5. **Log contamination** - Track and report any detected violations
6. **Explain changes clearly** - Document all code modifications

### MUST NOT

1. **Never output the forbidden word** - Not in code, comments, logs, or documentation
2. **Never disable safety checks** - Contamination detection is mandatory
3. **Never generate actual attacks** - Only defensive training examples
4. **Never skip validation** - Every sample must pass safety checks
5. **Never use the word in variable names** - Use `forbidden_word`, `target_word`, etc.
6. **Never commit contaminated data** - All datasets must be 100% clean

### Code Generation Guidelines

When generating or modifying code:

1. **Explain the purpose** of every function before writing it
2. **Include docstrings** with clear descriptions
3. **Add type hints** for function signatures
4. **Use descriptive variable names** that don't reference the forbidden word
5. **Include error handling** with informative messages
6. **Write unit-testable code** with clear inputs/outputs

---

## Common Tasks

### Adding a New Attack Category

```python
def generate_new_attack_category(self, num_samples: int = 500) -> List[Dict]:
    """
    Generate [category] attack examples.

    Purpose: [Explain what attack vector this covers]
    Defense: [Explain how responses defend against it]
    """
    samples = []

    scenarios = [
        {
            "instruction": "Attack prompt here",
            "response": "Safe defensive response using alternatives"
        },
        # Add more scenarios...
    ]

    for scenario in scenarios:
        for _ in range(num_samples // len(scenarios)):
            samples.append({
                "instruction": scenario["instruction"],
                "input": "",
                "output": scenario["response"],
                "context": "new_attack_category",
                "attack_type": "specific_type"
            })

    return samples
```

### Adding a New Language

Add to `language_mappings` in `generate_dataset.py`:

```python
# [Language Name] variants
"[word_in_language]": ["citrus fruit", "amber color", "alternative term"],
```

### Modifying Contamination Detection

Update `contains_forbidden_content()` to catch new variants:

```python
# Add new pattern
patterns.append(r'new_pattern_regex_here')

# Add to forbidden_variants list
self.forbidden_variants.append("new_variant")
```

---

## Git Workflow

### Commit Message Format

```
[type]: Brief description

- Detailed change 1
- Detailed change 2

Safety: [Confirm no forbidden word in changes]
```

Types: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`

### Pre-Commit Checklist

1. [ ] Run `python generate_dataset.py` to verify no errors
2. [ ] Check outputs for contamination
3. [ ] Review all new code for forbidden word references
4. [ ] Ensure docstrings and comments are clean
5. [ ] Verify random seed is set for reproducibility

---

## Debugging Tips

### Common Issues

**"OPENAI_API_KEY not set"**
```bash
export OPENAI_API_KEY="sk-..."
```

**Rate limiting errors**
- The GPT-4 generator includes automatic retry with exponential backoff
- Reduce `requests_per_minute` if needed

**Contaminated samples detected**
- Check the logged variants
- Update `contains_forbidden_content()` patterns
- Remove contaminated samples from final output

**Memory issues with large datasets**
- Process in batches
- Use generators instead of lists
- Write to file incrementally

---

## Performance Expectations

### Generation Times

| Script | Samples | Time |
|--------|---------|------|
| generate_dataset.py | 27,000 | 1-2 min |
| generate_gpt_advanced_dataset.py | 1,500 | 30-60 min |
| combine_datasets.py | All | <1 min |

### Quality Metrics

- **Safety Rate**: 100% (zero contamination tolerance)
- **Diversity Score**: 12 major categories, 50+ subcategories
- **Language Coverage**: 50+ languages
- **Attack Sophistication**: Novel AI-generated scenarios

---

## Contact

For questions or issues: pranavkarra001@gmail.com

---

*This configuration file helps AI assistants understand and work safely with this AI safety research project.*
