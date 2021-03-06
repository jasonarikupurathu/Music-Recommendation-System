# Music Recommendation System
![music-recommendation](https://user-images.githubusercontent.com/38678270/127258075-efe394e4-0e29-4e23-a9f8-ca8b6fce4353.jpeg) <sup>Getty Images</sup>

### Business Problem:

Musicians, often times, have varying styles from album to album and from track to track. They tend to dislike  being put in a “genre” box which many organizations tend to do. For example, following his first Grammy win for his album “Igor” in 2020, Tyler the Creator "admitted that while he was "very grateful" for his win, the categorizing of his album as rap was a "backhanded compliment."<sup>[1]</sup>

Spotify tends to label the genre of songs based off what genre the artist falls under which is quite unfair to an artist if said artist wants to branch out. Not only that, if a user likes just a particular song from an artist, but not every song from said artist, how can one recommend songs based off that particular song without influence from the artists genre? Can we use the predicted genre of a song, as well as other features, to make better song recommendations based off an inputted song?

<sup>[1]: [Tyler, The Creator slams Grammys..](https://www.cnn.com/2020/01/27/entertainment/tyler-the-creator-grammys-intl-scli/index.html)</sup>

---
### Methods
The data was acquired through the [Spotify API](https://developer.spotify.com/documentation/web-api/) alongside the [Spotipy library](https://spotipy.readthedocs.io/en/2.18.0/#). A Client ID, a Client Secret ID, and a Redirct URI is necessary to access the Spotify API, as well as to access the Spotipy Library, which any developer can do by sigining into the Spotify Devloper page.

The dataset included over 5000 songs, extracted from a JSON object returned from the API, ranging from genres of what users classified as Hip-hop, Pop, Alternative Metal, and Rock pulled from various user-created playlists. 

We want to score the model based on how correct it was in predicting the overall genre as well as taking a loss for predicting an incorrect genre. Since the severity of getting a genre wrong isn't high, the F1 score will be our metric since we want the model to get a general idea of what each genre may be. The f1-score won’t necessarily be extremely close to 1 because it may predict a hip-hop song as pop song and vice-versa and that line in actuality is sometimes blurred.  

When predicting the genres, the models consisted of Logistic Regressions, Gradient Boosted Classifiers, XGBoost Classifiers, and Voting Classifier. The data was altered using a combination of One Hot Encoder, SMOTE, Grid Search, Standard Scaling, Pipelines, or Normalization. When predicting for recommendations of songs, the model was the Nearest Neighbors with an n_neighbors of 15, the metric as cosine simliarity, and the radius of 0.45. 

  *Libraries Used*:
  
   - [Numpy](www.numpy.org)
   - [Pandas](https://pandas.pydata.org/)
   - [Spotipy](https://spotipy.readthedocs.io/en/2.18.0/#)
   - [Matplotlib](https://matplotlib.org/)
   - [Dotenv](https://www.npmjs.com/package/dotenv)
   - [Seaborn](https://seaborn.pydata.org/)
   - [OS](https://docs.python.org/3/library/os.html)
   - [Scipy](https://www.scipy.org/)
   - [Pickle](https://docs.python.org/3/library/pickle.html)
   - [SKLearn](https://scikit-learn.org/stable/)
   - [Imbalanced Learning](https://imbalanced-learn.org/stable/)
   - [XGBoost](https://xgboost.readthedocs.io/en/latest/)
   - [Shap](https://pypi.org/project/shap/)
   - [Streamlit](https://streamlit.io/)
    
---
### Results

Some Models Included: 
- FSM - Logistic Regression:
  - Training F1 Score:  0.63
  - Testing F1 Score:   0.62
 
- Logistic Regression + Pipeline(OHE + SS) + GridSearchCV:
  - Training F1 Score:  0.66
  - Testing F1 Score:   0.64

- XGBClassifier + OHE + SMOTE: 
  - Training F1 Score:  0.79
  - Testing F1 Score:   0.66
  
- **Voting Classifier ((GradientBoostingClassifier + OHE + SMOTE) + (XGBClassifier + OHE + Balanced Class Weight) + (RF + OHE + Balanced Class Weight))**
  - **Training F1 Score: 0.76**
  - **Testing F1 Score: 0.68**

The Voting Classifier yielded the best testing score (when comparing unrounded) with the lowest variance. The models were never expected to get a high f1-score but moreso learn the general idea of what each genre is while getting most of the genres correct. The wrong genres may not be actually wrong but that the song may actually belong to another genre. Following is the confusion matrix for the whole dataset with the best model:
<br>

<p align="center">
  <img  src="https://user-images.githubusercontent.com/38678270/127542159-61d76573-68fe-463f-a1ba-aeb0a3aac784.png">
</p>

With the nearest neighbors result, comparing the results is quite subjective. Although the model isn't quite perfect, I can say it gives some pretty good recommendations. From what I hear, I can make out why the songs recommended were recommended. <br><br>
<p align="center">
  <img  src="https://user-images.githubusercontent.com/38678270/127254200-9c07bb0e-7cf7-47b7-9c4d-e654a9df354b.png">
</p>

---
### Conclusion
We were able to first predict the genre of user inputted song and provide recommendations based off said song. Using the predicted genre rather than the artist's genre, we were able to provide users songs that relate to said song itself rather than having influence from the artist. The model isn't perfect when working with genres that it hasn't been trained on, but maybe adding songs from other genres, as well as more songs in general, can help the model predict better recommendations. 

---
### Further Exploration
  - Add more songs
  - Add more genres
  - More accurately predict genres for a song
  - Add a way to incorporate user listening history and predict songs from their history
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

- Try the [app](https://share.streamlit.io/jasonarikupurathu/music-recommendation-system/main/app.py) yourself!

- Please review the jupyter notebooks for analysis or view the [presentation](https://docs.google.com/presentation/d/1OVD3tPFMMoHLEK7HiTFsT0MCqxPxAglEr43XIT2fQG0/edit?usp=sharing).

---
### Github Directory


    ├── README.md                                         <- The top-level README for reviewers of this project
    ├── Notebook-1-Cleaning-Preprocessing.ipynb           <- Notebook for data cleaning and EDA
    ├── Notebook-2-Predict-Genre-Data-Modeling.ipynb      <- Notebook for genre prediction and model
    ├── Notebook-3-Nearest-Neighbors-Data-Modeling.ipynb  <- Notebook for music recommendations
    ├── app.py                                            <- Streamlit app of model
    ├── requirements.txt                                  <- Text file consisting of packages & package versions used for deployment   
    └── pickled_files                                     <- Contains Pickled Files
        └ df.pickle                                           <- DataFrame cleaned to predict genres pickled
        └ all_songs_genre_predicted.pickle                    <- Dataframe with genres predicted pickled
        
