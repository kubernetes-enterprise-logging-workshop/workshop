# Fluentd DaemonSet

> Estimated Time: 15-20 minutes

A DaemonSet is a Pod that runs on every node of a Kubernetes Cluster. Fluentd as a Log processor needs to be  deployed as a DaemonSet where it will take care of:

* Collect logs from running Pods/Containers
* Enrich logs with Kubernetes metadata \(labels/annotations\)
* Send logs to one or multiple destinations like a local database or cloud services.

For simplicity we have published Yaml files which are ready to deploy Fluentd, from your terminal where the command **kubectl **have access to the Azure Kubernetes cluster go through the following steps:

## Step 1: Namespace, Service Account and Roles

The following commands will create the Namespace, service account and roles to allow Fluentd collect the logs properly:

```
$ kubectl create namespace logging
$ kubectl create -f kelw/4.1/config/fluentd-service-account.yaml
$ kubectl create -f kelw/4.1/config/fluentd-role.yaml
$ kubectl create -f kelw/4.1/config/fluentd-role-binding.yaml
```

## Step 2: Configuration

Fluentd configuration will be set through a Kubernetes ConfigMap, to create it run the following command:

```
$ kubectl create -f kelw/4.1/config/fluentd-configmap.yaml
```

## Step 3: Edit DaemonSet Yaml file

The DaemonSet Yaml file also exports the required information to connect to the Elasticsearch Cloud Service that is being used on this workshop, locate the Fluentd Container section and fill the missing fields:

```js
      containers:
      - name: fluentd
        image: kelw/fluent:0.12
        env:
          - name:  FLUENT_ELASTICSEARCH_HOST
            value: ""
          - name:  FLUENT_ELASTICSEARCH_PORT
            value: ""
          - name: FLUENT_ELASTICSEARCH_SCHEME
            value: "https"
          # X-Pack Authentication
          # =====================
          - name: FLUENT_ELASTICSEARCH_USER
            value: "elastic"
          - name: FLUENT_ELASTICSEARCH_PASSWORD
            value: ""
```

## Step 4: Deploy Fluentd

```
$ kubectl create -f kelw/4.1/config/fluentd-ds.yaml
```



