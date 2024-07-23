# Machine Learning Project Report - Nicolas Debrito

## Project Overview

In recent years, the novel publishing industry has experienced significant growth. With the increasing number of novels published each year, readers often face the challenge of finding books that suit their tastes. Along with the development of technology, online platforms for reading and purchasing novels, such as Goodreads, Amazon, and various other reading apps, have become increasingly popular. One platform that also provides lists of published novels is MyAnimeList, which was originally known as a database for anime and manga, but now also includes light novels and other novels. However, the sheer number of options available can make the process of selecting the right novel very complicated and time-consuming.

A system such as a recommendation system can provide an effective solution to this problem. By analysing the user's preferences and reading patterns, recommendation systems are able to suggest novels that suit individual interests. This technology not only improves users' reading experience, but also helps online platforms improve user retention and increase book sales. 

According to (Lu, 2015) a common solution in recommendation systems is to use Content-based Filtering, where content is analysed before being presented to the user. However, this approach usually works well when users have sufficient reading records. Another major challenge is the lack of feedback from users. Since reading novels is usually not the main function of the platform, users may not provide enough feedback even if they are interested in the recommended content. The solution to this problem is to use a Collaborative Filtering approach, where users who provide feedback can help predict the interests of other users who rarely provide feedback.
  
References: Lu, Z., Dou, Z., Lian, J., Xie, X., & Yang, Q. (2015, February). [Content-based collaborative filtering for news topic recommendation](https://ojs.aaai.org/index.php/AAAI/article/view/9183). In Proceedings of the AAAI conference on artificial intelligence (Vol. 29, No. 1).

## Business Understanding

### Problem Statements

- How can users find novels that match their interests?
- How can a recommendation system help users find novels?
- Can the use of content based filtering and collaborative filtering help users find suitable novels?

### Goals

- Develop a search and filter that allows users to easily find novels based on their requests.
- Help analyse users' preferences and reading patterns to suggest relevant novels.
- Describe and evaluate the effectiveness of using content-based filtering and collaborative filtering in a novel recommendation system.

### Solution statements
- Use content-based filtering to analyse novel content features such as genre based on user preferences and previous reading patterns. The system will recommend novels that have similar features with novels that have positive responses from users.
- Using collabortive filtering to provide recommendations based on interaction patterns and feedback from many other users who have similar preferences.

## Data Understanding
The dataset used consists of 2 csv files, namely, novels containing a list of novels contained in the platform such as novel_id, title, synopsis, type, number of chapters, genre, author, status, release year, etc. 4209 lines and interactions containing user interactions in the platform such as username, novel_id, and interests 119295 lines. [Kaggle: MyAnimeList Novel Recommendation Dataset](https://www.kaggle.com/datasets/asad11914/myanimelist-novel-rating-dataset).

### The variables in the dataset are as follows:

novels.csv: list of novels

- novel_id: The id number of the novel
- title: Title of the novel
- title_eng: Title of the novel in English
- synopsis: Synopsis of the novel
- type: Novel type (light novel/novel)
- n_chapters: Number of chapters
- authors: Author
- genres: Genre of the novel
- n_volumes: Number of volumes
- status: Publication status
- score: Score of the novel
- scored_by: Number of users who entered the score
- popularty: Popularity score
- favourites: Number of favourites
- year_start: Year of release
- year_finnish: Year finished
- image: URL of the image

interactions.csv: user interactions
- username: user name
- novel_id: The id number of the novel
- interest: User interest 1 (interested) and 0 (not interested)

## Data Preparation

### Content-based Filtering

**Drop Missing Value**

Removing data containing missing values This approach is used because the number of missing values is relatively small and does not have a significant impact on the analysis or model performance.

**Drop Duplicate**

Dropping duplicates is used to ensure that analyses and models are based on unique and accurate data. In this project, dropping duplicates is done based on novel_id in order to get a unique value for each novel.

**Feature Selection**

Feature selection is used to select relevant features in a dataset, with the aim of improving the performance of machine learning models. This technique identifies and selects the features that are most influential in predicting whether a device is efficient or not. In this project the features to be used are id, title, genre.

### Collaborative Filtering

**Encoding & Decoding**

Encoding is used to convert categorical data into a format that can be used by machine learning algorithms. In addition, decode is also used to process the encoded data into its original format.

**Train Validation Split**

Train Validation Split is used to split the data that will become training data and data for validation in the model. In this project, the split is 80% for the trainset and 20% for the validationset.

## Modelling

1. **Content-based Filtering - Cosine Similarity**

Content-Based Filtering is a recommender system approach that uses the attributes of the items desired by the user to make recommendations. The system analyses various features of novel items in the form of novel genres and tries to recommend similar items. The cosine similarity model is used to measure the similarity between two vectors. It is used in recommendation systems to calculate the similarity between two entities, such as the similarity between two novels. Cosine Similarity measures the cosine angle between two vectors, which indicates how similar they are to each other.

Advantages:
- The system does not require data from other users to provide recommendations.
- New items can be recommended as soon as they are indexed, without waiting for user ratings.

Disadvantages:
- The quality of recommendations is highly dependent on the quality and completeness of item features.
- Tends to recommend items similar to those already favoured, thus reducing diversity and exploration.
- Cold start: If a new user has no preference history, the system cannot provide good recommendations.

Result:

![image](https://raw.githubusercontent.com/Reezzcy/Machine-Learning-Recommender-System/main/assets/Content-based_Filtering_Target.png)

![image](https://raw.githubusercontent.com/Reezzcy/Machine-Learning-Recommender-System/main/assets/Content-based_FIltering_TopN.png)

2. **Collaborative Filtering: User-based - RecommenderNet**

Collaborative Filtering using user-based is a recommendation system approach that uses information from user-item interactions to make recommendations. It identifies patterns from other users' preferences similar to the target user to recommend items. The RecommenderNet model uses neural networks to predict user preferences for novels based on user interaction data. This model can capture the complex relationship between users and novelties.

Advantages:
- Can provide more varied recommendations as it utilises preferences from multiple users.
- Can recommend items that are not similar to the user's history but favoured by other users with similar preferences.

Disadvantages:
- Managing interaction data from multiple users and items can require large computational resources.
- Cold start, new items or users with no interactions are quite difficult to recommend.

Results:

![image](https://raw.githubusercontent.com/Reezzcy/Machine-Learning-Recommender-System/main/assets/Collaborative_Filtering_TopN.png)

## Evaluation

**Content-based Filtering**

The results of the Top-5 novel recommendations for Shousetsu Sousou no Frieren: Zensou which has the genres Adventure, Drama, Fantasy has the following Top-5 results:

![image](https://raw.githubusercontent.com/Reezzcy/Machine-Learning-Recommender-System/main/assets/Content-based_FIltering_TopN.png)

Based on the recommendation of novels with similar genres, namely Adventure, Drama, Fantasy, it is found that all novels have at least 2 similar genres. So that the precision of the content-based filtering-based recommendation system that has been made successfully reaches 5/5 or 100%. 

Formula: 

Precision: Total Correct Recommendation Items/Total Recommendation Items

- Total Correct Recommended Items: the number of total items recommended by the model according to the user's preferences. If the model recommends 10 items but only 5 are appropriate then the Total Correct Recommended Items is 5.
- Total Recommended Items: The sum of all items recommended by the model. If the model recommends 10 items then the Total Recommended Items is 10.

**Collaborative Filtering**

The results of Tetsuka-B's Top-10 user recommendations. Tetsuka-B has a preference for novels in the School, Strategy Game, Action, Fantasy, Romance, Mythology, Adventure genres.

![image](https://raw.githubusercontent.com/Reezzcy/Machine-Learning-Recommender-System/main/assets/Collaborative_Filtering_TopN.png)

From recommendations other than Roman Album: Taishou Dennou Dadaism Emaki - Despera : Sci-Fi, Suspense, Psychological other novels have at least 1 genre from Tetsuka-B's preferences. So that the precision of the collaborative filtering-based recommendation system that has been made successfully reaches 9/10 or 90%.

Formula: 

Precision: Total Correct Recommended Items/Total Recommended Items

- Total Correct Recommended Items: the number of total items recommended by the model according to the user's preferences. If the model recommends 10 items but only 5 are appropriate then the Total Correct Recommended Items is 5.
- Total Recommended Items: The sum of all items recommended by the model. If the model recommends 10 items then the Total Recommended Items is 10.

![image](https://raw.githubusercontent.com/Reezzcy/Machine-Learning-Recommender-System/main/assets/Plot_RMSE.png)

RMSE is a metric that gives an idea of how much the average model prediction error is in the same units as the target data.

Formula:

![image](https://raw.githubusercontent.com/Reezzcy/Machine-Learning-Recommender-System/main/assets/RMSE.jpg)

Description:
- N = number of datasets
- Actual = actual value
- Predicted = predicted value

To answer business questions, to help users find novels that match their interests, an effective and efficient recommendation system is needed. Recommender systems can play an important role in this process by analysing and understanding user preferences to provide relevant suggestions. To achieve this, the system can utilise two main approaches: Content-Based Filtering and Collaborative Filtering. In this project, content-based filtering achieved 100% precision and collaborative filtering achieved 90% precision and 0.1347 rmse. This suggests that content-based filtering and collaborative filtering models can improve the effectiveness of recommendation systems, allowing users to find novels that match their interests more accurately. Content-Based Filtering ensures that recommendations are relevant to specific content preferences, while Collaborative Filtering expands the scope of recommendations by utilising social interaction patterns.