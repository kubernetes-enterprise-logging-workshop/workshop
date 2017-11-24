# Fluentd DaemonSet

A DaemonSet is a Pod that runs on every node of a Kubernetes Cluster. Fluentd as a Log processor tool when deployed as a DaemonSet will take care of:

* Collect logs from running Pods/Containers
* Enrich logs with Kubernetes metadata \(labels/annotations\)
* 


