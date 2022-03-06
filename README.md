# MovieRecommendations

This project was based on using Movie data to create recommendations for users. Movie Recommendations worked by using simple recommendation algorithms in order to find movies which are like on another. 

# A little bit about recommendations systems

Recommendation systems are used by many different avenues of business from shopping, to streaming music and shows. Some popular companies which use a recommendation system algorithm are large sites like YouTube, Netflix, Spotify, Amazon, Twitter and Facebook. Product recommendations drive business for many of these businesses by exposing customers to new products or services which in turn boost sales or engagement with a platform. The aim of this project will be to create a simmple recommendation system similar to those already implemented. 

# Data 

Data will be based on MovieLens dataset for movie recommendation. The dataset ‘MovieLens 20M Dataset’ contains over 26 million movie ratings across 270,000 users for 45,000 movies, with an overview of each movie and which have been rated by users on the platform. Each Movie in the dataset consists of a title, cast, crew, director, keywords and overview. The data we will be using will be the movies_metadata.csv which consists of the movies metadata file, the keywords.csv which consists of movie plot keywords, credits.csv which consists of cast and crew information for each movie. The dataset was collected from TMDB and GroupLens for buildings of various recommender systems. There are a total 45,466 movies with 24 columns featuring the various categories in which a movie can be identified such as release date, revenue, budget, keywords/genres, votes, production companies and languages.

# Simple Weighted Rating

![image](https://user-images.githubusercontent.com/70538240/156903758-cb5a6316-596d-480b-9a44-eb5c8863e7a8.png)

The image above shows the average vote for each movie which landed at 5.618, this means that out of a 10 rating most movies fall in the 5-6 range with a lot of movie receiving 0’s from users and very few movies receiving 10’s. Factoring down the movies based on more votes we can create a feature score called ‘weighted rating’ which can look at a combined rating of the vote count and the vote average. The weighted rating of each movie is essentially calculated by: ((v/(v+m))R))+((m(v+m))C). This is a rating system created by IMDB to construct weights on movie rating based on total votes and the score of the vote. In this case v is the number of votes for a given movie, m is the minimum votes required to be accounted in the formula, R is the average voting score of the movie and C is the mean of all votes across the board. In this case we want to grab the 80th percentile of movies which is every movie which has received 50 or more votes. Applying our weighted rating is a very simple form of a recommendation system which gives us a rating of top movies in a dataset according to the weighted rating system. 

![image](https://user-images.githubusercontent.com/70538240/156903776-08032492-90ab-4834-8d60-7a78f8c123e7.png)

Looking at all of the movies in the list, I can agree that they are generally really good movies, and are critically acclaimed. There are a few movies in the list which I haven’t heard of such as ‘Dilwale Dulhania Le Jayenge’ which is an Indian-film which one of the most successful films of all time for the Indian film industry. It could be weighted in the list due to its low vote count and high score creating a higher weight for the movie. 

# Methods

The method for the project will consists of creating a content-based recommendation as well as a collaborative based recommendation system. The content-based recommendation system aims to use features in the MovieLens dataset in order to create scores for each movie which is used to measure the similarity between two different objects. We will be creating a Content Based Recommendation system which will give recommendations based on an input of an item. For example, if we want to get recommendations for the movie: 'Lord of the Rings: The Fellowship of the Ring' we would expect an output of other 'Lord of the Ring' movies. In this case we will want to use NLP in order to create good recommendations as we will be basing our recommendations on similar content. For this, we will be using the keywords dataset which consists of keywords for each movie which include actors, directors and main word features to describe the plot. In this case, we will be merging our keywords dataset, our credit dataset and our movies dataset to base our content off the cast, crew, keywords, genres and director. We will then use literal_eval as part of the ast library to evaluate our strings and create a ‘soup of these features. From here we will use a Count Vectorizer to transform our data into a matrix and then apply a Cosine Similarity matrix in order to create our recommendation based on the movie input. Cosine similarity is a method of measuring the similarity between 2 vectors in an inner product spaced. This is measured by the cosine of the angle between the two vectors and essentially measuring the similarity of two objects. This is often done in text analysis, where an object can be represented of many attributes such as keyword, or title. This is a term-frequency vector and will examine the occurrences across a vector. From here we will apply the similarity matrix into a function to recommendations by inputting a film title and using cosine similarity matrix to grab the top 10 most similar films within the matrix.
In order to get user recommendations as a basis for a recommendation system, we will also rely on a similarity score, but this time we plan to use Pearson’s correlation to determine the similarity between movies. Pearson’s uses correlation coefficients to compute the correlation between two random variables in a distribution, in this case we see the recommendations between user ratings on a movie. This method is best accomplished by pivoting our data set that we can see each user ID and the rating for movies that they have done, at this point by applying Pearson’s correlation to our data frame we will be able to retrieve movies based on user input, which is essentially a very baseline version of a user-based collaboration system. 

# Analysis

![image](https://user-images.githubusercontent.com/70538240/156903786-e116c53f-7e87-43b5-9106-fe5e33c6f4ae.png)

Our first iteration of the recommendation system shows the movies that are recommended after inputting the 3rd movie of the Lord of the Rings franchise, here we can see that all movies listed follow a fantasy genre except for Behind Enemy Lines which is not a very accurate recommendation based on the Lord of The Rings

![image](https://user-images.githubusercontent.com/70538240/156903792-237b7da7-d11e-42ab-8e68-fc002bf0d21e.png)

Similarly in the next iteration we can see that the recommendations for ‘Pulp Fiction’ return other Quentin Tarantino Movies. 

![image](https://user-images.githubusercontent.com/70538240/156903796-1f404d7a-3a3f-4e02-a5ad-66999cfdea9b.png)

The image above shows the first results for a collaborative filtering-based method for recommending movies, movies recommended fall into the crime/action/mystery genre, but do not necessarily seem to be the most similar movies. This is due to collaborative filtering basing recommendations directly off user scores and not the content included within the movies themselves. 

# Overall

Looking at the differences between the two-recommendation system, the Content-Based system using cosine similarity seemed to have better suggestions when it comes to recommendations which were like what title is being searched for. The Collaborative method seems to miss out on content and more so gives suggestions based on what users chose which accounted for taste and not necessarily the content of the movie. 

Challenges for this project lie on the quality of the recommendation dataset and the decision making when it comes to creating a quality dataset. Challenges lie with the using specifically content or user-based recommendation systems. It seems best to use a hybrid of the two for recommendations of similar content as well as content that is liked by users with similar taste. User-based recommendation seems better at capturing a ‘taste’ or type of content a user likes, while the content-based recommendation exceeds in providing content which is similar to what a user likes. For example, our content based recommendations will recommend other Lord of the Rings/Fantasy movies, while our user based content system should excel in recommending movies which have a similar rating across different users. 
