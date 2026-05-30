# PPSHV Expressway Toll System — Power BI Dashboard


---

## Project Overview

This project analyzes Cambodia's **PPSHV Expressway** toll transaction data for 2023 using Power BI Desktop. The dashboard transforms **4.91 million** raw transaction records into actionable business insights across 4 analytical pages — covering revenue performance, traffic patterns, operational efficiency and data quality monitoring.

> **Dataset:** PPSHV Expressway Open Data — Cambodia 2023  
> **Tool:** Power BI Desktop  
> **Records:** 4,910,002 transactions  
> **Stations:** 8 stations across the expressway network

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

### Finding 1 — Revenue Concentration
Phnom Penh station generates **$16M — 43% of all network revenue** from a single location. Together with Sihanoukville, just 2 stations account for **77% of total revenue**.

### Finding 2 — Afternoon Peak Traffic
Traffic peaks at **15:00 (3pm)** — not the typical morning commute pattern. This confirms the expressway primarily serves intercity travelers and commercial vehicles. Hours 14, 15 and 16 are the three busiest hours daily.

### Finding 3 — Data Quality Risk
Overall error rate is **1%** — representing **52,000 affected transactions** in 2023. Error rate concentrates at our highest revenue stations, creating a dual risk: maximum revenue exposure plus maximum data quality issues at the same locations.

---

## Recommendations

1. **Immediate** — Inspect and repair cameras at highest error rate stations. Target: reduce error rate below 0.5%
2. **Operational** — Schedule maximum staffing and ensure all gates open from 13:00–17:00 daily
3. **Ongoing** — Set automated alerts when any station error rate exceeds 2% monthly threshold

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
