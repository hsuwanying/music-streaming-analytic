<p align = "center">
<img src = "https://user-images.githubusercontent.com/72688726/187465826-02188c10-55de-435f-81f7-ae27c2c61fcb.jpg">
</p>
<p align = "center">
 <a href="https://features.deezer.com/flow/?_gl=1*182jft9*_ga*MTg5MzU0MjMyNS4xNjYxODY5OTU1*_ga_71WQ7Y8JLG*MTY2MjA0NDM1MS4zLjEuMTY2MjA0NTM0NS4wLjAuMA..">Deezer FLOW</a>
</p>

# Music Recommender System Optimisation
### Improve the user experience by analysing user listening history data to optimize a recommender system feature for music streaming service provider

Music streaming services allow people to listen to various types of music and millions of tracks with their intelligent devices based on their preferences; these advanced features have made listening to music much more accessible than ever (Adiyansjan, Gunawan, & Suhartono, 2019). With the increased competitors in the music streaming industry, having a good user experience is essential to increase competitive advantages and strengthen customer stickiness. In this project, we derived actionable suggestions by analyzing the user's listening history data and experience with the recommender system for improving a music recommender system by Deezer.

# Author
[Carol Hsu](https://github.com/hsuwanying)

# Table of Content
 - [Background](https://github.com/hsuwanying/music-streaming-analytic/blob/main/README.md#background)
 - [Problem](https://github.com/hsuwanying/music-streaming-analytic/blob/main/README.md#problem)
 - [Solution](https://github.com/hsuwanying/music-streaming-analytic/blob/main/README.md#solution)
 - [Data Source](https://github.com/hsuwanying/music-streaming-analytic/blob/main/README.md#data-source)
 - [Methods](https://github.com/hsuwanying/music-streaming-analytic/blob/main/README.md#methods)
 - [Data Analysis](https://github.com/hsuwanying/music-streaming-analytic/blob/main/README.md#data-analysis)
 - [Key Findings](https://github.com/hsuwanying/music-streaming-analytic/blob/main/README.md#key-findings)
 - [Conclusion](https://github.com/hsuwanying/music-streaming-analytic/blob/main/README.md#conclusion)
 - [Project Reflection](https://github.com/hsuwanying/music-streaming-analytic/blob/main/README.md#project-reflection)
 - [Notebook](https://github.com/hsuwanying/music-streaming-analytic/blob/main/README.md#notebook)
 - [Reference](https://github.com/hsuwanying/music-streaming-analytic/blob/main/README.md#reference)


# Background
[Deezer](https://www.deezer.com/en/), iis a French music streaming service provider founded in 2006. It provides 73 million tracks and customized features based on subscription types. In addition, Deezer utilizes non-personalized recommendations based on common interests, which filter users' preferences and listening history. In 2016, Deezer introduced an exclusive feature - [Flow](https://features.deezer.com/flow/) - an optimized recommendation system based on the user's mood. According to the company, this new feature recommends new or have-listened tracks to users based on their listening history, context and time. In other words, users can listen to music depending on different moods, contexts or specific events.

# Problem
Users nowadays are exposed to tons of information and face the paradox of choice, which means, having an abundance of choices could delay users in making decisions and deterring their motivation to stay with the services (Maasø & Hagen, 2020). Hence, for businesses who wish to increase competitive advantages and enhance user stickiness towards digital products, it is essential to develop a recommender system, a mechanism that automatically suggests media meeting user’s expectations (Hansen et al., 2021)

<blockquote cite="https://www.kaggle.com/c/dsg17-online-phase">
The challenge was given by Kaggle: To predict whether the users of the test dataset listened to the first track Flow proposed them or not. Deezer considers that a track is "listened" if the user has listened to more than 30 seconds of it (is_listened =1). If the user presses the skip button to change the song before 30 seconds, then the track is not considered as being listened (is_listened = 0).
</blockquote>

# Solution
The original goal of this kaggle challenge is to improve the recommender system that can accurately predict and suggest a track the user will listen more than 30 seconds. Nonetheless, having a positive User experience is crucial when measuring product performance, besides predicting whether a user would skip a song or not to create a recommender system, in this project, I conducted a user preference analysis to generate insights from user age, user activities, music preference and listening patterns into the user experience to optimize Deezer's recommendation system.

# Data Source
The data is originated from a [Kaggle challenge](https://www.kaggle.com/c/dsg17-online-phase).

## Description
The target variable of this dataset is is_listened. There are 7'558'834 obersvations with 14 preditors.

 - `genre_id`: ID of the genre of the song
 - `media_id`: ID of the song listened by the user
 - `album_id`: ID of the album of the song
 - `media_duration`: duration of the song
 - `user_gender`: gender of the user
 - `user_id`: user ID
 - `context_type`:type of content where the song was listened: playlist, album ...
 - `release_date`: release date of the song with the format YYYYMMDD
 - `ts_listen`: timestamp of the listening in UNIX time
 - `platform_name`: type of os
 - `platform_family`: type of device
 - `user_age`: age of the user
 - `listen_type`: if the songs was listened in a **FLOW** or not
 - `artist_id`: ID of the artist of the song
 - `is_listened`: 1 refers to a track that has been listened to, 0 otherwise

# Methods
 - Data prepreocessing
 - Data Exploration
 - Feature Engnerring and Data Analysis

## Preprocessing
After the data exploration, we’ve found three main issues in the train dataset:
1. There 17 entries of `released_date` are 30000101, which cannot be recognized with the time format
2. 29,779 data entries where `ts_listen` is greater than `released_date`
3. There are 2 records where `ts_listen` is earlier than the time when Deezer was founded (in 2006) 

## Feature engineering
To better understand user preferences, behaviors and listening patterns, a series of feature engineering was conducted.
 - **Time-related features**: such as year, month, day, weekday, is_weekend, hour, minutes and seconds were derived from `ts_listen`, which indicates the time a user starts to listen to a track. After that, season and sessions were derived from month and hour, and ladled with four seasons and six different time sessions. 
 - **User-related features**: user behaviour and listening patterns are created by aggregating `user_id`, `ts_listen`,  `user_age`,  `media_duration` and `media_id`. 
  - `listen_diff`: User listen music duration
  - `listen_percent`: the percentage of a song is listened 
  - `time_gap`: the gap before the next listen sesstion  
  - `listen_start`: the time a user start to listen music
  - `listen_end`: the time a user stop to listen music

More detail can be seen in [Deezer data analysis result](https://github.com/hsuwanying/music-streaming-analytic/blob/main/deezer_dataanalysis_result.ipynb).

# Data Analysis
## Feature FLOW
Fistly, we quickly have a look at the **FLOW** feature, which is the column `listen_type`. The `listen_type` indicates a user listen music use FLOW(listen_type = 1) or not (listen_type = 0). Attributes `user_id`, `user_age`, `media_id` (songs) were aggregated for calculating average number of songs listened per user and the percentage of songs listened across each user age group.

Table 1 gives information about the avarage lenght of songs people listen and percentage of song listening within and without FLOW function. It clearly shows that, user do not use flow function listened 3 times longer than user in the FLOW. More specficly, users who do not use flow function listened nearly 60% of a song, while, users who use flow function only listened less than 20% of a song which is recommmaded by the system.

<br>
<p align = "center">
<img width="550" alt="ave_lis_perc" src="https://user-images.githubusercontent.com/72688726/187438440-81f05860-8157-4584-af35-dcd757395eb2.png">
</p>
<p align = "center">Table 1. Average media listening percentage with and wihout FLOW function
</p>
<br>


User age is added to Table 2 to compare user listening behaviour accros ten age groups
<br>
<p align = "center">
<img width="550" alt="media_perc" src="https://user-images.githubusercontent.com/72688726/187438204-b337eccb-5ba9-4c85-b684-266f76f08138.png">
</p>
<p align = "center">Table 2. Media listening duration 
</p>
<br>

`listen_type` is added to Table 3 to compare users listening behaviour accros ten age groups within and without FLOW function

<br>
<p align = "center">
<img width="550" alt="age_lis_perc_flow" src="https://user-images.githubusercontent.com/72688726/187438395-ae28615f-81c7-45d7-a94d-386f9f04e7d9.png">
</p>
<p align = "center">Table 3. Media listening percentage with and wihout FLOW function based on Age group 
</p>


## User behaviour & perference analysis

 - **Time**
Time is an essential factor which shifts users perderence from time to time. we divide 24 hours into six sessions including midnight, early morning, morning, afternoon, evening and night. The session graph below shows users started listening to music in the morning, reached the peak in the afternoon, and then dropped in the evening, and the hour graph gives information about user activity within with 24 hours.

<p float="center">
  <img width="400" alt="session" class="center" src="https://user-images.githubusercontent.com/72688726/187429311-17f417cd-42cd-46e6-bf64-eff373b30c3c.png">
   <img width="400" alt="hour" src="https://user-images.githubusercontent.com/72688726/187435624-c8dc0f3b-02c4-48c7-ab05-13459cb900a7.png"> 
</p>

 - **Medium**
Features `platform_family` and `platform_name` referes to devices and operating system a user use to access to Deezer app, as the data was encoded with numeric value, we cannot tell what devices or opreation system users use, nonetheless, the platform_family 0 and platform_name 0 are the most prefereable mediums amongest users

<p float="center">
 <img width="400" alt="platform_family" src="https://user-images.githubusercontent.com/72688726/187464284-094e1ac2-7136-499a-880b-06643ea597c4.png">
 <img width="400" alt="platform_name" src="https://user-images.githubusercontent.com/72688726/187464401-6844ab22-dd05-4b65-ab2c-2836ff935574.png">
</p>

## Genre Analysis
When it comes to content analysis, genre is one of the features that can differ from time to time, as well as influenced by the surrounding scenarios of users. We found that there are 6 main genres, genre id 0, 7, 10 ,25, 27 and 14, were very popular among all other attributes, such as hour, session, context, platform, listen type and user_age. In other words, no matter the time, the user age or the context, these 6 genres would be favored by the users. Key findings are listed below and graphical analysis can be seen in [deezer_eda_result](https://github.com/hsuwanying/music-streaming-analytic/blob/main/deezer_eda_result.ipynb) 

<p float="center">
 <img width="300" alt="album" src="https://user-images.githubusercontent.com/72688726/187462891-34b9a947-c38c-4de0-84b1-cefd5106def6.png">
 <img width="300" alt="artist" src="https://user-images.githubusercontent.com/72688726/187462960-7d3c728e-f9fb-492c-8ee3-201fa4096baa.png">
 <img width="300" alt="gerne" src="https://user-images.githubusercontent.com/72688726/187463242-3ad1876a-2039-46c4-9f51-f2a970c3ff1b.png">
</p>

# Key Findings
- Feature `Flow`  
  1. The number of songs, the length of songs and song listened percentage increased gradually as the age rises.
  2. Young users are more likely to skip songs than the 30-year-old age group.
  3. Users with a 30 year-old age are more likely to finish songs recommended by the system.
  4. Users aged 30 listened nearly two times more songs than users aged above 20.
  5. Majority of users listening in the flow skipped more songs than users who were not in a flow, except users aged 19 and 30 

- User Behaviour
  1. Number of active users dramatically increased between 5am to 6am.
  2. The highest number of listeners showed up between 4 to 6pm, with figures above 500,000.
  3. The number of users constantly decreased in the evening and dropped to 200,000 at 23 pm. 

- Gerne Preference
  1. Genre_id 0 was the most popular genre among the top 10 ranking.
  2. Genre_id 0, 7, 10 ,25, 27, 14, 734, 297, 2744 were the most popular.
  3. Popular genres are beloved across most sessions. Except that genre_id 2744 was not popular during night and midnight, genre_id 50 was preferable during the Night, and genre_id 3645 in the midnight.
  4. The Number of users listening to genre 0 was four times more without listening in the flow, whereas, there were more variety genres appearing when 6. users were listening in the flow.
  5. Genre preference was different between user age groups. Among that, gerne_id 0 domainted genre preference across all user age groups, while user age 19 is the main audience of this genre.

# Conclusion
To sum up, we found that time is one of the most critical elements that can affect the user when it comes to listening type of songs. Music preference also changed differently between user age groups, platform, and listen environments. To improve the new feature FLOW and reduce user bouncing rate, a context-based recommendation system is suggested, nevertheless, personalized features need to be considered when building such a model.

# Project Reflection

It was a great experience to work on a dataset which contains millions of entries. Ideally, it would be good to start data processing in a database due to the simplicity of programming. In addition, performing data queries can help us to have a quick glance of data and have better understanding when performing some statistical calculations. 

On the other hand, there are many categorical attributes which are replaced with numeric labels in the given dataset; it would be helpful to have the original labels of each categorical variable, which can help analysts form problem statements or hypotheses as well as provide better interpretation when analyzing data.

# Notebook
[Python Notebook](https://github.com/hsuwanying/music-streaming-analytic/blob/main/deezer_eda_result.ipynb)

# Reference
 - Adiyansjan, Gunawan, A. A., & Suhartono, D. (2019). Music Recommader Systen Based on Genre using COnvolutional Recurrent Neural Networls. Procedia Computer Science 157, 99-109.
 - Hansen, C., Mehrotra, R., Hansen, C., Brost, B., Maystre, L., & Lalmas, M. (2021). Shigting Consumption towards Diverse Content on Music Streaming Platforms. Proceedings of the 14th ACM International Conference on Web Search and Data MiningMarch, 238-246.
 - Maasø, A., & Hagen, A. N. (2020). Metrics and Decision-Making in music streaming. Popular communication Vol. 18, No. 1, 18-31.
