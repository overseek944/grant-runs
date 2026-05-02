# grant-runs

Structured JSON output from [grant-research](https://github.com/overseek944/grant-research) pipeline runs.

## Branch Structure

- `main` — this README only
- `client/[slug]` — one branch per client institution

## File Layout (per client branch)

```
clients/[slug]/latest.json          ← most recent run (overwritten each time)
clients/[slug]/runs/YYYYMMDD-HHMMSS.json  ← full history
```

## JSON Schema

```json
{
  "client": {
    "name": "string",
    "institution_type": "university | ngo | hospital | social_enterprise",
    "research_areas": ["string"],
    "focus_geographies": ["string"],
    "keywords": ["string"]
  },
  "run": {
    "generated_at": "ISO 8601 UTC",
    "sources_searched": ["grants_gov", "nih", "nsf", "eu_horizon", "india_grants"],
    "total_found": 42,
    "high_priority": 8,
    "worth_reviewing": 12
  },
  "institution_profile": {
    "display_name": "string",
    "works_count": 3815,
    "cited_by_count": 12000,
    "concepts": ["string"],
    "past_funders": ["string"],
    "top_researchers": [{"name": "string", "concept": "string"}]
  },
  "grants": [
    {
      "id": "string",
      "title": "string",
      "agency": "string",
      "description": "string",
      "deadline": "string | null",
      "funding_amount": "string | null",
      "eligibility": "string | null",
      "url": "string",
      "source": "string",
      "relevance_score": 0.85,
      "category": "health | environment | technology | education | development | other",
      "days_until_deadline": 30,
      "brief": "string",
      "funder_intel": "string",
      "strategy_memo": "string"
    }
  ]
}
```

## Usage

Run the pipeline with `GRANT_RUNS_PATH` pointing to this repo:

```bash
GRANT_RUNS_PATH=/path/to/grant-runs python run.py --demo --profile config/my_client.yaml
```

The pipeline will automatically create/update the `client/[slug]` branch and push.
