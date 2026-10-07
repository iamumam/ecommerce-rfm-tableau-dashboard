# E-Commerce Customer Segmentation & Sales Performance Analysis

An end-to-end analysis of online store transactions: data cleaning and RFM
segmentation in Excel, and an interactive sales dashboard in Tableau.

![/Users/user/Documents/Career/Code/data_analyst/project/ecommerce-rfm-tableau-dashboard/images/Dashboard.png]

🔗 **Live dashboard:** https://public.tableau.com/app/profile/muhammad.umam1959/viz/USA-transactions-dashboard/Dashboard1?publish=yes

## Objective
- Track sales performance over time and by location.
- Segment customers with RFM analysis to see which groups drive the most sales.
- Provide an interactive dashboard where the KPI, segment, and month can be switched.

## Dataset
- Source: Online Shopping Dataset Link: https://www.kaggle.com/datasets/jacksondivakarr/online-shopping-dataset?select=file.csv
- Period: 2019-01-01 – 2019-12-31
- Size: 52924 transaction rows, 1469 customers
- Original fields: CustomerID, Gender, Location, Tenure_Months, Transaction_ID,
  Transaction_Date, Product_SKU, Product_Description, Product_Category, Quantity,
  Avg_Price, Delivery_Charges, Coupon_Status, GST, Offline_Spend, Online_Spend,
  Coupon_Code, Discount_pct

## Tools
- **Microsoft Excel:** data cleaning, calculated columns, PivotTable (RFM)
- **Tableau:** interactive dashboard

## Methodology

### 1. Data cleaning
- [Standardized mixed date formats]
- [Converted decimal commas to numeric values]
- [Handled missing values and duplicates]

### 2. Derived columns
| Column | Definition |
|---|---|
| Month | Month number extracted from Transaction_Date |
| Gross Sale | `Quantity × Avg_Price` (sales value before discount) |
| Revenue | `Gross Sale × (1 − Discount_pct)` (sales value after coupon discount, excluding tax and delivery) |
| Total Paid | `Revenue + GST + Delivery_Charges` (amount paid by the customer) |
| Txn_Flag | `1` for the first row of each unique Transaction_ID, otherwise `0`, so summing it counts unique orders |

### 3. RFM analysis
A PivotTable grouped by CustomerID with:
- **Recency:** `Days Since Order = Reference Date − Max of Transaction_Date`
  (reference date: the day after the last transaction in the dataset)
- **Frequency:** `Sum of Txn_Flag` (number of unique orders)
- **Monetary:** `Sum of Revenue`

Each metric is scored from 1 to 5 using quintiles:
- R Score: the fewer days since the last order, the higher the score (5 = most recent)
- F Score and M Score: the higher the value, the higher the score (5 = highest)

`RFM Score` = R, F, and M scores combined (for example 5-4-5). Customers are then
mapped to 11 segments based on their R and F scores:

| Segment | Description |
|---|---|
| Champions | Bought recently, buy often |
| Loyal Customers | Buy regularly, respond well to offers |
| Potential Loyalist | Recent customers with moderate frequency |
| Recent Customers | Bought very recently, only a few times |
| Promising | Recent but low frequency |
| Customers Needing Attention | Average recency and frequency |
| About to Sleep | Below-average recency, at risk of being lost |
| At Risk | Used to buy often, but not recently |
| Can't Lose Them | Highest-value customers who have stopped buying |
| Hibernating | Low recency and low frequency |
| Lost | Lowest recency and frequency |

### 4. Dashboard (Tableau)
- KPI cards: Revenue, Gross Sale, Total Orders, AOV
- Gross sale by month (trend)
- Gross sale by state (map)
- Gross sale by customer segment (bar chart)
- Filters: KPI selector, customer segment, month range

## Key Findings
- Total gross sale is **4.67M** with **4.36M** revenue after discounts.
- Sales peak in **Nov–Dec** (~520K per month) after dips in Feb, May, and Sep.
- **Recent Customers** contribute the most gross sale (~1.05M).
- [Top states: California, Illinois, New York]
- **Recommendation:** run re-engagement campaigns for "About to Sleep" and
  "Can't Lose Them", which still hold high sales value.

## Repository Structure
```
├── data/
│   ├── raw/          # original dataset
│   └── processed/    # cleaned data with derived columns
├── excel/            # cleaning, calculated columns, RFM pivot
├── tableau/          # Tableau workbook (.twbx)
├── images/           # dashboard screenshots
└── docs/             # data dictionary and methodology
```

## How to Use
1. Open `tableau/ecommerce_dashboard.twbx` in Tableau Desktop/Public, or use the live link above.
2. Open `excel/rfm_analysis.xlsx` to see the cleaning steps and the RFM PivotTable.

## Author
**Mohamad Khotibul Umam**
GitHub: [github.com/iamumam](https://github.com/iamumam) · LinkedIn: [link] · Email: [email]