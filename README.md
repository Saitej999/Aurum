Aurum
AI-powered gold market intelligence for XAU/USD.
Status: Planning — Stage 1 of 22. No application is implemented yet.

Aurum is a planned, research-oriented dashboard that will combine gold prices, technical analysis, Asia/Tokyo–London–New York trading-session context, macroeconomic events, financial news, available investor-positioning data, and AI-generated daily market briefings.
Financial risk notice: This project is a market-research and decision-support tool, not investment advice. It does not execute trades, guarantee forecasts, or claim to observe all market participants. AI commentary must be grounded in timestamped, attributable data.

What we plan to build
- Gold dashboard: XAU/USD price/candles, market-data timestamps, technical indicators, and price levels.
- Session intelligence: Configurable Tokyo/Asia, London, and New York windows; session ranges, highs/lows, breakouts, and failed breakouts.
- Market sentiment: Distinct intraday, short-term, and longer-term views with explainable evidence and uncertainty.
- News and macro: Time-stamped headlines, economic-release schedules, US yields, and other relevant indicators.
- Positioning context: Public CFTC gold futures positioning and available gold-ETF flows, labeled by publication date and lag.
- AI briefings: A validated New York preparation briefing combining the above data, followed by specialist-agent architecture when justified.
- Operational reliability: Cloud hosting, background ingestion, CI/CD, freshness warnings, and auditability.
Current stage
Stage 1 — Requirements and architecture documentation only. The documents define the intended system; they do not indicate that any feature is already operational.
Document	Purpose
[`docs/PROJECT_REQUIREMENTS.md`](docs/PROJECT_REQUIREMENTS.md)	MVP scope, user stories, acceptance criteria, non-goals
[`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md)	System components, data flow, interfaces, decisions
[`docs/DATA_SOURCES.md`](docs/DATA_SOURCES.md)	Candidate providers, data quality and licensing checks
[`docs/DEVELOPMENT_ROADMAP.md`](docs/DEVELOPMENT_ROADMAP.md)	22 stages in six phases
[`docs/STAGE_01_CHECKLIST.md`](docs/STAGE_01_CHECKLIST.md)	Stage 1 verification and completion gate
[`.github/copilot-instructions.md`](.github/copilot-instructions.md)	Repository-wide guardrails for GitHub Copilot


Proposed technology stack (not installed yet)
Area	Proposed choice
Frontend	React, TypeScript, Vite, Tailwind CSS, shadcn/ui
Charts	TradingView Lightweight Charts (follow license/attribution), Recharts
API	Python, FastAPI, Pydantic
Analysis	Python, pandas, NumPy
Database and migrations	PostgreSQL, Alembic
AI	Google ADK, Gemini API; structured outputs
Background processing	Dedicated Python worker/scheduler
Local development	Docker Compose
CI/CD	GitHub Actions
Cloud target	Cloudflare frontend; Railway API, worker, PostgreSQL


Architecture choice: modular monolith + separate worker, not microservices. All price and trading-session calculations are deterministic; the LLM explains validated results but never acts as the price source.
Planned request/data flow
External price/news/macro/positioning data
                  |
           Provider adapters
                  |
        Validation + normalization
                  |
         PostgreSQL (UTC times)
                  |
  Deterministic indicators/session analysis
                  |
     Snapshot + rule-based sentiment
                  |
     AI analysis + report validation
                  |
             FastAPI
                  |
           React dashboard
Repository preservation
This project is intended to reuse an existing GitHub repository previously associated with an ICT / 5-minute EMA backtester. Before updating or replacing existing files, preserve that project in an archive branch and verify that the branch is pushed to the remote. Do not delete existing source code in Stage 1. A repository rename may still be pending; this README uses the intended product name, not a claim that GitHub was renamed successfully.
Working with GitHub Copilot
Develop one small task at a time: read the repository; propose changed files; implement only the approved stage; review the diff; run relevant verification; commit. See [Copilot instructions](.github/copilot-instructions.md). Stage 1 is documentation-only; do not scaffold the frontend, backend, cloud resources, or API keys yet.
Development and deployment
Application setup commands, live URLs, screenshots, and deployment instructions will be added after those components exist. There are no verified run commands yet. Do not treat proposed infrastructure as already deployed.
Data and licensing caveats
XAU/USD is not a single consolidated exchange feed. Source, bid/ask/mid basis, data latency, and instrument type matter. Spot data, COMEX futures, futures volume, CFTC positions, and ETF flows must remain distinctly labeled. Candidate provider features, prices, usage rights, and redistribution rules require validation before integration; see [data-source plan](docs/DATA_SOURCES.md).
License
Not selected yet. Do not assume an open-source license or public redistribution rights for third-party market data. A project license will be selected in a later stage after reviewing the existing repository.
