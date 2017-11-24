# Fluentd DaemonSet

A DaemonSet is a Pod that runs on every node of a Kubernetes Cluster. Fluentd as a Log processor tool when deployed as a DaemonSet will take care of:

* Collect logs from running Pods/Containers
* Enrich logs with Kubernetes metadata \(labels/annotations\)
* Send logs to one or multiple destinations like local database or cloud services.

For simplicity we have published Yaml files which are ready to deploy Fluentd, from your terminal where the command **kubectl **have access to the Azure Kubernetes cluster go through the following steps:

## Step 1: Deploy Fluentd



