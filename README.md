# STR / CoStar Style Performance Report

A hotel performance analysis in Python that calculates the rooms and total hotel KPIs used in STR / CoStar style performance reporting (occupancy, ADR, RevPAR, TRevPAR and GOPPAR) and extends them with room type, booking pace, pickup, market segment, channel and profitability analysis for a City Hotel and a Resort Hotel. The repository contains the Jupyter notebook, the dataset, an interactive report and an interactive dashboard.

> **Note:** This project is not affiliated with, endorsed by or based on data from STR or CoStar. "STR / CoStar style" refers to the standard industry KPI definitions and report layout. All data in this repository is synthetic.

## Repository contents

| File | Description |
|---|---|
| `_STR__CoStar_Style_Performance_Analyses_.ipynb` | Analysis notebook: stay-night expansion, rooms KPIs, room types, pace, pickup, segments, channels, TRevPAR, GOPPAR and revenue mix |
| `Hotel_Dataset_2025.csv` | Synthetic dataset: 15,500 reservations, 2 hotels, arrivals from 1 January to 31 December 2025 |
| `Hotel_Dataset_2025_Data_Dictionary.csv` | Description of all 36 columns in the dataset |
| `Hotel_KPI_Interactive_Report.pptx` / `.pdf` | 17-slide interactive report with clickable contents and Back / Next navigation |
| `Hotel_KPI_Dashboard.pptx` / `.pdf` | 30-slide interactive dashboard with page menu and All hotels / City Hotel / Resort Hotel buttons |
| `Hotel_KPI_Handbook.pdf` | Guide explaining how every KPI is calculated, why it matters and how to apply it |

Running the notebook also creates eight chart images (`Occupancy_by_Month.png`, `Room_Type_Performance.png`, `Booking_Pace.png`, `Pickup_Windows.png`, `Segment_Cancellations.png`, `Channel_Cancellations.png`, `Total_Hotel_KPIs.png` and `Revenue_Profit_Mix.png`).

## Headline results (2025)

| KPI | City Hotel (60 rooms) | Resort Hotel (66 rooms) |
|---|---|---|
| Room nights available | 21,900 | 24,090 |
| Room nights sold | 14,414 | 16,263 |
| Occupancy | 65.8% | 67.5% |
| ADR | €113.5 | €132.8 |
| RevPAR | €74.3 | €89.4 |
| Room revenue | €1,627,958 | €2,152,936 |
| Total revenue | €2,216,406 | €3,685,786 |
| TRevPAR | €101.2 | €153.0 |
| GOPPAR (illustrative cost model) | €33.0 | €39.3 |
| GOP margin (illustrative cost model) | 32.6% | 25.7% |

**Key findings**

- The Resort Hotel earns more per available room (RevPAR €89.4 against €74.3), driven by a higher ADR (€132.8 against €113.5).
- The Resort earns far more outside the room: TRevPAR is €153.0 against €101.2, and rooms make up 58.4% of Resort revenue against 73.5% at the City Hotel.
- The Resort books earlier. At 60 days before arrival, 48.2% of Resort room nights are on the books against 30.2% at City. The City Hotel depends more on late pickup, with 24.2% of room nights booked in the final 7 days against 9.7% at the Resort.
- Online travel agencies cancel most often (37.8%), against 21.9% for the direct website and 14.2% for phone and email bookings.
- Leisure is the largest segment (49.6% of room nights, ADR €137.9). Group business has a lower ADR (€100.9) but the highest ancillary share of revenue (47.3%).
- The Villa has the highest RevPAR of any room type (€197.2, ADR €310.9, 63.6% occupancy). The City Hotel's suites earn a high ADR (€239.6) but sell the fewest nights (40.8% occupancy).

## KPIs and formulas

| KPI | Formula |
|---|---|
| Occupancy % | Room nights sold / room nights available x 100 |
| ADR | Room revenue / paid room nights (complimentary stays excluded) |
| RevPAR | Room revenue / room nights available |
| Room type performance | Occupancy, ADR and RevPAR on each room type's own rooms and nights |
| Booking pace | Share of room nights booked at least N days before arrival |
| Pickup | Share of room nights booked within each window before arrival |
| Segment and channel analysis | Nights share, ADR, cancellation rate, median lead time and ancillary share |
| TRevPAR | Total revenue (all departments) / room nights available |
| GOPPAR | Gross operating profit / room nights available |
| Revenue mix and departmental profit | Department revenue and profit as a share of the total |

