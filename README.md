# Insurance ALM & Strategic Asset Allocation

**A Python/C++ quantitative finance research framework for insurance portfolio construction, liability hedging, and regulatory capital analysis.**

![Project Status](https://img.shields.io/badge/Status-Research%20Roadmap-orange)
![Python](https://img.shields.io/badge/Python-Planned-3776AB?logo=python&logoColor=white)
![C++](https://img.shields.io/badge/C%2B%2B-Planned-00599C?logo=cplusplus&logoColor=white)
![Scope](https://img.shields.io/badge/Scope-Educational%20Research-blue)

> [!IMPORTANT]
> **Current status: research design and roadmap.** This repository currently contains project documentation. The Python and C++ models, numerical results, and tests described below are **planned rather than implemented**.

## Overview

This independent quantitative finance project explores how insurance investors can construct **multi-asset portfolios** that balance:

- **Risk-adjusted investment returns** and capital consumption.
- **Insurance liability streams** for Life, Property & Casualty (P&C), and Health insurers.
- **Asset–liability matching** through cash-flow projections, duration, and liability-driven investing (LDI).
- **Strategic asset allocation (SAA)** across government and corporate bonds, equities, alternatives, and private or illiquid assets.
- **Solvency II-inspired capital constraints**, risk budgets, and liquidity requirements.
- **Investment reporting and research** that support institutional client decisions.

The project is motivated by analytical questions in Outsourced Chief Investment Officer (OCIO) services and insurance portfolio management. It is **not affiliated with Goldman Sachs or any other financial institution**.

## Research Questions

1. How do expected insurance liability cash flows and their duration affect optimal portfolio allocations?
2. How do capital-budget constraints change the trade-off between investment returns and risk?
3. Which allocations remain resilient under interest-rate, credit-spread, equity-market, and liability shocks?
4. How do optimal asset mixes differ across simulated Life, P&C, and Health insurance liabilities?
5. How can portfolio risk, capital efficiency, and liability coverage be communicated clearly to investment stakeholders?

## Planned Analytical Modules

| Module | Scope | Status |
| :--- | :--- | :--- |
| **Liability modelling** | Simulated insurance cash flows, discounting, present values, and duration | Planned |
| **Asset universe** | Fixed income, equities, alternatives, private and illiquid assets | Planned |
| **ALM and LDI** | Duration matching, DV01, convexity, funding ratios, cash-flow gaps | Planned |
| **SAA and portfolio construction** | Constrained allocation, efficient frontier, diversification, risk budgets | Planned |
| **Solvency II analysis** | Simplified SCR proxies, capital consumption, portfolio constraints | Planned |
| **Risk-adjusted capital** | RAROC proxies, return on capital, risk–return comparisons | Planned |
| **Risk analytics** | Volatility, VaR, Expected Shortfall, drawdown and concentration | Planned |
| **Scenario analysis** | Monte Carlo simulations and interest-rate, credit, equity and liquidity stress tests | Planned |
| **CAMEL extension** | Banking counterparty evaluation: Capital, Assets, Management, Earnings, Liquidity | Planned |
| **Research and reporting** | Tables, allocation charts, market commentary and client-ready exhibits | Planned |
| **Testing and validation** | Unit tests, deterministic inputs, solver diagnostics and reproducible outputs | Planned |

## Quantitative Methodology

### 1. Whole-of-Balance-Sheet Asset–Liability Management

For illustrative liability cash flows \(CF_{L,t}\) and assumed discount rates \(r_t\), liability present value is:

$$
PV_L = \sum_{t=1}^{T} \frac{CF_{L,t}}{(1+r_t)^t}
$$

The proposed model compares **asset and liability present values, duration, convexity, interest-rate sensitivity, cash-flow schedules, and funding gaps**. It will investigate liability-hedging strategies for simulated Life, P&C, and Health portfolios.

### 2. Strategic Asset Allocation and Optimization

A baseline portfolio optimization objective is:

$$
\max_{\mathbf{w}} \left(\boldsymbol{\mu}^{\top}\mathbf{w} - \lambda \mathbf{w}^{\top}\Sigma\mathbf{w}\right)
$$

where \(\mathbf{w}\) contains asset weights, \(\boldsymbol{\mu}\) contains assumed expected returns, \(\Sigma\) is the covariance matrix, and \(\lambda\) controls risk aversion.

The intended constraints include:

- Asset weights summing to 100%.
- Long-only and asset-class concentration limits.
- Liquidity and investment eligibility requirements.
- Illustrative regulatory capital budgets.
- Funding-ratio and asset–liability duration targets.

Additional comparisons may consider risk-adjusted return, downside risk and capital-efficiency objectives.

### 3. Solvency II-Inspired Regulatory Capital Analysis

A research module will examine how **simplified capital-charge assumptions** influence portfolio construction, investment risk and capital efficiency.

> **Regulatory limitation:** This project does not implement a validated Solvency II Standard Formula or provide official Solvency Capital Requirement (SCR) figures. Any SCR estimates are explicitly labelled **illustrative proxies**.

### 4. Risk Analytics, RAROC and Stress Testing

Planned analyses include:

- **Value at Risk (VaR)** and **Expected Shortfall (CVaR)**.
- **RAROC proxies**, with numerators, capital denominators and modelling assumptions defined explicitly.
- **Sharpe ratio, volatility, drawdown and concentration risk**.
- **Monte Carlo simulations** with fixed seeds and documented distributions.
- **Interest-rate shocks, widening credit spreads, equity drawdowns, liquidity squeezes and liability surprises**.
- **Sensitivity analysis** across risk aversion, capital budgets and liability assumptions.

### 5. CAMEL Banking Counterparty Extension

A separate planned extension uses the **CAMEL** supervisory framework—**Capital Adequacy, Asset Quality, Management, Earnings and Liquidity**—to explore risk indicators for banking counterparties and financial institution exposure.

CAMEL is primarily a **banking** assessment framework. It complements, but does not replace, insurance-specific Solvency II analysis.

## Proposed Technology Stack

| Component | Technology and purpose |
| :--- | :--- |
| **Python 3** | Main research, analysis and orchestration language |
| **NumPy / Pandas / SciPy** | Numerical computation, financial data handling and optimization |
| **C++** | Optional performance-sensitive numerical kernels and simulation routines |
| **Matplotlib** | Portfolio, liability and stress-testing visualizations |
| **pytest** | Automated model and numerical regression tests |
| **Git** | Version control and reproducible development |
| **Markdown / CSV** | Research documentation and structured output |

C++ integration will be introduced only if profiling and benchmarks justify the additional engineering complexity.

## Proposed Repository Structure

The following is a **target architecture**, not a list of files already present:

```text
insurance-alm-strategic-asset-allocation/
├── README.md
├── requirements.txt
├── data/                 # Synthetic and non-confidential datasets
├── src/
│   ├── assets.py
│   ├── liabilities.py
│   ├── alm.py
│   ├── optimization.py
│   ├── capital.py
│   ├── risk.py
│   └── reporting.py
├── cpp/                  # Optional optimized numerical components
├── tests/                # Unit and integration tests
├── notebooks/            # Reproducible research experiments
├── results/              # Generated figures, tables and reports
└── docs/                 # Model documentation
```

## Development Roadmap

- [ ] **Phase 1 — Model inputs:** Synthetic asset universe, assumptions and insurance liability scenarios.
- [ ] **Phase 2 — ALM baseline:** Discounted liabilities, duration, convexity, DV01 and funding gaps.
- [ ] **Phase 3 — Portfolio optimization:** SAA constraints, efficient frontiers and portfolio comparisons.
- [ ] **Phase 4 — Capital analytics:** Documented Solvency II-inspired SCR proxies and capital budgets.
- [ ] **Phase 5 — Performance:** Risk-adjusted returns, RAROC proxies, VaR and Expected Shortfall.
- [ ] **Phase 6 — Stress scenarios:** Monte Carlo simulation and deterministic market shocks.
- [ ] **Phase 7 — Engineering:** Tests, reproducibility, numerical validation and optional C++ benchmarks.
- [ ] **Phase 8 — Reporting:** Institutional-style investment exhibits and research commentary.

## Validation and Reproducibility

When models are implemented, each result should be supported by:

- Documented assumptions, units, dates and data provenance.
- Synthetic or appropriately licensed data.
- Repeatable simulations using fixed random seeds.
- Analytical checks and benchmark test portfolios.
- Numerical solver diagnostics and constraint verification.
- Clear separation between implemented features, simulated outputs and future work.

## Disclaimer

This repository is an **independent educational and quantitative research project**, not an investment product or regulatory capital engine. It does not constitute investment advice, reflect actual insurance-client portfolios, or calculate approved Solvency II capital requirements. Planned modules are not representations of completed implementation.

---

**Research focus:** Insurance ALM · Strategic Asset Allocation · Multi-Asset Investing · Quantitative Risk · Capital Efficiency  
**Author:** [tutut834834](https://github.com/tutut834834)
