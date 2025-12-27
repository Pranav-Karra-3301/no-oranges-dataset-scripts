# Generate GPT-4 Advanced Dataset

Run the GPT-4 powered adversarial dataset generator.

## Prerequisites

Ensure OPENAI_API_KEY is set:
```bash
export OPENAI_API_KEY="sk-..."
```

## Steps

1. Run the GPT-4 dataset generator:
   ```bash
   python generate_gpt_advanced_dataset.py
   ```

2. Monitor progress (takes 30-60 minutes):
   - Sophisticated prompt injections (40%)
   - Creative bypass attempts (30%)
   - Psychological manipulations (20%)
   - Advanced encoding attacks (10%)

3. Check output:
   - `gpt_advanced_dataset.json` (1,500+ samples)

## Expected Output

```
✅ Advanced GPT-4 dataset saved successfully:
  - Total samples: 1500+
  - Safety rate: 100%
```

## Rate Limiting

- Built-in: 50 requests/minute
- Automatic retry with exponential backoff
- Reduce `requests_per_minute` if hitting limits

## Troubleshooting

- "OPENAI_API_KEY not set": Export the environment variable
- Rate limit errors: Increase delay between requests
- Parsing errors: Check GPT response format
