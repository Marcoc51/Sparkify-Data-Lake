# Sparkify Data Warehouse

## Purpose
This database is designed to support the analytical goals of Sparkify, a startup in the music streaming industry. The database will store user activity data, such as songs played and user information, and enable analysts to query and derive insights from the data.

## Schema Design and ELT Pipeline
The database uses a star schema design, with a central fact table containing user activity data and multiple dimension tables that provide context for the activities. The ELT pipeline loads data from JSON files into staging tables, transforms the data using SQL queries, and then loads the data into the fact and dimension tables.

### Fact Table
- **songplays** - records in log data associated with song plays i.e. records with page NextSong
    - *songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent*

### Dimension Tables
- **users** - users in the app
    - *user_id, first_name, last_name, gender, level*
- **songs** - songs in music database
    - *song_id, title, artist_id, year, duration*
- **artists** - artists in music database
    - *artist_id, name, location, latitude, longitude*
- **time** - timestamps of records in songplays broken down into specific units
    - *start_time, hour, day, week, month, year, weekday*

### ETL Pipeline
1. Load data from JSON files into staging tables using COPY command.
2. Transform data in the staging tables using SQL queries.
3. Load data into fact and dimension tables using INSERT command.

## Usage
To create the database and tables, run `create_tables.py`. To load data into the tables, run `etl.py`.
