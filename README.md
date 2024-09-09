
# Citi Bike Station Visualization Project

This project visualizes Citi Bike station data from New York City using Google BigQuery and BigQuery Geo Viz. The dataset contains information about Citi Bike stations, including their geographic locations and the number of bikes available at each station.

## Project Overview

The goal of this project is to:
1. Query Citi Bike stations with more than 30 bikes available.
2. Visualize the geographic locations of these stations on an interactive map using Google BigQuery Geo Viz.

## Data Source

The data comes from the public dataset `bigquery-public-data.new_york.citibike_stations`, which contains information about Citi Bike stations in New York City.

### Key Columns:
- `longitude`: The longitude of a station (in WGS 84 decimal degrees).
- `latitude`: The latitude of a station (in WGS 84 decimal degrees).
- `num_bikes_available`: The number of bikes available for rental at the station.

## Queries Used

### Query 1: Sample Data from the Table
This query retrieves a sample of 10 rows from the `citibike_stations` table to explore the structure of the dataset.

```sql
SELECT
  *
FROM
  `bigquery-public-data.new_york_citibike.citibike_stations`
LIMIT
  10;
```

### Query 2: Find Stations with More Than 30 Bikes Available
This query selects all Citi Bike stations that have more than 30 bikes available, using the `ST_GeogPoint` function to convert the latitude and longitude values into a geospatial format (WKT).

```sql
-- Finds Citi Bike stations with > 30 bikes
SELECT
  ST_GeogPoint(longitude, latitude)  AS WKT,
  num_bikes_available
FROM
  `bigquery-public-data.new_york_citibike.citibike_stations`
WHERE num_bikes_available > 30;
```

## Visualization in BigQuery Geo Viz

After querying the data, the results are visualized using **BigQuery Geo Viz**, a web-based tool for geospatial data visualization. The visualization highlights stations with more than 30 bikes available using circles on a map, where:
- The circle size is proportional to the number of bikes available at each station.
- The circle color and opacity are customized for clarity.

### Visualization Steps:
1. **Authorization**: Authenticate using your Qwiklabs username in Geo Viz.
2. **Run the Query**: Use the SQL query mentioned above to retrieve the stations with more than 30 bikes available.
3. **Processing Location**: Ensure the processing location is set to `United States (US)`.
4. **Customize the Map**:
   - **Color**: Set the `fillColor` to `#0000FF` (blue).
   - **Opacity**: Set the `fillOpacity` to `0.5` (semi-transparent).
   - **Circle Radius**: Set the circle size based on the number of bikes available using a linear function:
     - Domain: [30, 60]
     - Range: [20, 450]

### Final Result:
The visualization shows stations on the map as blue circles. The radius of each circle is proportional to the number of available bikes at each station. Larger circles represent stations with more bikes.

## Tools and Technologies Used
- **Google BigQuery**: For querying and analyzing the dataset.
- **Google BigQuery Geo Viz**: For visualizing the geospatial data.
- **SQL**: Used to query the dataset and convert latitude/longitude into geospatial points.

## How to Reproduce

1. Open the **BigQuery web UI** in the Google Cloud Console.
2. Run the queries provided in this README to analyze the data.
3. Open **BigQuery Geo Viz** and authenticate using your Google Cloud or Qwiklabs credentials.
4. Visualize the queried data on the map and apply the styling steps provided.

## Screenshots

![Geo Viz Screenshot](screenshot.png)

---

Feel free to modify this README with any additional details or screenshots relevant to your project.
