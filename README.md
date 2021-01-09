PROJECT INTRODUCTION

Sparkify, has grown their user base and song database and want to move their processes and data onto the cloud. Their data resides in S3, in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

Task is to build an ETL Pipeline that extracts their data from S3, staging it in Redshift and then transforming data into a set of Dimensional and Fact Tables for their Analytics Team to continue finding Insights to what songs their users are listening to.

PROJECT DESCRIPTION

Application of Data warehouse and AWS to build an ETL Pipeline for a database hosted on Redshift Will need to load data from S3 to staging tables on Redshift and execute SQL Statements that create fact and dimension tables from these staging tables to create analytics

PROJECT DATASETS

1. Song Data Path     -->     s3://udacity-dend/song_data
2. Log Data Path      -->     s3://udacity-dend/log_data
3. Log Data JSON Path -->     s3://udacity-dend/log_json_path.json

SONG DATASET

The first dataset is a subset of real data from the Million Song Dataset. Each file is in JSON format and contains metadata about a song and the artist of that song. The files are partitioned by the first three letters of each song's track ID. For example:

song_data/A/B/C/TRABCEI128F424C983.json
song_data/A/A/B/TRAABJL12903CDCF1A.json

And below is an example of what a single song file, TRAABJL12903CDCF1A.json, looks like.

{"num_songs": 1, "artist_id": "ARJIE2Y1187B994AB7", "artist_latitude": null, "artist_longitude": null, "artist_location": "", "artist_name": "Line Renaud", "song_id": "SOUPIRU12A6D4FA1E1", "title": "Der Kleine Dompfaff", "duration": 152.92036, "year": 0}

LOG DATASET

The second dataset consists of log files in JSON format. The log files in the dataset with are partitioned by year and month.
For example:

log_data/2018/11/2018-11-12-events.json
log_data/2018/11/2018-11-13-events.json

And below is an example of what a single log file, 2018-11-13-events.json, looks like.

{"artist":"Pavement", "auth":"Logged In", "firstName":"Sylvie", "gender", "F", "itemInSession":0, "lastName":"Cruz", "length":99.16036, "level":"free", "location":"Klamath Falls, OR", "method":"PUT", "page":"NextSong", "registration":"1.541078e+12", "sessionId":345, "song":"Mercy:The Laundromat", "status":200, "ts":1541990258796, "userAgent":"Mozilla/5.0(Macintosh; Intel Mac OS X 10_9_4...)", "userId":10}

SCHEMA FOR SONG PLAY ANALYSIS

A Star Schema would be required for optimized queries on song play queries

FACT TABLE

songplays - records in event data associated with song plays i.e. records with page NextSong
songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent

DIMENSION TABLES

Dimension Table 1:
users - users in the app
user_id, first_name, last_name, gender, level

Dimension Table 2:
songs - songs in music database
song_id, title, artist_id, year, duration

Dimension Table 3:
artists - artists in music database
artist_id, name, location, lattitude, longitude

Dimension Table 4:
time - timestamps of records in songplays broken down into specific units
start_time, hour, day, week, month, year, weekday

PROJECT TEMPLATE

Project Template include four files:

1. create_tables.py is where you'll create your fact and dimension tables for the star schema in Redshift.

2. etl.py is where you'll load data from S3 into staging tables on Redshift and then process that data into your analytics tables on Redshift.

3. sql_queries.py is where you'll define you SQL statements, which will be imported into the two other files above.

4. README.md is where you'll provide discussion on your process and decisions for this ETL pipeline.

Creating Table Schema

1. Write a SQL CREATE statement for each of these tables in sql_queries.py
2. Complete the logic in create_tables.py to connect to the database and create these tables
3. Write SQL DROP statements to drop tables in the beginning of create_tables.py if the tables already exist. This way, you can run create_tables.py whenever you want to reset your database and test your ETL pipeline.
4. Launch a redshift cluster and create an IAM role that has read access to S3.
5. Add redshift database and IAM role info to dwh.cfg.
6. Test by running create_tables.py and checking the table schemas in your redshift database.

Building ETL Pipeline

1. Implement the logic in etl.py to load data from S3 to staging tables on Redshift.
2. Implement the logic in etl.py to load data from staging tables to analytics tables on Redshift.
3. Test by running etl.py after running create_tables.py and running the analytic queries on your Redshift database to compare your results with the expected results.
4. Delete your redshift cluster when finished.

FINAL INSTRUCTIONS

1. Import all the necessary libraries
2. Write the configuration of AWS Cluster, store the important parameter in some other file
3. Configuration of boto3 which is an AWS SDK for Python
4. Using the bucket, can check whether files log files and song data files are present
5. Create an IAM User Role, Assign appropriate permissions and create the Redshift Cluster
6. Get the Value of Endpoint and Role for put into main configuration file
7. Authorize Security Access Group to Default TCP/IP Address
8. Launch database connectivity configuration
9. Go to Terminal write the command "python create_tables.py" and then "etl.py"
10. Should take around 7-14 minutes in total
11. Then you go back to jupyter notebook to test everything is working fine
12. I counted all the records in my tables
13. Now can delete the cluster, roles and assigned permission