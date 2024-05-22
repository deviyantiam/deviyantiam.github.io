---
title: "Restaurant Recommendation"
excerpt: "This project helps people in Nashville find great restaurants easily. We use a hybrid method to make personalized recommendations for users, collaborative filtering and content-based filtering. I also handle cold start. <br/>
    <img src='/images/restaurant_result_new_user.png'>
"
collection: portfolio
---

**Project Description**
 
<span style="font-size: 12px;">[Click here to visit github repo](https://github.com/deviyantiam/resto_reco)</span>

This project aims to help people in Nashville find great restaurants easily. We use hybrid method to make personalized recommendations for users.

**Data**
restaurant&review:[here](https://www.kaggle.com/datasets/yelp-dataset/yelp-dataset/data)

zip code coordinate: [here](https://www.kaggle.com/datasets/jedwible/uszipcodes-20231227)


**Method**

- Collaborative Filtering:
Utilizing the Surprise library, we implement collaborative filtering to predict user preferences based on their past ratings and those of similar users. Multiple collaborative filtering algorithms are explored, including Singular Value Decomposition (SVD), Non-negative Matrix Factorization (NMF), and NormalPredictor. Hyperparameter tuning is conducted to optimize model performance, with the selection of the model with the lowest Root Mean Square Error (RMSE) against actual ratings

![model result](/images/restaurant_model.png)


![hyperparameter_tuning](/images/restaurant_hypertuning.png)

- Content-Based Filtering:
we use Latent Dirichlet Allocation (LDA) to extract topics from restaurant reviews. By combining these topics with available restaurant categories, we compute similarity scores between restaurants, enabling us to recommend restaurants that align closely with a user's preferences based on past experiences

Handling Cold Start:
For new users lacking sufficient historical data, we tackle the cold start problem by initially recommending restaurants with the highest average ratings within the user's zip code

Expected Outcome:
Our system combines collaborative filtering and content-based filtering within the user's chosen distance.  If we can't find any good options nearby or no data available, we'll tell the user clearly with a message saying "no results found."

Include a Streamlit file for internal user interaction and it provides a map visualization featuring restaurant markers.

![result](/images/restaurant_result.png)

![cold_start](/images/restaurant_result_new_user.png)

category: 
<button onclick="window.location.href='/machine_learning';">Machine Learning</button>
<button onclick="window.location.href='/recommendation_system';">Recommendation System</button>