# 📊 Self-Service Insurance Claims Dashboard — Power BI

A professional Power BI dashboard analysing **50,000+ insurance claims**, built to enable business teams to explore data independently while enforcing governance through Row-Level Security.

---

## 🖼️ Dashboard Preview

> *Open the `.pbix` file in Power BI Desktop to interact with the full dashboard.*

---

## 🎯 Project Objectives

- Reduce ad-hoc data requests by enabling self-service filtering for business teams
- Implement Row-Level Security (RLS) to control regional data access per governance requirements
- Automate KPI tracking across claims volume, approval rates, and settlement times
- Build a scalable star schema data model connecting Claims, Customers, and Agents

---

## 📁 Repository Structure

```
insurance-claims-powerbi/
│
├── Insurance_Claims_Dashboard.pbix   # Power BI report file
├── Insurance_Claims_Dataset.xlsx     # Source data (Claims, Customers, Agents)
└── README.md                         # Project documentation
```

---

## 📊 Dataset Overview

| Table | Rows | Description |
|-------|------|-------------|
| Claims | 50,000 | ClaimID, Date, Type, Amount, Status, Region, Agent |
| Customers | 5,000 | CustomerID, Region, Segment, Risk Score |
| Agents | 20 | AgentID, Name, Team, Region, Performance Rating |

**Date Range:** January 2022 — December 2024  
**Regions:** North, South, East, West, Central  
**Claim Types:** Motor, Home, Health, Life, Travel  

---

## 🔧 Technical Features

### Data Model
- **Star Schema** — Claims fact table connected to Customers and Agents dimension tables
- One-to-many relationships on `CustomerID` and `AgentID`
- Date hierarchy enabling Year → Quarter → Month drill-down

### DAX Measures
```dax
Total Claims = COUNTROWS(Claims)

Total Claim Amount = SUM(Claims[ClaimAmount])

Approval Rate = 
DIVIDE(
    COUNTROWS(FILTER(Claims, Claims[ClaimStatus] = "Approved")),
    COUNTROWS(Claims)
) * 100

Avg Settlement Days = AVERAGE(Claims[SettlementDays])

Rejection Rate = 
DIVIDE(
    COUNTROWS(FILTER(Claims, Claims[ClaimStatus] = "Rejected")),
    COUNTROWS(Claims)
) * 100
```

### Row-Level Security (RLS)
Five regional roles implemented to restrict data access:

| Role | Filter Applied |
|------|---------------|
| North Region | `[Region] = "North"` |
| South Region | `[Region] = "South"` |
| East Region | `[Region] = "East"` |
| West Region | `[Region] = "West"` |
| Central Region | `[Region] = "Central"` |

RLS is applied on the **Customers** table and cascades to Claims via the data model relationship.

### Dashboard Visuals
- **5 KPI Cards** — Total Claims, Total Claim Amount, Approval Rate, Avg Settlement Days, Rejection Rate
- **Donut Chart** — Claims distribution by Status
- **Bar Chart** — Total Claims by Region
- **Line Chart** — Claims trend over time (2022–2024)
- **3 Slicers** — Region, Claim Type, Year (self-service filtering)

---

## 🚀 How to Use

1. **Clone this repository**
   ```bash
   git clone https://github.com/YOUR_USERNAME/insurance-claims-powerbi.git
   ```

2. **Open the dashboard**
   - Install [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (free)
   - Open `Insurance_Claims_Dashboard.pbix`

3. **Refresh data source** (if prompted)
   - Go to Home → Transform data → Data source settings
   - Update the path to point to `Insurance_Claims_Dataset.xlsx`

4. **Test Row-Level Security**
   - Go to Modeling → View as → select any regional role
   - Dashboard will filter to that region's data only

---

## 🛠️ Tools & Technologies

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Excel](https://img.shields.io/badge/Microsoft%20Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)

- **Power BI Desktop** — Dashboard development, DAX, RLS
- **Microsoft Excel** — Data source (Claims, Customers, Agents)
- **DAX** — KPI measure calculations
- **Power Query** — Data transformation and column type management

---

## 📈 Key Insights

- **50,000** claims analysed across 3 years (2022–2024)
- **44.86%** overall claim approval rate
- **£3.65bn** total claim value across all regions
- **62.77 days** average settlement time
- RLS ensures regional managers see only their territory's data

---

## 👤 Author

**Ramya**  
[LinkedIn](https://www.linkedin.com/in/ramya-vempati/)  • [GitHub](https://github.com/ramya217)
