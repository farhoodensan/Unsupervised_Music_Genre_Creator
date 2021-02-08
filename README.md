# Subverting Genre Norms with Unsupervised Clustering

DSC160 Data Science and the Arts - Midterm Project Repository - Spring 2020

<b> Project Team Members: </b>
- Farhood Ensan, fensan@ucsd.edu
- Rebecca Hu, reh016@ucsd.edu
- Alex Luo, ayl081@ucsd.edu
- Sharmi Mathur, s3mathur@ucsd.edu

## Abstract

(10 points)

  Genre as we know it classifies music based on a variety of not only musical qualities but social ones. Music might be associated with each other because of their time period, the artist who produced them, their popularity, and myriad other components that may have little to do with how the music actually sounds. We decided to see if an unsupervised machine learning algorithm might spurn the biases of our social expectations of genre and cluster songs by the similarity of their audio features alone. We hypothesize that while the way people classify genres has a lot of historical and social context inherently, a machine algorithm could potentially draw unique connections between songs based purely on the audio features.

  Inspired by genre classification using an SVM in class, we instead use unsupervised learning for genre classification. We will scrape different genres of audio data from freemusicarchive.org. With the librosa library, we will use the librosa.feature functions to extract the features MFCC, CENS, and spectral contrast. We will test hierarchical density-based clustering, k-means, and affinity clustering and examine the way the grouping results interact genre conventions. Results will be presented in graphs, charts, and sonification. Because the algorithm will only intake data about what the song sounds like, we hope that it will draw novel connections between unusual songs in a potentially genre-breaking way.


## Data

(10 points)

