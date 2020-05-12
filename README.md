---
page_type: sample
description: "Deploy Python application using GitHub Actions"
products:
- GitHub Actions
- Azure App service
languages:
- Python
urlFragment: https://github.com/chrisdias/theCatSaidNo
---

# Deploying a Python Web App using GitHub actions

Learn to deploy a Python package to Azure App Service and set up a CI/CD workflow using GitHub Actions

## Overview

**GitHub Actions** gives you the flexibility to build an automated software development lifecycle workflow. You can write individual tasks ("Actions") and combine them to create a custom workflow. Workflows are configurable automated processes that you can set up in your repository to build, test, package, release, or deploy any project on GitHub.

With **GitHub Actions** you can build end-to-end continuous integration (CI) and continuous deployment (CD) capabilities directly in your repository. 

### Prerequisites

1. You will need a **GitHub** account. If you do not have one, you can sign up for free [here](https://github.com/join)

1. **Microsoft Azure Account**: You will need a valid and active Azure account for this lab. If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/en-us/free/).


### Setting up the GitHub repository

Fork this repo and open the sample app code in VS Code to get started.

## Create an Azure App Service

Create a web app hosted in Azure with a unique name, **Linux** as the OS and **Python 3.7** as the runtime. 

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-python%2Fazuredeploy.json" target="_blank">
<img src="https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazure.png"/>
</a>
<a href="http://armviz.io/#/?load=https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-python%2Fazuredeploy.json" target="_blank">
<img src="https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/visualizebutton.png"/>
</a>

This template creates a web app on azure with Python 3.7 enabled allowing you to run Python applications in Azure. 

The web app with Python is an app service that allow you to deploy your Django or Flask website. This will deploy a free tier Linux App Service Plan where you will host your App Service.

If you are new to Azure App Service, see:

- [Azure App Service](https://azure.microsoft.com/services/app-service/web/)
- [Template reference](https://docs.microsoft.com/azure/templates/microsoft.web/allversions)
- [Quickstart templates](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Compute&pageNumber=1&sort=Popular&term=web+apps)

If you are new to template deployment, see:

- [Azure Resource Manager documentation](https://docs.microsoft.com/azure/azure-resource-manager/)

- [Creating a Python App in Azure App Services](https://docs.microsoft.com/azure/app-service/containers/quickstart-python?tabs=bash)


## Set up CI/CD workflow with GitHub Actions 

We'll use GitHub actions to automate our deployment workflow for this web app. 

1. Navigate to the sample CI/CD workflow file `workflow.yml` in your GitHub repo under `.github/workflows/` folder path

1. Modify the values of the environment variables based on your Azure app:
```yaml
env:
  AZURE_WEBAPP_NAME: your-app-name    # set this to your application's name
  AZURE_WEBAPP_PACKAGE_PATH: '.'      # set this to the path to your web app project, defaults to the repository root
  PYTHON_VERSION: '3.7'                # set this to the Python version to use
```

1. In the portal, Overview page, click on "Get publish profile". A publish profile is a kind of deployment credential, useful when you don't own the Azure subscription. Open the downloaded settings file in VS Code and copy the contents of the file.

   ![](https://github.com/Azure/actions-workflow-samples/blob/master/assets/images/get-publish-profile.png)


1. We will now add the publish profile as a secret associated with this repo. On the GitHub repository, click on the "Settings" tab.

   ![](https://github.com/Azure/actions-workflow-samples/blob/master/assets/images/github-settings.png)


1. Go to "Secrets". Create a new secret called "AZURE_WEBAPP_PUBLISH_PROFILE" and paste the contents from the settings file.

   ![](https://github.com/Azure/actions-workflow-samples/blob/master/assets/images/create-secret.png)

1. Once you're done editing the workflow by configuring the required environment variables, click on "Start commit". Committing the file will trigger the workflow.

1. You can go back to the Actions tab, click on your workflow, and see that the workflow is queued or being deployed. Wait for the job to complete successfully.

1. Browse your app by pasting the URL of your Azure web app: https://AZURE_WEBAPP_NAME.azurewebsites.net

1. Make any changes by editing the app contents and commit the changes. Browse to the **Actions** tab in GitHub to view the live logs of your Action workflow which got triggered with the push of the commit.

1.  Once the workflow successfully completes execution, browse back to your website to visualise the new changes you introduced!

## Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.opensource.microsoft.com.

When you submit a pull request, a CLA bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., status check, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.
