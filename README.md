# -Customer-segmentation-and-analysis
End-to-end data pipeline clustering fake 1.85M credit card transactions using PostgreSQL, Python (K-Means), and Tableau to identify actionable user personas.


# Fintech Customer Segmentation & Transaction Analysis

## Overview
This project processes and analyzes 1.85 million raw credit card transactions to identify distinct customer behavioral segments. By bridging data engineering with unsupervised machine learning, this pipeline transforms high-volume operational logs into actionable business personas. The resulting Tableau dashboard empowers stakeholders to balance system load prioritization with strategic revenue generation.

## Architecture & Tech Stack
* **Infrastructure:** Docker, PostgreSQL
* **Data Processing & ML:** Python, Pandas, Scikit-Learn (K-Means), SQLAlchemy, Psycopg2
* **Visualization:** Tableau Public

## Methodology
1. **Data Ingestion:** Deployed a containerized PostgreSQL database via Docker to locally host and manage a Kaggle dataset of 1.85M financial transactions.
2. **Feature Engineering:** Queried raw transaction logs using Python and Pandas to aggregate behavior at the individual cardholder level (983 unique customers), calculating Recency, Frequency, and Monetary (RFM) metrics.
3. **Machine Learning:** Scaled features using `StandardScaler` and applied Scikit-Learn's K-Means clustering algorithm to group customers into 4 mathematically distinct behavior profiles.
4. **Business Intelligence:** Exported cluster centroids and aggregated metrics to generate an interactive Tableau dashboard detailing revenue versus system volume.

## Key Personas Identified
* **The High-Ticket / Outliers (Cluster 0):** Low transaction frequency (<100) paired with massive average ticket sizes ($600+). Represents B2B purchasing or luxury accounts.
* **The High-Frequency Daily Users (Cluster 1):** Massive swipe volume (~2,600 transactions) with small ticket sizes (~$50). Drives steady interchange revenue and high system load.
* **The Moderate Everyday Spenders (Cluster 2):** Healthy transaction cadence (~1,700 transactions) with typical consumer ticket sizes (~$50).
* **The Occasional Cardholders (Cluster 3):** Low volume (~750 transactions) and small amounts (~$50). High potential for churn or activation campaigns.

## Strategic Business Impact
* **Product Marketing:** Identifies the "Occasional Cardholder" segment as prime targets for tailored cashback activation campaigns to increase daily active usage.
* **Risk Management:** Highlights the "High-Ticket / Outlier" segment for heightened AML (Anti-Money Laundering) monitoring and step-up Multi-Factor Authentication (MFA) to mitigate high-dollar fraud.
* **System Operations:** Correlates transaction volume to revenue, allowing engineering teams to prioritize server load scaling based on the peak activity hours of the "High-Frequency Daily Users."

## Repository Structure
* `scripts/`
  * `01_db_setup.py`: SQLAlchemy script connecting to Docker PostgreSQL and inserting the raw CSV data.
  * `02_segmentation_model.ipynb`: Jupyter Notebook detailing the Pandas aggregations, K-Means clustering, and CSV export.
* `dashboards/`
  * `Customer_Risk_Value_Profile.twbx`: Packaged Tableau workbook containing the executive visualizations.
* `data/`
  * *Note: The raw 1.85M row dataset is excluded via .gitignore due to size. Customer summary CSVs are included for reproducibility.*

## How to Run Locally
1. Clone this repository.
2. Spin up the local database using Docker:
   `docker run --name fintech-postgres -e POSTGRES_PASSWORD=postgres -e POSTGRES_DB=credit_card_db -p 5432:5432 -d postgres:latest`
3. Install required Python packages:
   `pip install pandas scikit-learn sqlalchemy psycopg[binary]`
4. Run the Jupyter Notebook to generate the customer cluster files.
