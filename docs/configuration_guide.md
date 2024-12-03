# Configuration Guide

This guide provides a unified configuration for the Azure AI Basic Python project. It consolidates steps from various configuration files and documents.

## Azure Pipelines Configuration

The Azure Pipelines configuration is defined in the `.azdo/pipelines/azure-dev.yml` file. Below are the key steps:

1. **Trigger**: The pipeline is triggered on commits to the `main` or `master` branch.
2. **Pool**: Uses the `ubuntu-latest` VM image.
3. **Steps**:
   - Install `azd` using the `setup-azd@0` task.
   - Configure `azd` to use AZ CLI authentication.
   - Provision infrastructure using the `AzureCLI@2` task.
   - Deploy the application using the `AzureCLI@2` task.

## Dev Containers Configuration

The Dev Containers configuration is defined in the `.devcontainer/devcontainer.json` file. Below are the key settings:

1. **Name**: `azureai-basic-python`
2. **Image**: `mcr.microsoft.com/devcontainers/python:3.11-bullseye`
3. **Forward Ports**: `50505`
4. **Features**: Includes `ghcr.io/azure/azure-dev/azd:latest`
5. **Customizations**:
   - VS Code extensions: `ms-azuretools.azure-dev`, `ms-azuretools.vscode-bicep`, `ms-python.python`, `ms-toolsai.jupyter`, `GitHub.vscode-github-actions`
6. **Post Create Command**: Installs required Python packages.
7. **Remote User**: `vscode`
8. **Host Requirements**: `memory: 8gb`

## GitHub Actions Workflow Configuration

The GitHub Actions workflow configuration is defined in the `.github/workflows/azure-dev.yml` file. Below are the key steps:

1. **Trigger**: The workflow is triggered on commits to the `main` branch.
2. **Permissions**: Sets up permissions for deploying with secretless Azure federated credentials.
3. **Jobs**:
   - **Build**:
     - Runs on `ubuntu-latest`.
     - Sets environment variables for Azure credentials and resource names.
     - Steps:
       - Checkout the repository.
       - Install `azd` using `Azure/setup-azd@v1.0.0`.
       - Log in with Azure using federated credentials.
       - Provision infrastructure using `azd provision`.
       - Deploy the application using `azd deploy`.

## Azure AI Studio Deployment Customization

The Azure AI Studio deployment customization is documented in the `docs/deploy_customization.md` file. Below are the key customization options:

1. **Disabling Resources**:
   - Disable AI Search: `azd env set USE_SEARCH_SERVICE false`
   - Disable Application Insights: `azd env set USE_APPLICATION_INSIGHTS false`
   - Disable Container Registry: `azd env set USE_CONTAINER_REGISTRY false`

2. **Customizing Resource Names**:
   - Override default naming conventions using environment variables such as `AZURE_AIHUB_NAME`, `AZURE_AIPROJECT_NAME`, `AZURE_AIENDPOINT_NAME`, etc.

3. **Customizing Model Deployments**:
   - Change the chat deployment name: `azd env set AZURE_AI_CHAT_DEPLOYMENT_NAME <name>`
   - Change the chat model format: `azd env set AZURE_AI_CHAT_MODEL_FORMAT <format>`
   - Change the chat model name: `azd env set AZURE_AI_CHAT_MODEL_NAME <name>`
   - Set the version of the chat model: `azd env set AZURE_AI_CHAT_MODEL_VERSION <version>`
   - Change the capacity and SKU of the deployments using environment variables such as `AZURE_AI_CHAT_DEPLOYMENT_CAPACITY`, `AZURE_AI_CHAT_DEPLOYMENT_SKU`, etc.

4. **Bringing an Existing AI Project Resource**:
   - Set the connection string for an existing AI project: `azd env set AZURE_EXISTING_AIPROJECT_CONNECTION_STRING "<connection-string>"`

## Environment Variables for Deployment

The environment variables for deployment are listed in the `azure.yaml` file. Below are the key variables:

- `AZURE_RESOURCE_GROUP`
- `AZURE_AIHUB_NAME`
- `AZURE_AIPROJECT_NAME`
- `AZURE_AISERVICES_NAME`
- `AZURE_SEARCH_SERVICE_NAME`
- `AZURE_APPLICATION_INSIGHTS_NAME`
- `AZURE_CONTAINER_REGISTRY_NAME`
- `AZURE_KEYVAULT_NAME`
- `AZURE_STORAGE_ACCOUNT_NAME`
- `AZURE_LOG_ANALYTICS_WORKSPACE_NAME`
- `USE_CONTAINER_REGISTRY`
- `USE_APPLICATION_INSIGHTS`
- `USE_SEARCH_SERVICE`
- `AZURE_AI_CHAT_DEPLOYMENT_NAME`
- `AZURE_AI_CHAT_DEPLOYMENT_SKU`
- `AZURE_AI_CHAT_DEPLOYMENT_CAPACITY`
- `AZURE_AI_CHAT_MODEL_NAME`
- `AZURE_AI_CHAT_MODEL_FORMAT`
- `AZURE_AI_CHAT_MODEL_VERSION`
- `AZURE_AI_EMBED_DEPLOYMENT_NAME`
- `AZURE_AI_EMBED_DEPLOYMENT_SKU`
- `AZURE_AI_EMBED_DEPLOYMENT_CAPACITY`
- `AZURE_AI_EMBED_MODEL_NAME`
- `AZURE_AI_EMBED_MODEL_FORMAT`
- `AZURE_AI_EMBED_MODEL_VERSION`
- `AZURE_EXISTING_AIPROJECT_CONNECTION_STRING`
