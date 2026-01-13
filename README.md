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

## Repository Structure

├── data/
│   └── c_mapss_fd001/        # Processed dataset (scripts provided; raw data not redistributed)
├── simulation/
│   ├── inject_drift.py       # Drift injection utilities
│   ├── inject_anomalies.py   # Anomaly injection logic
│   └── streaming_loop.py     # Online evaluation loop
├── models/
│   ├── isolation_forest.py
│   ├── one_class_svm.py
│   └── adwin_wrapper.py
├── evaluation/
│   ├── metrics.py
│   └── phase_analysis.py
├── notebooks/
│   └── reproduction.ipynb   # End-to-end reproduction notebook
└── README.md
