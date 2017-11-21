# Configure your Azure Container Service

> Estimated Time: 30 minutes

Microsoft as a sponsor of Kubernetes Enterprise Logging Workshop, have provided Azure credits which can be used to test and try a Kubernetes cluster on Azure Container Service.

This benefit is exclusive for CloudNativeCon 2017 / Logging Workshop attendees.

## Activate your Account / Redeem Code

1. Go to [https://www.microsoftazurepass.com](https://www.microsoftazurepass.com)

2. Click on **Sign-in**

3. Active account and insert your Azure Code \(do not close the Browser until is done\)

4. Go to [https://portal.azure.com](https://portal.azure.com)

## Install Azure Cli

[https://docs.microsoft.com/en-us/cli/azure/install-azure-cli](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)

## Configure Azure Environment

Login:

```
$ az login
```

Register Provider:

```
$ az provider register -n Microsoft.ContainerService
```

Create Resource Group

```
$ az group create --name kelw --location eastus
```

## Create Kubernetes Cluster

```
$ az aks create --resource-group kelw --name k8s --node-count 1 --generate-ssh-keys
```

**FIXME &gt; NOT WORKING:**

Details: Required resource provider registrations Microsoft.Compute,Microsoft.Network are missing

