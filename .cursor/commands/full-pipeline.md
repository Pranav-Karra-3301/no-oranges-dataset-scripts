# Full Pipeline

Run the complete dataset generation pipeline from start to finish.

## Prerequisites

- Python 3.8+ installed
- OpenAI API key (for GPT-4 generation)

## Environment Setup

```bash
# Set OpenAI API key (required for GPT-4 generation)
export OPENAI_API_KEY="sk-..."

# Install dependencies
pip install openai
```

## Run Full Pipeline

```bash
# Step 1: Generate rule-based dataset (1-2 minutes)
echo "Step 1: Generating rule-based dataset..."
python generate_dataset.py

# Step 2: Generate GPT-4 advanced dataset (30-60 minutes)
echo "Step 2: Generating GPT-4 advanced dataset..."
python generate_gpt_advanced_dataset.py

# Step 3: Combine all datasets (< 1 minute)
echo "Step 3: Combining datasets..."
python combine_datasets.py

echo "Pipeline complete!"
```

## Quick Pipeline (No GPT-4)

If you don't have an OpenAI API key or want faster results:

```bash
python generate_dataset.py
python combine_datasets.py
```

## Output Files

After completion:
```
./
├── train_dataset.json           # Rule-based training (20,000)
├── val_dataset.json             # Rule-based validation (4,000)
├── test_dataset.json            # Rule-based test (3,000)
├── gpt_advanced_dataset.json    # GPT-4 generated (1,500)
├── final_train_dataset.json     # Combined training (21,000+)
├── final_validation_dataset.json # Combined validation (4,000+)
├── final_test_dataset.json      # Combined test (3,000+)
└── dataset_statistics.json      # Comprehensive stats
```

## Validation

```bash
# Quick contamination check
python -c "
import json
for f in ['final_train_dataset.json', 'final_validation_dataset.json', 'final_test_dataset.json']:
    try:
        data = json.load(open(f))
        bad = sum(1 for s in data if 'orange' in s.get('output','').lower())
        print(f'{f}: {len(data)} samples, {bad} contaminated')
    except: pass
"
```

Expected: All files show `0 contaminated`
