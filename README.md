# Introduction-Machine-Learning-Lab01
My first application of Machine Learning in practice.


This content is based on the Microsoft Azure AI Fundamentals Labs: https://learn.microsoft.com/en-us/training/paths/microsoft-azure-fundamentals-describe-cloud-concepts/ 



## Prerequisites

* An Azure subscription
* A Microsoft account
* Create an Azure Machine Learning Workspace

* Sign in to the Azure portal at https://azure.microsoft.com/en-us/get-started/azure-portal using your Microsoft credentials.
* Select "+ Create a resource," search for "Machine Learning," and create a new Azure Machine Learning resource.
* Configure the resource settings and create the workspace.
* Launch Azure Machine Learning studio (https://studio.azureml.net/).

  
  ## Use Automated Machine Learning to Train a Model

* In Azure Machine Learning studio, navigate to the Automated ML page.
* Create a new Automated ML job with the following settings:
* Job name: mslearn-bike-automl
* New experiment name: mslearn-bike-rental
* Description: Automated machine learning for bike rental prediction
* Task type: Regression
* Dataset: Create a new dataset named "bike-rentals" from the web URL: https://aka.ms/bike-rentals (refer to source material for detailed configuration)
* Target column: Rentals (integer)
* Allowed models: Select only RandomForest and LightGBM
* Limits:
* Max trials: 3
* Max concurrent trials: 3
* Max nodes: 3
* Metric score threshold: 0.085
* Timeout: 15
* Iteration timeout: 15
* Enable early termination: Selected
* Validation and test:
* Validation type: Train-validation split
* Percentage of validation data: 10
* Compute:
* Select compute type: Serverless
* Virtual machine type: CPU
* Virtual machine tier: Dedicated
* Virtual machine size: Standard_DS3_V2* (*choose any available size if restricted)
* Number of instances: 1
Submit the training job and wait for it to finish.
Note: Refer to the source material (https://learn.microsoft.com/en-us/training/paths/microsoft-azure-fundamentals-describe-cloud-concepts/) for detailed explanations and screenshots of each step.
![complete-run](https://github.com/lauracamarg0s/Introduction-Machine-Learning-Lab01/assets/116370422/5d87db03-c9f8-44ec-a076-6b5b35933c3f)


* Note: You may see a message under the status “Warning: User specified exit score reached…”. This is an expected message. Please continue to the next step.

* Select the text under Algorithm name for the best model to view its details.

* Select the Metrics tab and select the residuals and predicted_true charts if they are not already selected.

* Review the charts which show the performance of the model. The residuals chart shows the residuals (the differences between predicted and actual values) as a histogram. The predicted_true chart compares the predicted values against the true values.

## Deploy and test the model
* On the Model tab for the best model trained by your automated machine learning job, select Deploy and use the Web service option to deploy the model with the following settings:
* Name: predict-rentals
* Description: Predict cycle rentals
* Compute type: Azure Container Instance
* Enable authentication: Selected
* Wait for the deployment to start - this may take a few seconds. The * Deploy status for the predict-rentals endpoint will be indicated in the main part of the page as Running.
* Wait for the Deploy status to change to Succeeded. This may take 5-10 minutes.
* Test the deployed service
*Now you can test your deployed service.

* In Azure Machine Learning studio, on the left hand menu, select Endpoints and open the predict-rentals real-time endpoint.

* On the predict-rentals real-time endpoint page view the Test tab.

* In the Input data to test endpoint pane, replace the template JSON with the following input data:



```  {
   "Inputs": { 
     "data": [
       {
         "day": 1,
         "mnth": 1,   
         "year": 2022,
         "season": 2,
         "holiday": 0,
         "weekday": 1,
         "workingday": 1,
         "weathersit": 2, 
         "temp": 0.3, 
         "atemp": 0.3,
         "hum": 0.3,
         "windspeed": 0.3 
       }
     ]    
   },   
   "GlobalParameters": 1.0
 }

```
* Note: You may see a message under the status “Warning: User specified exit score reached…”. This is an expected message. Please continue to the next step.

* Select the text under Algorithm name for the best model to view its details.

* Select the Metrics tab and select the residuals and predicted_true charts if they are not already selected.

* Review the charts which show the performance of the model. The residuals chart shows the residuals (the differences between predicted and actual values) as a histogram. The predicted_true chart compares the predicted values against the true values.

## Deploy and test the model
* On the Model tab for the best model trained by your automated machine learning job, select Deploy and use the Web service option to deploy the model with the following settings:
* Name: predict-rentals
* Description: Predict cycle rentals
* Compute type: Azure Container Instance
* Enable authentication: Selected
* Wait for the deployment to start - this may take a few seconds. The * Deploy status for the predict-rentals endpoint will be indicated in the main part of the page as Running.
* Wait for the Deploy status to change to Succeeded. This may take 5-10 minutes.
* Test the deployed service
*Now you can test your deployed service.

* In Azure Machine Learning studio, on the left hand menu, select Endpoints and open the predict-rentals real-time endpoint.

* On the predict-rentals real-time endpoint page view the Test tab.

* In the Input data to test endpoint pane, replace the template JSON with the following input data:



* Click the Test button.

* Review the test results, which include a predicted number of rentals based on the input features - similar to this:

* Code

```
 {
   "Results": [
     444.27799000000000
   ]
 }

```

* The test pane took the input data and used the model you trained to return the predicted number of rentals.

* Let’s review what you have done. You used a dataset of historical bicycle rental data to train a model. The model predicts the number of bicycle rentals expected on a given day, based on seasonal and meteorological features.


## Clean-up
* The web service you created is hosted in an Azure Container Instance. If you don’t intend to experiment with it further, you should delete the endpoint to avoid accruing unnecessary Azure usage.

1) In Azure Machine Learning studio, on the Endpoints tab, select the predict-rentals endpoint. Then select Delete and confirm that you want to delete the endpoint.) )1

Deleting your compute ensures your subscription won’t be charged for compute resources. You will however be charged a small amount for data storage as long as the Azure Machine Learning workspace exists in your subscription. If you have finished exploring Azure Machine Learning, you can delete the Azure Machine Learning workspace and associated resources.

To delete your workspace:

1) In the Azure portal, in the Resource groups page, open the resource group you specified when creating your Azure Machine Learning workspace.
2) Click Delete resource group, type the resource group name to confirm you want to delete it, and select Delete.



