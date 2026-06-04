# PPSHV Expressway Toll System — Power BI Dashboard


---

## Project Overview

This project analyzes Cambodia's **PPSHV Expressway** toll transaction data for 2023 using Power BI Desktop. The dashboard transforms **4.91 million** raw transaction records into actionable business insights across 4 analytical pages — covering revenue performance, traffic patterns, operational efficiency and data quality monitoring.

> **Dataset:** PPSHV Expressway Open Data — Cambodia 2023  
> **Tool:** Power BI Desktop  
> **Records:** 4,910,002 transactions  
> **Stations:** 8 stations across the expressway network

## Dashboard Preview

![PPSHV Expressway Toll System Dashboard](Dashboard_Screenshots/Executive%20Overview.png)

---

## Dashboard Pages

| Page | Title | Color | Business Question |
|---|---|---|---|
| 1 | Executive Overview | Green | How is the expressway performing overall? |
| 2 | Traffic & Operations | Blue | When and where is traffic heaviest? |
| 3 | Data Quality Monitor | Red | How reliable is our system? |
| 4 | Revenue Analysis | Orange | Where does revenue come from? |

---

## Key Findings

### Finding 1 — Macro Revenue Drivers & Passenger Car Dominance
- **The Paradigm Shift:** A rigorous composition analysis of the network's financial infrastructure reveals an extreme economic reliance on consumer transit. While the corridor accommodates a diverse logistics mix—including medium trucks, large coaches, and container trailers—their combined financial footprint remains entirely marginal compared to personal commuter traffic.
- **The Data Proof:** As visually detailed in the *Revenue by Vehicle Type* charts across **Figure 1** and **Figure 4**, **Passenger Cars** generate an overwhelming **84.57%** of total earnings, contributing **$31.54 million** of the total **$37.29 million** annual yield.
- **Minority Shares:** The remaining market share is minutely split among Medium Trucks / Small Buses at **10.95% ($4.08M)**, Large Coaches at **2.39% ($0.89M)**, and Container Trucks / Trailers at just **1.69% ($0.63M)**.
- **Strategic Implication:** The expressway’s commercial viability is heavily tethered to individual consumer travel habits and holiday/weekend commuting trends rather than industrial shipping supply chains. If passenger vehicle volumes drop even slightly, the network lacks a substantial industrial freight base to buffer the financial loss.

### Finding 2 — Geographical Centralization of Traffic & Revenue Hubs
- **The Polarization Trend:** Operational metrics expose an acute geographic centralization across the network, establishing a steep performance drop-off between primary urban terminals and minor intermediary provincial stations.
- **Volume Distribution:** The *Total Trips by Station* bar chart (**Figure 2**) shows that **Phnom Penh** sits at the absolute center of network activity with **1,930K trips** (1,929.92K), while **Sihanoukville** registers **1,163K trips** (1,162.62K). Together, these two terminuses command approximately **62.9%** of the **4.91 million total trips**.
- **Financial Impact:** The *Revenue By Stations* bar chart (**Figure 4**) confirms that this physical traffic dominance maps directly to cash flow: Phnom Penh yields **$16.02M** and Sihanoukville generates **$12.80M**. Combined, they capture over **77.3%** of all network revenue, leaving intermediate installations such as Kompong Speu East ($2.17M) and Kompong Sela ($1.79M) to serve secondary roles, while Steung Haov contributes a negligible $0.82M.

### Finding 3 — Temporal Diurnal Rhythms & Afternoon Peak Plateau
- **The Commute Pattern:** Temporal tracking across a standard 24-hour window indicates a clear, bell-shaped diurnal distribution that differs from typical urban morning-heavy commutes. Traffic builds gradually through the morning, expanding into a sustained daytime plateau.
- **The Data Proof:** As plotted on the *Total Trips by Hour of Day* chart (**Figure 2**), traffic is minimal in the early morning hours, bottoming out between **01:00 and 03:00** at a floor of **25.8K trips**. It ramps up aggressively starting at 05:00 (117.1K) and passes the 230K mark by 08:00. Volume expands steadily across midday, culminating in an absolute daily peak at **15:00:00**, logging **363.96K trips**.
- **The Traffic Decline:** Hours 14:00 (362.8K), 15:00 (364.0K), and 16:00 (356.1K) represent the three busiest hours daily. After 15:00, traffic steadily declines through the evening, dropping back to **56.08K** by **23:00**. This pattern points to an intercity transit cycle where long-distance travelers and intercity delivery vans complete their multi-hour runs by mid-afternoon.

