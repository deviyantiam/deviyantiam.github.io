---
title: "House Price Prediction (Kubeflow)"
excerpt: "This project solely focuses on leveraging Kubeflow Pipelines for house price prediction, from organizing data, training model to saving it to GCS. Then it continues with deployment on kubernetes without getting into the details of methodology of building models. <br/>
    <img src='/images/kube_pipeline.png'>
"
collection: portfolio
---

**Project Description**
 
<span style="font-size: 12px;">[Click here to visit github repo](https://github.com/deviyantiam/house_price_kubeflow)</span>

This project focuses on using Kubeflow Pipeline to facilitate house price prediction model development without getting into model building methodology details. Google's team recommends Kubeflow as the preferred pipeline framework, especially for scenarios where your script does not utilize TensorFlow or manage large datasets, makes your pipelines easier to reuse. You can either create custom components or use existing ones. Due to my local resource constraints, Kubeflow is utilized up to model storage. Deployment involves Kubernetes with Docker, FastAPI, and Supervisorctl for the continuous operation of the API.

1. Develop a Kubeflow Pipeline for model training and storage.
2. Deploy the trained model on Kubernetes Locally. (unittest and loadtest script provided)


Include a Streamlit file for user interaction. If you opt to deploy on Google Cloud Platform (GCP), you can use App Engine for lower price and ease of management compared to Cloud Run.
![streamlit](/images/kube_streamlit.png)

### Developing a Kubeflow Pipeline for model training and storage

![pipeline](/images/kube_pipeline.png)

1. Download data
2. Prepare data (split into train test df)
3. Preprocess training data
4. Train model
5. Predict on test data
6. Get metrics
7. Store model to GCS

### Deploying the trained model on Kubernetes

![infra](/images/kube_infra.png)
1. Creating FastAPI Application and Utilizing Uvicorn
![unittest](/images/kube_unittest.png)
2. Configuring supervisor
3. Building and Pushing Docker Image to Hub
4. Deploy to kubernetes
![deploy](/images/kube_deploy.png)
5. Execute the images within pod and sending request to it
![postman](/images/kube_result.png)
6. Load test
tried 2 scenarios in locust,

    1. the number of users = 50 & spawn rate = 2 & duration 2m
    2. the number of users = 10 & spawn rate = 1 & duration 2m

where

- Number of Users: This determines the total load on the system being tested. More users mean more simultaneous interactions with the system
- Spawn Rate: This controls the rate at which users are introduced into the system. A higher spawn rate means more users are added quickly, ramping up the load on the system faster

![load testing](/images/kube_load_testing.png)
given chart, it shows that the response time increases a lot when running with 50 users (95th percentile ~4000ms) but when running with 10 users, it gets faster (400ms). For thorough analysis, we can compare the cpu usage and memory usage between those 2 scenarios. But for now, I'd say the system works well up to 10 users.

BTW I dont cover secret and load balancer, but for those interested in setting load balancer up on your local, try metallb

category: 
<button onclick="window.location.href='/data_analytics';">Data Analytics</button>
<button onclick="window.location.href='/nlp';">NLP</button>
<button onclick="window.location.href='/airflow';">Airflow</button>
<button onclick="window.location.href='/deployment';">Deployment</button>