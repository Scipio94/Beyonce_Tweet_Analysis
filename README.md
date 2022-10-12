# **Beyonce Twitter Dataset Analysis**


## **Abstract**
The analysis seeks to analyze the sentiment of fans towards the tracks of Beyonce’s album released July 2022 using twitter user data collected between August and September 2022.

## **Introduction**

The goal of this analysis is to analyze fan sentiment of Beyonce’s latest album, Renaissance, via twitter user data. There are several variables within the dataset that will have a significant impact on the outcome:

- **Date**: yyyy-mm-dd hh:mm:ss
- **Verified**: A method to distinguish regular users from distinguished users, e.g. celebrities, professional athletes, notable public figures, etc. 
- **Retweets**: The reposting of a tweet by a twitter user.
- **Replies**: A response to a tweet.
- **Like**: An indication that a tweet is well like by an individual twitter user.
- **Quote**: An action that allows a user to tweet another person’s tweet and add your own comment.
- **Language**: Language of the original tweet when it was published.
- **Media**: Media used in twitter interactions about a track on Renaissance.
- **Sentiment**: Twitter user sentiment toward tracks of Renaissance. 
- **Sentiment Score**: Numerical representation of twitter sentiment calculated via machine learning.

## **Objective**

Based on the data collected what was the overall sentiment of the Renaissance album among twitter users. The analysis will be guided by the following questions:

1. Which track was referenced the most times?
2. Which track was referenced the most times positively?
3. Which track was referenced the most times from verified accounts?



## **Analysis**

1. ***Which track was referenced the most time?***

~~~ SQL 
SELECT COUNT(*) as Track_Search_Tweet_Total
FROM `my-data-project-36654.Beyonce_Track_Tweets.Track_Tweet_Sentiment`
--Tweet Total
~~~ 

### **Result**
|Track Search Tweet Total|
|---|
|81,922|

~~~ SQL
SELECT 
  TrackSearched, COUNT(TrackSearched) as Track_Count,ROUND(COUNT(TrackSearched)/81922.00 * 100,1) as Track_Count_Percentage ,
  RANK() OVER (ORDER BY COUNT(TrackSearched) DESC ) as Track_Count_Rank
FROM `my-data-project-36654.Beyonce_Track_Tweets.Track_Tweet_Sentiment`
GROUP BY 
  TrackSearched
ORDER BY 
  Track_Count DESC
LIMIT 3

--Total Tweets 81922
~~~

### Result

|TrackSearched|Track_Count|Track_Count_Percentage|Rank|
|---|---|---|---|
|Move|5776|7.1%|1|
|All Up In Your Mind|5683|6.9%|2|
|America Has A Problem|5601|6.8%|3|

2. ***Which track was referenced the most times positively?***

~~~ SQL
SELECT  
  COUNT(*) as Positive_Tweet_Total
FROM `my-data-project-36654.Beyonce_Track_Tweets.Track_Tweet_Sentiment` 
WHERE 
  Sentiment = 'Positive'

--Total Positive Tweets
~~~
### **Result**

|Positive Tweet Total|
|---|
|17427|


~~~ SQL

SELECT  
  TrackSearched, COUNT(TrackSearched) as Track_Count, ROUND(COUNT(TrackSearched)/17427.00 * 100,1) as Track_Count_Percentage,
  Sentiment,ROUND(AVG(Score),3) as Avg_Score ,
  RANK () OVER (ORDER BY COUNT(TrackSearched) DESC ) as Rank
FROM `my-data-project-36654.Beyonce_Track_Tweets.Track_Tweet_Sentiment` 
WHERE 
  Sentiment = 'Positive'
GROUP BY 
  TrackSearched, Sentiment
ORDER BY 
    Track_Count DESC
LIMIT 3

  --Total Positive Tweets 17427
 ~~~
 
 ### **Result**
|TrackSearched|Track_Count|Track_Count_Percentage|Sentiment|Avg_Score|Rank|
|---|---|---|---|---|---|
|Cozy|1518|8.7%|Positive|0.792|1|
|Virgo's Groove|1445|8.3%|Positive|0.825|2|
|Heated|1407|8.1%|Positive|0.791|3|


3. ***Which track was referenced the most times from verified accounts?***

~~~SQL
SELECT 
  COUNT(*) as Verified_Account_Total
FROM `my-data-project-36654.Beyonce_Track_Tweets.Track_Tweet_Sentiment` 
WHERE 
  Verified IS true
-- Verified Accounts Total
~~~

### **Results**

|Verified_Account_Total|
|---|
|1247|

~~~ SQL
SELECT 
  TrackSearched, COUNT(TrackSearched) as Track_Count,ROUND(COUNT(TrackSearched)/ 1247.00 * 100,1) as Track_Count_Percentage,
  RANK() OVER (ORDER BY COUNT(TrackSearched) DESC ) as Rank 
 FROM `my-data-project-36654.Beyonce_Track_Tweets.Track_Tweet_Sentiment`
 WHERE 
  Verified IS true
 GROUP BY 
  TrackSearched
ORDER BY 
  Track_Count DESC

LIMIT 3

--Verified is a BOOLEAN data type 'True' indicates that an account is verified
--Total Tweet 1247
~~~~

### **Result**

|TrackSearched|Track_Count|Track_Count_Percentage|Rank|
|---|---|---|---|
|Break My Soul|181|14.5%|1|
|Alien Superstar|99|7.9%|2|
|I'm That Girl|97|7.8%|3|





