*NOTE:* This file is a template that you can use to create the README for your project. The *TODO* comments below will highlight the information you should be sure to include.


# Operationalizing Machine Learning

In this project, we have used <a href= 'https://automlsamplenotebookdata.blob.core.windows.net/automl-sample-notebook-data/bankmarketing_train.csv'> Bank Marketing dataset </a> to train a machine learning model using AutoML feature of Azure Machine Learning Studio and later configure it for production and deploy it using Azure Container Instance and later consume it using REST endpoints. We will also create, publish and consume a pipeline.

## Architectural Diagram

<img src= 'https://docs.microsoft.com/es-es/azure/architecture/reference-architectures/ai/_images/ml-ops-python.png'>
<p> In this work we are going to find the architecture that we use to create the model and publish its respective pipeline based on the proposed models, the architecture is presented as follows:
<ol>

  <li>Register the Dataset</li>
  <li>Specify the dataset and configuration details such as machine learning task, here in our case its a classification task, exit criteria, etc. for selecting the best model           that AutoML will produce.</li>
  <li>Based on the metric selected in AutoML, select the best model and deploy it using azure container instance(ACI)</li>
  <li>Enable logging and application insight service for keeping track of deployed model performance and number of request handled/failed.</li>
  <li>After deployment and enabling the logs and application insights use the REST endpoint to interact with the deployed model with sample data and check its prediction results. </li>
  <li>Using python SDK create a pipeline selecting the best AutoML model and publish it.</li>
</ol>
</p>


## Key Steps
*TODO*: Write a short discription of the key steps. Remeber to include all the screenshots required to demonstrate key steps. 

## Screen Recording
*TODO* Provide a link to a screen recording of the project in action. Remember that the screencast should demonstrate:

## Standout Suggestions
*TODO (Optional):* This is where you can provide information about any standout suggestions that you have attempted.
