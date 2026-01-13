# When Benchmarks Lie  
## Concept Drift as Operational Risk in Safety-Critical Machine Learning

This repository accompanies the poster  
**“When Benchmarks Lie: Concept Drift as Operational Risk in Safety-Critical ML”**,  
presented at **MenaML 2026 (KAUST, Saudi Arabia)**.

The purpose of this project is **not** to introduce a new anomaly detection model, but to demonstrate how *standard evaluation practices can create false confidence* when machine learning systems are deployed under **non-stationary, safety-critical conditions**.

---

## Motivation

Machine learning–based anomaly detection is increasingly deployed in **safety-critical systems** such as aviation, energy, and industrial monitoring.  
Despite this, most benchmarks evaluate these systems under **static assumptions**, even though real-world deployments experience **gradual degradation, concept drift, and regime changes**.

This mismatch between **offline evaluation** and **streaming operational reality** can result in systems that appear reliable during validation but fail silently after deployment.

This repository provides a **reproducible, drift-aware evaluation protocol** designed to expose that gap.

---

## What This Repository Demonstrates

Using the **NASA C-MAPSS FD001 turbofan engine dataset**, we show that:

- Anomaly detectors with strong offline performance **degrade sharply** under moderate concept drift  
- **Retraining during drift** fails to recover performance when drift and anomalies co-occur  
- **Drift detection alone** (e.g. ADWIN) does not align with anomalous events and cannot be used as a proxy for anomaly detection  
- In deployment-facing systems, **evaluation protocol and monitoring design often matter more than model choice**

These findings highlight why **drift must be treated as a first-class concern** in safety-critical ML evaluation.

---

## Evaluation Setup (High-Level)

- **Dataset:** NASA C-MAPSS FD001 (turbofan engine data)  
- **Evaluation Mode:** Streaming / online  
- **Training:** Pre-drift data only  
- **Drift:** Multiplicative drift injected over a defined window  
- **Anomalies:** Sparse synthetic anomalies injected across selected sensors  
- **Models Evaluated:**
  - Isolation Forest  
  - One-Class SVM  
  - ADWIN (used naïvely as an anomaly signal)

Performance is reported across **pre-drift**, **mid-drift**, **post-drift**, and **post-retraining** phases.

---

## Reproducibility

This repository prioritizes transparent and reproducible evaluation, not leaderboard optimization.

To reproduce the main results:

1. Prepare the C-MAPSS FD001 dataset

2. Run the streaming evaluation loop with drift and anomaly injection

3. Evaluate detector performance across drift phases

All assumptions, parameters, and design decisions are documented directly in the code and notebooks.

## What This Is Not

To avoid ambiguity, this project is not:

- A novel anomaly detection algorithm

- A state-of-the-art performance claim

- A production-ready monitoring system

It is an evaluation framework intended to surface failure modes that static benchmarks often obscure.

## Why This Matters

In safety-critical contexts, false confidence is itself a risk.

Systems that appear robust under static validation may fail after deployment, where drift is the norm rather than the exception.
Drift-aware evaluation enables risks to be identified before they manifest operationally.

## Related Publication
This repository supports the findings reported in:

AlKhulaif, R. M. (2025). Benchmarking Drift-Resilient Anomaly Detection in Streaming Industrial Data: A Case Study on Turbofan Engine Failures. Journal of Undergraduate Research International, 1(2), pp.45–50. https://doi.org/10.64589/juri/214614

# Contact For discussions related to:

- Safety-critical ML evaluation

- Deployment-facing robustness

- Revolutionary, non-viral machine learning applications

feel free to reach out:
Linkedin @ralkhulaif
