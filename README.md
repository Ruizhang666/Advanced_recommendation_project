# Advanced_recommendation_project


Suumary for part I.

	1.	Data Loading and Parsing: We loaded movies.csv, users.csv, and ratings.csv, splitting movie titles into title and year and converting genres into multi-hot vectors.
	2.	Feature Transformation:
	•	Genres: Converted genres to multi-hot encoding.
	•	Title Embeddings: Used GloVe-Twitter-25 to convert movie titles into 25-dimensional vectors.
	3.	Data Splitting: Sorted data by timestamp and split it into 95% training and 5% test sets using index % 20 == 0.
	4.	User Embedding Strategy: Focused on the top 2500 most active users, responsible for 80% of the traffic, and used an Out Of Vocabulary (OOV) embedding for inactive users.
	5.	Metadata Creation: Created metadata for embeddings, categorical values, and OOV tokens to ensure consistent data processing.


 
