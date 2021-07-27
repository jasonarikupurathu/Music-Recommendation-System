# Music Recommendation System

### Business Problem:

Musicians, often times, have varying styles from album to album and from track to track. They tend to dislike  being put in a “genre” box which many organizations tend to do. For example, following his first Grammy win for his album “Igor” in 2020, Tyler the Creator "admitted that while he was "very grateful" for his win, the categorizing of his album as rap was a "backhanded compliment." 

Spotify tends to label the genre of songs based off what genre the artist falls under which is quite unfair to an artist if said artist wants to branch out. Not only that, if a user likes just a particular song from an artist, but not every song from said artist, how can one recommend songs based off that particular song without influence from the artists genre? Can we use the predicted genre of a song, as well as other features, to make better song recommendations based off an inputted song?

---
### Methods
The data was acquired, through the Spotify api alongside the Spotipy library, from various playlists. The dataset included over 5000 songs, extracted from a JSON object returned from the API, ranging from genres of what users classified as Hip-hop, Pop, Alternative Metal, and Rock. 

We want to score the model based on how correct it was in predicting the overall genre as well as taking a loss for predicting an incorrect genre. Since the severity of getting a genre wrong isn't high, the F1 score will be our metric since we want the model to get a general idea of what each genre may be. The f1-score won’t necessarily be extremely close to 1 because it may predict a hip-hop song as pop song and vice-versa and that line in actuality is sometimes blurred.  

When predicting the genres, the models consisted of Logistic Regressions, Gradient Boosted Classifiers, XGBoost Classifiers, and Voting Classifier. The data was altered using a combination of One Hot Encoder, SMOTE, Grid Search, Standard Scaling, Pipelines, or Normalization. When predicting for recommendations of songs, the model was the Nearest Neighbors with an n_neighbors of 15, the metric as cosine simliarity, and the radius of 0.45. 

---
### Results
- FSM - Logistic Regression:
  - Training F1 Score: 0.64
  - Testing F1 Score: 0.63
- Logistic Regression + Pipeline(OHE + SS) + GridSearchCV:
  - Training F1 Score: 0.66
  - Testing F1 Score: 0.63
- XGBClassifier + OHE + SMOTE: 
  - Training F1 Score: 0.79 
  - Testing F1 Score: 0.67
- GradientBoostingClassifier + OHE + SMOTE:
  - Training F1 Score: 0.81
  - Testing F1 Score: 0.68
- XGBClassifier + OHE + Balanced Class Weight:
  - Training F1 Score: 0.74
  - Testing F1 Score: 0.68

---
### Conclusion
We were able to first predict the genre of user inputted song and provide recommendations based off said song. Using the predicted genre rather than the artist's genre, we were able to provide users songs that relate to said song itself rather than having influence from the artist. The model isn't perfect when working with genres that it hasn't been trained on, but maybe adding songs from other genres can help the model predict better recommendations. 

---
### Further Exploration
  - Add more songs
  - Add more genres
  - More accurately predict genres for a song
---
### Attributes

    Primary:
    - id (Id of track generated by Spotify)

    Numerical:
    - acousticness (Ranges from 0 to 1)
        - whether the song is acoustic or not, 0(not acoustic)->1(very acoustic)
    - danceability (Ranges from 0 to 1)
        - how suitable the track is for dancing, 0(not danceable)->1(very danceable)
    - energy (Ranges from 0 to 1)
        - how energetic the track is, 0(less energetic)->1(very energetic)
    - duration_ms (Integer typically ranging from 200k to 300k)
        - Time in MS
    - instrumentalness (Ranges from 0 to 1)
        - the ratio of instrumental sounds overall, 0(lot of vocal sounds)->1(instrument sounds)
    - valence (Ranges from 0 to 1)
        - how positive the music is, 0(sad)->1(cheerful)
    - tempo (Float typically ranging from 50 to 150)
        - tempo of track in BPM
    - liveness (Ranges from 0 to 1)
        - presence of audience, 0(studio record)->1(concert)
    - loudness (Float typically ranging from -60 to 0)
        - how loud the song is in dB -60(very quiet)->0(very loud)
    - speechiness (Ranges from 0 to 1)
        - the ratio of spoken words to the overall, 0(instrumental)->1(talk show)

    Categorical:
    - mode 
        - (0 = Minor, 1 = Major)
    - key (All keys on octave encoded as values ranging from 0 to 11, starting on C as 0, C# as 1 and so on…)
        - the major key of the track, 0:C, 1:C#, 2:D, ..., 11:B
            0. Key of C
            1. Key of C#/Db (enharmonic keys)
            2. Key of D
            3. Key of D#/Eb
            4. Key of E
            5. Key of F
            6. Key of F#/Gb (enharmonic keys)
            7. Key of G
            8. Key of G#/Ab
            9. Key of A
            10. Key of A#/Bb
            11. Key of B
    - timesignature 
        - (The predicted timesignature, most typically 4)
---
### For More Information

Please review the jupyter notebooks for analysis or view the [presentation](https://docs.google.com/presentation/d/1OVD3tPFMMoHLEK7HiTFsT0MCqxPxAglEr43XIT2fQG0/edit?usp=sharing).

---
### Github Directory


    ├── README.md                                         <- The top-level README for reviewers of this project
    ├── Notebook-1-Cleaning-Preprocessing.ipynb           <- Notebook for data cleaning and EDA
    ├── Notebook-2-Predict-Genre-Data-Modeling.ipynb      <- Notebook for genre prediction and model
    ├── Notebook-3-Nearest-Neighbors-Data-Modeling.ipynb  <- Notebook for music recommendations
    ├── app.py                                            <- Streamlit app of model
    └── pickled_files                                     <- Contains Pickled Files
        └ df.pickle                                           <- DataFrame cleaned to predict genres pickled
        └ all_songs_genre_predicted.pickle                    <- Dataframe with genres predicted pickled
        
