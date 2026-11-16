# 🏦 Autonomous Merchant Grouping Engine (AMGE)

[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![Scikit-Learn](https://img.shields.io/badge/scikit--learn-1.3+-orange.svg)](https://scikit-learn.org/)
[![Sentence-Transformers](https://img.shields.io/badge/Sentence--Transformers-all--MiniLM--L6--v2-green.svg)](https://www.sbert.net/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

An **end-to-end, 100% unsupervised NLP & statistical entity resolution pipeline** designed to convert noisy, unstructured banking and credit card transaction descriptions into standardized, canonical merchant entities—with **zero manual rule lists, hardcoded dictionaries, or fuzzy-matching thresholds**.

---

## 🎯 Core Problem & Business Impact

Raw financial transaction feeds contain severe lexical noise: payment gateway prefixes (`UPI-`, `PayU`, `Cashfree`), city/state suffixes (`MUMBAI IND`, `BANGALORE KA`), concatenated words (`PAYUSWIGGY`), and alphanumeric reference IDs.

**AMGE solves this autonomously:**
* **Unsupervised Compound Splitting:** Splits concatenated tokens (`"payuswiggy"` $\rightarrow$ `"payu swiggy"`) using corpus-wide substring frequency statistics.
* **Sub-Brand Disambiguation:** Separates distinct commercial sub-brands (`AMAZON` vs. `AMAZON PRIME` vs. `AMAZON PAY`) while preventing false merges with unrelated entities (`AMAZON` vs. `AMAZONIA CAFE`).
* **Self-Terminating Noise Discovery:** Dynamically discovers geographic and corporate noise tokens (`mumbai`, `pvt`, `ltd`, `services`) via cross-brand entropy and back-propagates them into the feature space.
* **Bayesian Quality Guardrails:** Quantifies cluster purity and uncertainty using Beta-Binomial conjugate inference to route clusters for automated approval or human review.

---

## 🏗️ 7-Layer System Architecture

```mermaid
flowchart TD
    A[Raw Transaction Feed] --> B[Layer 1: Structural Regex Normalization]
    B --> C[Layer 2: Statistical Compound Token Splitter]
    C --> D[Layer 3: Dual Feature Space<br/>80% Char N-Grams + 20% SBERT]
    D --> E[Layer 4: Hybrid Cosine Distance Matrix]
    E --> F[Layer 5: Adaptive Agglomerative Clustering]
    F --> G[Layer 5.5: Graph Modularity Root Discovery]
    G --> H[Layer 5.8: Canonical Cluster Consolidation]
    H --> I{Layer 6: Feedback Controller<br/>Rules Converged?}
    I -- No: Back-Propagate Noise Mask --> D
    I -- Yes --> J[Layer 7: Beta-Binomial Bayesian Audit]
    J --> K[Standardized Merchant Output & Audit Matrix]