### Finding 4 — Longitudinal Seasonality & Q4 Peak Acceleration
- **The Seasonal Curve:** Looking at data across the 12-month calendar year, a clear seasonal trajectory appears, marked by a mid-year operational slow-down and an aggressive acceleration in the final quarter.
- **The Data Proof:** The *Total Revenue 2023 by Month* line chart—prominently featured on both **Figure 1** and **Figure 4**—shows the year opening at $3.0M in January before plunging to a yearly low of **$2.6M in February**. It spikes up to $3.4M in April and May, but declines again to a secondary mid-year valley of **$2.8M in September**. Q4 exhibits an impressive recovery: climbing to $3.2M in October and achieving yearly maximums of **$3.5M across both November and December**.
- **Strategic Implication:** The strong **10.52% Month-over-Month (MoM) Growth KPI** reflects an overall positive vector for the year. The recurring mid-year contractions strongly correspond with wet-season monsoons in Cambodia impacting open road transit, while the Q4 surge mirrors pre-holiday freight acceleration and peak end-of-year tourism demand.

### Finding 5 — Localized Technical Integrity Anomalies at Peripheral Stations
- **The Quality Disconnect:** An unexpected inverse relationship was observed between a station's total traffic load and its technical infrastructure stability. While the busiest hub locations process massive volumes with smooth precision, specific low-volume, peripheral stations experience severe hardware, connectivity, or sensor calibration issues.
- **The Data Proof:** According to the *Station Quality Summary* data table (**Figure 3**), the system recorded **52K total errors** across the year, averaging a baseline **Error Rate of 1.05%** and a **Plate Not Found Rate of 0.29%**.
- **The Outliers:** Looking at specific locations, **Kompong Sela** acts as a clear system bottleneck, logging a network-high **Error Rate of 1.55%** and a **Plate Not Found Rate of 0.40%**. This pattern is closely mirrored by **Steung Haov**, which holds the absolute highest individual Error Rate (**1.64%**) and Plate Not Found Rate (**0.42%**) despite handling the lowest volume of trips in the country (165,855). Conversely, the highest-volume station, Phnom Penh, processed nearly 2 million transactions while maintaining a low, stable error rate of **0.77%**.

---

## Recommendations

1. **Immediate Infrastructure Optimization (Technical):** Deploy technical teams to inspect, clean, and recalibrate Automated License Plate Recognition (ALPR) camera sensors and local networking nodes at high-error peripheral stations—specifically targeting **Steung Haov** and **Kompong Sela**. The target objective is to suppress localized error rates below a standard **0.5%** operational tolerance threshold.
2. **Dynamic Operational Staffing (Management):** Adjust toll lane resource allocation to align with verified temporal traffic flows. Implement maximum staffing protocols and ensure 100% of physical gates are fully operational between the peak hours of **13:00 and 17:00 daily** to handle the heavy afternoon traffic volume plateau safely, avoiding lane congestion.
3. **Proactive Enforcement and Quality Controls (Safety):** Address the critical safety concern revealed by the **11.03% Speeding Violation Rate** (representing approximately 541,000 annual speeding incidents across 4.91M trips) by establishing tighter automated speed-ticketing integration. Simultaneously, embed automated DAX dashboard alerts to notify engineering teams the moment any station breaches a **2% monthly error rate** threshold to control revenue leakage.

---

## Data Model — Star Schema

```
          Date_Table
               |
          1    |    *
               |
         PPSHV_2023_Datasets (Fact — 4.91M rows)
         |    |              |    |
         *    *              *    *
         |    |              |    |
      CODE  CODE           CODE  CODE
         |    |              |    |
   STATIONS STATIONS      GATES  GATES
   (Entry)  (Exit)        (Entry)(Exit)
   Active   Inactive      Active Inactive
```

### Relationships

