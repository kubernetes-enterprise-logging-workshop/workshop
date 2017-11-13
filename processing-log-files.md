# Processing Data / Log Files

> Estimated Time: 5 - 10 minutes

Fluentd as a log processor, aggregator and forwarder, support many sources to listen from data, the most common source of data is through _log files_. The following section focus on Tail input plugin which allows Fluentd to consume log files and handle them properly.

The example configuration files and data for this laboratory is on **kewl/labs/2.3**, make sure to position in the right directory before running the steps below:

```
$ cd kewl/labs/2.3
```

## Step 1: Read example log files

```
$ docker run -v $PWD:/kelw kelw/fluentd:0.12 fluentd -c /kelw/config/01_tail_stdout.conf
```





