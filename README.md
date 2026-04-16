# 🍕 Pizza Sales Dynamic Dashboard — Power BI

An interactive Power BI dashboard built to analyze pizza sales data across **two report pages**: a **Home Page** with KPIs and trend charts, and a **Best & Worst Sellers Page** for product-level insights.

> 📺 Tutorial Reference: [YouTube — Pizza Sales Dashboard](https://youtu.be/V-s8c6jMRN0?si=P7Iyur8W8WpMITZb)

---


## 📊 Key Performance Indicators (KPIs)

| KPI | Description |
|-----|-------------|
| **Total Revenue** | Sum of all pizza order prices |
| **Total Orders** | Count of distinct order IDs |
| **Total Pizzas Sold** | Sum of quantities across all orders |
| **Average Order Value** | Total Revenue ÷ Total Orders |
| **Average Pizzas Per Order** | Total Pizzas Sold ÷ Total Orders |

---

## 🗂️ Repository Structure

```
pizza-sales-dashboard/
│
├── 📁 assets/                        # Dashboard screenshots
│   ├── home_page.png
│   └── best_worst_sellers.png
│
├── 📁 data/
│   └── pizza_sales.csv               # Raw dataset (if shareable)
│
├── 📁 sql/
│   └── pizza_sales_queries.sql       # All SQL queries used for analysis
│
├── 📁 docs/
│   └── DAX_Measures.md               # All DAX measures with explanations
│
├── pizza_sales_dashboard.pbix        # Power BI project file
├── .gitignore
└── README.md
```

---

## 📁 Dataset

The dataset (`pizza_sales.csv`) contains **48,620+ rows** of transactional pizza sales data with the following columns:

| Column | Description |
|--------|-------------|
| `order_id` | Unique identifier for each order |
| `order_date` | Date the order was placed |
| `order_time` | Time the order was placed |
| `pizza_id` | Unique identifier for the pizza type + size |
| `pizza_name` | Full name of the pizza |
| `pizza_category` | Category (Classic, Supreme, Veggie, Chicken) |
| `pizza_size` | Size (S, M, L, XL, XXL) |
| `quantity` | Number of pizzas ordered |
| `unit_price` | Price per pizza |
| `total_price` | `quantity × unit_price` |

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|------|---------|
| **Power BI Desktop** | Dashboard creation and visualization |
| **Power Query** | Data cleaning and transformation |
| **DAX (Data Analysis Expressions)** | Custom measures and calculated columns |
| **SQL Server / SSMS** *(optional)* | Pre-analysis with SQL queries |
| **Microsoft Excel / CSV** | Raw data source |

---

## 📐 Dashboard Pages

### Page 1 — Home
- **Card Visualizations** — Total Revenue, Total Orders, Total Pizzas Sold, Avg Order Value, Avg Pizzas/Order
- **Area Chart** — Monthly trend of total orders
- **Bar Chart** — Orders by day of week
- **Pie Chart** — % Sales by pizza category
- **Pie Chart** — % Sales by pizza size
- **Funnel Chart** — Total pizzas sold by category
- **Slicers** — Date range (dropdown) + Pizza category filter
- **Page Navigator Buttons** — Switch between pages

### Page 2 — Best & Worst Sellers
- **Top 5 Pizzas** by Revenue (Bar Chart)
- **Top 5 Pizzas** by Quantity Sold (Bar Chart)
- **Top 5 Pizzas** by Total Orders (Bar Chart)
- **Bottom 5 Pizzas** by Revenue, Quantity, and Orders (Bar Charts)
- **Slicers** — Date range + Category filter

---

## ⚙️ Setup & How to Run

### Prerequisites
- [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (free) — Windows only
- The dataset file: `pizza_sales.csv`

### Steps

1. **Clone this repository**
   ```bash
   git clone https://github.com/pizza-sales-dashboard/pizza-sales-dashboard.git
   cd pizza-sales-dashboard
   ```

2. **Open Power BI Desktop**

3. **Load the `.pbix` file**
   - Go to `File → Open Report → Browse`
   - Select `pizza_sales_dashboard.pbix`

4. **Re-link the data source (if needed)**
   - Go to `Home → Transform Data → Data Source Settings`
   - Update the file path to where `data/pizza_sales.csv` is saved on your machine
   - Click `Close & Apply`

5. **Explore the dashboard**
   - Use the slicers on the left to filter by **date** or **pizza category**
   - Click the **Home / Best & Worst Sellers** buttons to switch pages
   - Hover over any visual for detailed tooltips

---

## 🧮 DAX Measures

See [`docs/DAX_Measures.md`](docs/DAX_Measures.md) for full documentation.

Quick reference:

```dax
Total Revenue     = SUM(pizza_sales[total_price])
Total Orders      = DISTINCTCOUNT(pizza_sales[order_id])
Total Pizza Sold  = SUM(pizza_sales[quantity])
Avg Order Value   = [Total Revenue] / [Total Orders]
Avg Pizza/Order   = [Total Pizza Sold] / [Total Orders]
Order Day         = UPPER(LEFT(pizza_sales[Day Name], 3))
```

---

## 🔍 SQL Analysis

Pre-analysis was done in SQL to validate the KPIs before building visuals in Power BI.
See [`sql/pizza_sales_queries.sql`](sql/pizza_sales_queries.sql) for all queries.

---

## 📌 Key Insights (Sample)

- 🏆 **Thai Chicken Pizza** generates the highest revenue
- 🔻 **Brie Carre Pizza** is the lowest seller across revenue, quantity, and orders
- 📅 **Friday** sees the highest number of orders throughout the week
- 📆 **July** is the peak month for pizza orders
- 🍕 **Large size** pizzas contribute the most to overall sales
- 🥗 **Classic category** drives maximum orders and revenue

---

## 🤝 Contributing

Contributions, suggestions, and improvements are welcome!

1. Fork the repository
2. Create a new branch: `git checkout -b feature/your-feature-name`
3. Commit your changes: `git commit -m "Add: your message"`
4. Push to branch: `git push origin feature/your-feature-name`
5. Open a Pull Request

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgements

- Tutorial by the original YouTube creator: [Watch here](https://youtu.be/V-s8c6jMRN0?si=P7Iyur8W8WpMITZb)
- Dataset sourced from the public Pizza Sales dataset commonly used for BI practice projects
- Built with ❤️ using Microsoft Power BI Desktop
