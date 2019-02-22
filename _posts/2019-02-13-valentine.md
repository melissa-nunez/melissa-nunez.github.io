---
title: "Clustering and Sentiment Analysis of Spotify's Top Valentine's Day Songs"
date: 2019-02-13
tags: [unsupervised learning, k-means, clustering, R, sentiment, NLP]
excerpt: "Clustering Spotify's Valentine's Day playlist followed by sentiment analysis"
header:
  image: "/images/hearts.jpg"
---

The connotation for Valentine's Day can differ depending on who you ask. Although it is suppose to be a joyous day for lovers to express their affection towards one another, it can also be a depressing holiday for those you have no one to share it with. So this year, as someone who fell into the later category, I decided to celebrate the holiday by analyzing Spotify's Valentine's Day playlist with the goal of identifying which song is the saddest Valentine's Day song. I achieved this by clustering the playlist into songs with low valence and low energy vs those with high valence and high energy and then filtering based on the percentage of sad words found in the lyrics.

### Installing

The first step was to get access to [Spotify's API](https://developer.spotify.com/documentation/web-api/). Next, create a developer's account to access the API [here](https://developer.spotify.com/dashboard/). For further instructions on setting up, you can visit the spotifyr website [here](https://www.rcharlie.com/spotifyr/index.html).

To install and load the package, use the following:

```r
devtools::install_github('charlie86/spotifyr')
library(spotifyr)
```

## Data
There is a plethora of Valentine's Day romance songs that I could have used for this analysis. I did plenty of research on "Top Romance Songs" & "Top Valentine's Day Songs" prior to beginning, however I decided on Spotify's own Valentine's Day playlist. This playlist is made up of 90 songs.

The Spoitfy API gives information on a songs danceability, energy, key, loudness, mode, speechiness, acousticness, instrumentalness, liveness, valence, and tempo. I saved the Valentine's Day playlist as my own and then accessed it through the API. I then pulled out the tracks from the playlist and extracted the features.

This is the code used:

```r
# Pull playlist
valentines_playlist <- playlists %>%  filter(playlist_name == "Valentine's Day Love")

# Get tracks
valentine_tracks <- get_playlist_tracks(valentines_playlist)

# Get features
track_features <- get_track_audio_features(valentine_tracks)
```
