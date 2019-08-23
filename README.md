# ETL Project Report

## EXTRACT:
* Our original data source was from https://www.kaggle.com/datasnaek/youtube-new By Mitchell J. There are two forms of data, .json and CSV. We took 6 files in total, 1 json, 1 csv for 3 countries; Canada, Great Britain, and United States. We uploaded all of the files into Pandas.


## TRANSFORM:
JSON:
* Cleaned up CA, US, GB dataframe with json_normalize (pulls dictionary items into their own columns).
* Drop static YouTube info not needed for video database ('etag', 'kind', 'snippet.assignable', 'snippet.channelId').
* Renameed columns - 'id': 'category_id', 'snippet.title': 'category_name'
* Cast category_id to number for merging with csv dataframes
CSV:
* Added a column to each country's df to define which country info in the final df.
* Merge category_names from respective .json files into each country's df
* Groupby video_id, pull most recent date for each video and assign that value to a new 'MaxDate' column.
* Pull only the most recent 'trending_date' for each video_id into a new df.
* Filled empty ‘descriptions’ in the dataset with "No description provided." to fill all NaN values in that series.
* Filled NaN in 'category_name' where 'category_id' was 29 with the proper category name. This only filled for US and left 55 NaN values between CA and GB.
* Changed format for date in ‘publish_time’ to match ‘trending_date’.
* Dropped ‘thumbnail_link', ‘ratings_disabled', 'video_error_or_removed', 'publish_time', 'MaxDate' from final table before push.
* Reorganize columns to 'video_id', 'title'video_id', 'title', 'channel_title', 'views', 'likes', 'dislikes',                         'comments_disabled', 'comment_count', 'description', 'tags', 'category_id', 'category_name', 'publish_date', 'trending_date', 'country'.


## LOAD:
* Used pandas to_sql method, to transform into SQL.
* Pushed from notebook with connection to pgAdmin.


<br><br><br><br>




# Guidelines for ETL Project

This document contains guidelines, requirements, and suggestions for Project 1.

## Team Effort

Due to the short timeline, teamwork will be crucial to the success of this project! Work closely with your team through all phases of the project to ensure that there are no surprises at the end of the week.

Working in a group enables you to tackle more difficult problems than you'd be able to working alone. In other words, working in a group allows you to **work smart** and **dream big**. Take advantage of it!

## Project Proposal

Before you start writing any code, remember that you only have one week to complete this project. View this project as a typical assignment from work. Imagine a bunch of data came in and you and your team are tasked with migrating it to a production data base.

Take advantage of your Instructor and TA support during office hours and class project work time. They are a valuable resource and can help you stay on track.

## Finding Data

Your project must use 2 or more sources of data. We recommend the following sites to use as sources of data:

* [data.world](https://data.world/)

* [Kaggle](https://www.kaggle.com/)

You can also use APIs or data scraped from the web. However, get approval from your instructor first. Again, there is only a week to complete this!

## Data Cleanup & Analysis

Once you have identified your datasets, perform ETL on the data. Make sure to plan and document the following:

* The sources of data that you will extract from.

* The type of transformation needed for this data (cleaning, joining, filtering, aggregating, etc).

* The type of final production database to load the data into (relational or non-relational).

* The final tables or collections that will be used in the production database.

You will be required to submit a final technical report with the above information and steps required to reproduce your ETL process.

## Project Report

At the end of the week, your team will submit a Final Report that describes the following:

* **E**xtract: your original data sources and how the data was formatted (CSV, JSON, pgAdmin 4, etc).

* **T**ransform: what data cleaning or transformation was required.

* **L**oad: the final database, tables/collections, and why this was chosen.

Please upload the report to Github and submit a link to Bootcampspot.

- - -

### Copyright

Coding Boot Camp © 2019. All Rights Reserved.
