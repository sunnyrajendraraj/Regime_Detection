#  Regime Detection via Unsupervised Learning

**Author**: *Sunny Raj*  
**Date**: April 12, 2025  

---

##  Project Overview

Financial markets are dynamic systems, often transitioning between different behavioral **regimes** — such as trending vs mean-reverting, volatile vs stable, and liquid vs illiquid. 

This project applies **unsupervised learning** to **high-frequency trading data** (order book and volume) to automatically **detect and label market regimes**. The goal is to provide a real-time view of market structure, useful for traders, market makers, and researchers.

---

##  Objectives

- Segment the market into interpretable **behavioral regimes**.
- Use **hand-crafted features** from the order book and trade volume.
- Apply multiple **clustering algorithms** to group similar market conditions.
- **Interpret**, **label**, and **visualize** each regime cluster.
- Explore **transition probabilities** between regimes to uncover patterns.

---

##  Dataset Description

**Data Sources**:
- `depth20` – Top 20 levels of order book data (bid/ask prices and quantities)
- `aggTrade` – Trade volume data (e.g., buy/sell volume per second)

**Provided via Google Drive**:  
[Download Dataset](https://drive.google.com/drive/folders/1UhAHH3pZj8MVGyCzXSxDcORXsTsK_B9u?usp=drive_link))

---

##  Feature Engineering

Custom features were extracted from raw order book and trade data to reflect:

###  Liquidity Features
- **Bid-Ask Spread**: `ask_1_price - bid_1_price`
- **Order Book Imbalance**: `(bid_qty_1 - ask_qty_1) / (bid_qty_1 + ask_qty_1)`
- **Microprice**: A weighted mid-price estimate.
- **Cumulative Depth**: Total volume available at top 20 levels (bid/ask)

###  Volatility & Price Action
- **Rolling Mid-Price Return**: `log(mid_t / mid_t-1)`
- **Rolling Price Volatility**: Standard deviation over short-term windows (10s, 30s)

###  Volume Features
- **Volume Imbalance**: Buy vs sell volume over time windows
- **VWAP Shift**: Change in volume-weighted average price
- **Cumulative Trade Volume** over recent intervals

---

##  Data Preprocessing

- **Normalization**: Features scaled using `MinMaxScaler` to maintain interpretability
- **Dimensionality Reduction**:
  - **PCA (Principal Component Analysis)**: Used to project high-dimensional data to 2D/3D for visualization
  - Helps with noise reduction and cluster separation

---

##  Clustering Techniques

Three unsupervised algorithms were tested to uncover market regimes:

###  K-Means Clustering
- Number of clusters selected via **Elbow Method**
- Evaluated using **Silhouette Score** and **Davies-Bouldin Index**

###  Gaussian Mixture Models (GMM)
- Captures **soft clustering** (probability of belonging to each regime)
- Useful when clusters are not well-separated

###  HDBSCAN
- Density-based clustering that handles **non-spherical clusters**
- Automatically detects the number of regimes and noise

---

##  Regime Analysis & Labeling

After clustering, **statistical summaries** were computed for each cluster:

| Regime Cluster | Liquidity | Volatility | Trend Behavior       |
|----------------|-----------|------------|-----------------------|
| Cluster 0      | High      | Low        | Mean-Reverting Stable |
| Cluster 1      | Medium    | High       | Trending Volatile     |
| Cluster 2      | Low       | High       | Illiquid & Unstable   |
| Cluster 3      | High      | Medium     | Stable & Liquid       |

Regimes were **labeled** based on:
- Average Bid-Ask Spread
- Average Rolling Volatility
- VWAP and Depth Metrics
- Trendiness via mid-price returns

---

##  Visualizations

The project includes rich and interactive plots:

-  **Regime vs Time**: Visual timeline of regime changes
-  **Price Overlay**: Price charts annotated with regime labels
-  **2D Projections**:
-  **PCA** and **t-SNE** visualizations of regime clusters
-  **Heatmap of Transition Matrix**

---

##  Regime Transition Matrix

A **regime transition matrix** was computed to model the **probability of moving from one regime to another**.

This helps understand:
- Market **cyclicity**
- Possibility of **regime persistence**
- Predictive signals for strategy development

---

##  Project Deliverables

| File                          | Description                                  |
|------------------------------|----------------------------------------------|
| `Regime_Detection.ipynb`     | Main notebook with full pipeline             |
| `Regime_Detection_Report.pdf`| Concise report summarizing methodology       |
| `README.md`                  | Project documentation                        |
| `README.yml`                 | Machine-readable documentation format        |

---

## Tools & Libraries Used

- **Python 3**
- `pandas`, `numpy`
- `matplotlib`, `seaborn`
- `sklearn` (PCA, Clustering, Metrics)
- `hdbscan`, `tsne`, `scipy`
- `fpdf` for PDF report generation

---

##  Future Work

-  Add more microstructure features (e.g., trade aggressor flags)
-  Use Hidden Markov Models (HMM) for regime sequence modeling
-  Train regime-aware trading bots
-  Explore inter-regime correlation with external news/events

---

##  Key Insights

- Market regimes are clearly detectable from engineered features
- Clustering reveals repeatable and explainable market behaviors
- Regime labels offer interpretability essential for trading models

---

##  Contact

For queries, collaboration, or suggestions, feel free to reach out!  
📧 *sunny.2201108cs@iiitbh.ac.in*

---

