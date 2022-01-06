## Amazon SageMaker Overview

When it comes to Machine Learning (ML) and giving it as a service, it requires Data Engineering, ML, and DevOps expertise. While deploying a production model, several issues arise like versioning issues, problems in the model pipeline, etc. Solving out these issues is time-consuming. ML Research Scientists and practitioners at Amazon came out with a solution to run the entire pipeline of machine learning-powered by AWS called Amazon Sagemaker. With the availability of tools for every stage, various in-house tools are available to ease the model building and deployment.

Amazon SageMaker uses Jupyter Notebook and Python with boto to connect with the s3 bucket, or it has its high-level Python API for model building. The compatibility with modern deep learning libraries like TensorFlow, PyTorch, and MXNet reduces the model building time.


![image](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/jei1395jlo8nxkh9861z.png)
 

My Background: Cloud Engineer | AWS Community Builder | AWS Educate Cloud Ambassador | 4x AWS Certified | 3x OCI Certified | 3x Azure Certified.

**The Introduction to AWS Services** is a mini Series containing different articles that provide a basic introduction to different aws services. Each article covers the detailed guide on how to Use the AWS Service. This series aims at providing "A Getting Started Guide on Different AWS Services."

This Blog Post gives an Overview of Amazon SageMaker. It Talks about machine Learning Pipeline , Importance of using Amazon SageMaker , Data Preparation using SageMaker , Hyperparameter Tuning at SageMaker , Best practices for Amazon Sagemaker and Security at SageMaker among other topics.

## What is Machine Learning Pipeline?

A Machine Learning Pipeline is an executable workflow of the machine learning task. It helps to optimize, build, and manage ML workflows. Listed below are the features of the ML pipeline:

**Fetch data –** Get real-time data from Kafka streams or repository hosting data. SageMaker requires the data to be in an AWS s3 bucket for setting up the training job.

**Data Pre-processing –** This step involves data wrangling and data preparation for training. Data wrangling is one of the most time-consuming steps in a machine learning project. Amazon SageMaker Processing enables the running jobs to pre-process data for training and post-process for generating the inference, feature engineering, and model evaluation at scale.

**Model Training –** The pre-processing pipeline is for both training and testing data. Amazon SageMaker has popular algorithms already built in it. Import the library and use it.
The following is the working training pipeline at Amazon SageMaker:

1. import the training data from the s3 bucket.
2. The training is started by calling the ML to compute instances stored in the EC2 container registry.
3. The model artifacts s3 bucket store the trained model artifacts.

> Many different approaches are possible when using ML to recognize patterns in data.

![image](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/352k0wp3t3qfim2h25af.png)
 

## Why is Amazon SageMaker Important?

There are several important features of Amazon SageMaker to streamline the ML workflow. Listed below are the :

**Model Evaluation-** Evaluating a trained model on SageMaker in two ways offline testing or online testing. In offline testing, requests are made through Jupyter notebook’s endpoint on historical data (data separated previously) by validation set or using cross-validation. In online testing, the model is deployed, and a traffic threshold is set to handle requests. The traffic threshold is 100% if it is working fine.

**Model Deployment-** The model has crossed the baseline, and it’s time to deploy it: the trained model artifacts path and the Docker registry path of the inference code. In SageMaker, the model can be implemented by using CreateModel API, defining the configuration of HTTPS endpoint and creating it.

**Monitoring-** The model performance is monitored in real-time, the ground values of data are saved into s3, and the performance deviation is analyzed. This will give the instance where the drift started; then, it is trained on new samples saving in real-time in a bucket.

### Data Preparation using SageMaker 

A machine learning model depends entirely upon the data. Higher the data quality more efficient the model will be.

At Amazon SageMaker, the labeling of data is not too difficult. The user can either opt for the private, public, or vendor workforce. In the private and vendor, the user runs the labeling job on its own or uses third-party APIs, and it requires some agreement of confidentiality statements. In the public workforce, a service called Amazon Mechanical Turk Workforce creates a labeling job and gives the status of successful or failed labeled jobs. Below are the steps –

* Store data in the s3 bucket and define a manifest file for which the labeling job will run.
* Create a labeling workforce by choosing the workforce type.
* Create a labeling job by choosing the job type such as Image Classification, Text Classification, Bounding Box, etc.
* For example, the chosen job is of Bounding Box, then draw a bounding box around your desired object and give it a label.
Visualize your results by seeing the confidence score and other metrics.

![image](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/8hi4whfl0uo1bixnxrjo.png)
 

## What is Hyperparameter Tuning at SageMaker?

Parameters that define the model architecture Known as hyperparameters, and the process of searching for the ideal model architecture is called hyperparameter tuning. It consists of listed below methods:

**Random Search-** As the defined list of hyperparameters for the name implies, select the combinations at random, and a training job is run on it. SageMaker provides the concurrent running of jobs for finding the best hyperparameter without interrupting the current training job.

**Bayesian Search-** SageMaker has its Bayesian Search algorithm. The algorithm works by checking the performance of previously used combinations of hyperparameters in a job and explores the new combination using the supplied list.

## Steps for Hyperparameter Tuning

