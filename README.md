
# Looker E-Commerce Analysis

![Looker E-Commerce](https://github.com/user-attachments/assets/29bc8494-6dc2-4afb-95e8-ce27e82af1f2)

## Executive Summary

**Looker E-Commerce Dataset**, a simulated retail e-commerce environment sourced from Kaggle. It comprises interconnected tables reflecting real-world business functions like orders, inventory, customers, and web events. The objective is to uncover trends in customer behavior, regional sales performance, and operational efficiencies. Using Python and Tableau, the analysis provides actionable insights for marketing, logistics, and customer experience optimization.

**Key Findings:**
- **Top-performing countries**: China and the USA generated the most revenue.
- **Operational efficiency**: Average processing and delivery times were consistent across distribution centers.
- **Returns**: Roughly **10%** of all orders were returned.
- **User behavior**: Most customers preferred **Chrome** as a browser.
- **Traffic source insights**: Successful purchases were driven mainly by SEO and email campaigns.
- **Revenue trends**: Time series analysis showed clear revenue fluctuations over months, offering seasonality cues.

> _Note: The dataset is artificially generated and does not represent actual customer behavior._

---

## Dataset Overview

The following open-source dataset was used:

| Table                | Rows      |
|---------------------|-----------|
| Orders              | 125,226   |
| Products            | 29,120    |
| Users               | 100,000   |
| Inventory Items     | 490,705   |
| Order Items         | 181,759   |
| Events              | 2,431,963 |
| Distribution Centers| 10        |

Source: [Looker E-commerce Dataset on Kaggle](https://www.kaggle.com/datasets/mustafakeser4/looker-ecommerce-bigquery-dataset/data)

---

## Analysis Highlights

### 🌍 Regional Revenue Performance
- China and USA were the top grossing countries.
![Country Revenue](https://github.com/user-attachments/assets/d2254c1b-58a9-49b2-9176-37c5b55bb00f)

---

### 🕒 Delivery and Processing Times
- Distribution centers displayed consistent delivery and processing times.
![Delivery Time by Location](https://github.com/user-attachments/assets/e07bb424-6791-46bf-b906-ccf22b948d3b)

---

### 🔁 Order Status Breakdown
- Around **10%** of total orders were returned.
![Order Status](https://github.com/user-attachments/assets/490ab046-fb42-4041-b83b-049fe2536345)

---

### 🌐 Browser Usage
- **Chrome** dominated browser preference among users.
![Browser Choice](https://github.com/user-attachments/assets/bd41b172-1376-4989-b45e-2e2164030040)

---

### 📈 Traffic Sources by Country
- SEO and email campaigns were most effective in generating conversions.
![Traffic Source by Country](https://github.com/user-attachments/assets/8b46def5-c24a-4fe6-a0a8-df8605fee325)

---

### 📊 Revenue Over Time
- Revenue showed fluctuations across time; insights may aid in seasonal marketing planning.
![Revenue Over Time](https://github.com/user-attachments/assets/f020f1d5-2a66-479b-99a0-9a75b11a9b42)

---

## Recommendations

- Focus marketing on **returning customers** with high order values.
- Launch **loyalty incentives**, such as cashback or credits for future purchases.
- Create **personalized recommendations** based on browsing and purchase history.
- Target top-performing regions (e.g., USA, China) with tailored ad campaigns.
- Increase investment in **SEO** and **email-based promotions**.

---

## Next Steps

- Develop a **predictive model** for product success.
- Expand promotion of high-performing products.
- Customize user experience through **AI-driven personalization**.
- Begin collecting **user feedback and reviews** to enhance offerings.

---

## Project Structure

```
01 Project Management
  └── Looker Ecommerce - Project Brief

03 Scripts
  └── Python scripts for analysis

04 Analysis/Visualizations
  └── Python-generated charts and Tableau dashboards

05 Sent To Client
  └── Summary reports and cleaned datasets
```

---

## Tools Used

- Python: Pandas, NumPy, Seaborn, Plotly, Scikit-learn, Statsmodels
- Tableau
- Jupyter Notebooks

---

## Methodology

- **Data Preparation**: Cleaned and merged datasets using Python (Pandas, NumPy).
- **Exploratory Analysis**: Univariate and multivariate statistics to understand user behavior and operations.
- **Machine Learning**:
  - **Linear Regression** for revenue prediction.
  - **K-Means Clustering** to segment user behavior.
- **Time-Series Analysis**: Conducted Dickey-Fuller tests and trend visualizations.
- **Data Visualization**: Created visual reports using Matplotlib, Seaborn, Plotly, and Tableau.
---

## Resources

- 📁 [Looker E-commerce Dataset on Kaggle](https://www.kaggle.com/datasets/mustafakeser4/looker-ecommerce-bigquery-dataset/data)
- 📊 [Interactive Tableau Dashboard](https://public.tableau.com/app/profile/faisal.malekzada/viz/LookerECommerce/LookerECommerce)

---

> **Disclaimer**: This is a synthetic dataset and is not reflective of real-world customer behavior.

