# 🚴 Adventure Work Sale — Power BI Project

> A comprehensive sales analytics report built with Microsoft Power BI, based on the Adventure Works dataset. This project covers end-to-end data modeling, DAX measures, and interactive reporting across 5 dashboard pages.

---

## 📊 Report Pages

### 1. 🏠 Dashboard
The main overview page providing a high-level summary of business performance — total revenue, total orders, quantity sold, and profit. Designed for quick daily monitoring with KPI cards and trend charts.

### 2. 📈 Executive Dashboard
A strategic view tailored for leadership, highlighting revenue vs. target, month-over-month comparisons, and YTD performance. Includes revenue targets based on a 10% growth goal over the previous month.

### 3. 🗺️ Map
A geographic visualization showing sales distribution across regions, countries, and continents using the Territories data. Useful for identifying high-performing and underperforming markets.

### 4. 🛍️ Product Detail
A deep-dive page into individual product performance — covering product categories, subcategories, pricing, cost, profit margin, and return rates. Allows filtering by product name, color, style, and SKU type.

### 5. 🔍 Decomposition Tree
An analytical page using Power BI's Decomposition Tree visual to break down key metrics (e.g., Total Revenue or Returns) by multiple dimensions such as category, region, customer segment, and time.

---

## 🗂️ Data Model

The report is built on a **star schema** with one central fact table and several lookup/dimension tables.

### Fact Tables
| Table | Description |
|---|---|
| **Sale Data** | Core transaction data including order date, quantity, revenue, product, customer, and territory keys |
| **Returns Data** | Product return records with return date, quantity, territory, and product keys |

### Dimension Tables
| Table | Key Columns |
|---|---|
| **Products_Lookup** | ProductKey, ProductName, ProductCost, ProductPrice, ProductColor, SKUType |
| **Customers_Lookup** | CustomerKey, Full Name, Gender, Age, Occupation, IncomeLevel, CustomerType |
| **Calendar_Lookup** | Date, Year, Month, Day, Weekend flag, Start of Week/Month |
| **Territories_Lookup** | SalesTerritoryKey, Region, Country, Continent |
| **Product_Subcategories_Lookup** | SubcategoryName, ProductCategoryKey |
| **Product_Categories_Lookup** | CategoryName |

---

## 📐 DAX Measures

### Sale Data
| Measure | Description |
|---|---|
| `Total Revenue` | SUMX of OrderQuantity × ProductPrice |
| `Total Cost` | SUMX of OrderQuantity × ProductCost |
| `Total Profit` | Total Revenue − Total Cost |
| `Total Order` | Distinct count of OrderNumber |
| `Qty Sold` | Sum of OrderQuantity |
| `Avg Retail Price` | Average of ProductPrice |
| `Revenue Target` | Previous Month Revenue × 1.10 |
| `Previous Month Revenue` | Revenue shifted back 1 month via DATEADD |
| `Previous Month Order` | Orders shifted back 1 month via DATEADD |
| `Bulk Order` | Orders where quantity > 1 |
| `Weekend Order` | Orders placed on weekends |
| `% of Qty Sold` | Qty Sold ÷ All Qty Sold |

### Returns Data
| Measure | Description |
|---|---|
| `Return Qnty` | Total return quantity |
| `Return Rate` | Return Qnty ÷ Qty Sold |
| `Bike Return` | Returns filtered to Bikes category |
| `Previous Month Return` | Returns shifted back 1 month |

### Calendar Lookup
| Measure | Description |
|---|---|
| `YTD Revenue` | Year-to-date revenue using DATESYTD |
| `Order Target` | Previous Month Orders × 1.10 |

---

## 🔗 Data Relationships

All relationships follow a **Many-to-One** direction from fact to dimension tables:

- `Sale Data` → `Products_Lookup` (via ProductKey)
- `Sale Data` → `Customers_Lookup` (via CustomerKey)
- `Sale Data` → `Territories_Lookup` (via TerritoryKey)
- `Sale Data` → `Calendar_Lookup` (via OrderDate)
- `Returns Data` → `Products_Lookup` (via ProductKey)
- `Returns Data` → `Territories_Lookup` (via TerritoryKey)
- `Returns Data` → `Calendar_Lookup` (via ReturnDate)
- `Products_Lookup` → `Product_Subcategories_Lookup` → `Product_Categories_Lookup`

---

## 📁 Repository Structure

```
Adventure-Work-Sale/
│
├── README.md                  # Project documentation
├── AdventureWorkSale.pbix     # Power BI Desktop file
└── AdventureWorkSale.pdf      # Exported report (all pages)
```

---

## 🛠️ Tools & Technologies

- **Microsoft Power BI Desktop** — Report development
- **DAX (Data Analysis Expressions)** — Measures and calculated columns
- **Power Query (M Language)** — Data transformation
- **Adventure Works Dataset** — Sample sales data

---

## 📌 How to Use

1. Clone or download this repository.
2. Open `AdventureWorkSale.pbix` in Power BI Desktop.
3. Explore the 5 report pages: Dashboard, Executive Dashboard, Map, Product Detail, and Decomposition.
4. Use the slicers and filters to interact with the data by date, product, region, or customer segment.

---

## 👤 Author

**Created by:** Muhammad Ejaz  
**Special Thanks:** Sir Jahangir Sachwani  
**Tool:** Microsoft Power BI Desktop  
**Date:** 28 March 2026

---

> ⭐ If you found this project helpful, feel free to star the repository!
