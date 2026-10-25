# Smart Transit Load Balancing and Route Optimization Using Big Data

This project estimates how crowded Hyderabad's TGSRTC bus trips are at each stop. It uses the official timetable with Apache Spark, and stores and queries the results in Google BigQuery.

## Live dashboard
[Paste your Looker Studio share link here]

## Report
The full project report is in [Transit_Load.pdf](Transit_Load.pdf).

## What is real and what is estimated
- **Real:** the TGSRTC bus timetable (stops, routes, trips and stop times), from the Mobility Database.
- **Estimated:** passenger boardings and alightings, from a documented rule with a time-of-day factor. GTFS does not include passenger counts, so loads show the method, not measured crowding.

## Data source
- TGSRTC bus GTFS feed: https://mobilitydatabase.org/feeds/mdb-3361
- Licence and terms: https://hmrl.co.in/open-data.html (check before any public reuse)

## Tools
- Apache Spark 4.0.4 (PySpark) for processing
- Google Colab for development
- Google BigQuery for storage and SQL queries
- Looker Studio for the live dashboard
- Matplotlib for figures

## Repository contents
- `hyderabad_transit_load.ipynb`: final analysis notebook (GTFS loading, load estimation, hourly summary, figures, BigQuery upload)
- `transit_load_pbl.ipynb`: earlier sample notebook with synthetic data, used to test the method
- `hyderabad_hour_summary.csv`, `route_hour_summary.csv`, `stop_load_summary.csv`: summary tables used for BigQuery and the dashboard
- `figures/`: stop map and route-by-hour heatmap produced by the notebook
- `Transit_Load.pdf`: project report

## How to run
1. Open `hyderabad_transit_load.ipynb` in Google Colab.
2. Upload the five GTFS files (`stop_times.txt`, `trips.txt`, `routes.txt`, `stops.txt`, `calendar.txt`) to the Colab session, or keep them in Google Drive.
3. Run the cells in order, from the top.
4. The BigQuery cells need a Google account with access to the project.

## Results (Hyderabad timetable)
- 1,132,807 scheduled stop visits, 1,031 routes, 5,028 stops
- 108,074 overloaded visits (estimated, load factor above 0.85)
- Average estimated load factor: 0.235
- Scheduled visits peak in the evening. Estimated loads carry over through each trip, see limitations.

## Limitations
- Passenger loads are estimated, not measured.
- The boarding rule and time factors are assumptions, so the load pattern reflects them.
- Loads carry through each trip, which affects late-night hours.
- Bus capacity is a single value (60) for all buses.
- Colab sessions are temporary, so keep the input files in Google Drive.

## Future work
- Replace estimated boardings with real passenger counts
- Add GraphFrames analysis of the stop network
- Balance load by moving trips between routes
