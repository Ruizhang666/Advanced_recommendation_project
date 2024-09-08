# Advanced_recommendation_project


1.	Offline Precomputation (Retrieval Stage):
	•	We used a retrieval model to precompute top 100 movie lists for each state.
	•	The retrieval model was optimized for speed by using simplified user and item embeddings based on state and movie IDs.
	•	These precomputed lists were stored in a feature store (represented as a pandas DataFrame) for quick access during online predictions.
2.	Online Prediction (Ranking Stage):
	•	For real-time recommendations, the system retrieves the precomputed list of movies for a user’s state from the offline store.
	•	The ranking model then refines this list by predicting the user’s rating for each movie based on richer user and movie features (e.g., genres, title embeddings, demographics).
	•	The final top 10 movies are selected and returned as recommendations based on the highest predicted ratings.
