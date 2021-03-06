# Project: Spark and Data Lake
This project builds an **ETL pipeline** for a **data lake**. The data resides in S3, in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in the app. We loaded data from S3, process the data into analytics tables using **Spark**, and load them back into S3.

## Introduction
A music streaming startup, Sparkify, has grown their user base and song database even more and want to move their data warehouse to a data lake. Their data resides in S3, in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

As their data engineer, you are tasked with building an ETL pipeline that extracts their data from S3, processes them using Spark, and loads the data back into S3 as a set of dimensional tables. This will allow their analytics team to continue finding insights in what songs their users are listening to.

You'll be able to test your database and ETL pipeline by running queries given to you by the analytics team from Sparkify and compare your results with their expected results.

## Project Description
In this project, you'll apply what you've learned on Spark and data lakes to build an ETL pipeline for a data lake hosted on S3. To complete the project, you will need to load data from S3, process the data into analytics tables using Spark, and load them back into S3. You'll deploy this Spark process on a cluster using AWS.


## Project Structure

```
Spark and Data Lake
|____etl.py              # ETL builder
|____dl.cfg              # AWS configuration file
|____test.ipynb          # testing
```

## How to Run
1. Add AWS credentials and S3 target bucket endpoint in dl.cfg

   **Please do not put your access/secret key in public**

	```
	[AWS]
	AWS_ACCESS_KEY_ID = [your access key]
	AWS_SECRET_ACCESS_KEY = [your secret key]
	
	[S3]
	SOURCE_S3_BUCKET = s3a://udacity-dend/
	DEST_S3_BUCKET = [your S3 endpoint]
	```

2. In the terminal, install pyspark and run etl.py python script

	```
	pip install pyspark
	python3 etl.py
	```
3. Test and check the results by directly running test.ipynb jupyter notebook

## ELT Pipeline
### etl.py
ELT pipeline builder

1. `process_song_data`
	* Load raw data from S3 buckets to Spark stonealone server and process song dataset to insert record into _songs_ and _artists_ dimension table

2. `process_log_data`
	* Load raw data from S3 buckets to Spark stonealone server and Process event(log) dataset to insert record into _time_ and _users_ dimensio table and _songplays_ fact table


## Database Schema

![Fig.1](img/Song_ERD.png)

### Fact table

#### songplays table

|  songplays  |    type   |
|-------------|-----------|
| songplay_id | INT       |
| start_time  | TIMESTAMP |
| user_id     | INT       |
| level       | VARCHAR   |
| song_id     | VARCHAR   |
| artist_id   | VARCHAR   |
| session_id  | INT       |
| location    | TEXT      |
| user_agent  | TEXT      |


### Dimension tables

#### user table

|    users   |   type  |
|------------|---------|
| user_id    | INT     |
| first_name | VARCHAR |
| last_name  | VARCHAR |
| gender     | CHAR(1) |
| level      | VARCHAR |

#### songs table

|   songs   |   type  |
|-----------|---------|
| song_id   | VARCHAR |
| title     | VARCHAR |
| artist_id | VARCHAR |
| year      | INT     |
| duration  | FLOAT   |

#### artists table

|   artists  |   type  |
|------------|---------|
| artist_id  | VARCHAR |
| name       | VARCHAR |
| location   | TEXT    |
| latitude   | FLOAT   |
| logitude   | FLOAT   |

#### time table

|    time    |    type   |
|------------|-----------|
| start_time | TIMESTAMP |
| hour       | INT       |
| day        | INT       |
| week       | INT       |
| month      | INT       |
| year       | INT       |
| weekday    | VARCHAR   |