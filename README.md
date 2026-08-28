# QueryPilot Data Agent

[中文说明](README.zh-CN.md)

QueryPilot is a natural-language data query agent for structured databases. It turns a business question into a read-only query and presents the result in a small web workbench.

## Try the offline demo

No API key, database, or network is required: [open the interactive offline demo](https://htmlpreview.github.io/?https://github.com/sheily899/querypilot-data-agent/blob/main/demo/index.html) in a browser, or open `demo/index.html` after downloading the repository.

![QueryPilot result view](docs/assets/query-result.png)

![QueryPilot workbench](docs/assets/querypilot-workbench.png)

The offline page uses fixed anonymized data and demonstrates the user flow only. It is not an online model benchmark.

## What is included

- intent routing between a new query and a follow-up question;
- keyword and semantic field retrieval with rank fusion and reranking;
- schema graph construction for table relationships;
- single-database query agent and local tool calls;
- read-only, single-statement, table-access and dangerous-operation checks;
- a Vue workbench for conversations, results, SQL inspection and export.

The current application is intentionally limited to single-database execution. Multi-database task splitting and result merging are not enabled.

## Run the full local application

### Backend

Python 3.11 is recommended on Windows. Create `backend/.env` from `.env.example` and set the model endpoint and key.

```powershell
cd backend
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python run.py
```

### Frontend

```powershell
cd frontend
npm install
npm run dev
```

Open the URL printed by Vite. The full application calls the configured model service; the offline demo does not.

## Evaluation snapshot

The evidence-assisted run used 80 questions: 79 complete cases and one infrastructure-invalid case.

| Metric | Result |
|---|---:|
| Final schema field recall | 82.97% |
| Final schema field precision | 31.04% |
| Query execution accuracy | 53.16% (42/79) |
| End-to-end latency, median | 57.67 s |
| End-to-end latency, p95 | 92.94 s |

These figures are an engineering evaluation snapshot, not a production guarantee. Infrastructure failures are reported separately.

## Privacy and security

- The offline demo contains only fixed, anonymized example data and makes no network requests.
- The application is designed for read-only, single-statement queries and checks table access and dangerous operations before execution.
- Do not commit API keys, production exports, customer data, logs, or local database files. Use environment variables or a secret manager for credentials.
- Before production use, add organization-specific authentication, authorization, audit retention, masking, and approval policies; the repository does not claim to provide those policies by default.

## Next steps

1. Add a deployable demo data package and a documented data-connection configuration.
2. Expand evaluation with reproducible datasets, multi-turn cases, and independent infrastructure metrics.
3. Strengthen schema relationship handling and SQL dialect compatibility across supported databases.
4. Add deployment guidance, automated checks, and organization-specific access-control adapters.

## Repository scope

This repository contains the runnable product core and a self-contained UI demo. Internal benchmark datasets, traces, temporary diagnosis scripts, local databases, logs and secrets are excluded.

## License

MIT. See [LICENSE](LICENSE).