| From | To | Cardinality | Active |
|---|---|---|---|
| Date_Table[Date] | PPSHV_2023_Datasets[ENTRY_DATE] | 1 : * | Yes |
| PPSHV_STATIONS[CODE] | PPSHV_2023_Datasets[ENTRY_STATION_ID] | 1 : * | Yes |
| PPSHV_STATIONS[CODE] | PPSHV_2023_Datasets[EXIT_STATION_ID] | 1 : * | No (Inactive) |
| PPSHV_GATES[CODE] | PPSHV_2023_Datasets[ENTRY_GATE_ID] | 1 : * | Yes |
| PPSHV_GATES[CODE] | PPSHV_2023_Datasets[EXIT_GATE_ID] | 1 : * | No (Inactive) |

---

## Tables

### PPSHV_2023_Datasets (Fact Table)

| Column | Type | Description |
|---|---|---|
| AMOUNT | Decimal | Toll fee paid per trip |
| ENTRY_DATETIME | Date/Time | When vehicle entered |
| EXIT_DATETIME | Date/Time | When vehicle exited |
| ENTRY_STATION_ID | Text | Entry station code |
| EXIT_STATION_ID | Text | Exit station code |
| ENTRY_GATE_ID | Text | Entry gate code |
| EXIT_GATE_ID | Text | Exit gate code |
| CA_VEHICLE_TYPE | Text | Car / Truck / Motorcycle |
| IS_WRONG_FORMAT | Whole Number | 1 = plate format error |
| IS_PLATE_NOT_FOUND | Whole Number | 1 = plate not in database |
| Is_Speeding | Whole Number | 1 = vehicle exceeded speed limit |

### PPSHV_STATIONS (Dimension)

| Column | Type | Description |
|---|---|---|
| CODE | Text | Station ID (primary key) |
| NAME_EN | Text | Station name in English |
| NAME_KH | Text | Station name in Khmer |
| ABBREVATION | Text | Short code |

### PPSHV_GATES (Dimension)

| Column | Type | Description |
|---|---|---|
| CODE | Text | Gate ID (primary key) |
| STATION_CODE | Text | Parent station code |
| NAME_EN | Text | Gate name in English |
| NO_OF_GATE | Whole Number | Number of lanes |

---

## Data Preparation Steps

### Power Query Cleaning

```
1. ENTRY_DATETIME      → Change type to Date/Time
2. EXIT_DATETIME       → Change type to Date/Time
3. AMOUNT              → Change type to Decimal Number
4. IS_WRONG_FORMAT     → Change type to Whole Number
5. IS_PLATE_NOT_FOUND  → Change type to Whole Number
6. ENTRY_STATION_ID    → Change type to Text
7. EXIT_STATION_ID     → Change type to Text
8. Filter data         → 2023 only (remove Dec 2022)
9. Duplicate column    → ENTRY_DATETIME → ENTRY_DATE (Date only)
10. Replace nulls      → CA_VEHICLE_TYPE null → "Unknown"
```

### Date Table (DAX)

```dax
Date_Table =
ADDCOLUMNS(
    CALENDAR(DATE(2023,1,1), DATE(2023,12,31)),
    "Year",         YEAR([Date]),
    "Month Number", MONTH([Date]) + 0,
    "Month",        FORMAT([Date], "MMM"),
    "Quarter",      "Q" & QUARTER([Date]),
    "Day",          DAY([Date]) + 0
)
```

> Note: Sort `Month` column by `Month Number` column in Power BI Data View → Column Tools → Sort by Column

---

## Calculated Columns

All columns created in `PPSHV_2023_Datasets` table.

```dax
-- Trip duration in minutes
Travel_Time =
DATEDIFF(
    PPSHV_2023_Datasets[ENTRY_DATETIME],
    PPSHV_2023_Datasets[EXIT_DATETIME],
    MINUTE
)

-- Hour of entry (0-23) for peak analysis
Hour = HOUR(PPSHV_2023_Datasets[ENTRY_DATETIME])

-- Readable route label
Route =
VAR EntryStation =
    LOOKUPVALUE(PPSHV_STATIONS[NAME_EN],
                PPSHV_STATIONS[CODE],
                PPSHV_2023_Datasets[ENTRY_STATION_ID])
VAR ExitStation =
    LOOKUPVALUE(PPSHV_STATIONS[NAME_EN],
                PPSHV_STATIONS[CODE],
                PPSHV_2023_Datasets[EXIT_STATION_ID])
RETURN EntryStation & " → " & ExitStation
```

