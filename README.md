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

## Theoretical foundation
We wanted to create the chatbot based on a Large Language Model, 

## Argumentation
We wanted to train our chatbot based on the movie data that we had, but since the movie plot_summary, plot_synopsis and reviews were made by users, we were unsure of how accurate the information was, so we chose to collect data about the movies from wikipedia instead. 

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
Go to [this repo](https://github.com/Gruppe-H/DB_Exam_frontend) and clone it and follow the setup guide in the README. Then open a browser on [http://localhost:3000/chatbot](http://localhost:3000/chatbot) and ask questions. 

Note: The chatbot can be slow to answer.



#### Our project

- Create a chatbot, trained on review, plot and can be asked about a movie question.
- Create prediction of movie sucess
- Create user profiling and clustering based on past watched movies


### Business case

Select one or more business or social domains, where AI can bring value. Formulate a problem statement, context,
research question(s), and hypotheses for your AI solution.

### Data

Searching Internet and other media, find relevant data sources that can be used in your experiments.
Ingest and pre-process the collected data into proper data structures, applying data wrangling techniques. Explore
and explain the data by statistics and visualisation.

### AI Models

Select three or more AI methods and algorithms that could solve the problem. Create, train, and/or augment
relevant data models applying supervised or unsupervised machine learning, artificial neural networks, knowledge
graphs, or large language models.
Test the models created by the learners operating on test data sets, as well as on new data sets (training, test and
validation sets)

### Quality Assessment

Select appropriate statistics for measuring the quality of your models. Calculate measures assessing the quality of
the models and their ability to produce intelligent prediction, prescription, or generation.
Iterate the data modelling operations, improving the quality of the models, as much as possible.
Compare the assessment results and use them to select the best performing models. Save these models in data
stores for further implementation.

### AI Application

Implement the data and the successful AI operations into an interactive application with simple user interface,
presenting the process and results in human-understandable form.
Apply various visualisation and explanation techniques to guide the users through the application and interpret the
insights revealed by the AI algorithms.

Deploy the solution locally (on localhost) or on a cloud of your choice.
