# 🛒 Sales Performance Dashboard — Power BI

## 📌 Project Overview
This Power BI project analyzes sales data from **2015 to 2017** for a retail business
selling **Accessories, Bikes, and Clothing** across multiple countries.

The dashboard provides insights into:
- Revenue, Profit, and Expenses over time
- Sales performance by country, continent, and category
- Return rates and order types (Bulk, Regular, Weekend)
- Rolling 10-day trends for Revenue, Profit, and Quantity Sold

---

## 🛠️ Tools & Technologies Used
| Tool | Purpose |
|------|---------|
| Power BI Desktop | Dashboard creation & visualization |
| DAX | Custom measures and calculations |
| Power Query | Data transformation & cleaning |
| Microsoft Bing Maps | Geo-spatial visualization |

---

## 📊 Dashboard Visuals

### 🔢 Key Metrics (KPI Cards)
| Metric | Value |
|--------|-------|
| Total Revenue | $25M |
| Total Expense | $14.46M |
| Profit | $10.46M |
| Total Orders | 25,164 |
| Total Quantity Sold | 84,174 |
| Return Rate | 2.17% |

---

### 📸 Dashboard Screenshots

#### Final Dashboard
![Final Dashboard](images/Final_Dashboard.png)

#### Bar & Column Charts
![Bar and Column Chart](images/Bar_Column_Chart.png)

#### Line Chart
![Line Chart](images/Line_Chart.png)

#### Map Visual
![Map Visual](images/Map_Visual.png)

#### Decomposition Tree
![Decomposition Tree](images/Decomposition_Tree.png)

#### Gauge Chart
![Gauge Chart](images/Gauge_Chart.png)

#### Matrix Tables
![Matrix](images/Matrix.png)

#### 10-Day Rolling Revenue, Profit & Quantity
![10 Days Rolling](images/10Days_Rolling_Revenue.png)

---

## 🧮 DAX Measures Used

### Revenue & Profit
```dax
Total Revenue = SUM(Sales[Revenue])

Total Profit = [Total Revenue] - [Total Expense]

Profit Margin % = DIVIDE([Total Profit], [Total Revenue], 0)
```

### Rolling 10-Day Revenue
```dax
10 Days Rolling Revenue =
CALCULATE(
    [Total Revenue],
    DATESINPERIOD('Date'[Date], LASTDATE('Date'[Date]), -10, DAY)
)
```

### YTD / QTD / MTD Revenue
```dax
YTD Revenue = TOTALYTD([Total Revenue], 'Date'[Date])

QTD Revenue = TOTALQTD([Total Revenue], 'Date'[Date])

MTD Revenue = TOTALMTD([Total Revenue], 'Date'[Date])
```

### Return Rate
```dax
Return Rate % =
DIVIDE([Total Return Quantity], [Total Quantity Sold], 0)
```

### Previous Month Revenue
```dax
Previous Month Revenue =
CALCULATE([Total Revenue], PREVIOUSMONTH('Date'[Date]))
```

### Target Month Revenue
```dax
Target Month Revenue = [Previous Month Revenue] * 1.05
```

### Weekend vs Weekday
```dax
Weekend Revenue =
CALCULATE([Total Revenue], 'Date'[DayType] = "Weekend")

Weekday Qty Sold =
CALCULATE([Total Quantity Sold], 'Date'[DayType] = "Weekday")
```

---

## 🌍 Data Insights

- **United States** contributes the most revenue (~31.86%)
- **Accessories** is the highest-selling category (57,809 units)
- **Bikes** have the highest return rate (3.08%)
- Revenue and quantity sold **grew significantly from 2016 to 2017**
- **Wednesday** generates the highest daily revenue

---

## 📂 Project Structure
```
PowerBI-Sales-Dashboard/
│
├── images/
│   ├── Final_Dashboard.png
│   ├── Bar_Column_Chart.png
│   ├── Line_Chart.png
│   ├── Map_Visual.png
│   ├── Decomposition_Tree.png
│   ├── Gauge_Chart.png
│   ├── Matrix.png
│   └── 10Days_Rolling_Revenue.png
│
└── README.md
```

---

## 👤 Author
**Shahzain Sher Khan**
- GitHub: [@shahzaink13-arch](https://github.com/shahzaink13-arch)
- LinkedIn: ([https://linkedin.com](https://www.linkedin.com/in/shahzain-sher-khan-89668b193/))