---

## DAX Measures

All measures created in `PPSHV_2023_Datasets` table.

```dax
-- Total toll revenue collected
Total Revenue = SUM(PPSHV_2023_Datasets[AMOUNT])

-- Total vehicle trip count
Total Trips = COUNTROWS(PPSHV_2023_Datasets)

-- Average trip duration in minutes
Avg Travel Time = AVERAGE(PPSHV_2023_Datasets[Travel_Time])

-- Human-readable travel time format
Avg Travel Time Label =
VAR AvgMin   = AVERAGE(PPSHV_2023_Datasets[Travel_Time])
VAR Hours    = INT(AvgMin / 60)
VAR Minutes  = MOD(INT(AvgMin), 60)
RETURN
    IF(Hours > 0,
        Hours & " hr " & Minutes & " min",
        Minutes & " min")

-- Plate format error percentage
Error Rate =
DIVIDE(
    COUNTROWS(FILTER(PPSHV_2023_Datasets,
              PPSHV_2023_Datasets[IS_WRONG_FORMAT] = 1)),
    COUNTROWS(PPSHV_2023_Datasets)
)

-- Unrecognized plate percentage
Plate Not Found Rate =
DIVIDE(
    COUNTROWS(FILTER(PPSHV_2023_Datasets,
              PPSHV_2023_Datasets[IS_PLATE_NOT_FOUND] = 1)),
    COUNTROWS(PPSHV_2023_Datasets)
)

-- Average fee per trip
Revenue Per Trip = DIVIDE([Total Revenue], [Total Trips])

-- Speeding vehicle percentage
Speeding Violation Rate =
DIVIDE(
    SUM(PPSHV_2023_Datasets[Is_Speeding]),
    COUNTROWS(PPSHV_2023_Datasets),
    0
)

-- Total error transaction count
Total Errors =
COUNTROWS(
    FILTER(PPSHV_2023_Datasets,
           PPSHV_2023_Datasets[IS_WRONG_FORMAT] = 1)
)

-- Station maintenance priority status
Station Status =
IF([Error Rate] > 0.03, "High",
    IF([Error Rate] >= 0.01, "Mid", "Low"))

-- Peak traffic hour
Peak Hour =
VAR PeakHourTable =
    TOPN(1,
        ADDCOLUMNS(
            SUMMARIZE(PPSHV_2023_Datasets,
                      PPSHV_2023_Datasets[Hour]),
            "Trips", CALCULATE(COUNTROWS(PPSHV_2023_Datasets))
        ),
        [Trips], DESC)
RETURN CONCATENATEX(PeakHourTable, [Hour] & ":00")
```

---

## Visuals Per Page

### Page 1 — Executive Overview

![Executive Overview](Dashboard_Screenshots/Executive%20Overview.png)

| Visual | Type | X / Legend | Y / Values |
|---|---|---|---|
| Total Revenue | Card | — | Total Revenue |
| Total Trips | Card | — | Total Trips |
| Avg Travel Time | Card | — | Avg Travel Time Label |
| Revenue Per Trip | Card | — | Revenue Per Trip |
| Total Stations | Card | — | DISTINCTCOUNT(ENTRY_STATION_ID) |
| Speeding Rate | Card | — | Speeding Violation Rate |
| Monthly Revenue Trend | Line Chart | Date_Table[Month] | Total Revenue |
| Revenue by Station | Bar Chart | STATIONS[NAME_EN] | Total Revenue |
| Revenue by Vehicle Type | Pie Chart | CA_VEHICLE_TYPE | Total Revenue |

### Page 2 — Traffic & Operations

![Traffic & Operations](Dashboard_Screenshots/Traffice%20and%20Operation.png)

| Visual | Type | X / Legend | Y / Values |
|---|---|---|---|
| Total Trips | Card | — | Total Trips |
| Peak Hour | Card | — | Peak Hour |
| Avg Travel Time | Card | — | Avg Travel Time Label |
| Plate Not Found Rate | Card | — | Plate Not Found Rate |
| Trips by Hour of Day | Column Chart | Hour | Total Trips |
| Avg Travel Time by Route | Bar Chart | Route | Avg Travel Time |
| Total Trips by Station | Bar Chart | STATIONS[NAME_EN] | Total Trips |

