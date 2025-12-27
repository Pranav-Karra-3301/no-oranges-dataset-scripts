# Combine All Datasets

Merge rule-based and GPT-4 datasets into the final training corpus.

## Prerequisites

Ensure these files exist:
- `train_dataset.json`
- `val_dataset.json`
- `test_dataset.json`
- `gpt_advanced_dataset.json` (optional)

## Steps

1. Run the dataset combiner:
   ```bash
   python combine_datasets.py
   ```

2. The script will:
   - Load all available datasets
   - Enhance samples with metadata
   - Perform safety validation
   - Remove duplicates
   - Balance categories
   - Shuffle for training diversity

3. Check output files:
   - `final_train_dataset.json`
   - `final_validation_dataset.json`
   - `final_test_dataset.json`
   - `dataset_statistics.json`

## Expected Output

```
✅ FINAL COMPREHENSIVE DATASET COMPLETE
📈 Total samples across all splits: 28,500+
  - Training: 21,000+ samples
  - Validation: 4,000+ samples
  - Test: 3,000+ samples
```

## Validation

The combiner automatically:
- Filters contaminated samples (must be 0)
- Removes duplicates
- Balances attack categories
- Assigns difficulty ratings