The cultural data source we use in our project is an audio dataset from Free Music Archive (FMA), an online audio library containing legal music from various genres and artists. The dataset was created in 2016 and contains data that is natively digital. This open-source dataset was created by Defferrard, et al. and more information regarding the collection and curation of this dataset can be found in [their paper](https://arxiv.org/pdf/1612.01840.pdf). The specific files we used for our analysis included features of audio files extracted using the Librosa library, as well as metadata regarding each track's associated genres and artist.


## Code

(20 points)

<b>Data Acquisition: </b>
- [Data Acquisition](https://github.com/ucsd-dsc-arts/dsc160-midterm-group2/blob/master/code/data_acquisition.ipynb): This notebook cleans the reorganizes the multi-indices in the <i>features.csv</i> and removes unnecessary columns to simplify our analysis. Note: Data can be downloaded from [this repository](https://github.com/mdeff/fma).

<b>Preprocessing: </b>
- [Feature Extraction](https://github.com/ucsd-dsc-arts/dsc160-midterm-group2/blob/master/code/Data_Sampling.ipynb) We chose 1600 of the many songs, 400 from each genre, randomly sampled. We had to make sure each of these songs were present in the small FMA dataset that was available.

<b>Analysis: </b>
- [EDA](https://github.com/ucsd-dsc-arts/dsc160-midterm-group2/blob/master/code/eda.ipynb): This notebook calculates some basic statistics on the dataset to gain a general understanding of how the genres are distributed and how long the tracks are on average. It generate outputs inline within the notebook.

<b>Clustering: </b>
- [Affinity Propagation](https://github.com/ucsd-dsc-arts/dsc160-midterm-group2/blob/master/code/affinity_propagation.ipynb): Affinity propagation is a graph-based clustering method that relies on the concept of passing messages between data points. Unlike many other clustering algorithms, affinity propagation does not require an inputted parameter to specify a fixed number of clusters.

- [Agglomerative Clustering](https://github.com/ucsd-dsc-arts/dsc160-midterm-group2/blob/master/code/Agglomerative_UMAP.ipynb): Hierarchical clustering is a general family of clustering algorithms that build nested clusters by merging or splitting them successively. Agglomerative clustering recursively merges the pair of clusters that minimally increases a given linkage distance. The linkage criteria determines the metric used for the merge strategy. We used the default ward which is a variance-minimizing approach and in this sense is similar to the k-means objective function but tackled with an agglomerative hierarchical approach.

- [DBSCAN with UMAP](https://github.com/ucsd-dsc-arts/dsc160-midterm-group2/blob/master/code/UMAP_DBSCAN.ipynb): DBSCAN is a density-based clustering method that divides the dataset into n dimensions. DBSCAN forms an n dimensional shape around each point in the dataset and counts how many data points are in said shape. Each shape is a cluster, and the clusters are iteratively expanded by going through every individual point. It essentially views clusters as areas of high density separated by areas of low density.

- [K-Means with PCA](https://github.com/ucsd-dsc-arts/dsc160-midterm-group2/blob/master/code/Kmeans_PCA.ipynb): The KMeans algorithm clusters data by trying to separate samples in n groups of equal variance, minimizing a criterion known as the inertia or within-cluster sum-of-squares. This algorithm requires the number of clusters to be specified.
PCA (Principal Component Analysis) is a technique which finds the major patterns in data for dimensionality reduction. It has been around for a very long time and it’s a linear algorithm.

- [K-Means with UMAP](https://github.com/ucsd-dsc-arts/dsc160-midterm-group2/blob/master/code/UMAP.ipynb): The KMeans algorithm clusters data by trying to separate samples in n groups of equal variance, minimizing a criterion known as the inertia or within-cluster sum-of-squares. This algorithm requires the number of clusters to be specified. UMAP stands for Uniform Manifold Approximation and Projection. It’s the new kid on the dimensionality reduction block. The idea is that it uses the nature of Riemannian Manifold to preserve the topology of the higher dimension as they are abstracted into lower dimensions, making its projection quite useful for analyzing our many dimensional. The results of UMAP are very similar to t-SNE but UMAP is faster and more applicable to different problems. 

- [MeanShift with UMAP](https://github.com/ucsd-dsc-arts/dsc160-midterm-group2/blob/master/code/UMAP_MEANSHIFT.ipynb): Mean Shift clustering is also a centriod-based clustering method that is similar to K-means, but does not need a set number of clusters in advance. MeanShift discovers "blobs" in a smooth density of samples. The algorithm iteratively updates each point to be at the top of its nearest KDE surface peak.

<b>Results:</b>
- [Cluster Characterization](https://github.com/ucsd-dsc-arts/dsc160-midterm-group2/blob/master/code/Cluster_Characterization.ipynb): We chose to explore the groupings created by the K-means UMAP because of the clarity of its groupings by listening to the music that is found in each grouping.

## Results

(30 points)

- [Affinity Propagation Results](https://github.com/ucsd-dsc-arts/dsc160-midterm-group2/blob/master/results/af_results.jpg): We concluded that affinity propagation was not an appropriate algorithm for our problem. The number of resulting clusters is not predefined with this algorithm and so we often obtained results with over 100 unique clusters. With this number of clusters, we found it difficult to uniquely identify characteristics of each cluster and difficult to visualize.

- [Agglomerative Clustering with UMAP Results](https://github.com/ucsd-dsc-arts/dsc160-midterm-group2/tree/master/results/Agglomerative_UMAP): We used UMAP to reduce the dimension of the data down to 2 and then we trained the afflomerative clustering algorithm. The resulting 4 clusters were very similar to kmeans with a slight difference in clustering borders in the graph. Because of this similarity, we chose to go with KMeans for the further analysis. 

- [DBSCAN with UMAP Results](https://github.com/ucsd-dsc-arts/dsc160-midterm-group2/tree/master/results/UMAP_DBSCAN): DBSCAN ended up not being the proper algorithm for our problem. It resulted in 27 unique clusters, even after measuring the optimal values for the parameters. It seemed to group together electronic and hiphop, as well rock songs with folk songs. All other clusters were small and varied mixes of the four genres. Considering that DBSCAN does not work well with high dimensional data, we could understand these results. However, we still have questions, as we applied the dimensionality reduction algorithm UMAP to the data. 

- [K-Means with UMAP Results](https://github.com/ucsd-dsc-arts/dsc160-midterm-group2/tree/master/results/Kmeans_UMAP): 
K-means in conjunction with UMAP feature reduction resulted in distinct clustering that had notable sonic differences. The charts here show that genre lines were not particularly influential in the groupings, but further listening analysis (see below) showed that songs put were still similar in other ways.

- [K-Means with PCA Results](https://github.com/ucsd-dsc-arts/dsc160-midterm-group2/tree/master/results/Kmeans_PCA): After reducing the dimension of the data down to 2 using PCA, the kmeans algorithm returned clusters that were mostly similar to the kmeans with UMAP, with one difference. Since PCA is a linear dimentionality reduction algorithm, the reduced data contained less useful information compared to the UMAP, and as a result did slighly worse than the UMAP version after comparing song samples for the clusters. For that reason, we went with Kmeans with UMAP for the full cluster analysis.

- [MeanShift with UMAP Results](https://github.com/ucsd-dsc-arts/dsc160-midterm-group2/tree/master/results/UMAP_MeanShift): MeanShift with UMAP ended up being a close runner up to the K-Means with UMAP algorithm. Mean Shift created similar, distinct clusters to K-Means. It can be seen, however, that electronic and hiphop music were once again confused, as well as folk and rock. Rock may typically be confused for folk, while folk would not normally be confused for anything else. We ultimately decided to go with KMeans and UMAP for its more distinct clusters.

<b>K-Means with UMAP Clustering Characteristics: </b>
- [Cluster Characteristics](https://github.com/ucsd-dsc-arts/dsc160-midterm-group2/blob/master/code/Cluster_Characterization.ipynb):
K-means together with UMAP seemed to have the most ideal results as far as unsupervised clustering went, so we chose these clusters to explore more in depth. In this notebook we reverse tracked the songs that were in each cluster, listened to some of those songs, and characterized the nature of those clusters. We found that in some ways it almost feels that we've stumbled upon a sentiment classifier. A lot of the songs retain the auditory distinctions of their genre, but they are instead grouped around other songs of different genre that simply communicate a similar sonic feeling.

  #### Cluster Bottom Center
  Mood: Heavy/Amped

  Noisy, aggressive sounding music. Driving kick beat and rhythms. Heavy drums, aggressive electric guitar.

  #### Cluster Left
  Mood: Ethereal, Spacious

  Mellow vibe in this cluster, with a reverbrating, floating quality. Mid to slow tempo, melodic lines. Lack notable drum presence. Acoustic guitar, piano/keyboard.

  #### Cluster Top Center
  Mood: Rhythmic/Chill

  Mid tempo but still with a forward driving rhythm. Kickdrum/bassline/downbeats are quite present, but the sounds are still quite relaxed. Heavy drum beats act as a backbone for the song, but melodies have softer feel to them.

  #### Cluster Right
  Mood: Glitchy/Synth

  Heavily synthetic computer generated sounds with high tempos. Almost all hip hop and electronic music. Extremely electronic, almost dubstep-esque. Even the folk songs have a more synth-like quality to them.

## Discussion

(30 points)

The UMAP feature reduction combined with K-means seemed to have the clearest results, yielding the interesting perspective that the genre is not all that predictive of audio groupings. By listening to the tracks in each cluster, we found that the songs nearly seemed to have been categorized into mood/sentiment, the descriptions of which are above. This affirms a hypothesis that a classification of music based purely on audio features would actually be very different from the way genres group music through a myriad of social constructs.

The way that songs are thought to be classified into genres can be described as hierarchical in nature. There are broad buckets that most songs fit into, and then some songs can be further classified into subgenres. However, the labeled genre of a song can also be influenced by non-musical factors, like who the artist is or other cultural and societal reasons. The results of our project suggest that genres of music may be more fluid than we previously believed. We intentionally chose songs from four very distinct genres (Rock, Hip Hop, Electronic, and Folk) to see how an unsupervised algorithm would form new clusters of similar songs along novel dimensions based on Librosa-derived audio features.

Factors that go into determining a song’s genres include, but are not limited to, its audio qualities, the artist(s) that created the piece, the time period during which it was made, and its lyrics. Although there is no objectively correct way of categorizing music, generally we assume to only find music with similar audial characteristics within a particular genre. However, if an artist typically known for their rock music releases a song with heavy folk influences, it is possible that the song could lack a “folk” genre label, even if such a label would be appropriate. We sought to explore how songs might be classified into genres if only the audio features, rather than any metadata, of the music were used to determine what category each song belonged to.

Having listened to a variety of the clustered tracks, it would be interesting to hear from the artists what their personal goal for the sound was and compare it to the groupings that their music was ultimately placed in. They might be surprised that, to a computer’s purely audio based interpretation, their rock songs might be considered much more similar to a folk or hip hop song than other rock songs. We’d hope that this would inspire musicians to not restrict themselves to a certain genre; rather they should be free to make the music they want. Genre is fluid and classifying a song can be subjective, especially when many elements of different genres could be incorporated.

Future directions for this project could include refining the resulting visualizations to include tooltips that would allow users to listen to the audio files as they scroll over each data point on the scatterplot. This would allow for a user-friendly interface to allow us to characterize the resulting clusters more efficiently. Given more time, we would have also liked to try more clustering algorithms as well as different feature selection methods.



## Team Roles

- Farhood Ensan: Farhood implemented KMeans with PCA and the Agglomerative clustering with UMAP. He helped other members with visualization and helped writing different parts of the report.
- Rebecca Hu: Rebecca created the EDA and affinity propagation notebooks. She listened to the tracks in each of the clusters to help characterize the mood of the songs. She also contributed by writing several sections in the final report.
- Alex Luo: Alex implemented KMeans clustering with UMAP. He also generated the sample features file consisting of 1600 tracks that we used to train all our models. He listened to the tracks in each of the clusters to help characterize the mood of the songs. He participated in writing different parts of the report as well.
- Sharmi Mathur: Sharmi did the initial data cleaning and data acquisition. She implemented the density-based clustering algorithm DBSCAN and centroid-based clustering algorithm Mean Shift with UMAP. She also wrote different parts of the final report.

## Technical Notes and Dependencies

Non-DataHub Libraries:
- Plotly
- Librosa
- Umap-learn
- Sklearn

## Reference

References to any papers, techniques, repositories you used:
- https://github.com/roberttwomey/dsc160-code/blob/master/examples/audio-cluster-dim-reduction.ipynb
- https://arxiv.org/pdf/1612.01840.pdf
- https://github.com/mdeff/fma
- https://towardsdatascience.com/how-to-cluster-in-high-dimensions-4ef693bacc6
- https://medium.com/latinxinai/discovering-descriptive-music-genres-using-k-means-clustering-d19bdea5e443
