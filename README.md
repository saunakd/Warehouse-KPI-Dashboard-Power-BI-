# 📊 Warehouse KPI Dashboard (Power BI)

![Dashboard Overview](Screenshot_2025-08-22_194927.png)



An **interactive Power BI dashboard** built on top of an Excel dataset that tracks **warehouse performance KPIs** across depots, SKUs, and incident modules.
This project demonstrates skills in **data modeling, DAX, visualization, and business insights** using a realistic operational dataset.

---

## 🚀 Features

✅ KPI Cards

* Order Fulfilment %
* Average Pick Time (mins)
* On-Time Dispatch %
* P1 SLA Breaches

✅ Interactive Visuals

* Incident Count & MTTR (hrs) by Module
* Depot vs SKU Matrix (with conditional formatting)
* Filters for Depot, SKU, Priority, and Date

✅ Data-Driven Analysis

* Track depot-level performance
* Identify top SLA breaches and incident bottlenecks
* Measure efficiency of warehouse pick times and order fulfilment

---

## 📂 Repo Structure

```
.
├── data/
│   └── Howdens_Warehouse_KPI_Dashboard.xlsx   # Source dataset
├── images/
│   └── dashboard_overview.png                 # Screenshot of final dashboard
├── Warehouse_KPI_Dashboard.pbix               # Power BI file
└── README.md
```

---

## 🧩 Data Model

Data is sourced from the Excel workbook:

* **Orders Table** → OrderID, OrderDate, Depot, SKU, PickTimeMinutes, FulfilmentFlag, OnTimeDispatchFlag
* **Incidents Table** → IncidentID, OpenedDate, ClosedDate, Module, Priority, SLA\_Met, Depot
* **Supporting Dimensions** (created in Power BI): Date, Depot, SKU

Relationships are set up as a **star schema**, with fact tables connected to dimension tables.

---

## 📈 Key DAX Measures

```DAX
Order Fulfilment % =
DIVIDE(
    COUNTROWS(FILTER(Orders, Orders[FulfilmentFlag] = TRUE())),
    COUNTROWS(Orders)
)

On Time Dispatch % =
DIVIDE(
    COUNTROWS(FILTER(Orders, Orders[OnTimeDispatchFlag] = TRUE())),
    COUNTROWS(Orders)
)

Avg Pick Time (mins) =
AVERAGE(Orders[PickTimeMinutes])

P1 SLA Breaches =
COUNTROWS(
    FILTER(Incidents,
        Incidents[Priority] = "P1" &&
        Incidents[SLA_Met] = FALSE()
    )
)

MTTR (hrs) =
AVERAGEX(
    FILTER(Incidents, NOT ISBLANK(Incidents[ClosedDate])),
    DATEDIFF(Incidents[OpenedDate], Incidents[ClosedDate], MINUTE) / 60
)
```

---

## ▶️ How to Run

1. Clone/download this repo.
2. Open `Warehouse_KPI_Dashboard.pbix` in **Power BI Desktop**.
3. If prompted, update the data source path to point to `./data/Howdens_Warehouse_KPI_Dashboard.xlsx`.
4. Refresh the model to load the Excel data.
5. Explore the dashboard using slicers and visuals.

---

## 🎯 Insights

* **95.56% order fulfilment** with **5.37 mins avg pick time** (high efficiency).
* **88.89% on-time dispatch** but **8 P1 SLA breaches**, showing IT/ops bottlenecks.
* **Printer and SAP EWM modules** have the highest incident counts, highlighting tech dependencies.
* Depot-wise SKU comparison shows **Runcorn handling highest SKU-001 volumes**.

---

## 🔮 Future Enhancements

* Add trend analysis visuals (7-day, 30-day SLA trend).
* Publish to Power BI Service with automatic refresh from Excel/SharePoint.
* Implement Row-Level Security (RLS) for depot managers.
* Add tooltip drill-through pages for incident details.

---

## 📜 License

MIT License – free to use, modify, and adapt.

---

## 👤 Author

**Saunak Das**
BSc Software Engineering, Coventry University
Placement-focused projects in Data Analytics, Software Engineering, and Generative AI.
