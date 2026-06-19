# Gridlock Hackathon - Flipkart x BTP

Identifying illegal parking hotspots and quantifying their congestion impact
using real BTP enforcement data, to enable targeted patrol deployment.

Built for BTP x Flipkart Traffic Hackathon - Round 2 (June 2026)


## The Problem

Bengaluru traffic enforcement is entirely reactive. Officers patrol fixed routes
with no visibility into where illegal parking is actually choking the city.
The result - high-impact zones go unattended while low-impact areas get patrolled.


## What This Does

- Clusters 248,376 confirmed parking violations using DBSCAN (eps=75m)
- Scores each zone 0-100 based on severity, vehicle type, peak-hour share, and persistence
- Produces a ranked enforcement priority list with patrol windows per zone
- Visualizes all hotspots on an interactive Bengaluru map

## Key Results

- 325 hotspot clusters identified across Bengaluru
- Top 10 zones (3% of clusters) account for 38% of total violation volume
- Top 10 zones show 54.4% peak-hour concentration vs 46.8% baseline (16.2% lift)
- KR Market Junction - impact score 92.2/100, 49,795 violations over 152 days
- Safina Plaza Junction - impact score 53.1/100, 72.7% peak-hour share
  

## Hotspot Map

![Bengaluru Parking Hotspot Map](assets/bengaluru_hotspot_map.png)

Red = Score 50+ | Orange = Score 30-50 | Blue = Score below 30
Circle size = violation volume


## How to Run

1. Clone the repo

   Link -

2. Install dependencies
  pip install -r requirements.txt

3. Download the dataset

Get the dataset from the HackerEarth portal and place it in the root folder as:
`jan_to_may_police_violation_anonymized791b166.csv`

4. Run the notebook

Open `notebook/Round2FlipKartGridlock_Hackathon.ipynb` in Jupyter or Google Colab
and run all cells top to bottom.


## Output Files

| File | Description |

| outputs/enforcement_priority.csv | Top 15 zones ranked by impact score with patrol windows |
| outputs/hotspots_full.csv | All 325 clusters with scores and coordinates |
| outputs/heatmap.html | Interactive Folium map - open in any browser |


## Impact Score Formula

Each cluster is scored as:

- 0.40 x severity-weighted volume
- 0.30 x raw violation count
- 0.15 x peak-hour share (08:00-13:00 IST)
- 0.15 x days active

Severity weights - double parking, parking near zebra cross = 2.0x
Vehicle weights - buses/LGVs = 2.0x, cars = 1.0x, two-wheelers = 0.5x


## How Enforcement Teams Use This

1. Open heatmap.html in a browser each morning
2. Filter by current shift window to see active priority zones
3. Dispatch patrol to top-ranked zones matching that time window
4. enforcement_priority.csv can feed directly into scheduling systems
   

## Tech Stack

- Python, pandas, numpy
- scikit-learn (DBSCAN clustering)
- scipy (Pearson correlation)
- Folium + OpenStreetMap (interactive map)


## Dataset

Source - BTP enforcement records provided by HackerEarth
Period - November 2023 to April 2024
Size - 298,450 records, 24 columns
Note - Raw dataset not included due to size and licensing. Download from the hackathon portal.


## Author

Username - SOUL665
Profile Link - 
