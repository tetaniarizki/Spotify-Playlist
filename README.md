# Implementation of a Music Recommendation System for Spotify Application Users

> ![gambar spotify](https://user-images.githubusercontent.com/88262711/206826750-ca6c97f1-56d7-4fab-9a9d-8ecc09776774.jpg)

this project was done by
- [Rufina Indriani](https://www.linkedin.com/in/rufina-indriani-/)
- [Rizki Tetania](https://www.linkedin.com/in/rizki-tetania-mahalang/)

you can access our PPT, [here](https://docs.google.com/presentation/d/1w8gmlk62u0HrcDuTwCOf7OzGr1iisE7T_SLTOXJX05s/edit?usp=sharing).


Song is one of the entertainment media that never escapes the times. For the connoisseurs, the song is something that is very important because the song is an entertainment that will be listened to according to their mood. Until now, there are already 20+ music streaming application platforms, one of which is the Spotify music platform which has been established since 2006. [Spotify](https://support.spotify.com/en/article/what-is-spotify/) is a digital music, podcast and video service that gives you access to millions of songs and other content from creators around the world. Spotify is also known as a music streaming service, where the service provides a feature that can make a playlist recommendation for users. These recommendations were developed to provide song recommendations according to the user's preferred music preferences.

A recommendation system is a system that refers to predicting a number of items or data for future users, then making the top item recommendations (Top-N). The recommendation system provides information that is relevant to what users are looking for, so that the use of this system is needed by companies. There are 3 types of recommendation system methods, which consist of *Content-Based Filtering, Collaborative Filtering* and *Hybrid Filtering*.

In this project the method used is *Hybrid Filtering*, where in the research conducted by Yohana Imelda Lubis entitled "Implementation of Hybrid Filtering (Collaborative and Content-based) Methods for the Tourism Recommendation System" provides information that the *Hybrid Filtering* method is proven to be better than the *Collaborative* method and *Content-based* based on MAE value evaluation metric. This research resulted in the MAE value obtained in the *Hybrid Filtering* method of 0.3741, which is smaller than the MAE value in *Collaborative* of 1.1742 and *Content-based* of 0.3768 [[1]](https://citee.ft.ugm.ac.id/download51.php?f=TI-5%20-%20Implementasi%20Metode%20Hybrid%20Filtering.pdf). This is also supported by research entitled "Enhancing Book Recommendation with the use of Reviews" shows that the *Hybrid Filtering* method, namely LightFM, provides better performance compared to *Collaborative Filtering* methods such as k-Nearest Neighbor and SVD based on the AUC value evaluation metric [[2]](https://dl.ucsc.cmb.ac.lk/jspui/bitstream/123456789/4596/1/2018%20BA%20033.pdf). So in this project, we will focus on building a *Machine Learning* recommendation system model using *Hybrid Filtering*, namely the LightFM method to form a recommendation system with the best AUC value.

## *Business Understanding*

Song is one of the entertainment media that never escapes the times. For the connoisseurs, the song is something that is very important because the song is an entertainment that will be listened to according to their mood. Because there are so many songs available, it makes it difficult for many people to choose the song they want to hear. So that with the Recommendation System, it is hoped that it can provide information that is relevant to what the user wants.

### *Problem Statement*

Based on this statement, the issues raised in this project are explained as follows:
- Who is the user_id who listens to music the most?
- Who is the artist whose songs are played the most?
- What is the title of the song that the user likes the most?
- What is the name of the playlist most often played by the majority of users?
- Based on the insights obtained from the data, what is the right way to develop a recommendation system model for users?

### *Goals*

To answer these questions, create a recommendation system with the following goals:
- Get insight of data.
- Develop model with minimizing error values in order to form the best recommendation system in predicting artists that are relevant to user interests.

### *Solution Statement*

So to achieve the desired goals, a recommendation system will be formed with the following flow.
- Data Understanding
> Data Understanding is the initial stage of the project to understand data. In this case, we have 4 variables which is user_id, artistname, trackname and playlistname.
- Univariate Exploratory Data Analysis
> At this stage, analyze and explore several variables in the data. So knowing the relationship between one variable with other variables.
- Data Preparation
> This is the data preparation stage before the data is used for further processing. At this stage, several variables will be combined so that they become one unified file that is intact and ready to be used in the modeling stage, like user_id, artist_id, song playback frequency and artist or singer name.
- Model Delopment with Hybrid Filtering
> At this stage the system recommends several singers for the user, where the recommendation is obtained from the closeness between the recommended singers and the frequency history of the user listening to songs from several singers. From the number of times the singer's song is played, other singers will be identified with almost the same song genre as the singer to be recommended to the user. **The algorithm used is LightFM, a combined method of collaborative filtering and content-based filtering**. *LightFM produces more relevant recommendations compared to collaborative filtering or content-based filtering in general.*

## *Data Understanding*

The data used in this project is data about music playlist users of the Spotify application or [Spotify Playlist Dataset](https://www.kaggle.com/datasets/andrewmvd/spotify-playlists). The data consists of 4 variables namely user_id, artistname, trackname and playlistname. Where in this project, only 50% of the data from the total dataset taken randomly is 6,447,654 data. An explanation of the four variables is as follows.

Table 1. Variable of Project

| Variable | Description |
| ---------- | -------------- |
| *user_id* | Id of spotify app user |
|*artistname*| The name of the artist or singer that the user listens to|
|*trackname*| The name of the song played by the user|
|*playlistname*| The name of the playlist of the song the user is currently listening to|

Of the 220,001 existing artists, Daft Punk is a singer whose songs are frequently played by users.
And there is indications that there are missing value data or 'Not Specified' data in the artist, track and playlist columns.

## *Univariate Exploratory Data Analysis*

Tahapan ini bertujuan untuk memahami data secara diskripsi maupun visualisasi yang dijelaskan sebagai berikut.

- Top User

The most song played by user was hit 147,506 play, which is by user id '4398de6902abde3351347b048fcdc287'. This is more than three times than the second rank user

![download](https://user-images.githubusercontent.com/88262711/207790860-faee03be-6295-4754-af5b-bb49b1740c23.png)

Figure 1. Histogram of user whom play song less than 25% of others

Figure 1 provides information that, we still have more data on the right, so that means a lot of users only play songs a few times

- Top Playlist

![topplaylist](https://user-images.githubusercontent.com/88262711/207791476-a5fbbb11-4491-4464-8101-b32e7675177a.png)

Figure 2. Top Playlist

Based on figure 2 provides information that the most played playlist by user is Starred and played 668,203 times. Other playlists that have been played by users are Liked from Radio, Favoritas de la radio, and Rock.


- Top Tracks

![toptracks](https://user-images.githubusercontent.com/88262711/207791852-0ce5fb80-08f3-4812-9901-b91ffd4e01e1.png)

Figure 3. Top Tracks

Based on Figure 3, it shows that The most played songs by user is Intro and played 3,336 times.
And three songs that are most often heard, namely Intro, Home, and Closer

- Top Artist

![topartist](https://user-images.githubusercontent.com/88262711/207792255-8498a0ae-22b8-4565-b450-1a4e710ef6b8.png)

Figure 4. Top Artist

Figure 4 shows that The most played artist by user is Daft Punk and played 18,141 times. So, the three artists whose songs are heard the most are Daft Punk, Coldplay, and Radiohead

## *Data Preparation*

At this stage, there are 5 steps before the data is ready for training. Consists of the process of filtering data to merge data into one unit.
- In the first step, the data will be filtered based on artists whose songs have been listened to more than 50 times from the total data.
- Then step 2, the data will be filtered based on the user id which is in the unique data category regardless of the NaN value and has listened to more than 10 songs.
- The 3rd step, calculates the frequency of the number of songs that the user_id listens to for each artist. The calculation of the number of frequencies is stored in a new table, namely spotify_freq,
- Step 4, get a list of artists including unique data from spotify_freq data. Where the list is stored in the spotify_artist table, so that the dataset is the name of the artist (singer) and the id of the artist.
- The 5th step, which is to merge the data in the spotify_freq data with spotify_artist. The data is stored in the spotify_freq dataset. 

And the data is ready for the artist recommendation system modeling process based on the frequency with which the user listens to the artist's songs.

## *Model Delopment with Hybrid Filtering*

In this project, the proportion of data sharing *training* : *testing* is 99:1. While the method used is LightFM which is a hybrid matrix factorization model which represents users and items as latent vectors (embeddings) similar to traditional collaborative filtering models. In addition to this, similar to a content-based model, it also utilizes linear combinations of embeddings of content features to describe each product and user. Thus, LightFM combines the advantages of content-based and collaborative filtering methods to:
- Perform as well as content-based systems in cold-start and low-density scenarios.
- Performs as well as traditional collaborative filtering methods when interaction data
are available.

When both features and interaction data are available, LightFM performs significantly better
than both *Collaboratiive* and *Content Based* methods. The LightFM model's prediction for user u and item i is given by the dot product of user and item representations, adjusted by user and item feature biases:

![lightfm](https://user-images.githubusercontent.com/88262711/206838314-07c2ee1c-a64b-44f4-aa01-50206592c3a0.PNG)


-----

The algorithm used to build the LightFM model is by *importing* the LightFM library. As for the parameter values used are as follows.

- no_components : the dimensionality of the feature latent embeddings, where in this project the value of n_components is 30.
- loss : one of (‘logistic’, ‘bpr’, ‘warp’, ‘warp-kos’): the loss function, where in the project we use wrap loss.
- n_jobs : is an integer, specifying the maximum number of concurrently running workers. In this project the value of n_jobs is 4.
- epoch : The epoch is a hyperparameter that determines how many times the deep learning algorithm works through the entire dataset, both forward and backward. In this project the epoch value used is 30.

-----


### *Evaluation Metrics*

The evaluation metric used in this project is Area Under Curve (AUC). AUC is the area under the curve, where the area shows the level of accuracy of the prediction model. The area is a square whose value is always between 0 and 1. AUC value classification is as follows.

Table 2. AUC value classification

|Value of AUC| Description|
|-----|------|
|>0,9 - 1| Excellent|
|>0,8 - 0,9| Very Good|
|>0,7 - 0,8| Good|
|>0,6 - 0,7| Not Bad|
|0,5 - 0,6| Bad|

## *Conclusion*

The conclusion of this project is that by using the LightFM method, 10 artists are recommended for users, where the model formed has an AUC training value of 96.75% and AUC testing of 96.28%. As well as the difference between the AUC values of the training data and the testing data is not far enough, the possibility of a bias value is also quite small.


## *Reference*

[[1]](https://citee.ft.ugm.ac.id/download51.php?f=TI-5%20-%20Implementasi%20Metode%20Hybrid%20Filtering.pdf) Lubis, dkk. (2020). *Implementation of Hybrid Filtering (Collaborative and Content-based) Methods forthe Tourism Recommendation System*. Yogyakarta: ISSN: 2085-6350.

[[2]](https://dl.ucsc.cmb.ac.lk/jspui/bitstream/123456789/4596/1/2018%20BA%20033.pdf) Sudasighe, P.G. (2019). *Enhancing Book Recomemendation with the use of Reviews*. Sri Lanka: University of Colombo School of Computing.
