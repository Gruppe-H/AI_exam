# AI and Movies
### By Group H - Caroline and Maria
#### AI_exam

## Problem statement
Although there are many movies to choose from, it can be difficult to find a movie to watch. We have decided to use AI to make it easier, and we will achive this by creating three different models; one for user profiling and clustering, one for predicting movie success, and a chatbot to answer movie-related questions.

## Motivation
With the amount of streaming platforms and movies being produced each year, it should be easy to find an interesting movie to watch whenever you want. However, it can be quite overwhelming when you open up a streaming platform and see the many options, which can lead to decision fatique and disinterest. Therefor, we wanted to create an AI model for user profiling based on past watched movies, so we can use it to recommend new movies to the users. Futhermore, we also wanted to create a chatbot that can answer movie-related questions, so a viewer could get help when choosing what to watch. Lastly, since it can be expensive to both produce movies, but also for the viewer to watch new movies, we wanted to create an AI model that can predict the succes and revenue of new movies.

## Research questions
1. How can users' viewing histories and ratings be used to profile new users and for recommendations?
2. Which features influence the revenue of a new movie?
3. How can generative AI be used to make it easier for a person to choose a movie to watch?

## Argumentation

### Data
We have used these datasets:
1. Datasets from (IMDb)[https://datasets.imdbws.com/]
2. The review dataset from (kaggle.com)[https://www.kaggle.com/datasets/rmisra/imdb-spoiler-dataset?select=IMDB_reviews.json]
3. Movies_metadata.csv from (kaggle.com)[https://www.kaggle.com/datasets/rounakbanik/the-movies-dataset/code]. It contains 45466 entries and 24 different columns, incl. budget, revenue, popularity, votes, genres, and more.

We created a folder called 'Data' in the root of our project, but since the files were too big for GitHub, it has been ignored in commits. We have used data wrangling to preprocess the data to be able to use it for our different models.

### AI models and ML algorithms
We wanted to create the chatbot based on a Large Language Model.
The predictions are expected to be made with regression, and should predict revenue.
And for the recommendations we want to use clustering. 

#### Chatbot
The chatbot should be able to answer most questions a user could have about the movies on the page. Therefore, we first wanted to train our chatbot based on the movie data that we had, but since the movie plot_summary, plot_synopsis and reviews were made by users, we were unsure of how accurate the information was, and chose to collect data about the movies from wikipedia instead. 

So when designing it, we first found all the titles of the movies in the dataset and then found and loaded the wikipedia pages of those names. We also chose to load the more generic Wikipedia page called 'Film' that explains more in general what movies are. 

When we had collected our data, we used chunking to split the data, and vectorized it with `HuggingFaceEmbeddings`, so we could store the embeddings in a vector store called `Chroma`. We then trained a mistral model from Ollama on the embeddings. 

It was created mostly by Caroline.

##### Demo
We created a demo of the chatbot
https://github.com/Gruppe-H/AI_exam/assets/49302236/2baefb2f-6c79-4d44-bd79-458795c31d76

From our chatbot, we can conclude that it doesn't seem to be able to help a user find a movie to watch, but it can answer simple questions about a movie, which might still help a user decide wether or not to watch that specific movie. But as we wanted the viewer to have less options and movies to concider, as to not be overwhelmed by the choices, the chatbot is not very helpful. 

### User Profiling and Recommendations
We created multiple K-Means models, experimenting how we could best get recommendations based on the user's viewing history and previous reviews. We weren't satisfied with a lot of them, so we will not the describe the design of each, but just the design and process of the model, we chose to integrate into our [Movie Information System](https://github.com/Gruppe-H/DB_Exam_frontend), which is found in [this notebook](https://github.com/Gruppe-H/AI_exam/blob/main/profiling-Copy1.ipynb).

First, we collected and cleaned the movie information data and the user reviews data, and created some visualizations to gain more insight. We then cleaned the reviews and vectorized them using `TfidfVectorizer`. 

We wanted to use K-Means to cluster our movie and user data. To find the optimal amount of clusters ($k$), we fitted multiple K-Means models on the data with $k$=1 to $k$=50 and then created an Elbow Curve graph.
![Elbow Curve](https://github.com/Gruppe-H/AI_exam/assets/49302236/60c51306-c761-4dab-b879-5c841c831641)

Since we weren't very sure of the optimal $k$, we also tested the silhoutte score for $k$=1 to $k$=50 and plotted the silhoutte score.
![Silhouette Score](https://github.com/Gruppe-H/AI_exam/assets/49302236/4feb441a-db76-4dc8-a4fb-985416b5ffdd)

The optimal number of clusters seemed to be 32, so we used this amount to train our K-Means model. We wanted to plot the clusters, so we used Priciple Component Analysis (PCA) to reduce the dimensions to 2D and plotted the clusters.
![Movie Clusters PCA 2D](https://github.com/Gruppe-H/AI_exam/assets/49302236/e75996cb-0368-4214-adfd-2f1894910b4e)
Since the clustering seemed to overlab a lot, we also plotted the clusters in 3D.
![image](https://github.com/Gruppe-H/AI_exam/assets/49302236/96d41390-f4a3-4494-89dc-f9d87a14bf81)
We still weren't sure of the quality of the clustering, but wanted to see the predictions and recommendations our model would come up with for some different users. To test the quality of the recommended movies, we look at the user's previously liked movies and checked if the recommendations were new for the user. 

We concluded that although the recommendations weren't what we had expected, they were similar in some ways to the movies that the user had previously enjoyed and the overall ratings and reviews mattered in the recommendations.

We both worked on versions of this model.

### Movie Success Prediction
First, we collected and cleaned the data, handling missing and duplicated data. Then we visulied the data to gain more insight, including a pairplot to explore the correlations between different pairs of features. Then we split and tested the method of splitting our data.

We then used feature engineering to create some combined features; `budget_per_popularity`, `revenue_per_budget`, and `vote_count_per_revenue` and looked at the corelation matrix.
We then created a transformation pipeline to preprocess our data and trained a Linear Regression model.

Created mainly by Maria.

## Implementation
To run our chatbot follow these steps:

### Run Ollama

first check if ollama is running:
``` sudo lsof -i :11434```

- Enter your password.

Close Ollama if its running and you cant connect:
``` osascript -e 'tell app "Ollama" to quit' ```

Then in one terminal enter:
``` ollama serve ```

And in another enter: 
``` ollama run mistral ```

### Run frontend
Go to [this repo](https://github.com/Gruppe-H/DB_Exam_frontend) and clone it and follow the setup guide in the README. Then open a browser on [http://localhost:3000/chatbot](http://localhost:3000/chatbot) and ask questions. Or login with a user to see personalized recommendations. 

Note: The chatbot can be slow to answer.
