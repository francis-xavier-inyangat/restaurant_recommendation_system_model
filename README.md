### **Project Documentation: Restaurant Recommendation System**

**Author: Xavier**
**Project Title: Hybrid & Item-Based Collaborative Filtering for Restaurant Recommendations**
**Dataset: Yelp Business & Review Data**

### 1️. Introduction

Choosing a restaurant can be overwhelming, especially with thousands of options available. Traditional recommendation methods, such as filters and manual reviews, often fail to capture personalized preferences effectively.

This project aims to develop an AI-powered recommendation system that suggests relevant restaurants based on business attributes and customer reviews. Using Item-Based Collaborative Filtering (CF) and a Hybrid Model (CF + Content-Based Filtering), we enhance the recommendation process by analyzing restaurant features, customer sentiment, and textual similarities.

### 2️.Objectives
	•	Develop a restaurant recommendation system based on business features and customer sentiment.
	•	Implement Item-Based Collaborative Filtering to recommend similar restaurants.
	•	Explore a Hybrid Model combining CF and Content-Based Filtering to improve diversity in recommendations.
	•	Evaluate the models using Precision@K, Recall@K, MAP@K, and NDCG@K.

### 3 Methodology

3.1 Data Preprocessing & Feature Engineering

To create a meaningful representation of each restaurant, we processed structured business data and unstructured review text:
	•	Extracted Business Features:
	•	stars_y (average restaurant rating)
	•	review_count (number of reviews)
	•	categories (TF-IDF vectorized for similarity calculations)
	•	Computed Sentiment Scores:
	•	Applied VADER Sentiment Analysis on customer reviews.
	•	Aggregated average sentiment per restaurant.
	•	Generated Restaurant Feature Vectors:
	•	Standardized numerical features (ratings, sentiment, review count).
	•	Vectorized restaurant categories using TF-IDF.
	•	Combined all features into a structured feature matrix.

3.2 Item-Based Collaborative Filtering (CF)

This approach recommends restaurants based on feature similarity rather than user interactions.
	•	Step 1: Compute Cosine Similarity between restaurant feature vectors (ratings, sentiment, categories).
	•	Step 2: Store the results in an Item-Based CF Similarity Matrix.
	•	Step 3: Generate recommendations by retrieving the Top-N most similar restaurants to a given restaurant.

Why Use Item-Based CF?
	•	Works without relying on user interactions (solves the user sparsity issue).
	•	Captures business feature similarities rather than relying on user behavior.

3.3 Content-Based Filtering (CBF)

This approach recommends restaurants based on textual similarity in descriptions and reviews.
	•	Step 1: Convert restaurant descriptions into TF-IDF Vectors.
	•	Step 2: Compute Cosine Similarity between restaurant descriptions.
	•	Step 3: Retrieve the Top-N most similar restaurants based on content similarity.

Why Use Content-Based Filtering?
	•	Works well for new restaurants with few reviews.
	•	Helps find textually similar restaurants, even if their ratings differ.

3.4 Hybrid Model: Item-Based CF + Content-Based Filtering

To improve recall while maintaining high precision, we combine Item-Based CF and CBF in a Hybrid Recommendation Model.
	•	Step 1: Compute Item-Based CF Similarity.
	•	Step 2: Compute Content-Based Similarity (TF-IDF on restaurant descriptions).
	•	Step 3: Merge both similarity scores using a weighted sum:

￼
	•	Step 4: Retrieve the Top-N most similar restaurants based on the hybrid similarity score.

Why Use the Hybrid Model?
	•	Balances rating-based and text-based similarity, increasing recall while maintaining precision.
	•	Works for both well-reviewed and new restaurants.

### 4. Model Evaluation

We evaluated our models using four ranking-based metrics:

4.1 Precision@K
	•	Measures how many of the Top-K recommendations are relevant.
	•	Higher Precision@10 means the model retrieves highly relevant results.

4.2 Recall@K
	•	Measures how well the system retrieves all relevant restaurants.
	•	Higher Recall@K ensures that the model does not miss relevant items.

4.3 Mean Average Precision (MAP@K)
	•	Evaluates how well relevant recommendations are ranked within the Top-K results.
	•	Higher MAP@K indicates strong ranking performance.

4.4 Normalized Discounted Cumulative Gain (NDCG@K)
	•	Measures how well the model orders relevant recommendations compared to an ideal ranking.

### 5️. Results & Performance

Model	Precision@10	Recall@10	MAP@10	NDCG@10
Item-Based CF	0.9000	0.0314	0.7071	0.8329
Hybrid (CF + CBF)	0.5000	0.0174	0.2222	0.5663
Content-Based Filtering	0.1000	0.0015	0.2929	1.0000

Key Observations:
	•	Item-Based CF achieved the highest precision (90%), meaning most recommendations were relevant.
	•	Recall was low across all models, indicating the need for improved diversity in recommendations.
	•	The Hybrid Model improved recall slightly but reduced precision due to noise from content-based filtering.

### 6. Challenges & Areas for Improvement

1️ Cold Start Problem for New Restaurants
	•	Restaurants with few reviews had poor similarity matches.
	•	Potential Fix: Introduce popularity-based fallback recommendations for sparse data.

2️ Over-Reliance on Certain Features (Category Bias)
	•	Some restaurant categories dominated similarity calculations.
	•	Potential Fix: Adjust TF-IDF category weighting dynamically.

3️ Limited Recall (Fails to Retrieve Enough Relevant Items)
	•	Recall@10 was low (~3%), meaning the model retrieved only a small fraction of relevant restaurants.
	•	Potential Fix: Increase content similarity weighting for restaurants with fewer ratings.

### 7️. Why BERT-Based Topic Modeling Failed

We attempted to use BERT-based topic modeling (BERTopic) to improve restaurant similarity but encountered issues:
	1.	Too Few Topics Were Extracted (Only 23 Topics for 1641 Restaurants)
	2.	Topic Similarity Scores Were Weak and did not meaningfully rank restaurants.
	3.	BERT Requires Large, Diverse Text Data, which our dataset lacked.
	4.	Topic Similarity Did Not Improve Recommendations, reducing ranking quality.

🔹 Best Solution: Item-Based CF performed better because it used structured business features (ratings, sentiment, review count, categories) rather than noisy topic embeddings.

### 8️ Conclusion & Final Takeaways

Our evaluation shows that Item-Based CF is the best performing model, achieving high precision (90%) and strong ranking quality. The Hybrid Model improves recall slightly but sacrifices precision. Future improvements should focus on increasing recall while maintaining strong ranking quality.”

- *Final Recommendation: Deploy Item-Based CF for best results.*
- *Future Work: Improve recall with a fallback popularity-based approach & deep learning-based embeddings.*

### 9️ Next Steps
	•	Deploy Item-Based CF as the primary recommendation model.
	•	Refine Hybrid Model to improve recall without reducing precision.
	•	Explore deep learning approaches (BERT sentence embeddings) for better text understanding.



