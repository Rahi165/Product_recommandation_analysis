# Product_recommandation_analysis
The Product Recommendation System is a machine learning project that offers customers customized product suggestions based on their past purchases and browsing activities. The system analyzes user activity and produces pertinent suggestions by using content-based filtering algorithms and collaborative filtering. The goal of this initiative is to enhance customers' entire purchasing experiences and boost e-commerce companies' revenues.

## Dataset
I utilized a user-rated Amazon dataset (which lacks headers) for electronic goods ratings. Each product and user is given a unique identification in place of their name or any other potentially biased information in order to prevent prejudices.
Link of dataset: https://www.kaggle.com/datasets/vibivij/amazon-electronics-rating-datasetrecommendation/download?datasetVersionNumber=1

## Approach
### 1) Top-Rated Product Recommendation
Objective- 

The aim is to recommend products based on their rating popularity, helping to:

- Highlight products with the most ratings.
- Introduce new customers to the most popular products.
- Mitigate the Cold Start Problem.

Outputs
- Provide the top 5 products that have received at least 50 or 100 ratings/interactions.

Approach

- Compute the average rating for each product.
- Calculate the total number of ratings each product has received.
- Organize these values into a DataFrame and sort it by the average rating.
- Develop a function to extract the top 'n' products meeting a specified minimum number of interactions.

### 2) Similarity based Collaborative filtering
Objective -
- Provide personalized and relevant recommendations to users.

Outputs -
- Recommend top 5 products based on interactions of similar users.

Approach -
- Here, user_id is of object, for our convenience we convert it to value of 0 to 1539(integer type).
- We write a function to find similar users -
-- Find the similarity score of the desired user with each user in the interaction matrix using cosine_similarity and append to an empty list and sort it.
-- extract the similar user and similarity scores from the sorted list
-- remove original user and its similarity score and return the rest.
- We write a function to recommend users -
-- Call the previous similar users function to get the similar users for the desired user_id.
-- Find prod_ids with which the original user has interacted -> observed_interactions
-- For each similar user Find 'n' products with which the similar user has interacted with but not the actual user.
-- return the specified number of products.
