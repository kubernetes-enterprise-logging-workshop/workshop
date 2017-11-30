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

Register Providers:

```
$ az provider register -n Microsoft.ContainerService
$ az provider register -n Microsoft.Compute
$ az provider register -n Microsoft.Network
```

Create Resource Group

```
$ az group create --name kelw --location centralus
```

## Create Kubernetes Cluster

```
$ az aks create --resource-group kelw --name k8s --node-count 1 --generate-ssh-keys
```

## Connect to the Cluster

Load creadentials for Kubernetes client tool:

> Credentials to be stored on ~/.kube/aks

```
$ az aks get-credentials --resource-group kelw --name k8s -f ~/.kube/aks
```

Export the configuration

```
$ export KUBECONFIG=~/.kube/aks
```

List nodes

```
$ kubectl get nodes
```