## Method in brief

1. **Stayed bookings only.** Cancelled bookings are removed from revenue and room nights, but kept to calculate cancellation rates.
2. **Stay-night expansion.** Each stay is expanded into one record per night, so revenue and occupancy fall in the month in which they are earned. Nights after 31 December 2025 are dropped.
3. **Even spreading.** Each stay's revenue by department is spread evenly across its nights.
4. **Pace and pickup** use lead time (arrival date minus booking date) and are weighted by length of stay.
5. **Cost model.** The dataset has no cost data, so GOPPAR and departmental profit use illustrative margins: Rooms 72%, Food & Beverage 30%, Spa 35%, Meetings & Events 45%, Other 50%, with undistributed expenses at 30% of total revenue.

## Notebook walkthrough

| Step | Analysis | Chart saved |
|---|---|---|
| 1 and 2 | Setup, stay-night expansion, rooms KPIs (occupancy, ADR, RevPAR, room revenue) | `Occupancy_by_Month.png` |
| 3 | Room type performance | `Room_Type_Performance.png` |
| 4 | Booking pace | `Booking_Pace.png` |
| 5 | Pickup by booking window | `Pickup_Windows.png` |
| 6 | Market segment analysis | `Segment_Cancellations.png` |
| 7 | Channel analysis | `Channel_Cancellations.png` |
| 8 | Total hotel KPIs (TRevPAR, GOPPAR) | `Total_Hotel_KPIs.png` |
| 9 | Revenue mix and departmental profit contribution | `Revenue_Profit_Mix.png` |

The report and dashboard also cover F&B and spa revenue per guest, ancillary contribution and meetings and events revenue, which are not calculated in the notebook.

## Getting started

```bash
git clone <repository-url>
cd <repository-folder>
pip install pandas numpy matplotlib seaborn jupyter
jupyter notebook
```

1. Open the notebook.
2. In the first code cell, set `file_path` to the location of the dataset, for example `file_path = "Hotel_Dataset_2025.csv"` if the CSV is in the same folder.
3. Run the cells in order from top to bottom. The results print in each cell and the charts are saved in the working folder.

## Dataset

`Hotel_Dataset_2025.csv` is a synthetic reservation-level dataset with 15,500 bookings (24.4% cancelled), a City Hotel with 60 rooms and a Resort Hotel with 66 rooms. It models seasonal demand, weekday patterns, trade fair and holiday periods, group blocks and cancellations. Each row is one room booking, and `Date` is the arrival date. Columns cover booking and stay dates, hotel and room type, channel, market segment, rate plan, lead time, length of stay, ADR, guests, revenue by department (rooms, restaurant, bar, spa, meetings and events, other) and cancellation status. See the data dictionary for all 36 columns.

## Report and dashboard

Open the PowerPoint files in **Slide Show mode (F5)**.

- **Report:** a clickable contents page, Back and Next buttons on every slide, and a KPI definitions slide that links to each KPI.
- **Dashboard:** a left menu for nine pages (Overview, Rooms KPIs, Room Types, Pace and Pickup, Segments, Channels, Total Hotel KPIs, F&B Spa and Events, Profitability) and three buttons at the top right to switch between All hotels, City Hotel and Resort Hotel. Hover over a chart to see its values.

The PDF versions keep the clickable links in most PDF viewers but are not editable. Google Slides and Keynote may not keep all links from the PowerPoint files.

## Assumptions and limitations

- The data is synthetic. The results teach the method and are not market benchmarks.
- GOPPAR, GOP margin and departmental profit rest on illustrative margins, not recorded costs. Replace them with actual departmental costs before using them for decisions.
- Stays that began in December 2024 are not in the file, so early-January occupancy is slightly understated.
- Competitive set indices (occupancy, ADR and RevPAR indices) are not calculated, because the dataset has no competitor data.
- Pace curves and pickup windows are annual averages. A real analysis would build them by season, weekday and segment.

## Tools

Python, pandas, NumPy, Matplotlib, Seaborn, Jupyter Notebook, PowerPoint.

## Author and rights

Produced by **Hosea Ngo Sali**. All rights reserved. This work is not to be duplicated or redistributed.
