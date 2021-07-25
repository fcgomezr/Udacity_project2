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

### Future Project

Class imbalance is a very common issue in classification problems in machine learning. Imbalanced data negatively impact the model's accuracy because it is easy for the model to be very accurate just by predicting the majority class, while the accuracy for the minority class can fail miserably. This means that taking into account a simple metric like **accuracy** in order to judge how good our model is can be misleading.

There are many ways to deal with imbalanced data. These include using: 
1. A different metric; for example, AUC_weighted which is more fit for imbalanced data
2. A different algorithm
3. Random Under-Sampling of majority class 
4. Random Over-Sampling of minority class
5. The [imbalanced-learn package](https://imbalanced-learn.readthedocs.io/en/stable/)

There are many other methods as well, but I will not get into much details here as it is out of scope. 

Concluding, the high data imbalance is something that can be handled in a future execution, leading to an obvious improvement of the model.

* Another factor that I would improve is **n_cross_validations**. As cross-validation is the process of taking many subsets of the full training data and training a model on each subset, the higher the number of cross validations is, the higher the accuracy achieved is. However, a high number also raises computation time (a.k.a. training time) thus costs so there must be a balance between the two factors.

## Key Steps
### Registered Datasets

In first intance we update the dataset that we worked 

<p float="left">   
    <img src= 'https://github.com/fcgomezr/Udacity_project2/blob/main/process/datasets.png' width="100%" />
   </p>




### Create a new AutoML run
<section>
  <p> In this step, we have created an experiment using Automated ML, configured a compute cluster, and used that cluster to run the experiment. The below images shows the             dataset used, completion status of the experiment and the different models generated by AutoML. We can also notice that the best model generated is <b>voting ensemble           model </b> with an approximate accuracy of <b>91.8%</b>

     
  <p float="left">   
    <img src= 'https://github.com/fcgomezr/Udacity_project2/blob/main/process/task%202.1.png' width="100%" />
   </p>
  

 ###  Enable Application Insights
  
  
  
In the next step we run the log.py of the model,, the result is show next picture in script run successfully:
   <p float="left">   
    <img src= 'https://github.com/fcgomezr/Udacity_project2/blob/main/process/logrun.png' width="100%" />
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
  
  ### Consume Model Endpoints
  
  
For this case we must be careful, since the structure of the database that is in the endpoint is different from the one that was corrected in the swagger, the order of the variables is different, this can cause a mismatch in the endpoint and therefore reason may cause errors. This is solved by changing the input order of the [endpoint.py](https://github.com/fcgomezr/Udacity_project2/blob/main/process/endpoint.py "Operationalizing Machine Learning")
 data. 

<img src= 'https://github.com/fcgomezr/Udacity_project2/blob/main/process/endpoint.png'>

  
  Once the model is deployed, use the <endpoint.py> script provided to interact with the trained model.
  In this case the run endpoint.py created a new file with name data.json and display the next: 
  
  
  
  
  
  
  <img src= 'https://github.com/fcgomezr/Udacity_project2/blob/main/process/endpoint2.png'>

  
  
  
  ### Publish an ML Pipeline
<section>
  In this step, we have used python SDK to create and publish the pipeline, whose details are shown and highlighted in below images. We can see that:
  <ul>
    <li> pipeline scheduled run details </li>
    <li> pipeline has been successfully created </li>
    <li> pipeline REST endpoint in active state </li>
  </ul>
  
     
  <img src= 'https://github.com/fcgomezr/Udacity_project2/blob/main/process/task%2012r.png'/>
   
 
  
#### Jupyter Notebook showing the “Use RunDetails Widget” 
    
  <p>  
    <img src='https://github.com/fcgomezr/Udacity_project2/blob/main/process/rundetails.png'/>
    <img src= 'https://github.com/fcgomezr/Udacity_project2/blob/main/process/task%2016.png'/>
    <img src= 'https://github.com/fcgomezr/Udacity_project2/blob/main/process/task%2015.png'/>
  </p>
</section>

####  showing a REST endpoint and a status 
   
   <img src= 'https://github.com/fcgomezr/Udacity_project2/blob/main/process/pipelineactive.png'/>
   
  
  ## Screen Recording
      
[![Operationalizing Machine Learning](https://github.com/fcgomezr/Udacity_project2/blob/main/process/task%202.1.png)](https://youtu.be/KYdhStljgvc "Operationalizing Machine Learning")

