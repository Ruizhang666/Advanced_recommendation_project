# Advanced_recommendation_project


This project focused on building a recommendation system using TensorFlow Recommenders (TFRS) with both retrieval and ranking models. Throughout the project, we explored key techniques for providing recommendations, balancing accuracy, and exploration, and enhancing the visibility of lesser-known items. The system was built on the MovieLens 1M dataset, which includes 1 million movie ratings from users, and each milestone addressed a key element of modern recommender systems.

Project Breakdown by Milestones

Milestone 1: Data Preprocessing and Feature Engineering

In this milestone, we loaded and cleaned the dataset. The key objectives included:

	•	Splitting data into relevant features like title, genres, and year from raw text.
	•	Standardizing the user ZIP code to 5 digits and extracting city/state using the uszipcode library.
	•	Timestamp processing: We converted raw timestamps into more meaningful features like hour, day of the week, and month to capture user behavior patterns.
	•	Combining all features from the movies.csv, users.csv, and ratings.csv into a single dataset.

Milestone 2: Exploratory Data Analysis (EDA)

EDA was essential for understanding the distribution of the data and uncovering patterns:

	•	Activity Trends: Identified the most and least active hours, days, and months for user interactions.
	•	Demographic Trends: Analyzed user age groups, occupations, and gender ratios to understand user diversity.
	•	Geographic Trends: Studied how city and state influenced user traffic and activity.
	•	Movie Trends: Uncovered the most popular genres and the release years users tend to prefer.
	•	Ratings Distribution: Analyzed biases in user ratings and correlations between features and ratings.

Milestone 3: Building Baseline Models for RMSE Calculation

We calculated baseline Root Mean Squared Error (RMSE) to assess the simplest predictive models before implementing complex models. These baseline models included:

	1.	Random Guessing: Randomly predicted movie ratings.
	2.	Weighted Sampling: Based predictions on the distribution of ratings in the training set.
	3.	Majority Class: Predicted the most frequent rating (majority class).
	4.	Mean Value: Predicted the average rating.

The baseline RMSE was around 1.12, meaning any sophisticated model should aim to achieve an RMSE lower than this threshold.

Milestone 4: Two-Tower Model using TensorFlow Recommenders (TFRS)

We developed our first recommendation model using the two-tower architecture:

	•	User Tower: Consisting of features such as user_id, city, state, age, and occupation.
	•	Movie Tower: Using movie-specific features like movie_id, genres, title embedding, and year.
	•	Two-Tower Architecture: The model separately embedded the user and movie features into dense vectors and combined them to predict ratings.
	•	Loss Function: RMSE was used as the evaluation metric for the model’s performance.
	•	Retraining and Evaluation: The model was trained and evaluated with the goal of achieving an RMSE below 1.0.

Milestone 5: Retrieval Model for Implicit Feedback

The focus shifted to learning on implicit feedback using a retrieval model in TFRS, which is optimized for tasks like finding relevant items for users based on their behavior:

	•	Implicit Feedback: Rather than relying on ratings, the system considered user-movie interactions as positive feedback.
	•	FactorizedTopK: This metric was used to assess the top-k retrieval accuracy of the model.
	•	BruteForce and ScaNN: We experimented with using BruteForce for exhaustive retrieval and explored the faster ScaNN for large-scale approximate nearest-neighbor searches.

Milestone 6: Integrating Retrieval and Ranking Models

Here, we combined retrieval and ranking models to form a complete recommendation pipeline:

	•	Retrieval Model: Filtered out a large number of items and provided a shortlist of movies.
	•	Ranking Model: Used detailed features to predict the final ranking of the shortlisted movies based on user preferences.
	•	Feature Store: We created a feature store using a pandas DataFrame to store movie features (e.g., title, genres, year) that were needed by the ranking model for real-time predictions.
	•	Mimicking Online Prediction: The retrieval model outputted a list of movies, which was passed to the feature store and then through the ranking model to finalize the top 10 recommendations.

Milestone 7: Post-Prediction Exploration via Weighted Sampling

Exploration was introduced to combat the feedback loop problem. Post-prediction exploration involved weighted sampling to rerank movies based on their predicted ratings:

	•	Weighted Sampling: Movies with higher predicted ratings were more likely to be selected at the top, but lower-ranked movies still had a chance to surface.
	•	Reranking: We reranked movie lists multiple times (20–30 iterations) and visualized how the average rank across all rerankings remained close to the original prediction.

Milestone 8: In-Prediction Exploration with Gaussian Noise

In this milestone, we explored how to introduce randomness during prediction by adding Gaussian noise to the learned embeddings:

	•	Gaussian Noise Layer: We modified the user or movie embeddings during prediction by adding small, random perturbations, resulting in diverse predictions.
	•	Training vs. Prediction: Noise was only added during inference (prediction) to ensure that the training process remained unaffected.
	•	In-Prediction Exploration: This allowed the model to explore new recommendations while maintaining the core learned patterns.

Milestone 9: Least-Viewed Movies Exploration

The final exploration milestone tackled the cold start problem by incorporating least-viewed movies into the ranking process:

	•	Retrieval Model: Limited the number of retrieved movies to the top 10 from the retrieval phase.
	•	Least-Viewed Movies: We identified movies that had only been watched once and combined these with the retrieved top movies.
	•	Ranking Model: The final list of movies (top retrieved + least viewed) was passed through the ranking model, ensuring that lesser-known movies also had a chance to be ranked higher.
	•	Identification of Movie Sources: We identified which of the final top 10 movies came from the retrieval model and which came from the least-viewed list.

Key Techniques and Learnings:

	1.	Two-Tower Architecture: Separation of user and item embeddings into two distinct models, combined during prediction.
	2.	Retrieval and Ranking: Using a retrieval model to generate a candidate pool of items and a ranking model to finalize recommendations.
	3.	Exploration: Various exploration techniques such as post-prediction weighted sampling, in-prediction Gaussian noise, and least-viewed movie promotion to improve recommendation diversity.
	4.	Feature Store: Storing preprocessed features to efficiently retrieve data for ranking models during real-time predictions.
	5.	Feedback Loop Prevention: Introducing randomness and exploration to avoid the model reinforcing its own biases over time.

Conclusion:

This project successfully built a fully-fledged recommendation system that balances accuracy with exploration. We handled both ranking and retrieval models, incorporated various exploration strategies, and addressed issues like feedback loops and the cold start problem (least-viewed items). By doing so, we created a robust recommendation pipeline capable of delivering personalized and diverse recommendations to users.
