ENVISION-HACKATHON
ROUND : 1 

# TEAM NAME : C-Suite
TEAM MEMBERS 
1.SANIYA
2.NANDANI
3.KOMAL

Abstract : 
        This project creates a Music Recommendation System by collecting data from the Spotify Web API using the Spotipy library.
        It gathers details on 600 pop tracks, including song names, artists, albums, and genres, to help generate personalized music recommendations.
        The data is organized with Pandas and stored in a CSV file, forming the basis for future user-driven recommendations based on preferences.
        project aims to help by providing personalized music recommendations based on user preferences, focusing on genre and artist information. By collecting data from the Spotify Web API, it helps users discover new songs tailored to their tastes. 
        In the future, the system can evolve to adapt to individual listening habits, enhancing the overall music discovery experience.
        
Title: Music Data Collection and Mood Classification using Spotify API.

Description: 
        This project collects music data from the Spotify Web API, including song names, artists, albums, classification . The project uses the Spotipy library for accessing Spotify's API
        The data is then saved into a CSV file for further analysis. TOTAL 2000+ entries collected

Data Source:
        The data for this project was collected using the **Spotify Web API**, which provides access to Spotify's music catalog, including track information, artist details, and genres.

Methods of Data Collection:
        1. Spotify Web API: The data was retrieved using the `Spotipy` Python library, a client for the Spotify Web API.
        2. Search Query: The query used to retrieve music data was for tracks in the 'pop' genre: `genre:pop`.
        3. Pagination: Since the API allows fetching up to 50 items per request, the data was paginated, retrieving a total of **600 tracks**.
        4. Data Columns:
           - Song Name: The title of the track.
           - Artist: The name of the artist(s) associated with the track.
           - Album: The name of the album the track belongs to.
           - Genre: The genre of the artist retrieved from their profile.

Tools Used:
         - Spotipy: Python library to interact with the Spotify Web API.
         - Pandas: Python library used to organize and structure the collected data.
         - CSV: The final dataset was saved in CSV format for further analysis.

Data Collection Code:
  The data was collected using the following Python code:

      import spotipy
      from spotipy.oauth2 import SpotifyClientCredentials
      import pandas as pd
      
      
      client_id = 'your-client-id'
      client_secret = 'your-client-secret'
      client_credentials_manager = SpotifyClientCredentials(client_id=client_id, client_secret=client_secret)
      sp = spotipy.Spotify(client_credentials_manager=client_credentials_manager)
      
      songs = []
      artists = []
      genres = [] 
      albums = []
      
      num_songs = 2000
      limit = 50  
      iterations = num_songs // limit  
      
      for offset in range(0, num_songs, limit):
          results = sp.search(q='genre:pop', type='track', limit=limit, offset=offset)
          
         
          for track in results['tracks']['items']:
              songs.append(track['name'])
              artist_name = track['artists'][0]['name']
              artists.append(artist_name)
              albums.append(track['album']['name'])
             
              artist_info = sp.artist(track['artists'][0]['id'])
              genres.append(artist_info['genres'][0] if artist_info['genres'] else 'Unknown')  # Handle case with no genre
      
      
      music_data = pd.DataFrame({
          'Song Name': songs,
          'Artist': artists,
          'Album': albums,
          'Genre': genres  # Add the genre column
      })
      music_data.to_csv('music.csv', index=False)


Output:
                      Song Name          Artist  
0                  Jo Tum Mere Ho       Anuv Jain   
1                          Sahiba   Jasleen Royal   
2                Die With A Smile       Lady Gaga   
3    Aaj Ki Raat (From "Stree 2")    Sachin-Jigar   
4                  Pehle Bhi Main   Vishal Mishra   
  

                                Album           Genre  
0                          Jo Tum Mere Ho  indian indie  
1                                  Sahiba     hindi pop  
2                        Die With A Smile       art pop  
3            Aaj Ki Raat (From "Stree 2")  gujarati pop  
4                                  ANIMAL     hindi pop  

