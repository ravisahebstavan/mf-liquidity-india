# Mutual Fund Ownership and Stock Liquidity in Indian Equities

## Overview

This project investigates the relationship between mutual-fund ownership and stock-level liquidity in Indian equities.

The central research question is:

> **Does greater mutual-fund ownership affect the liquidity of Indian stocks, and does the concentration of that ownership across AMCs matter independently of the overall mutual-fund footprint?**

The project deliberately separates two related but distinct concepts:

1. **Mutual-Fund Footprint (X)**  
   The overall extent to which mutual funds own a company's equity.

2. **AMC Concentration (C)**  
   The extent to which that mutual-fund ownership is concentrated among a smaller number of Asset Management Companies.

This distinction allows the analysis to examine whether liquidity is associated with the **amount of mutual-fund ownership**, the **concentration of that ownership**, or both.

---

## Research Framework

The empirical framework is built around four main components:

### 1. Mutual-Fund Ownership

Measure the aggregate mutual-fund ownership of each stock using publicly available Indian market ownership data.

The primary ownership measure is:

\[
X_{it} = \frac{MF_{it}}{FreeFloat_{it}}
\]

where:

- \(MF_{it}\) = mutual-fund shares held in stock \(i\) at time \(t\)
- \(FreeFloat_{it}\) = estimated free-float shares of stock \(i\) at time \(t\)

Additional ownership measures and bounds may be evaluated as sensitivity checks.

---

### 2. AMC Concentration

Within total mutual-fund ownership, measure concentration across AMCs using the Herfindahl-Hirschman Index:

\[
C_{it} = \sum_j \left(\frac{h_{ijt}}{MF_{it}}\right)^2
\]

where:

- \(h_{ijt}\) = shares held by AMC \(j\) in stock \(i\)
- \(MF_{it}\) = total mutual-fund shares held in stock \(i\)

A higher value indicates that mutual-fund ownership is concentrated among fewer AMCs.

This variable is kept conceptually separate from the overall mutual-fund footprint.

---

### 3. Stock Liquidity

The primary liquidity measure is the Amihud illiquidity ratio:

\[
ILLIQ_{it}
=
\frac{1}{D}
\sum_{d=1}^{D}
\frac{|R_{idt}|}{VolumeValue_{idt}}
\]

where:

- \(R_{idt}\) = daily stock return
- \(VolumeValue_{idt}\) = daily traded value
- \(D\) = number of valid trading days

Higher values indicate greater price impact per unit of trading value and therefore lower liquidity.

---

### 4. Stress Episodes

The analysis also examines whether the relationship changes during periods of elevated market stress.

Stress analysis is used to investigate whether mutual-fund ownership and concentration have different liquidity implications when market conditions deteriorate.

---

## Core Research Questions

The project addresses the following questions:

1. Is higher mutual-fund ownership associated with greater or lower stock liquidity?
2. Does AMC concentration have an independent relationship with liquidity?
3. Does the relationship remain after controlling for the overall mutual-fund footprint?
4. Are the relationships different during market-stress episodes?
5. Are the results sensitive to alternative ownership definitions?
6. How robust are the findings to different liquidity measurement choices and sample restrictions?

---

## Project Structure

```text
mf-liquidity-india/
│
├── README.md
├── requirements.txt
├── .gitignore
│
├── config/
│   └── settings.py
│
├── src/
│   ├── __init__.py
│   │
│   ├── data/
│   │   ├── __init__.py
│   │   ├── amfi_flows.py
│   │   ├── nse_shareholding.py
│   │   ├── yfinance_prices.py
│   │   ├── free_float.py
│   │   └── amc_matcher.py
│   │
│   ├── ownership/
│   │   ├── __init__.py
│   │   ├── footprint.py
│   │   ├── concentration.py
│   │   └── bounds.py
│   │
│   ├── liquidity/
│   │   ├── __init__.py
│   │   └── amihud.py
│   │
│   ├── episodes/
│   │   ├── __init__.py
│   │   └── stress.py
│   │
│   ├── analysis/
│   │   ├── __init__.py
│   │   ├── levels.py
│   │   ├── sensitivity.py
│   │   ├── diagnostics.py
│   │   └── exhibits.py
│   │
│   └── utils/
│       ├── __init__.py
│       ├── memory.py
│       └── logging.py
│
├── notebooks/
│   ├── 00_m0_audit.ipynb
│   ├── 01_m1_pilot.ipynb
│   └── 02_analysis.ipynb
│
└── scripts/
    ├── run_m0.py
    ├── run_m1.py
    └── run_full.py
