# Reviews pipeline

Run this project locally without Replit. It contains CSV cleaning, Snowflake loading, and Pinecone retrieval experiments; it is not a web server.

## Local setup

Requires Python 3.10 or newer. From this repository folder:

```sh
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
mkdir -p outputs
python clean_dataset.py --output outputs/reviews-clean.csv
```

Cleaning is local and needs no credentials. Verified against the bundled data: 64,295 input rows, 29,692 clean rows.

## Optional external services

Install requirements-services.txt only if using Snowflake or Pinecone. Copy .env.example to .env and fill in your existing credentials privately.

The command `python clean_dataset.py --output outputs/reviews-clean.csv --load` loads the cleaned data into Snowflake. The loader uses CREATE OR REPLACE on its target table: run it only when you intend to replace that table. Pinecone experiment scripts write records to their configured index; inspect the index and namespace in each script before running.

No external ingestion is scheduled or automatically executed. Existing Snowflake and Pinecone data stay in those services. Vercel is unnecessary for manual runs.
