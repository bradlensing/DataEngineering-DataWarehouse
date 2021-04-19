# Create an AWS Redshift Data Warehouse

## Project Summary

### Introduction

A music streaming startup, Sparkify, has grown their user base and song database and want to move their processes and data onto the cloud. Their data resides in S3, in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

### Description

You will load data from S3 to staging tables on Redshift and execute SQL statements that create the analytics tables from these staging tables.

## Data

You'll be working with two datasets that reside in S3. Here are the S3 links for each.

### Song data

Song data: s3://udacity-dend/song_data

- For example, here are filepaths to two files in this dataset.

  - `{song_data/A/A/A/TRAAAAW128F429D538.json}`
  - `{song_data/A/B/B/TRABBAM128F429D223.json}`

- This is an example of what a single song file, TRAABJL12903CDCF1A.json, looks like.
  ```json
  {
  	"num_songs": 1,
  	"artist_id": "ARJIE2Y1187B994AB7",
  	"artist_latitude": null,
  	"artist_longitude": null,
  	"artist_location": "",
  	"artist_name": "Line Renaud",
  	"song_id": "SOUPIRU12A6D4FA1E1",
  	"title": "Der Kleine Dompfaff",
  	"duration": 152.92036,
  	"year": 0
  }
  ```

### Log data

Log data: s3://udacity-dend/log_data

- For example, here are filepaths to two files in this dataset.

  - `{log_data/2018/11/2018-11-12-events.json}`
  - `{log_data/2018/11/2018-11-13-events.json}`

### Schemas

Fact Table

1. songplays - records in event data associated with song plays i.e. records with page NextSong

   `songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent`

Dimension Tables

2. users - users in the app

   `user_id, first_name, last_name, gender, level `

3. songs - songs in music database

   `song_id, title, artist_id, year, duration`

4. artists - artists in music database

   ` artist_id, name, location, lattitude, longitude`

5. time - timestamps of records in songplays broken down into specific units

   `start_time, hour, day, week, month, year, weekday`

## How to Run

1. **Create a Redshift Cluster** either through the website or the [2.0-IaC_Redshift.ipynb](../2.0-IaC_Redshift.ipynb) from the Data Engineering Projects.

1. **Setup the configurations** with your specific information in the dwh.cfg file.

   - [CLUSTER]
     HOST=
     DB_NAME=
     DB_USER=
     DB_PASSWORD=
     DB_PORT=

     [IAM_ROLE]
     ARN=''

     [S3]
     LOG_DATA='s3://udacity-dend/log_data'
     LOG_JSONPATH='s3://udacity-dend/log_json_path.json'
     SONG_DATA='s3://udacity-dend/song_data'

1. #### Create tables

   `$ python create_tables.py `

1. #### Load the data
   `$ python etl.py`
