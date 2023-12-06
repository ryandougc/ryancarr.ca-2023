# Tastify Case Study

## Project Description

Analyze your music taste through your Spotify account. See your top genres, and compare your music taste with your friends.

## Skills Used

- Node.js Express RESTful API written in TypeScript
- Consuming a third party API (Spotify API)
- MongoDB NoSQL database

## Lessons Learned

### API Data Aggregation

This was my first project where I was taking large amounts data from multiple different API endpoints and manipulating it to extract the useful data. The Spotify API is (mostly) well documented and is a great place to start learning how to work with APIs. It takes you through the process of authenticating and authorizing requests, saving the authorization keys in a private and secure manner, and handling authentication refresh tokens. 

The biggest hurdle for using data from an API is cleaning the data and putting it into a format that is able to be manipulated. This wasn’t an easy task with the Spotify API, as I was working with API endpoints limited to retrieving 50 items at a time, with the number of total items to pull being in the thousands. I had to understand how to break up the requests to retrieve all the data required in a timely manner, but also stay within the unspecified API rate limits. 

 Another difficulty is that the data I was looking for was separated into different endpoints. When pulling a track (the name Spotify gives to a song) from the API, there is no genre information attached to it, despite what the documentation says. This meant that I had to get the genre from the track’s artist. The sequence of events required are:

1. Get all of the tracks from the user’s liked songs and playlists
2. Find the primary artist of each track (since there could be multiple artists)
3. Get the data for every artist
4. Take the genres of each artist and append them to the track they are associated with

This is a costly process and would quickly exceed the rate limit of the API. Since the user may have multiple instances of the same song, or many instances of the same artist, I decided to group items together so that I can perform as few operation as possible. I created a hash table to store every unique song from the user’s playlists and liked songs, keeping track of the number of times a single track is seen. Then I iterate over the hash table of tracks and push every track’s primary artist into a second hash table. 
Now that I had a unique list of every artist, I could start fetching the artists genres from the API, knowing that the minimal amount of data will be retrieved. The Spotify API has an endpoint to get the data of 50 artists at a time. I created comma separated strings of 50 artist IDs to cover every unique artist and pulled that data. Once the artists genre was pulled, I could append it to the corresponding artist in the hash table. 

Next I iterate over the track hash table, looking up each unique track’s artist in the artist hash table and appending the artist’s genre to the track. Now I have all of the data I need, cleaned and ready to manipulate

## Project Outcome

This project is still a work in progress, as I am collaborating with a UX designer to develop a front-end for this project. We are currently doing some planning and user research. Once we have designs created, I will be coding the front-end of the website with either Vue.js or React. Then I can connect the API that I have created to bring the functionality into a usable medium for the general population.

### Room for Improvement

When getting genres from an artist and adding them to a track, there are 2 downfalls. 

The first is that an artist may have 1 or more genres associated with them. This program takes all of the genres associated with an artist and appends it to a song, despite whether that genre matches a song or not. A better way to use the data provided by Spotify would be to use the track features, the data descriptors that represent the track, to classify a song. However this is above my current knowledge of song structure. I will be looking into how the soundscape of audio can be manipulated to find trends in similar songs.

The second downfall is that many genres are hyper specific and could potentially skew the data. Some genres are generic like Pop, Hip hop, Classical or Rock but many are sub genres like Conscious Hip Hop, Southern Rap, or Singer-songwriter Indie Folk. Using a k pair matching algorithm could potentially improve the results to match sub genres into their parent genres. My attempts at this did not go well and will need to be improved to be a useful improvement to the dataset. However, this would likely not improve the dataset very much and I currently don’t see this as being a high priority for the future of this project.