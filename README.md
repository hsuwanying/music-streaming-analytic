<p align = "center">
<img src = "https://user-images.githubusercontent.com/72688726/187309445-3085b23f-55d6-4212-bb72-5a5c6a506ad5.jpg">
</p>
<p align = "center"> Photo by
 <a href="https://unsplash.com/@sonance?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Viktor Forgac</a> on <a href="https://unsplash.com/photos/B88PgQXS4qg">Unsplash</a>
</p>

# Music Streaming Analytics: Improving user listenting experience with music listening history data analysis

Music streaming services allow people to access various types of music and millions of tracks with their smart devices and to customize playlists based on their preferences. These advanced features have made listening to music much easier than ever (Adiyansjan, Gunawan, & Suhartono, 2019). Neverthless, having an abundance of choices could delay users at making decisions and detering their motivation to stay with the services (Maasø & Hagen, 2020). Hence, businesses who wish to increase competitive advantages and enhance user stickiness towards digital products, it is essential to develop a recommender system, a mechanism that can automatically suggest media meeting user’s expectation (Hansen, et al., 2021). 

This project is submitted as part of assignemnt the Recommader System module for MSc in [IDS](https://www.hslu.ch/en/lucerne-school-of-business/degree-programmes/master/applied-information-and-data-science/) at [HSLU](https://www.hslu.ch/de-ch/)

# Author
[Carol Hsu](https://github.com/hsuwanying)

# Table of Content
 - [Initial Situation](https://github.com/hsuwanying/music-streaming-analytic/blob/main/README.md#initial-situation)
 - [Business Problem](https://github.com/hsuwanying/music-streaming-analytic/blob/main/README.md#business-problem)
 - [Solution](https://github.com/hsuwanying/music-streaming-analytic/blob/main/README.md#solution)
 - [Data Source](https://github.com/hsuwanying/music-streaming-analytic/blob/main/README.md#data-source)
 - [Methods](https://github.com/hsuwanying/music-streaming-analytic/blob/main/README.md#methods)
 - [Data Analysis](https://github.com/hsuwanying/music-streaming-analytic/blob/main/README.md#data-analysis)
 - [Conclusion](https://github.com/hsuwanying/music-streaming-analytic/blob/main/README.md#conclusion)
 - [Project Reflection](https://github.com/hsuwanying/music-streaming-analytic/blob/main/README.md#project-reflection)
 - [Notebook](https://github.com/hsuwanying/music-streaming-analytic/blob/main/README.md#notebook)
 - [Reference](https://github.com/hsuwanying/music-streaming-analytic/blob/main/README.md#reference)


# Initial Situation
[Deezer](https://www.deezer.com/en/), is a French music streaming service provider founded in 2006. It provides 73 million tracks and customized features based on subscription types. In addition, Deezer utilizes non-personalized recommendations based on common interests, which filter user's preference and listening history. In 2016, Deezer introduced an exclusive feature - [Flow](https://features.deezer.com/flow/) - an optimized recommendation system based on the user's mood. According to the company, this new feature recommends new or have listened tracks based on users' favorites, and provides users with various music choices based on the time. In other words, users are able to listen to music depending on different moods, contexts or specific events.

# Business Problem
<blockquote cite="https://www.kaggle.com/c/dsg17-online-phase">
Kaggle Challenge: To predict whether the users of the test dataset listened to the first track Flow proposed them or not. Deezer considers that a track is "listened" if the user has listened to more than 30 seconds of it (is_listened =1). If the user presses the skip button to change the song before 30 seconds, then the track is not considered as being listened (is_listened = 0).
</blockquote>

<figure>
 <img width="817" alt="flow" align = "center" src="https://user-images.githubusercontent.com/72688726/187404204-8281894e-390a-4094-aae8-d29a0015a06c.png">
 <figcaption>Deezer - FLOW</figcaption>
</figure>

# Solution
The original goal of this kaggle challenge is to improve the recommender system that can accurately predict and suggest a track the user will listen more than 30 seconds. Notheless, having positive **User experience** matters to business success and is crucial when measuring product performance. Besides predicting whether a user would skip a song or not to create a recommender system, in this project, I conducted a user preference analysis to generate insights from user age, user activities, music preference and listening patterns into the user experience to optimize Deezer's recommendation system. 

# Data Source
The data is originated from a [Kaggle challenge](https://www.kaggle.com/c/dsg17-online-phase).

## Description
The target variable of this dataset is is_listened. There are 7'558'834 obersvations with 14 preditors.

 - genre_id: identifiant of the genre of the song
 - media_id: identifiant of the song listened by the user
 - album_id: identifiant of the album of the song
 - media_duration: duration of the song
 - user_gender: gender of the user
 - user_id: anonymized id of the user
 - context_type :type of content where the song was listened: playlist, album ...
 - release_date: release date of the song with the format YYYYMMDD
 - ts_listen: timestamp of the listening in UNIX time
 - platform_name: type of os
 - platform_family: type of device
 - user_age: age of the user
 - listen_type if the songs was listened in a flow or not
 - artist_id: identifiant of the artist of the song
 - is_listened: 1 refers a track was listened, 0 otherwise

# Methods
 - Data prepreocessing
 - Data Exploration
 - Feature Engnerring and Data Analysis

## Preprocessing
After the data exploration, we’ve found three main issues in the train dataset:
1. There 17 entries of released_date is 30000101, which cannot be recognized with the time format
2. 29,779 data entries where ts_listen is greater than released_date
3. There are 2 records where ts_listen is earlier than the time when Deezer was founded (in 2006) 

## Feature engineering
To better understand user preferences, behaviors and listening patterns, a series of feature engineering was conducted. 

 - **Time-related features**: such as year, month, day, weekday, is_weekend, hour, minutes and seconds were derived from `ts_listen`, which indicates the time a user starts to listen to a track. After that, season and sessions were derived from month and hour, and ladled with four seasons and six different time sessions. 
 - **User-related features**: user behaviour and listening patterns are created by aggregating `user_id`, `ts_listen`,  `user_age`,  `media_duration` and `media_id`. 
  - `listen_diff: User listen music duration
  - `listen_percent`: the percentage of a song is listened 
  - `time_gap`: the gap before the next listen sesstion  
  - `listen_start`: the time a user start to listen music
  - `listen_end`: the time a user stop to listen music

More detail can be seen in [Deezer data analysis result](https://github.com/hsuwanying/music-streaming-analytic/blob/main/deezer_dataanalysis_result.ipynb)file.

# Data Analysis

## User behaviour analysis
Time is an essential factor which shifts users perderence from time to time. 

24 hours are divded into six sesession, the graph below shows user listening time based on `session`,
<p float="left">
  <img width="400" alt="session" class="center" src="https://user-images.githubusercontent.com/72688726/187429311-17f417cd-42cd-46e6-bf64-eff373b30c3c.png">
   <img width="407" alt="hour" src="https://user-images.githubusercontent.com/72688726/187435624-c8dc0f3b-02c4-48c7-ab05-13459cb900a7.png">
</p>

we found that users started listening to music in the morning, reached the peak in the afternoon, and then dropped in the evening. The image  gives more detail about the variety of number of users changes hourly-based. Key findings are summarized as following:

1. Number of active users dramatically increased between 5am to 6am.
2. The highest number of listeners showed up between 4 to 6pm, with figures above 500,000.
3. The number of users constantly decreased in the evening and dropped to 200,000 at 23 pm. 

## User listening pattern analysis based on user age

Attributes ‘user_id’, ‘user_age’, ‘media_id’ (songs) were aggregated for calculating average number of songs listened per user and the percentage of songs listened across each user age group. The result is summarized as below:

1. The number of songs, the length of songs and song listened percentage increased gradually as the age rises.
2. Young users were more likely to skip songs than the 30-year-old age group.
3. Users with a 30 year-old age were more likely to finish songs recommended by the system.
4. Users aged 30 listened to nearly two times more songs than users aged above 20.
5. Majority of users listening in the flow skipped more songs than users who were not in a flow, except users aged 19 and 30 

## Genre Analysis
When it comes to content analysis, genre is one of the features that can differ from time to time, as well as influenced by the surrounding scenarios of users. We found that there are 6 main genres, genre id 0, 7, 10 ,25, 27 and 14, were very popular among all other attributes, such as hour, session, context, platform, listen type and user_age. In other words, no matter the time, the user age or the context, these 6 genres would be favored by the users. Key findings are listed below and graphical analysis can be seen in [deezer_eda_result](https://github.com/hsuwanying/music-streaming-analytic/blob/main/deezer_eda_result.ipynb) 

1. Genre_id 0 was the most popular genre among the top 10 ranking.
2. Genre_id 0, 7, 10 ,25, 27, 14, 734, 297, 2744 were the most popular.
3. Popular genres are beloved across most sessions. Except that genre_id 2744 was not popular during night and midnight, genre_id 50 was preferable during 4. the Night, and genre_id 3645 in the midnight.
5. The Number of users listening to genre 0 was four times more without listening in the flow, whereas, there were more variety genres appearing when 6. users were listening in the flow.
7. Genre preference was different between user age groups. Among that, gerne_id 0 domainted genre preference across all user age groups, while user age 19 8. is the main audience of this genre.

# Conclusion
To sum up, we found that **time** is one of the most critical elements that can affect the user when it comes to listening type of songs. Music preference also changed differently between user age groups, platform, and listen environments. To improve the new feature FLOW and reduce user bouncing rate, a context-based recommendation system is suggested, nevertheless, personalized features need to be considered when building such a model.

# Project Reflection

It was a great experience to work on a dataset which contains millions of entries. Ideally, it would be good to start data processing in a database due to the simplicity of programming. In addition, performing data queries can help us to have a quick glance of data and have better understanding when performing some statistical calculations. 

On the other hand, there are many categorical attributes which are replaced with numeric labels in the given dataset; it would be helpful to have the original labels of each categorical variable, which can help analysts form problem statements or hypotheses as well as provide better interpretation when analyzing data.

# Notebook
[Python Notebook](https://github.com/hsuwanying/music-streaming-analytic/blob/main/deezer_eda_result.ipynb)

# Reference
 - Adiyansjan, Gunawan, A. A., & Suhartono, D. (2019). Music Recommader Systen Based on Genre using COnvolutional Recurrent Neural Networls. Procedia Computer Science 157, 99-109.
 - Hansen, C., Mehrotra, R., Hansen, C., Brost, B., Maystre, L., & Lalmas, M. (2021). Shigting Consumption towards Diverse Content on Music Streaming Platforms. Proceedings of the 14th ACM International Conference on Web Search and Data MiningMarch, 238-246.
 - Maasø, A., & Hagen, A. N. (2020). Metrics and Decision-Making in music streaming. Popular communication Vol. 18, No. 1, 18-31.
