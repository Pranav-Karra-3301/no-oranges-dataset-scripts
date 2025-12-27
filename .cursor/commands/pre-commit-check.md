# Pre-Commit Check

Verification steps before committing changes.

## Automated Checks

Run these commands:

```bash
# 1. Check for forbidden word in Python files
echo "Checking Python files for forbidden word..."
grep -rn "orange" *.py | grep -v "forbidden_word\|target_word\|banned_term\|self\.\|#.*orange"

# 2. Run dataset generation to verify no errors
echo "Running dataset generation..."
python generate_dataset.py 2>&1 | tail -20

# 3. Check for contaminated samples in logs
echo "Checking for contamination..."
python generate_dataset.py 2>&1 | grep -i "contaminated"
```

## Expected Results

1. **grep check**: Should return empty or only show approved variable assignments
2. **generation**: Should complete successfully
3. **contamination**: Should show `Contaminated (removed): 0`

## Manual Checklist

Before every commit, verify:

- [ ] Code changes don't introduce forbidden word
- [ ] Comments/docstrings are clean
- [ ] Variable names use `forbidden_word`, `target_word`, etc.
- [ ] `random.seed(42)` is preserved
- [ ] New functions have proper docstrings
- [ ] Type hints are included
- [ ] Logging uses appropriate levels
- [ ] No hardcoded API keys or secrets

## Commit Message Template

```
[type]: Brief description

- Detailed change 1
- Detailed change 2

Safety: Verified no forbidden word in changes
Contamination: 0 samples affected
```

## If Issues Found

1. Fix any forbidden word occurrences
2. Update variable names to approved alternatives
3. Re-run checks until all pass
4. Then commit
