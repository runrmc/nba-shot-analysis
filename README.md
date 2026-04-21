# NBA Shot Analysis: The Evolution of Modern Basketball

An interactive data visualization project exploring how NBA shot selection has changed over 14 seasons (2011–2025), using shot-by-shot data from the top 25 scorers (by points per game) each year.

**→ [View the live project page](https://runrmc.github.io/projects/nba-shot-analysis.html)**

---

## Overview

This project analyzes 828,368 shot attempts to answer a single question: *how has NBA shot selection evolved, and which shooting zones are actually efficient?*

Four complementary interactive visualizations — each chosen for a specific analytical purpose — let you explore the data by player and season:

| Visualization | Purpose |
|---|---|
| Scatter Plot | Spatial shot distribution across the half-court |
| Efficiency Histogram | Points per attempt by distance zone |
| Line Chart | Three-point vs. two-point split over time |
| Stacked Bar Chart | Total scoring output by shot type per season |

The dashboard is built with [Plotly](https://plotly.com/python/) and `ipywidgets`, with a shared player and season filter that updates all charts simultaneously.

---

## Key Findings

- **The mid-range shot is quantifiably inefficient.** Shots from 10–16 feet yield the lowest points per attempt of any zone — below both rim attempts and three-pointers — across nearly every player and season in the dataset.
- **The three-point revolution is real and measurable.** Three-point attempts as a share of total shots rose steadily across all 14 seasons, with the sharpest increases in the mid-2010s.
- **Player shot profiles are spatially distinct.** Filtering the scatter plot to individual players reveals strikingly different spatial signatures — some dominated by rim attempts, others with dense three-point clusters and nearly empty mid-range zones.

---

## Dataset

The dataset contains shot-by-shot records scraped from the NBA Stats API, filtered to the top 25 players by points per game in each season from 2011–12 through 2024–25.

Each record includes:
- Court coordinates (`LOC_X`, `LOC_Y`) and shot distance
- Shot type (2PT or 3PT) and outcome (made or missed)
- Player, team, season, game date, quarter, and time remaining

**Note:** The raw CSV (~828K rows, ~150MB) is not included in this repository due to size. To reproduce the analysis, collect shot chart data from the [NBA Stats API](https://www.nba.com/stats) using [`nba_api`](https://github.com/swar/nba_api) for the players and seasons of interest, then combine into a single file matching the column schema in the notebook.

---

## Project Structure

```
nba-shot-analysis/
├── README.md
├── requirements.txt
├── notebooks/
│   └── nba_shot_analysis.ipynb   # Data cleaning + full dashboard
├── data/
│   └── README.md                 # Dataset schema and collection notes
└── exports/
    ├── scatter_plot.html         # Interactive Plotly exports
    ├── histogram.html
    ├── line_chart.html
    └── stacked_bar.html
```

---

## Setup

**Requirements:** Python 3.9+

```bash
git clone https://github.com/runrmc/nba-shot-analysis.git
cd nba-shot-analysis
pip install -r requirements.txt
```

Add your CSV to the project root (named `top_50_combined_shot_charts.csv`), then open the notebook:

```bash
jupyter notebook notebooks/nba_shot_analysis.ipynb
```

To export interactive charts after running the notebook:

```python
fig.write_html("exports/scatter_plot.html", include_plotlyjs="cdn")
```

---

## Tools & Libraries

- **[Plotly](https://plotly.com/python/)** — interactive visualization (scatter, bar, histogram, line)
- **[ipywidgets](https://ipywidgets.readthedocs.io/)** — dropdown and slider controls
- **[pandas](https://pandas.pydata.org/)** — data cleaning and aggregation
- **[NumPy](https://numpy.org/)** — numerical operations

---

## About

This project was completed as part of **SIADS 521: Visual Exploration of Data** at the University of Michigan School of Information (MS in Applied Data Science, AI concentration).

[runrmc.github.io](https://runrmc.github.io) · [LinkedIn](https://linkedin.com/in/ryanmccurry)
