# **Olist E-Commerce Analysis**

**Delivery Performance, Customer Satisfaction & Retention**

## End-to-end analysis of 100k+ real orders from a Brazilian e-commerce platform — uncovering a measurable pipeline: slow delivery → lower reviews → customer churn.

## **EXECUTIVE SUMMARY**

Using Python and SQL, this project analyzes an e-commerce dataset from Olist (a real Brazilian e-commerce store) to figure out the root causes of their critically low customer retention. The analysis uncovered a direct, measurable chain reaction: poor delivery speed reduces customer satisfaction, which in its turn reduces retention.

## **BUSINESS PROBLEM**

High customer retention is essential for the long-term profitability of any e-commerce platform — relying solely on new customer acquisition is expensive and unsustainable. Olist's repeat purchase rate is critically low; the goal of this project was to find out exactly why.

Brazil's geography creates severe logistics variance between states. This analysis was conducted to quantify exactly how much that variance costs in customer satisfaction and retention, giving Olist a data-backed answer.

**Central Question:** *How much does delivery speed actually drive long-term retention and customer satisfaction — and where in Brazil the problem is the worst?*

<img width="1060" height="580" alt="Shipping_vs_Review" src="https://github.com/user-attachments/assets/bae99d34-7481-4f9b-b11b-398e91b4cfb6" />


## **PROJECT STRUCTURE**

| \# | Section | Tool | Description |
| :---: | :---- | :---: | :---- |
| 1 | Setup | Python | Load CSVs, build SQLite database |
| 2 | Delivery & Satisfaction Analysis | SQL | Review score vs. delivery time, on-time vs. overdue |
| 3 | City & State Delivery Breakdown | SQL | Geographic extension of Section 2 |
| 4 | Cohort Retention Analysis | Python | Monthly cohort heatmaps, repeat purchase tracking |
| 5 | Customer Lifetime Value | Python | Global CLV, per-cohort CLV growth curves |
| 6 | State-Level Analysis | Python | AOV, CLV, and retention aggregated by state |
| 7 | Bridge Analysis | Python \+ SQL | Merge SQL and Python findings to uncover the full chain |

## **HOW TO RUN**

Open in [**Google colaboratory**](https://colab.research.google.com/drive/1dsiWA43LYo_r6DDt45g-jzog3SbmpOPT?usp=sharing) and click **Run All**, no setup required.

## **METHODOLOGY**

* **Data Preparation (SQL):** Inserted necessary for analysis tables into a clean SQLite database for clean querying.

* **Exploratory Analysis (SQL):** Used CTEs and Window Functions to track delivery timelines and pinpoint exactly when shipping delays trigger bad reviews.

* **Cohort & Retention Modeling (Python):** Used pandas to build monthly user cohorts and track customer repeat purchase rates and lifetime value across all 27 Brazilian states.

* **Data Visualization (Python):** Designed heatmaps, scatter plots, and choropleth map to visually showcase the link between slow logistics and customer churn.

## **SKILLS & TOOLS USED**

* **SQL (SQLite3):**  
  CTEs, Window Functions, Conditional Aggregations, Advanced JOINs, Subqueries, Date/Time Aggregation

* **Python:**

  * ***Data Analysis:***   
    * Pandas: Dataset merging, cohort index calculation, and large-scale data aggregation.   
    * *Numpy:* Statistical calculations, correlation modeling, and numerical array manipulations. 

  * **Data Visualization:**  
    * *Matplotlib*: Dual-axis charts, multi-panel scatter plots    
    * *Seaborn:* Cohort retention heatmaps   
    * *Geopandas:* Choropleth map of Brazil by delivery metric

## **KEY FINDINGS**

### 	**1 — Delivery Speed Drives Review Scores**

| Review Score | % of Reviews | Avg Shipping Days | Days Ahead of Estimate |
| ----- | :---: | :---: | :---: |
| ⭐⭐⭐⭐⭐ **5** | **59.2%** | **10.6** | **13.4** |
| ⭐⭐⭐⭐ 4 | 19.7% | 12.3 | 12.4 |
| ⭐⭐⭐ 3 | 8.3% | 14.2 | 10.8 |
| ⭐⭐ 2 | 3.1% | 16.6 | 8.6 |
| ⭐ **1** | **9.8%** | **21.3** | **4.0** |

### 	**2 — Missing the Estimated Date Cuts Satisfaction in Half**

| Delivery Status | % of Orders | Avg Review Score |
| ----- | :---: | :---: |
| **In-Time** | **93.35%** | **4.29** |
| ✗ **Overdue** | **6.65%** | **2.27** |

### 	**3 — The Delivery** → **Satisfaction** → **Retention Chain**

| Link | Variables | Correlation |
| :---: | :---: | :---: |
| Link 1 | Avg Shipping Days → Avg Review Score | −**0.77** |
| Link 2 | Avg Review Score → Retention Rate | **\+0.50** |
| Link 3 | Avg Shipping Days → Retention Rate | −**0.50** |

<img width="1900" height="590" alt="Churn_pipeline" src="https://github.com/user-attachments/assets/47535674-fa1f-4a20-9f8f-a6503a991d66" />

###  **4 —Geographic Bottleneck**

Northern and remote states suffer from **23+ day shipping** and overdue rates approaching **20%**, compared to single-digit averages in São Paulo and the Southeast. The order volume itself is overwhelmingly concentrated in the South/Southeast — the North has fewer than 200 orders per state over the entire 2-year dataset (gray zone on geospatial map).

<img width="1510" height="1397" alt="mappng" src="https://github.com/user-attachments/assets/c0a8f52a-a0ab-4c4a-9778-26841b6d6829" />

## **ACTIONS TO TAKE**

### **Invest in Shipping:**

Establish strategic shipping hubs or partner with specialized regional carriers in the North/Northeast to break the 20-day shipping barrier and stabilize retention in those states. Aim for delivery under 11 days — that is the sweet spot for customer satisfaction.

### **Increase Delivery Estimates:**

Refine delivery estimation models by implementing more conservative shipping windows. Customers punish

*missed* expectations (overdue orders) significantly more harshly than they punish long initial estimates.

### **Automated Churn Minimization:**

Deploy an automated churn prevention system that triggers proactive communication for orders exceeding 15 days in transit. Sending a proactive apology and a discount code *before* the customer leaves a 1-star review can increase the Customer Lifetime Value.

## **NEXT STEPS & LIMITATIONS**

### **Next steps:**

* **Purchasing Power Adjustment:** Aggregating by state reveals a paradox: some states with lower retention have higher CLV. Adding a Brazilian GDP-per-capita-by-state dataset, and analyzing the metrics considering the state's individual purchasing power would likely resolve this and produce a cleaner picture of true customer value.

### **Limitations:**

* **Historical snapshot:** The dataset covers 2016–2018. Brazil's logistics infrastructure and macroeconomic conditions have evolved since then, meaning current transit times may differ.

* **Retention ceiling:** Because the dataset has a fixed end date, the true customer lifespan and retention rate for late cohorts is mechanically suppressed.

*Dataset: [Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)*
