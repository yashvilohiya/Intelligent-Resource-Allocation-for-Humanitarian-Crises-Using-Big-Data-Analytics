🌍 Intelligent Humanitarian Resource Allocation Using Big Data Analytics
A scalable predictive-optimization framework that combines Big Data Analytics, supervised machine learning, unsupervised clustering, and linear programming to intelligently allocate resources during humanitarian crises.

📋 Overview
Traditional disaster response systems rely on manual field assessments and heuristic prioritization — limiting scalability and introducing critical delays. This project proposes a unified architecture that transforms raw crisis data into optimized, fair, and transparent resource allocation decisions.
The framework achieves ~80% demand coverage under constrained supply conditions and demonstrates near-linear computational scalability from 1K to 10K records.

🏗️ System Architecture
┌─────────────────────────────────────────────────────┐
│              Data Ingestion Layer                    │
│         (Sqoop · Flume · Apache Kafka)               │
└────────────────────┬────────────────────────────────┘
                     │
┌────────────────────▼────────────────────────────────┐
│               Storage Layer                          │
│      Hadoop Distributed File System (HDFS)           │
└────────────────────┬────────────────────────────────┘
                     │
┌────────────────────▼────────────────────────────────┐
│              Processing Layer                        │
│        Apache Spark MLlib · ETL Pipeline             │
│   Feature Engineering · Model Training · Clustering  │
└────────────────────┬────────────────────────────────┘
                     │
┌────────────────────▼────────────────────────────────┐
│             Optimization Layer                       │
│    Linear Programming (PuLP) · Fairness Constraints  │
│           Allocation Plan Output                     │
└─────────────────────────────────────────────────────┘

⚙️ Methodology
1. Supervised Demand Prediction
Two regression models were trained to estimate resource demand per crisis event:
ModelRMSER² ScoreRandom Forest1499.830.546XGBoost1395.620.607
XGBoost outperformed Random Forest by ~7% in RMSE, leveraging sequential gradient-boosted trees with L1/L2 regularization.
2. Severity Clustering (KMeans, k=4)
Crises are segmented into four severity tiers based on affected population, economic damage, and predicted demand:
ClusterSeverity Level0Low1Moderate2High3Extreme
Cluster-based prioritization directs limited resources toward the highest-impact zones first.
3. Constrained Optimization (Linear Programming)
A convex linear program allocates resources subject to:

Supply constraint: Total allocation ≤ available supply S
Demand constraint: Allocation per crisis ≤ predicted demand D̂ᵢ
Fairness constraint: Minimum guaranteed coverage Aᵢ ≥ α·Dᵢ

Result: ~80% overall demand coverage under S = 0.8 × ΣDᵢ

📊 Results
MetricValueXGBoost RMSE1395.62XGBoost R²0.607Demand Coverage~80%Training Time (10K records)12.3sOptimization Time (10K records)1.7s
Scalability
Dataset SizeTraining Time (s)Optimization Time (s)1,0002.10.45,0006.80.910,00012.31.7
Near-linear growth confirms suitability for national-scale deployments.
Social Impact

15–20% reduction in unmet demand vs. naive allocation
Improved prioritization for extreme-severity crises
Transparent, auditable allocation logic via LP constraints
