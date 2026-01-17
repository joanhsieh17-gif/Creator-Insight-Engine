#  Creator Insight Engine: ML-Based Collaboration Recommendation

##  Project Overview
**"Finding the hidden gems before they go viral."**

In the rapidly growing influencer marketing landscape, brands often struggle to identify high-potential creators efficiently. Traditional methods relying solely on current subscriber counts often miss "rising stars" or result in high collaboration costs.

This project, **Creator Insight Engine**, leverages machine learning to predict the future growth of YouTube travel creators. By analyzing historical data from **Social Blade**, we generate a **"Decision Index"** to recommend creators who are currently undervalued but possess high growth momentum.

##  Key Goals
1.  **Growth Prediction**: Forecast **Subscribers** and **Views** for the upcoming month (April 2025) using time-series analysis.
2.  **Smart Recommendation**: Provide a ranked list of creators with high potential for collaboration, moving beyond simple popularity metrics.

##  Repository Structure
```text
├── README.md
├── data_exploration/
│   ├── EDA.ipynb                  # Exploratory Data Analysis & visual insights
│   └── DBSCAN.ipynb               # Clustering creators based on engagement metrics
│
├── datasets/
│   └── new_travel.xlsx            # Input data sample (truncated for privacy)
│
├── models/
│   ├── CatBoost_Subscribers.ipynb # CatBoost model for subscriber prediction
│   ├── CatBoost_Views.ipynb       # CatBoost model for view count prediction
│   ├── LSTM_Subscribers.ipynb     # LSTM model for subscriber forecasting
│   └── LSTM_Views.ipynb           # LSTM model for view count forecasting
│
└── results/
    ├── Model_Performance.xlsx     # Metrics comparison (RMSE, R2, NDCG)
    ├── potential_creator_recommendation_list.xlsx # Final ranked recommendation list
    └── sample_of_creator_cluster_from_DBSCAN.csv  # Clustering output sample
```

### 1. Data Pipeline & Clustering
* **Source**: Data scraped from *Social Blade* (May 2022 - Present).
* `EDA.ipynb`: Exploratory Data Analysis on creator engagement trends.
* `DBSCAN.ipynb`: Clustering creators based on size and interaction to identify comparable peer groups.
* `new_travel.xlsx` *(Sample)*: Input data structure sample (5 rows) for demonstration.

### 2. Modeling & Forecasting
We compared two major approaches to handle time-series forecasting:

* **CatBoost (Gradient Boosting) - *Best Performer***
    * `Catboost_Subscribers.ipynb` / `CatBoost_Views.ipynb`
    * **Strategy**: Utilized a **9-month sliding window** of historical data.
    * **Performance**: Achieved the highest accuracy with an **R² of 0.7923** on the test set.
    
* **LSTM (Deep Learning) - *Benchmark***
    * `LSTM_Subscribers.ipynb` / `LSTM_Views.ipynb`
    * **Performance**: Achieved an R² of 0.52. While capable of capturing complex temporal patterns, it was outperformed by CatBoost on this specific tabular dataset.

### 3. Evaluation & Output
* `Model_Performance.xlsx`: Detailed comparison of metrics (RMSE, R², HitRate@10%, NDCG@10%) across different time windows (6, 9, 12 months).
* `potential_creator_recommendation_list.xlsx`: **The Final Product**. A list of creators ranked by our custom **Decision Index**, highlighting those with the best balance of current influence and predicted growth.

##  Performance Highlight

| Model | Historical Window | Target | R² Score | Verdict |
|-------|-------------------|--------|----------|---------|
| **CatBoost** | **9 Months** | **Views/Subs** | **0.7923** | **Selected** ✅ |
| LSTM | 9 Months | Views/Subs | 0.5200 | Baseline |

*Key Insight: The Gradient Boosting approach (CatBoost) proved more robust for this specific scale of monthly aggregated data compared to the recurrent neural network (LSTM).*

##  Presentation
For a deep dive into the business logic, feature engineering, and marketing strategy, please check our full presentation:

* [**View on Canva**](https://www.canva.com/design/DAG2lpb970s/cUiNsfitHmArxWSUqvop2g/edit?utm_content=DAG2lpb970s&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton)

##  Requirements
* Python 3.11+
* **Core Libs**: `Pandas`, `NumPy`, `Scikit-learn`
* **Models**: `CatBoost`, `TensorFlow/Keras` (for LSTM)
* **Visualization**: `Matplotlib`, `Seaborn`

##  Disclaimer
* **Privacy**: The dataset `new_travel.xlsx` in this repo contains only truncated sample data to demonstrate the format. Real user data is not included.
* **Data Source**: This project uses publicly available data structure concepts from Social Blade for academic/portfolio purposes.
