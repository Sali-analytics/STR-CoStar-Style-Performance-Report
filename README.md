# STR / CoStar Style Performance Report

A hotel performance analysis in Python that calculates the rooms and total hotel KPIs used in STR / CoStar style performance reporting (occupancy, ADR, RevPAR, TRevPAR and GOPPAR) and extends them with room type, booking pace, pickup, market segment, channel, revenue mix, F&B and spa, meetings and events, and departmental profitability analysis for a City Hotel and a Resort Hotel. The repository contains the Jupyter notebook, the dataset, an interactive report and an interactive dashboard.

> **Note:** This project is not affiliated with, endorsed by or based on data from STR or CoStar. "STR / CoStar style" refers to the standard industry KPI definitions and report layout. All data in this repository is synthetic.

## Repository contents

| File | Description |
|---|---|
| `_STR__CoStar_Style_Performance_Analyses.ipynb` | Analysis notebook with 12 sections that reproduce every KPI in the report and dashboard |
| `Hotel_Dataset_2025.csv` | Synthetic dataset: 15,500 reservations, 2 hotels, arrivals from 1 January to 31 December 2025 |
| `Hotel_Dataset_2025_Data_Dictionary.csv` | Description of all 36 columns in the dataset |
| `Hotel_KPI_Interactive_Report.pptx` / `.pdf` | 17-slide interactive report with clickable contents and Back / Next navigation |
| `Hotel_KPI_Dashboard.pptx` / `.pdf` | 30-slide interactive dashboard with page menu and All hotels / City Hotel / Resort Hotel buttons |
| `Hotel_KPI_Handbook.pdf` | Guide explaining how every KPI is calculated, why it matters and how to apply it |

## Headline results (2025)

| KPI | Portfolio (126 rooms) | City Hotel (60 rooms) | Resort Hotel (66 rooms) |
|---|---|---|---|
| Occupancy | 66.7% | 65.8% | 67.5% |
| ADR | €123.7 | €113.5 | €132.8 |
| RevPAR | €82.2 | €74.3 | €89.4 |
| Room revenue | €3.78M | €1.63M | €2.15M |
| TRevPAR | €128.3 | €101.2 | €153.0 |
| GOPPAR (illustrative cost model) | €36.3 | €33.0 | €39.3 |
| GOP margin (illustrative cost model) | 28.3% | 32.6% | 25.7% |
| Ancillary share of revenue | 35.9% | 26.5% | 41.6% |

**Key findings**

- The Resort Hotel earns more per available room (RevPAR €89.4 against €74.3), driven by a higher ADR (€132.8 against €113.5).
- The Resort earns far more outside the room: TRevPAR is €153.0 against €101.2, and rooms make up 58.4% of Resort revenue against 73.5% at the City Hotel.
- The Resort books earlier. At 60 days before arrival, 48.2% of Resort room nights are on the books against 30.2% at City. The City Hotel depends more on late pickup, with 24.2% of room nights booked in the final 7 days against 9.7% at the Resort.
- Online travel agencies cancel most often (37.8%), against 21.9% for the direct website and 14.2% for phone and email bookings.
- Leisure is the largest segment (49.6% of room nights, ADR €138). Group business has a lower ADR (€101) but the highest ancillary share of revenue (47.3%).
- The Villa has the highest RevPAR of any room type (€197, ADR €311, 63.6% occupancy). The City Hotel's suites earn a high ADR (€240) but sell the fewest nights (40.8% occupancy).
- Resort guests spend €27.6 on F&B per guest night against €13.9 at City, and 29.1% of Resort stays include spa spend against 7.8%. About half of Resort stays (49.8%) are on half-board or full-board plans, against 4.8% at City.
- Meetings and events bring €190k (3.2% of revenue), and Group bookings generate 80.8% of it.
- Rooms provide 79.2% of departmental profit under the illustrative cost model.

## Notebook sections

Each section prints its results table and displays its charts. The section numbers match the report and dashboard.

| Section | Analysis |
|---|---|
| 01 | Executive summary: headline KPIs, monthly occupancy, cancellation rates |
| 02 | Rooms KPIs: occupancy, ADR, RevPAR and room revenue by hotel and month |
| 03 | Room type performance |
| 04 | Booking pace by hotel and by market segment |
| 05 | Pickup by booking window and by arrival month |
| 06 | Market segment analysis |
| 07 | Channel analysis |
| 08 | Total hotel KPIs: TRevPAR and GOPPAR |
| 09 | Revenue mix and ancillary contribution |
| 10 | F&B and spa revenue per guest night, spa penetration, meal plans |
| 11 | Meetings and events revenue |
| 12 | Profitability by department and P&L summary |

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
| Revenue mix and ancillary contribution | Department revenue and non-room revenue as a share of total revenue |
| F&B and spa per guest night | (Restaurant + bar) or spa revenue / guest nights |
| Meetings and events revenue | Meeting and event revenue by hotel, month and segment |
| GOPPAR | Gross operating profit / room nights available |
| Departmental profit | Department revenue x assumed margin |

## Method in brief

1. **Stayed bookings only.** Cancelled bookings are removed from revenue and room nights, but kept to calculate cancellation rates. Of 15,500 bookings, 11,720 were stayed and 3,780 (24.4%) were cancelled.
2. **Stay-night expansion.** Each stay is expanded into one record per night, giving 30,677 stay-nights in 2025 (30,557 paid), so revenue and occupancy fall in the month in which they are earned. Nights after 31 December 2025 are dropped.
3. **Even spreading.** Each stay's revenue by department is spread evenly across its nights.
4. **Pace and pickup** use lead time (arrival date minus booking date) and are weighted by length of stay.
5. **Cost model.** The dataset has no cost data, so GOPPAR and departmental profit use illustrative margins: Rooms 72%, Food & Beverage 30%, Spa 35%, Meetings & Events 45%, Other 50%, with undistributed expenses at 30% of total revenue.

## Getting started

```bash
git clone <repository-url>
cd <repository-folder>
pip install pandas numpy matplotlib jupyter
jupyter notebook
```

1. Open the notebook.
2. In the first code cell, set `file_path` to the location of the dataset, for example `file_path = "Hotel_Dataset_2025.csv"` if the CSV is in the same folder.
3. Run the cells in order from top to bottom.

## Dataset

`Hotel_Dataset_2025.csv` is a synthetic reservation-level dataset with 15,500 bookings, a City Hotel with 60 rooms and a Resort Hotel with 66 rooms. It models seasonal demand, weekday patterns, trade fair and holiday periods, group blocks and cancellations. Each row is one room booking, and `Date` is the arrival date. Columns cover booking and stay dates, hotel and room type, channel, market segment, rate plan, lead time, length of stay, ADR, guests, revenue by department (rooms, restaurant, bar, spa, meetings and events, other) and cancellation status. See the data dictionary for all 36 columns.

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

Python, pandas, NumPy, Matplotlib, Jupyter Notebook, PowerPoint.

## Author and rights

Produced by **Hosea Ngo Sali**. All rights reserved. This work is not to be duplicated or redistributed.
