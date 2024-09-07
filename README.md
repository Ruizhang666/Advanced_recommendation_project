# Advanced_recommendation_project


Suumary 

	1.	Data Loading and Parsing: We loaded movies.csv, users.csv, and ratings.csv, splitting movie titles into title and year and converting genres into multi-hot vectors.
	2.	Feature Transformation:
	•	Genres: Converted genres to multi-hot encoding.
	•	Title Embeddings: Used GloVe-Twitter-25 to convert movie titles into 25-dimensional vectors.
	3.	Data Splitting: Sorted data by timestamp and split it into 95% training and 5% test sets using index % 20 == 0.
	4.	User Embedding Strategy: Focused on the top 2500 most active users, responsible for 80% of the traffic, and used an Out Of Vocabulary (OOV) embedding for inactive users.
	5.	Metadata Creation: Created metadata for embeddings, categorical values, and OOV tokens to ensure consistent data processing.


The two-tower model is a neural network architecture used for recommendation systems. It consists of:

User Tower:

	•	Embeds user-related features: user_id, city, state, age, occupation, and time-based features like hour, day, and month.
	•	Features are concatenated and passed through dense layers to generate a user representation.

Movie Tower:

	•	Embeds movie-related features: movie_id, title, genres, and year.
	•	These features are concatenated and passed through dense layers to produce a movie representation.

Combining Towers:

	•	The user and movie representations are multiplied element-wise, followed by further dense layers.
	•	The final output is a predicted rating.

Training:

	•	Loss: Mean Squared Error (MSE)
	•	Metric: Root Mean Squared Error (RMSE)

The two-tower model efficiently handles user and movie interactions, making it suitable for large-scale recommendation systems.
