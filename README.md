# Azure Data Factory CI/CD Data Engineering

End-to-end Azure Data Factory data pipelines with Azure DevOps CI/CD using ARM templates and multi-environment deployment.

## Project Overview

This project demonstrates the development and deployment of Azure Data Factory pipelines using Azure DevOps CI/CD.

The solution covers data movement using Azure Data Factory, pipeline orchestration, ARM template generation, artifact publishing, and automated deployment across Development, QA, and Production environments.

## Architecture

The overall workflow is:

Azure Data Factory

↓

Git and Azure DevOps

↓

Build ARM Template

↓

Publish ARM Template as Artifact

↓

Deploy to Development

↓

Deploy to QA

↓

Deploy to Production

## Technologies Used

Azure Data Factory

Azure Data Lake Storage Gen2

Azure DevOps

Git

Azure Resource Manager ARM Templates

Azure PowerShell

Node.js

NPM

YAML

## ADF Pipeline Implementation

The Azure Data Factory pipeline demonstrates dynamic data processing using Lookup, ForEach, and Copy Data activities.

The Lookup activity retrieves the required parameters or file information.

The ForEach activity iterates through the returned items.

The Copy Data activity moves the required files between storage locations.

This approach allows the pipeline to process multiple files dynamically rather than creating separate activities for each file.

## CI/CD Implementation

Azure DevOps is used to automate the build and deployment process.

The CI/CD pipeline contains the following stages:

Build ARM Template

Deploy to Development

Deploy to QA

Deploy to Production

The pipeline is configured using YAML templates to separate the build and deployment logic.

## Build Process

The build process performs the following operations:

1. Installs Node.js.

2. Installs the Azure Data Factory utilities package using NPM.

3. Validates the Azure Data Factory resources.

4. Generates the ARM template.

5. Publishes the generated ARM template as a pipeline artifact.

The generated ARM template contains the infrastructure configuration required to deploy the Azure Data Factory resources.

## Deployment Process

The deployment process downloads the ARM template artifact generated during the build stage.

Before deployment, the ADF triggers are stopped using the PrePostDeploymentScript.ps1 script.

The ARM template is then deployed to the target resource group.

After successful deployment, the ADF triggers are started again.

The same deployment process is reused for Development, QA, and Production environments.

## Environment Configuration

Separate parameter files are maintained for each environment.

Development uses dev.json.

QA uses qa.json.

Production uses pd.json.

These parameter files provide environment-specific values such as the Data Factory name, Azure Key Vault URL, HTTP server URL, and Azure Data Lake Storage URL.

This allows the same ARM template to be reused across multiple environments while changing only the environment-specific configuration.

## Project Structure

```text
azure-adf-cicd-data-engineering
│
├── cicd
│   ├── cicd_pipeline.yml
│   ├── cicd_build.yml
│   ├── cd_deploy.yml
│   │
│   └── ARMParams
│       ├── dev.json
│       ├── qa.json
│       └── pd.json
│
├── images
│   ├── adf-pipeline.png
│   ├── azure-devops-build.png
│   ├── azure-devops-release.png
│   └── successful-production-deployment.png
│
├── package.json
│
└── README.md
