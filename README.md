# Overview

The goal of this project is to demonstrate the usage of a CI/CD pipeline for an Azure deployment, demonstrating code testing and automation. For a working demo we use the application `flask-sklearn`.

## Project Plan

* [Trello board](https://trello.com/invite/b/rurN4FDz/ATTIe5a5be77180e3ca007b461ef0090f41d1D789419/udacity)
* [Excel Spreadsheet](project-management-template.xlsx)

## Instructions

### Architectural Diagram (Shows how key parts of the system work)

![Architecture](screenshots/20230110_architecture.png)

To make this project work we have to do the follwing steps

### Resource group

First step is to create a resource group in Azure for our resources. I named it `udacity-project-2`.

![Resource Group](screenshots/20230110_Azure_Resource_Group.png)

### Project running on Azure App Service

Next step is the creation of an Azure AppService. The CD pipeline will deploy the python application (`flask-sklearn`) into this AppService. I named it `udacity-devops-2`.

![Azure Webapp](screenshots/20230105_screenshot_Azure_Webapp.png)

### Project cloned into Azure Cloud Shell

To test the application later we clone our Github repo into Microsoft Azure CloudShell.

```bash
cd ~
git clone git@github.com:daniel-mersch/udacity-devops-2.git
cd udacity-devops-2
```

![Repository cloned](screenshots/20230105_screenshot_repo_cloned.png)

### Preparations    

To run a python app in CloudShell we have to first install a virtual environment and all dependencies. This is done by executing our Makefile.

```bash
make all
```

![make all](screenshots/20230110_Azure_CloudShell_make_all.png)

### Output of a test run

Now we run a test of our code.

```bash
make test
```

![make test](screenshots/20230105_Azure_CloudShell_make_test.png)

### Successful deploy of the project in Azure Pipelines.

With each push to the Github repo the CI pipeline runs.

![Github Action](screenshots/20230110_Github_Action.png)

A successful run of the CI pipeline triggers a run of the CD pipeline in Azure.

![Webapp Deployment](screenshots/20230110_Azure_Pipeline_WebApp_Deployment.png)

### Running Azure App Service from Azure Pipelines automatic deployment

The Webapp can be accessed via webbrowser: [https://udacity-devops-2.azurewebsites.net/](https://udacity-devops-2.azurewebsites.net/)

![Azure Webapp](screenshots/20230105_Azure_Webapp_running.png)

### Successful prediction from deployed flask app in Azure Cloud Shell. 

We have a little shell script called `make_predict_azure_app.sh`, which makes a test call to our WebApp.

```bash
./make_predict_azure_app.sh
```

![Output running Prediction](screenshots/20230110_Running_Prediction_on_Appservice.png)

### Output of streamed log files from deployed application

Last step is to verify, that our Webapp is running like expected. Therefore we take a look at the streamed log.

[Streamed Log](https://portal.azure.com/#@danielmerschweb.onmicrosoft.com/resource/subscriptions/1d777ce9-774b-4c85-8d8b-c7fb09bd2644/resourceGroups/udacity-project-2/providers/Microsoft.Web/sites/udacity-devops-2/logStream)
![AppService Log Stream](screenshots/20230110_Azure_Webapp_Log_Stream.png)

## Enhancements

For the future we should update the application to a current python version. The used version 3.5 is no longer supported, neither by Github Actions nor by Azure AppService, therefore we need to update the requirements.

### Python error

Python 3.5 throws deprecated error.
![Python 3.5 throws deprecated error](screenshots/20230105_screenshot_github_action_python35_error.png)

Python 3.7 is the minimum supported version.
![Python 3.7 is the minimum supported version](screenshots/20230105_screenshot_github_action_python37_ok.png)

## Demo 

<TODO: Add link Screencast on YouTube>
