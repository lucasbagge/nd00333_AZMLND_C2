# How to operationalize a Machine Learning project with Azure ML

In this project I wil work on the [Bank Marketing dataset](https://automlsamplenotebookdata.blob.core.windows.net/automl-sample-notebook-data/bankmarketing_train.csv) and use Azure to configure a cloud based Machine Learning production model, deploy it, and consume it. To this we will also create, publish and consume a pipeline.

## Architectural Diagram

Let us have a look at the *Architectural Diagram* which help us in seeing the flow of a project and the steps that are critical for the process to work.

![](../screenshots/arc-diagram.png)

Each steps in the process is essentiel and important to understand.

- Dataset: At first we need to upload and register the data to AML.
- AutoML: In the process of running a AutoML we need to configure the; compute cluster, ML task and exit criterion. In doing that we train models on the data we uploaded in the last step.
- Best model: When the AutoML process has finished we can choose the model that has shown the best results and deploy it. For deploying it we can either use **Azure Container Instance (ACI)** or **Azure Kubernetes Service (AKS)**.
- Enable Application insight: Application insight help us keep track of our deployed model and how it perform and if there is problems with the requests. To enabled it you can either use python sdk or from the studio.
- Endpoint: When we have deployed the model we can start consuming it though a REST endpoint. From the endpoint we can send request and recieve predictions.
- Pipeline: Pipelines are used for automate the process of traning the model to deploying and consume it. With python sdk we can create and publish a pipeline.

### Future Work

The project is a beginner projects and can be impoved though various more advanced methos. We could use *parrallel run* in our pipeline to make the process faster. Also with the pipeline we could add a pipeline for the data preparation, so we could skip the manual task.

In the course we have looked at [Apache Benchmark](http://httpd.apache.org/docs/2.4/programs/ab.html) which is a tool for measuing performance. We could also include test and the program for measure the performance.

## Key steps

1) AutoML: The first thing to do is to register your data to the data storage. After registered the data we can configure the AutoML run where we train several models on the  given data, here it is the Bank Marketing Data. Here we specify the compute cluser, ML task and other settings. After the experiment is done we can se what model has the best results. In our case the algoritme `VotingsEnsemble` has the highest accuracy on **0.92** and we choose that to go with.  

### Dataset registed

![](../screenshots/dataset.png)

### Experiment compledted

![](../screenshots/experiment.png)

### The best model

![](../screenshots/best.png)

2) Take the best model and deploy it: Now we have the best model we would like to deploy it so other can consume it and we also enable `Aucthentication` and deploying it using Azure Container Instance (ACI). For enable Application Insight we use the file logs.py. If we dont execute logs.py **Application Insights** would be disabled.

### Application insights

![](../screenshots/app-in.png)

### Running logs

![](../screenshots/app-logs.png)

3) Swagger: Now we need to build an REST Api (application programming interface) and to do that we use **Swagger** which is a tool that is very common to use for building REST Apis. Here we can make documentation for our colleagues so they now how to consume the model. It is also essentiel in the automated process so we can make request to the site. At first we need to run swagger.sh that pulls an docker image with our swagger ui. For running the REST Api we run serve.py that exposes our local swagger.json settings. From the Swagger REST Api we can access the model at test if we can request prediction from the given model.   

### My Swagger output

![](../screenshots/swagger-user.png)

![](../screenshots/swagger-local.png)

![](../screenshots/swagger-results.png)

4) Consume endpoint: The model is now deployed and we can interact with it. For doing that we use endpoint.py where we specify the web service and keys so we can send request to the model. When we send a request to the model we will recieve a prediction for the given data like is shown in the below picture.  

### My output for endpoint.py

![](../screenshots/enpoint.png)

5) Create, Publish and consume a pipeline: Pipelines is the process of automat the MLOps process. Here we build a jupyter aml-pipelines-with-automated-machine-learning-step.ipynb where we create, publish. and consume the pipeline so we the user can interact with it. At first we show a create pipeline, the endpoint where people interact with it. For showing that we are running a pipeline though the mention ipynb script we have included seceral picture for this.

### Publied pipeline

![](../screenshots/pipelines-create.png)

### Endpoint pipeline

![](../screenshots/pipelines-endpoint.png)

### Running pipeline

![](../screenshots/pipelines-running.png)

### Rest pipeline

![](../screenshots/pipelines-rest.png)

### Run pipeline

![](../screenshots/pipelines-run.png)

### Completed pipeline

![](../screenshots/pipelines-completed.png)

### Scheduled pipeline

![](../screenshots/pipelines-scheduled.png)

## Screen Recording

For showing the process I have made a short video where I highlight the process of creating a model to consuming it and can be seen at [youtube](https://www.youtube.com/watch?v=UuzyFGixeps). 