# Dataset Notes

The raw CSV used in this project is not included in this repository due to file size (~150MB, 828K rows).

## Schema

The notebook expects a CSV named `top_50_combined_shot_charts.csv` in the project root with the following columns:

| Column | Type | Description |
|---|---|---|
| `GAME_DATE` | int | Game date in `YYYYMMDD` format |
| `season` | str | NBA season label (e.g. `2023-24`) |
| `PLAYER_NAME` | str | Player full name |
| `PERIOD` | int | Quarter (1–4, or OT) |
| `MINUTES_REMAINING` | int | Minutes remaining in the period |
| `SHOT_TYPE` | str | `2PT Field Goal` or `3PT Field Goal` |
| `EVENT_TYPE` | str | `Made Shot` or `Missed Shot` |
| `SHOT_DISTANCE` | int | Distance from basket in feet |
| `LOC_X` | float | Court x-coordinate (tenths of a foot from basket) |
| `LOC_Y` | float | Court y-coordinate (tenths of a foot from baseline) |

## Collecting the Data

Shot chart data can be collected using the [`nba_api`](https://github.com/swar/nba_api) Python library:

```python
from nba_api.stats.endpoints import shotchartdetail

shot_data = shotchartdetail.ShotChartDetail(
    team_id=0,
    player_id=player_id,
    season_nullable=season,
    season_type_all_star="Regular Season",
    context_measure_simple="FGA"
)

df = shot_data.get_data_frames()[0]
```

Repeat for each player and season of interest, then concatenate into a single DataFrame and export to CSV.
