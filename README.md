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

### 3) Model based Collaborative filtering

Objective -
- Provide personalized recommendations to users based on their past behavior and preferences, while also addressing the challenges of sparsity and scalability that can arise in other collaborative filtering techniques.
- 
Outputs -
- Recommend top 5 products for a particular user.
  
Approach -

- creating a CSR (compressed sparse row) matrix from the product rating matrix. Since only the non-zero values need to be saved, this is done to reduce the amount of memory and processing time used.
- taking the sparse or csr matrix and applying singular value decomposition (SVD) on it. A matrix's dimensionality can be decreased by applying the SVD matrix decomposition technique. In this instance, the product rating matrix's dimensionality is decreased to 50 latent features using the SVD.
- use SVD to determine each user's expected rating. The U matrix, the sigma matrix, and the Vt matrix are multiplied to provide the expected ratings.

### Evaluating the model :
- Calculate the average rating for all the movies by dividing the sum of all the ratings by the number of ratings. 2, Calculate the average rating for all the predicted ratings by dividing the sum of all the predicted ratings by the number of ratings.
- Create a DataFrame called rmse_df that contains the average actual ratings and the average predicted ratings.
- Calculate the RMSE of the SVD model by taking the square root of the mean of the squared errors between the average actual ratings and the average predicted ratings.
