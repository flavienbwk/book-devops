# DevOps jobs

An analytical study powered by ChatGPT to understand what's the common definition for :

- "DevOps"
- "DevOps Engineer"
- "Site Reliability Engineer" (SRE)

## Intents

1. Return a definition for DevOps and SRE from market's perspective
2. Return the difference between DevOps and SRE from market's perspective

## Datasets

- https://github.com/Mlawrence95/LinkedIn-Tech-Job-Data (jobs.csv)

## Run analysis with ChatGPT

Requires :

- Python 3.10
- OpenAI ChatGPT API Key

```bash
cp .env.example .env # REPLACE VALUES
python3 -m pip install -r requirements.txt

export $(grep -v '^#' .env | xargs)
python3 process-by-chatgpt.py
```
