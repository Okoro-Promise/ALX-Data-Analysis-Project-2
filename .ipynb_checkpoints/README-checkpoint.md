<font size="+3"><strong>Wrangle and Analyze Data</strong></font>

## Dataset(s)
Three different Datasets were used for this study

1. WeRateDogs Twitter archive (file on hand, manual download of 'twitter-archive-enhanced.csv').

2. The tweet image predictions ('image_predictions.tsv'). This file was be downloaded programmatically using the Requests library from a provided URL.

3. Each tweet's entire set of JSON data (with at minimum tweet ID, retweet count, and favorite count) in a file called 'tweet_json.txt' were stored using Twitter API and Python's Tweepy library. Each tweet's JSON data was written to its own line.


## Summary of Wrangling

After data assessment, I went on to clean each DataFrame one after the other and the cleaning 
steps used are as followed

__df_api__

1. First created a copy of df_api called df_api_clean.
2. Dropped redundant columns i.e. columns with over 70% NAN values.
3. Next step to cleaning df_api_clean was dropping single cardinality variables that do not offer any information to us i.e. columns with only one value.
4. During assessment, found that the "id" column is duplicated in id_str so we drop id_str column and rename id to tweet_id.
5. Columns entities, user, and extended_entities contain data in other columns/tables and appear to be very noisy, so dropped them.
6. During Data Tidiness Assessment, found that column full_text contains the ratings and the tweet link alongside the tweet, extracted all three into different columns using Regular Expression and created a function extract_multi_cols in order to avoid repetition of this task.

__df_archive__
1. First created a copy of df_archive called df_archive_clean.
2. Again, the first step of cleaning df_api_clean was to drop redundant columns i.e columns with over 70% NAN values.
3. Convert column timestamp to a pandas Datetime object as observed during assessment.
4. Rename column text to full_text.
5. Use extract_multi_cols function to solve the same tidiness issues we saw while cleaning df_api.

__df_img_pred__
1. First, make a copy of df_img_pred called df_pred_clean.
2. Convert the dog breed names in columns p1, p2 and p3 to lowercase.

## Storing Data
Combine our three cleaned Dataframes and store it as a csv file twitter_archive_master.csv


## Questions for Analysis
1. What are the names of the top 10 dogs with the highest retweet count and their ratings?
2. What is the average Retweet counts by rating of the top ten dogs with the most retweets?
3. What is the Proportion of each dog rating in our Dataset and which rating appeared more frequently?


## Summary of Findings
I found that tweets with dogs named **Stephan, Duddles, Bo, Jamesy, Kenneth, quite, Buddy, Zoey** and **Sunny** were retweeted the most in that order.

I saw that the dogs rated **13** and **10** recorded the highest average retweet count whilst **14** had the lowest average rating among the dogs named above.

I found that in the Entire dataset, only one dog received a **15** rating, and well over 471 dogs recieved **12** rating, With **471** Dogs rated as 12 that represents about **29%** of the dogs in our Dataset


### NB
The Wrangling and Exploration of the datasets in this project does not clean all noise in the datasets as that was beyond the scope of study as at the time of this project.
