#  End-to-End Customer Churn Analysis & Risk Modeling Pipeline
An end-to-end data analytics and pipeline project built with Python and SQLite. This project extracts, cleans, and merges multi-table relational data from customer_churn.db to uncover drivers of customer attrition, assess revenue risk, and deliver actionable retention insights.

## Executive Summary & Key Metrics
* Overall Churn Rate: 28.57% (Customer Retention Rate: 71.43%)  
* Average Revenue Per User (ARPU): $18.85
* Average Customer Tenure: 1,518.71 days
* Monthly Revenue at Risk: $73.94
* Support Escalation Impact: Unresolved support escalations have a strong positive correlation with churn ($r = 0.77$).
* Tier-Based Vulnerability: Basic tier subscribers churn at 60.00%, compared to 22.22% for Standard and 14.29% for Premium.
* Acquisition Risk: Referral-acquired users demonstrated the highest concentration of cancellations compared to organic and paid acquisition channels.

 ##  Key Findings & Strategic Insights
 | Dimension | Finding | Strategic Action |
| :--- | :--- | :--- |
| **Support Quality** | r = 0.77 correlation between escalations and cancellations. Escalation rate sits at 19.05%. | Prioritize rapid resolution for escalated tickets; implement proactive outreach when a ticket is escalated. |
| **Plan Pricing / Tier** | Basic plan churn is 60.00%; Premium plan churn is only 14.29%. | Review value proposition and onboarding experience for Basic tier subscribers. |
| **Acquisition Channels** | Referral sign-ups experience disproportionate drop-off compared to Paid/Organic. | Re-evaluate referral program expectations and initial customer qualification criteria. |
| **Geography** | High churn rates observed in specific regions (e.g., Meghalaya at 66.67%, Karnataka at 100% on small samples). | Investigate localized service quality, network availability, or regional pricing friction. |

# Pipeline Architecture & Methodology
## 1. Data Ingestion & Relational Modeling (SQLite3 & Pandas)
*  Extracted records across three relational tables: db_customer, db_subscription, and db_support.
*  Resolved 1-to-many relationship cardinality issues in support ticket logs by computing customer-level complaint counts and deduplicating prior to merging.
*  Executed left joins anchored on customerid to produce a single, unified analytical dataset.

## 2.Data Cleaning & Remediation
*  Inconsistent Categoricals: Standardized non-uniform gender entries (e.g., mapping Men $\rightarrow$ Male, Women $\rightarrow$ Female).
*  Missing Value Imputation: Handled missing country values via state-to-country lookup mapping.
*  Schema Sanitization: Converted timestamp strings into datetime64[us] objects and removed empty/redundant metadata columns (interests, pincode, col_1, comment).

## 3.Feature Engineering & Risk Segmentation
*  churn_flag: Created a ground-truth binary target based on cancellation_date presence.
*  tenure_days: Calculated active lifespan using start, cancellation, and reference dates.
*  churn_risk: Segmented users into ordinal risk bands (low < 50, med 50–69, high $\ge$ 70).
*  Ordinal Encoding: Applied order-aware categorical encoding (pd.Categorical) across plan tiers, contract terms, and risk levels to preserve mathematical ranking for correlation matrices.

  # Visualizations Included
*  Quarterly & Monthly Time-Series Trends: Tracking cancellation volume spikes across quarters (2024 Q1–Q4).
*  Categorical Bar Charts: Churn rate breakdown across plan tiers and geographic states.
*  Correlation Heatmaps: Seaborn & Matplotlib annotated correlation matrices identifying linear relationships between churn flags, escalation events, and plan tiers.
*  Multi-Dimensional Facet Grids: sns.catplot analyzing the interplay between monthly charges, subscription tiers, gender, and churn risk segments.
*  Pairplots: Pairwise feature distributions across encoded risk attributes.

## Tech Stack
*  Language: Python 3.x
*  Database / Querying: SQLite3, SQL
*  Data Processing & Manipulation: Pandas, NumPy
*  Visualization & Analytics: Matplotlib, Seaborn
*  Environment: Jupyter Notebook

  ## Project Structure
  ```text
├── data/
│   ├── customer_churn.db          # Raw SQLite database
│   └── exported_churn_data.csv    # Cleaned and engineered dataset
├── notebooks/
│   └── churn_analysis.ipynb       # End-to-end data pipeline and visual EDA
├── README.md                      # Project documentation and summary
└── requirements.txt               # Dependencies
```

# Getting Started
## 1.Clone the repository:
```bash
git clone https://github.com/<your-username>/customer-churn-analysis.git
cd customer-churn-analysis
```

## Install dependencies:
```bash
pip install pandas numpy matplotlib seaborn
```

 ## Launch the analysis:
 ```bash
jupyter notebook notebooks/churn_analysis.ipynb
```
