# Generate Data Samples

> Estimated Time: 3 minutes

Run a simple deployment image:

```
$ kubectl run json --image=kelw/json-random
```

Check the Pods available

```
$ kubectl get pods
```

Locate the json Pod and watch the logs generated

```
$ kubectl logs -f json
```





