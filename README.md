# Sparkify Data Lake

## Purpose
The purpose of this database is to provide Sparkify with a data analytics tool that enables them to extract meaningful insights from their user and song data. With this database, Sparkify will be able to run queries on user listening patterns, most popular songs/artists, and other trends that will help them make better business decisions.

## Schema Design and ELT Pipeline
The database uses a star schema that is optimized for analytical queries. The schema consists of four tables:

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
    - *start_time, hour, day, week, month, year*

The schema design is based on the principle of data normalization. The data is separated into tables in such a way that each table is dedicated to a specific type of information. In addition, the schema uses surrogate keys in order to avoid data duplication and improve performance.

## ETL Pipeline
The ETL pipeline consists of two main functions that extract the data from AWS S3, transform it into a format suitable for the database, and load it into the appropriate tables.

### `process_song_data`
This function extracts song data from JSON files stored in AWS S3, transforms it into the appropriate format, and loads it into two tables: `songs` and `artists`. The songs table is partitioned by year and artist_id.

### `process_log_data`
This function extracts log data from JSON files stored in AWS S3, transforms it into the appropriate format, and loads it into three tables: users, time, and songplays. The time table is partitioned by year and month, and the songplays table is partitioned by year and month as well.

## Running the ETL Pipeline
To run the ETL pipeline, follow these steps:

Add AWS access and secret keys to the `dl.cfg` file.
Run the `etl.py` script using the command `python etl.py`.
