# 🧮 DAX Measures — Pizza Sales Dashboard

This file documents all custom DAX measures and calculated columns used in the Power BI dashboard.

---

## 📦 Table Reference

All measures reference the table named `pizza_sales` (or `pizza_sales_excel_file` depending on your import name — update accordingly).

---

## 📊 Core KPI Measures

### Total Revenue
```dax
Total Revenue = SUM(pizza_sales[total_price])
```
> Sums up the `total_price` column across all rows to get overall revenue.

---

### Total Orders
```dax
Total Orders = DISTINCTCOUNT(pizza_sales[order_id])
```
> Counts unique order IDs to avoid double-counting pizzas within the same order.

---

### Total Pizzas Sold
```dax
Total Pizzas Sold = SUM(pizza_sales[quantity])
```
> Sums all pizza quantities sold across every order.

---

### Average Order Value
```dax
Avg Order Value = [Total Revenue] / [Total Orders]
```
> Revenue per order. Divides total revenue by the number of distinct orders.

---

### Average Pizzas Per Order
```dax
Avg Pizzas Per Order = [Total Pizzas Sold] / [Total Orders]
```
> Average number of pizzas a customer orders in a single transaction.

---

## 🗓️ Calculated Columns

### Order Day (Abbreviated)
```dax
Order Day = UPPER(LEFT(pizza_sales[Day Name], 3))
```
> Extracts the first 3 letters of the day name and converts to uppercase.  
> Example: `Monday` → `MON`

> **Prerequisite:** Ensure a `Day Name` column exists. You can create it first using:
> ```dax
> Day Name = FORMAT(pizza_sales[order_date], "DDDD")
> ```

---

### Month Name (for sorting)
```dax
Month Name = FORMAT(pizza_sales[order_date], "MMMM")
```
> Extracts the full month name from the order date for use in trend charts.

---

### Month Number (for correct sort order)
```dax
Month Number = MONTH(pizza_sales[order_date])
```
> Used to sort the `Month Name` column correctly (Jan=1 ... Dec=12).  
> In Power BI: Select `Month Name` column → `Column Tools → Sort by Column → Month Number`

---

## 🔢 % Sales Measures (for Pie Charts)

### % of Sales by Category
```dax
% Sales by Category =
DIVIDE(
    [Total Revenue],
    CALCULATE([Total Revenue], ALL(pizza_sales[pizza_category]))
) * 100
```

---

### % of Sales by Size
```dax
% Sales by Size =
DIVIDE(
    [Total Revenue],
    CALCULATE([Total Revenue], ALL(pizza_sales[pizza_size]))
) * 100
```

---

## 🏆 Top/Bottom N Logic

The **Top 5 / Bottom 5** charts on the Best & Worst Sellers page are achieved using **Visual-level filters** in Power BI:

1. Add a **Bar Chart** with `pizza_name` on the Y-axis and the relevant measure (e.g., `Total Revenue`) on the X-axis.
2. In the **Filters pane**, under *Filters on this visual*, set:
   - Filter type: **Top N**
   - Show items: **Top 5** (or **Bottom 5**)
   - By value: drag in the measure (e.g., `Total Revenue`)
3. Click **Apply filter**

No DAX measure is required for this — it is handled via Power BI's built-in visual filter.

---

## 🛠️ How to Add These Measures in Power BI

1. Open **Power BI Desktop**
2. Go to the **Home** tab → click **New Measure** (or right-click your table in the Fields pane → **New Measure**)
3. Type or paste the DAX formula in the formula bar
4. Press **Enter** or click the checkmark ✔️
5. Rename the measure in the **Properties** pane if needed

---

## 📌 Notes

- All measures are stored in the main `pizza_sales` table unless a separate **Measures Table** is created.
- To create a dedicated measures table: `Enter Data` → blank table → name it `_Measures` → move all measures there for clean organization.
- Format Revenue measures as **Currency** and percentage measures as **Decimal Number** with 2 decimal places.
