# Automated Playlist Creation Using K-Means Clustering on Spotify Audio Features

## Project Overview

Moosic is a startup that curates playlists by hand, but their team of music experts can't keep up with growing demand. This project explores whether Spotify's numerical audio features (danceability, energy, valence, tempo) are enough to automatically group ~5,000 songs into clusters that could serve as playlists. We test DBSCAN for outlier detection and K-Means for the actual clustering, and evaluate the results both statistically (silhouette scores) and by manually inspecting the generated playlists.

## Dataset & Sources

- **Source**: [Spotify Web API - Audio Features](https://developer.spotify.com/documentation/web-api/reference/get-audio-features)
- **Size**: 5,235 songs, 19 columns (5,112 after deduplication)
- **Key Features Used**: danceability, energy, valence, tempo
- **Limitations**: No genre labels, no lyrics, no user listening data. Only numerical audio characteristics computed by Spotify from the raw audio signal.

## Key Findings & Results

- **DBSCAN found no meaningful outliers.** The data is too uniformly distributed across the 4 selected features for density-based methods to find structure. Every eps setting either produces one giant cluster or arbitrary splits with negative silhouette scores.
- **K-Means with k=46 produces musically coherent playlists.** Clusters clearly separate calm jazz/classical tracks from high-energy dance music and upbeat feel-good songs.
- **Silhouette score of 0.21** with only 4.8% of songs having negative silhouette values (likely misplacements). Moderate but consistent.
- **Feature selection was the most impactful decision.** Reducing from 9 to 4 features (removing skewed and redundant ones) improved playlist coherence significantly.
- **Audio features capture energy, not genre.** Songs with similar audio profiles end up together even if they're from completely different genres. Jazz and classical mix, reggaeton sits next to rock.

## Technologies Used

- **Programming**: Python
- **Libraries**: pandas, numpy, scikit-learn, matplotlib, seaborn
- **Machine Learning**: K-Means Clustering, DBSCAN, MinMaxScaler, Silhouette Analysis
- **Environment**: Jupyter Notebook

## Project Structure

```
music_playlist_clustering_spotify/
|
|- README.md                          # This file
|- moosic_playlist_clustering.ipynb   # Full analysis notebook
|
|- data/
   |- 3_spotify_5000_songs.csv        # Original dataset (5,235 songs)
```

## Visualisations

The notebook contains the following key plots:

- **Audio feature distributions** showing the spread of all 11 features across the dataset
- **Correlation heatmap** revealing which features overlap and which are independent
- **Elbow and silhouette plots** for choosing the optimal number of clusters
- **Silhouette blade plot** showing how well each individual song fits its assigned cluster

## How to Use This Project

1. **Main Analysis**: Open [moosic_playlist_clustering.ipynb](moosic_playlist_clustering.ipynb) to see the full workflow from EDA through clustering to evaluation
2. **Data**: The dataset is included in the `/data` folder
3. **Run the Code**: Open the notebook in Jupyter and run all cells top to bottom
4. **Dependencies**: Standard data science stack (pandas, numpy, scikit-learn, matplotlib, seaborn)

## Future Work

- **Genre data**: Pulling genre labels from the Spotify API would immediately improve cluster coherence
- **User listening data**: What songs people actually play back-to-back captures the subjective "vibe" that audio features miss
- **Post-processing**: Splitting oversized clusters and merging small ones to hit the ~50 song editorial target
- **NLP on lyrics**: Adding a text dimension could help separate songs that sound alike but feel different
- **Semi-supervised refinement**: Using feedback from Moosic's music team to gradually improve the clusters

## Contact

- **GitHub**: [Robin-Reiche](https://github.com/Robin-Reiche)