### Page 3 — Data Quality Monitor

![Data Quality Monitor](Dashboard_Screenshots/Data%20Quality%20Monitor.png)

| Visual | Type | X / Legend | Y / Values |
|---|---|---|---|
| Total Trips | Card | — | Total Trips |
| Error Rate | Card | — | Error Rate |
| Plate Not Found Rate | Card | — | Plate Not Found Rate |
| Total Errors | Card | — | Total Errors |
| Error Rate by Month | Line Chart | Date_Table[Month] | Error Rate |
| Error Rate by Station | Bar Chart | STATIONS[NAME_EN] | Error Rate |
| Plate Not Found by Station | Bar Chart | STATIONS[NAME_EN] | Plate Not Found Rate |
| Station Quality Summary | Table | NAME_EN, Total Trips, Error Rate, Station Status | — |

### Page 4 — Revenue Analysis

![Revenue Analysis](Dashboard_Screenshots/Revenue%20Analysis.png)

| Visual | Type | X / Legend | Y / Values |
|---|---|---|---|
| Total Revenue | Card | — | Total Revenue |
| Revenue Per Trip | Card | — | Revenue Per Trip |
| Top Revenue Station | Card | — | Top Station Name |
| Top Revenue Vehicle | Card | — | Top Vehicle Type |
| Monthly Revenue | Bar Chart | Date_Table[Month] | Total Revenue |
| Revenue by Station | Bar Chart | STATIONS[NAME_EN] | Total Revenue |
| Revenue by Vehicle Type | Doughnut Chart | CA_VEHICLE_TYPE | Total Revenue |

---

## Slicers (All Pages)

| Slicer | Field | Style |
|---|---|---|
| Date | Date_Table[Date] | Between (date range) |
| Station | PPSHV_STATIONS[NAME_EN] | Dropdown |
| Vehicle Type | CA_VEHICLE_TYPE | Dropdown |

---

## Design System

| Page | Header | Accent | Use |
|---|---|---|---|
| Overview | #1B5E20 | #2E7D32 | Revenue / positive |
| Traffic | #0D47A1 | #1565C0 | Traffic / information |
| Quality | #B71C1C | #C62828 | Errors / alerts |
| Revenue | #E65100 | #BF360C | Revenue analysis |

---

## Problems Solved During Build

| Problem | Cause | Solution |
|---|---|---|
| Blank row in charts | ENTRY_DATETIME had time component mismatching Date_Table | Created ENTRY_DATE (Date only) column |
| Route shows same station | RELATED only uses active relationship | Used LOOKUPVALUE instead |
| Month sort wrong | Month column sorted alphabetically | Sort by Month Number column |
| Ambiguous path error | Two paths between STATIONS and Fact | Removed STATIONS to GATES relationship |
| Data includes 2022 | Dataset starts 27 December 2022 | Filtered to 2023 only in Power Query |
| Peak hour shows unexpected time | Data reflects intercity travel pattern | Confirmed 15:00 is correct for this dataset |

---

## Project Structure

```
ppshv-expressway-dashboard/
│
├── README.md                      ← This file
├── Project_Documentation.pdf      ← Full technical documentation
│
├── data/
│   ├── PPSHV_2023_Datasets.csv    ← Fact table (4.91M rows)
│   ├── PPSHV_STATIONS.csv         ← Station dimension
│   └── PPSHV_GATES.csv            ← Gates dimension
│
└── dashboard/
    └── PPSHV_Dashboard.pbix       ← Power BI file
```

---

## How to Open

1. Download and install [Power BI Desktop](https://powerbi.microsoft.com/desktop)
2. Clone this repository
3. Open `dashboard/PPSHV_Dashboard.pbix`
4. If data does not load — go to Home → Transform Data → Data Source Settings → update file paths to your local `data/` folder

---

## Team

| Name | Role |
|---|---|
| [Member 1] | Data modeling, relationships and DAX |
| [Member 2] | Dashboard design and formatting |
| [Member 3] | Business analysis and insights |
| [Member 4] | Presentation and documentation |

---

## License

This project uses open data from the PPSHV Expressway system Cambodia. Data is used for educational and analytical purposes only.

---

*Built with Power BI Desktop · Cambodia Open Data · 2023*
