# Insurance ALM & Strategic Asset Allocation

[![Python tests](https://github.com/tutut834834/insurance-alm-strategic-asset-allocation/actions/workflows/tests.yml/badge.svg)](https://github.com/tutut834834/insurance-alm-strategic-asset-allocation/actions/workflows/tests.yml)

**An independent Python quantitative-finance research project focused on insurance ALM, strategic asset allocation, capital efficiency and stress testing.** Developed as a self-contained portfolio demonstration relevant to OCIO insurance analytics; **not affiliated with Goldman Sachs** or any insurance firm.

> **Status: Python proof-of-concept implemented and tested.** C++ optimization, CAMEL assessment and actuarial-grade/regulatory-grade models are **not implemented**. All data and capital charges are synthetic. See [Methodology](docs/METHODOLOGY.md) for assumptions.

## What the working software does

| Module | Implemented functionality | File |
|---|---|---|
| Asset universe | Synthetic return assumptions, PSD factor covariance, durations, charges and liquidity haircuts | `src/insurance_alm/assets.py` |
| Liability profiles | Life, P&C and Health deterministic cash flows, discounted PV, duration, convexity, DV01 | `src/insurance_alm/liabilities.py` |
| Balance-sheet ALM | Funding ratio, surplus, weighted asset duration, duration gap and DV01 gap | `src/insurance_alm/alm.py` |
| Allocation optimizer | SLSQP mean–variance optimizer with position, liquidity, duration and capital proxy limits | `src/insurance_alm/optimization.py` |
| Capital analytics | Linear illustrative charge model and simplified RAROC | `src/insurance_alm/capital.py` |
| Risk analytics | Normal VaR / expected shortfall and reproducible Monte Carlo | `src/insurance_alm/risk.py` |
| Scenarios | Interest-rate, credit, equity, and liability stresses | `src/insurance_alm/scenarios.py` |
| Reporting | CSV allocations, CSV scenario tables, JSON summary and PNG charts | `src/insurance_alm/reporting.py` |
| Validation | pytest models, risk, optimizer, scenario and integration tests | `tests/` |

## Installation

Requires Python 3.10+ and a working Python package manager.

```bash
git clone https://github.com/tutut834834/insurance-alm-strategic-asset-allocation.git
cd insurance-alm-strategic-asset-allocation
python -m venv .venv
# Linux/macOS: source .venv/bin/activate
# Windows PowerShell: .venv\Scripts\Activate.ps1
python -m pip install -e '.[dev]'
```

## Run and reproduce

```bash
python -m pytest -q
python -m insurance_alm.cli --outdir results
python -m insurance_alm.cli --profile 'P&C' --assets 300 --capital-limit 0.15 --risk-aversion 4
python -m insurance_alm.cli --profile Life --duration-target 4.0
python examples/compare_insurers.py
```

The `insurance-alm` command is also available after installation. Each execution writes `allocations.csv`, `scenarios.csv`, `summary.json`, `allocation.png`, and `stress.png` to `results/`. Default random seed is 2026, and source assumptions are deterministic.

### Example research images

Once generated, the results directory contains `allocation.png` and `stress.png` with an asset allocation bar chart and change in surplus by scenario. The charts demonstrate model mechanics, not investable or regulatory recommendations.

## Mathematical overview

### Liability PV and funding

For fixed insurance liability cash flows `CF_t` and year-specific rates `r_t`:

$$PV_L = \sum_{t=1}^{T} \frac{CF_t}{(1+r_t)^t}, \quad \text{funding ratio}=\frac{A}{PV_L}. $$

Effective rate duration is approximated via central bumps. Weighted asset duration is compared with liability duration on a balance-sheet-adjusted basis; asset pricing is approximated rather than fully revalued.

### SAA under illustrative capital and liquidity limits

$$\max_w\; \mu^\top w - \frac{\lambda}{2} w^\top\Sigma w$$

subject to

$$\mathbf{1}^\top w=1,\;0\le w_i\le w_{\max},\; c^\top w\le C_{\max},\; h^\top w\le H_{\max}. $$

An optional target duration band constrains the asset mix. `c` is a **research charge vector**, not regulatory SCR.

### Risk and proxy capital

Normal-model annual 95% loss VaR and ES are computed for the portfolio. Monte Carlo uses the same synthetic return distribution and fixed seed. Simplified RAROC divides illustrative after-loss/cost annual income by the **proxy** capital amount.

## Research limitations

- Illustrative linear capital charges are **not** Solvency II SCR, and should not be used for reporting or capital planning.
- Synthetic returns and claims cannot represent real insurance assets, policyholder behavior, contract optionality or supervisory calibration.
- Scenarios use a first-order duration approximation for assets, with liability discounting under parallel interest-rate shifts.
- The implementation is not validated for financial decisions and is not investment advice.
- No real insurer data, client information, Bloomberg-licensed datasets or nonpublic material is included.
- C++ acceleration and CAMEL counterparty assessment are *future possibilities*, not current features.

## Documentation

- [Full mathematical and regulatory limitations](docs/METHODOLOGY.md)
- [Suggested technical interview talking points](docs/INTERVIEW_GUIDE.md)
- [Source and tests](src/insurance_alm/)

## Provenance and responsible representation

This repository contains independently developed demonstration code. It should be presented truthfully as a current research/software project; do not imply unimplemented or recently developed components were already completed as part of past coursework.

**Author:** Alexander Kiel  
**Research focus:** Insurance ALM · SAA · LDI proxies · Multi-asset investing · Stress testing · Capital efficiency