1. For the testing of a training task, the metrics are specified when developing a hyperparameter tuning work. Only 20 criteria can be specified for a single task; the parameters have a unique name with their regular expression to extract information from the logs.
2. The defined hyperparameter ranges for the parameter type, i.e., a distinction is between the parameter type in the ParameterRanges JSON object.
3. Create a notebook on SageMaker and connect with SageMaker’s Boto3 client.
4. Specify the bucket and data output location and launch the configured hyperparameter tuning job defined in step 1. and 2.
5. Monitor the progress of concurrently running hyperparameter tuning jobs and find the best model on SageMaker’s console by clicking on the best training job.
[Read more about How Hyperparameter Tuning Works.](https://docs.aws.amazon.com/sagemaker/latest/dg/automatic-model-tuning-how-it-works.html)

## Best practices for Amazon Sagemaker

**Defining the number of parameters:** To limit the search space and find the best variables for a model, SageMaker allows the use of 20 parameters in a hyperparameter tuning job.

**Defining the range of hyperparameters:** Defining a broader range for hyperparameters allows finding the best possible values, but it is time-consuming. Find the best value by limiting the range of benefits, and limit the search space for that range.

**Logarithmic scaling of hyperparameters:** If the search space is small, define hyperparameters’ scaling as linear. If the search space is a large opt logarithmic scaling because it decreases the running time of jobs.

**Finding the best number of concurrent training jobs:** More work done quickly in concurrent jobs, but the tuning jobs depend upon previous runs’ results. In other words, running a job can achieve the best results with the least amount of computing time.

**Running training jobs on multiple instances:** Running a training job on multiple instances uses the last-reported objective metric. For examining all the parameters, design a distributed training job architecture for getting the logs of the desired metric.

## What is Amazon SageMaker Studio?

SageMaker studio is for doing machine learning with a fully functional Integrated Development Environment (IDE). It is a unification of all the key features of SageMaker. In SageMaker Studio, the user can write code in the notebook environment, perform visualization, debugging, model tracking, and monitor the model performance in a single window. It uses the following features of SageMaker.

![image](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/vvj3qe2lm0wplsqi4v5n.png)
 
## Amazon SageMaker Debugger

The SageMaker debugger will monitor the values of feature vectors and hyperparameters. Store the logs of a debug job in CloudWatch, check the exploding tensors, examine the vanishing gradient problems, and save the tensor values in the s3 bucket. By placing SaveConfig from the debugger SDK at the instance where the value of the tensors needs to be checked and SessionHook will be associated at the start of every debugging job run.

![image](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/j0ewfzyj61c0g8zjq0ut.png)
 

## Amazon SageMaker Model Monitor

SageMaker model monitors the model performance by examining the data drift. The defined constraints and statistics file of features are in JSON. The constraint.json file contains the list of features with their type, and the required status is defined by the completeness field whose value ranges from 0-1, and statistics.json the file contains the mean, median, quantile, etc. information for each feature. The reports are saved in s3 and can be viewed in detail under constraint_violations.json which consists of feature names and type of violation (data type, min or max value of a feature, etc.)

## Amazon SageMaker Model Experiment

Tracking several experiments (training, hyperparameter tuning jobs, etc.) is easier than SageMaker. Just initialize an Estimator object and log the experiment values. It is possible to import values stored in the experiment into a pandas data frame and makes analysis easier.

![image](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/rqk9klqutcels1tj9z17.png)
 

## Amazon SageMaker AutoPilot

ML using AutoPilot is just a click away. Specify the data path and the target attribute(regression, binary classification, or multi-class classification) type. If not specified, the built-in algorithms automatically specify the target type and run the data preprocessing and model according to it. The data preprocessing step automatically generates Python code to use for further jobs. A defined custom pipeline use for it. DescribeAutoMlJob API.

> The Objective of the Machine learning pipeline is to exercise control over the ML model.


### Running custom training algorithms

* Run the dockerized training image on SageMaker
* The SageMaker calls a CreateTrainingJob the function which runs training for a specific period
* Specify the hyperparameters in TrainingJobName
* Check the status by TrainingJobStatus

## Security at SageMaker

**Cloud Security:** AWS uses a shared responsibility model, which involves security in the cloud by AWS for securing the infrastructure and security of the cloud, which involves the services opted by a customer, IAM key management, and privileges to different users, keeping the credentials secure, etc.

**Data Security:** SageMaker keeps the data and model artifacts encrypted in transit and rest. Requests for a secure (SSL) connection to the Amazon SageMaker API and console. Encrypted notebooks and scripts are using AWS KMS(Key Management Service) Key. If the key is not available, these are encrypted by using the transient key. After the decryption, this transient key becomes obsolete.

## What are the Advantages of SageMaker?

* It uses a debugger in training that has a specified range of hyperparameters automatically.
* Helps to deploy End to end ML pipeline quickly.
* It helps to deploy ML models at the edge using SageMaker Neo.
* ML compute instance suggests the instance type while running the training.

## Conclusion

AWS charges each SageMaker customer for the computation, storage, and data processing tools used to build, train, perform and log machine learning models and predictions, along with the S3 costs to maintain the data sets used for training and ongoing predictions. The SageMaker framework’s design supports ML applications’ and end-to-end lifecycle, from model data creation to model execution, and the scalable construction also makes it versatile. That means you can choose to use SageMaker independently for model construction, training, or deployment.

Hope this guide helps you understand on How to Get Started With AWS SageMaker, feel free to connect with me on [LinkedIn.](https://www.linkedin.com/in/adit-modi-2a4362191/)
You can view my badges [here.](https://www.youracclaim.com/users/adit-modi/badges)
If you are interested in learning more about AWS Services then follow me on [github.](https://github.com/AditModi)
If you liked this content then do clap and share it . Thank You .