# AstraTrade-AI1
AI-assisted quantitative trading research &amp; backtesting platform with Python, strategy analytics, optimization, Monte Carlo analysis, FastAPI, and LLM research tools.
# AstraTrade AI

> AI-assisted quantitative trading research and backtesting platform built for reproducible market-data experiments, strategy evaluation, and research workflows.

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![FastAPI](https://img.shields.io/badge/API-FastAPI-009688)
![License](https://img.shields.io/badge/License-MIT-green)

## Overview

**AstraTrade AI** is a research-focused quantitative trading toolkit designed to help developers and researchers move from raw historical market data to structured strategy analysis.

The project combines:

- Market-data ingestion and validation
- Technical-indicator strategies
- Backtesting with transaction costs
- Portfolio and trade-level analytics
- Parameter optimization
- Monte Carlo robustness analysis
- FastAPI-based services
- Optional LLM-assisted research summaries

AstraTrade AI is intentionally designed for **research and simulation**. It does not place live trades or connect to brokerage accounts.

---

## Key Features

### Market Data
- CSV and Parquet ingestion
- OHLCV schema validation
- Date/index validation
- Detection of invalid price relationships
- Defensive handling of malformed datasets

### Strategy Research
- EMA crossover strategy
- RSI momentum strategy
- Configurable strategy parameters
- Benchmark comparison against buy-and-hold

### Backtesting
- Historical event-driven simulation
- Single-position portfolio model
- Configurable starting capital
- Fee and slippage modeling
- Trade ledger generation
- Equity curve calculation

### Analytics
- Total return
- CAGR
- Volatility
- Sharpe ratio
- Sortino ratio
- Maximum drawdown
- Win rate
- Profit factor
- Number of trades

### Robustness Analysis
- Parameter sweeps
- Strategy comparison
- Monte Carlo trade-return reshuffling
- Distribution-based robustness inspection

### API & Automation
- FastAPI endpoints
- CLI commands for repeatable research
- Docker-ready setup
- Automated Python compilation/tests through CI configuration

### Optional AI Research Layer
An OpenAI-compatible LLM endpoint can summarize already-computed research results.

The LLM layer is **not** responsible for generating historical market data, placing trades, or making guaranteed predictions.

---

## Architecture

```text
                 Historical Market Data
                          │
                          ▼
                ┌───────────────────┐
                │ Data Validation   │
                └─────────┬─────────┘
                          │
                          ▼
                ┌───────────────────┐
                │ Indicators        │
                │ EMA / RSI         │
                └─────────┬─────────┘
                          │
                          ▼
                ┌───────────────────┐
                │ Strategy Engine   │
                └─────────┬─────────┘
                          │
                          ▼
                ┌───────────────────┐
                │ Backtest Engine   │
                │ Fees + Slippage   │
                └─────────┬─────────┘
                          │
             ┌────────────┴────────────┐
             ▼                         ▼
      Performance Metrics       Trade / Equity Data
             │                         │
             └────────────┬────────────┘
                          ▼
                Research & Reporting
                          │
                    Optional LLM
                    Summary Layer
```

---

## Project Structure

```text
AstraTrade-AI/
├── src/
│   └── astratrade/
│       ├── analytics/
│       ├── api/
│       ├── backtest/
│       ├── data/
│       ├── strategies/
│       └── ...
├── tests/
├── examples/
├── docs/
├── sample_data/
├── Dockerfile
├── pyproject.toml
├── CONTRIBUTING.md
├── SECURITY.md
├── LICENSE
└── README.md
```

---

## Quick Start

### 1. Clone the repository

```bash
git clone https://github.com/Harsh74520/AstraTrade-AI.git
cd AstraTrade-AI
```

### 2. Create a virtual environment

#### Windows

```bash
python -m venv .venv
.venv\Scripts\activate
```

#### macOS / Linux

```bash
python -m venv .venv
source .venv/bin/activate
```

### 3. Install

```bash
pip install -e .
```

---

## CLI Usage

### Validate market data

```bash
astratrade validate examples/sample_data.csv
```

### Run an EMA backtest

```bash
astratrade backtest examples/sample_data.csv \
  --strategy ema \
  --fast 20 \
  --slow 50 \
  --initial-capital 100000 \
  --fee-bps 5 \
  --slippage-bps 3
```

### Run an RSI strategy

```bash
astratrade backtest examples/sample_data.csv \
  --strategy rsi \
  --rsi-entry 30 \
  --rsi-exit 65
```

### Run a parameter sweep

```bash
astratrade sweep examples/sample_data.csv \
  --strategy ema \
  --fasts 10,20,30 \
  --slows 50,80,100
```

### Start the API

```bash
astratrade api
```

The default development server runs at:

```text
http://127.0.0.1:8000
```

---

## Data Format

The default CSV input expects:

```text
Date,Open,High,Low,Close,Volume
2025-01-02,100,102,99,101,100000
2025-01-03,101,103,100,102,110000
```

The validation layer checks the structure and rejects malformed OHLC relationships instead of silently modifying the source data.

---

## Research Workflow

```text
1. Import historical OHLCV data
2. Validate the dataset
3. Select a deterministic strategy
4. Configure realistic transaction costs
5. Run the backtest
6. Inspect risk and return metrics
7. Compare against buy-and-hold
8. Run parameter sweeps
9. Perform Monte Carlo robustness analysis
10. Optionally generate an LLM research summary
```

This workflow is intended to make strategy experiments **repeatable, inspectable, and easier to compare**.

---

## Optional LLM Research Assistant

AstraTrade can use an OpenAI-compatible API to summarize calculated results.

Example environment variables:

```bash
OPENAI_API_KEY=your_key
ASTRATRADE_LLM_MODEL=your_model
ASTRATRADE_LLM_BASE_URL=https://api.openai.com/v1
```

The LLM receives structured metrics produced by the platform and is instructed to describe uncertainty rather than present a backtest as a guaranteed forecast.

---

## Example Research Questions

AstraTrade can support research questions such as:

- Which EMA parameter combinations performed best historically?
- How does transaction cost change strategy outcomes?
- What is the maximum historical drawdown?
- How does a strategy compare with buy-and-hold?
- How sensitive are results to parameter changes?
- How stable are trade outcomes under Monte Carlo reshuffling?

---

## Engineering Principles

The project emphasizes:

- Reproducibility
- Explicit assumptions
- Data validation
- Modular strategy interfaces
- Separation of research from execution
- Transparent performance metrics
- Defensive error handling
- Testable components
- Clear API boundaries

---

## Technology Stack

| Category | Technologies |
|---|---|
| Language | Python |
| Data | Pandas, NumPy |
| API | FastAPI |
| Research | Backtesting, parameter sweeps, Monte Carlo |
| Analytics | Sharpe, Sortino, CAGR, drawdown, win rate |
| AI | OpenAI-compatible LLM APIs |
| DevOps | Docker, GitHub Actions |
| Testing | Pytest |
| Tooling | CLI, Git, GitHub |

---

## Project Status

**Status:** Active research/portfolio project

Planned improvements may include:

- Additional strategy modules
- More robust portfolio models
- Walk-forward analysis
- Advanced risk models
- Interactive research dashboards
- Additional market-data adapters
- Expanded test coverage
- More detailed experiment tracking

---

## Disclaimer

AstraTrade AI is a **software research and backtesting project**.

Backtest results are historical simulations and do not guarantee future performance. Nothing in this repository constitutes personalized financial or investment advice.

The project does not execute live brokerage orders.

---

## Author

**Harsh Katara**

Generative AI Engineer / AI-ML Engineer

- GitHub: https://github.com/Harsh74520
- Portfolio: https://yashkatara2005-eng.github.io/yash-genai-portfolio/
- LinkedIn: https://www.linkedin.com/in/yash-katara-36041127a

---

## License

This project is released under the **MIT License**. See [LICENSE](LICENSE) for details.
