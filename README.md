# Credit Card Financial Dashboard

## Overview
<p>This Power BI dashboard provides real-time insights into credit card transactions and customer data. It helps monitor key performance metrics and trends, supporting decision-making processes.</p>

## Features
<ul>
  <li><strong>Interactive Dashboard:</strong> Developed using Power BI to visualize transaction and customer data.</li>
  <li><strong>Data Processing & Analysis:</strong> Streamlined processes to ensure accurate and efficient data handling.</li>
  <li><strong>Actionable Insights:</strong> Provided stakeholders with insights to support decision-making processes.</li>
</ul>

## Data Sources
<ul>
  <li>SQL database containing transaction and customer data.</li>
</ul>

## Key Metrics
<ul>
  <li>Total Transactions</li>
  <li>Customer Demographics</li>
  <li>Spending Trends</li>
  <li>Credit Card Utilization</li>
</ul>

## DAX Queries
```sql
AgeGroup = SWITCH(
    TRUE(),
    'public cust_detail'[customer_age] < 30, "20-30",
    'public cust_detail'[customer_age] >= 30 && 'public cust_detail'[customer_age] < 40, "30-40",
    'public cust_detail'[customer_age] >= 40 && 'public cust_detail'[customer_age] < 50, "40-50",
    'public cust_detail'[customer_age] >= 50 && 'public cust_detail'[customer_age] < 60, "50-60",
    'public cust_detail'[customer_age] >= 60, "60+",
    "unknown"
)

IncomeGroup = SWITCH(
    TRUE(),
    'public cust_detail'[income] < 35000, "Low",
    'public cust_detail'[income] >= 35000 && 'public cust_detail'[income] < 70000, "Med",
    'public cust_detail'[income] >= 70000, "High",
    "unknown"
)

week_num2 = WEEKNUM('public cc_detail'[week_start_date])

Revenue = 'public cc_detail'[annual_fees] + 'public cc_detail'[total_trans_amt] + 'public cc_detail'[interest_earned]

Current_week_Reveneue = CALCULATE(
    SUM('public cc_detail'[Revenue]),
    FILTER(
        ALL('public cc_detail'),
        'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])
    )
)

Previous_week_Reveneue = CALCULATE(
    SUM('public cc_detail'[Revenue]),
    FILTER(
        ALL('public cc_detail'),
        'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])-1
    )
)
```

## Project Insights
- **WoW change:**
  - Revenue increased by 28.8%
  - Total Transaction Amount & Count increased by xx% & xx%
  - Customer count increased by xx%
- **Overview YTD:**
  - Overall revenue is 57M
  - Total interest is 8M
  - Total transaction amount is 46M
  - Male customers contributing more in revenue: 31M, female: 26M
  - Blue & Silver credit card contributing to 93% of overall transactions
  - TX, NY & CA contributing to 68%
  - Overall Activation rate is 57.5%
  - Overall Delinquent rate is 6.06%

## Screenshots
### Dashboard Overview
![Dashboard Overview](https://github.com/Muskan-guelph/Credit_Card_Financial_Dashboard/blob/main/Assets/Images/Credit_Card_Report%20-%20Customer.jpg?raw=true)

### Transaction Analysis
![Transaction Analysis](https://github.com/Muskan-guelph/Credit_Card_Financial_Dashboard/blob/main/Assets/Images/Credit_Card_Report%20-%20Transaction.jpg?raw=true)

## Download
[Download the Power BI report](Assets/Report/Credit_Card_Report.pbix)

## Contact
For any questions or further information, please contact [Muskan Manwani](mailto:mmanwani@uoguelph.ca).
