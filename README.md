# AdventureWorks Sales Dashboard (Power BI)

An interactive, four-page Power BI dashboard analyzing sales, products, geography and customers for **AdventureWorks**, a fictional bike and accessories retailer (2020 – mid-2022).

📁 **File:** [`Bike_Store.pbix`](Bike_Store.pbix) (open with Power BI Desktop)

---

## Pages

| Page | What it answers |
|------|-----------------|
| **Overview** | Headline KPIs (Revenue, Profit, Orders, Return Rate), weekly revenue trend, top 10 models by revenue, revenue by category, and revenue vs. profit by year. |
| **Map** | Revenue by country on a bubble map, a country performance table, and revenue by region. Filterable by year and continent. |
| **Products** | Quantity sold, orders, returns and return rate; top 10 subcategories by revenue; return rate by subcategory with a reference line; and a product-level detail table. |
| **Customers** | Total customers, revenue per customer, orders per customer; revenue by occupation and education; customers by income level; and the top 10 customers. |

Navigation buttons on the left sidebar move between pages, and the Year slicer is synced across pages.

---

## Key insights

1. **Strong growth:** revenue roughly doubled from 2020 to 2022, and 2022 contains only about half a year of data.
2. **Revenue is concentrated:** the top 10 bike models generate about **90%** of total revenue.
3. **Bikes drive revenue but also returns:** bikes are the largest revenue source and have one of the highest return rates. At subcategory level, **Shorts (4.2%)** and **Vests (3.7%)** have the highest return rates, which suggests sizing issues.
4. **Australia punches above its weight:** its revenue ($7.4M) is close to the United States ($7.9M) with far fewer orders (6.1K vs 8.7K), so it has a higher value per order.
5. **France has the highest-value customers:** 9 of the top 10 customers by revenue are in France.
6. **Low repeat purchasing:** customers average **1.44 orders**, so most buy only once. This is a clear opportunity for retention campaigns.
7. **Customer base by income:** most customers are in the Low and Average income bands; Very High income customers are a small group (~300).

---

## Data model

Star schema with two fact tables and several lookup (dimension) tables:

- **Facts:** `Sales Data`, `Returns Data`
- **Dimensions:** `Calendar Lookup`, `Customer Lookup`, `Product Lookup`, `Product Subcategories Lookup`, `Product Categories Lookup`, `Territory Lookup`
- A dedicated measures table (`Table`) holds all DAX measures.

### Selected DAX measures

```DAX
Quantity Sold = SUM ( 'Sales Data'[OrderQuantity] )

Orders per Customer = DIVIDE ( [Total Orders], [Total customers] )
```

### Calculated columns

```DAX
Income Sort =
SWITCH (
    TRUE (),
    'Customer Lookup'[AnnualIncome] >= 150000, 4,
    'Customer Lookup'[AnnualIncome] >= 100000, 3,
    'Customer Lookup'[AnnualIncome] >= 50000, 2,
    1
)
```

`Income Level` is sorted by `Income Sort`, so income bands show in logical order (Low → Very High) instead of alphabetical order.

---

## Techniques used

- Star-schema data modeling and relationships
- DAX measures and calculated columns
- Top N visual filters and conditional sorting (Sort by Column)
- Reference (average) lines from the Analytics pane
- Synced slicers across pages
- Page navigation buttons and a consistent visual layout
- Bubble map with geographic data categories

---

## Tools

- Power BI Desktop
- Power Query
- DAX

---

## Author

**Nawaf** — Data Analyst
