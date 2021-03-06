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
### Create a new AutoML run
<section>
  <p> In this step, we have created an experiment using Automated ML, configured a compute cluster, and used that cluster to run the experiment. The below images shows the             dataset used, completion status of the experiment and the different models generated by AutoML. We can also notice that the best model generated is <b>voting ensemble           model </b> with an approximate accuracy of <b>91.8%</b>

     
  <p float="left">   
    <img src= 'https://github.com/fcgomezr/Udacity_project2/blob/main/process/task%202.1.png' width="100%" />
   </p>

  
  ### Deploy best automl model and consume the model endpoint via an HTTP API
<section>
  <p> In this step, we have deployed the best model(voting ensemle) whose details are shown in below images, we can see that :
    <ul>
      <li> we have enabled key based authentication so that only authorized users having the key can interact with the model, </li>
      <li> we have also enabled application insights to track the request received by the model enpoint and its performance and usage details and </li>
      <li> we have enabled the logging feature to capture the logs and check them, when required. </li>
    </ul>
  </p>

  <p float="left">   
    <img src= 'https://github.com/fcgomezr/Udacity_project2/blob/main/process/task%203.png' width="100%" />
   </p>

  
  #### Loggin Enable 
   
  
  <p float="left">   
    <img src= 'https://github.com/fcgomezr/Udacity_project2/blob/main/process/task%204.png' width="100%" />
    <img src= 'https://github.com/fcgomezr/Udacity_project2/blob/main/process/task%205.png' width="100%" />
   </p>
  </section>
  
  Also, we have used swagger tool that helps build, document, and consume RESTful web services like the ones we have deployed.It further explains what types of HTTP requests that an API can consume, like POST and GET. Azure provides a swagger.json that is used to create a web site that documents the HTTP endpoint for a deployed model.
  ### Publish an ML Pipeline
<section>
  In this step, we have used python SDK to create and publish the pipeline, whose details are shown and highlighted in below images. We can see that:
  <ul>
    <li> pipeline scheduled run details </li>
    <li> pipeline has been successfully created </li>
    <li> pipeline REST endpoint in active state </li>
  </ul>
  <p>
    <img src= 'https://github.com/fcgomezr/Udacity_project2/blob/main/process/task%2012r.png'/>
    <img src= 'https://github.com/fcgomezr/Udacity_project2/blob/main/process/task%2016.png'/>
    <img src= 'https://github.com/fcgomezr/Udacity_project2/blob/main/process/task%2015.png'/>
  </p>
</section>
  
  
  
### Future Project
    
<p> The project can be further improved by:
  <ul>
    <li> Creating an interactive frontend to display the deployed models prediction result instead of showing on git bash </li>
    <li> Get more user for testing so as to get service insights through <i> application insights </i> </li>
  </ul>
</p>
    
    ## Screen Recording
[![Operationalizing Machine Learning](http://img.youtube.com/vi/6hU1IKibDeQ/0.jpg)](https://youtu.be/ToWRj8m-LBI "Operationalizing Machine Learning")

