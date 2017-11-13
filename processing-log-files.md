# Processing Data / Log Files

> Estimated Time: 5 - 10 minutes

Fluentd as a log processor, aggregator and forwarder, support many sources to listen from data, the most common source of data is through _log files_. The following section focus on Tail input plugin which allows Fluentd to consume log files and handle them properly.

The example configuration files and data for this laboratory is on **kelw/labs/2.3**, make sure to position in the right directory before running the steps below:

```
$ cd kelw/labs/2.3
```

## Step 1: Read example log files

Look the content of the data sample files provided:

```
$ cat data/simple.txt
$ cat data/apache.log
```

Let Fluentd process the data sample files using different configuration for each one:

**File: simple.txt**

```
$ docker run -v $PWD:/kelw kelw/fluentd:0.12 fluentd -c /kelw/config/01_tail_stdout.conf
```

**File: apache.log**

```
$ docker run -v $PWD:/kelw kelw/fluentd:0.12 fluentd -c /kelw/config/02_tail_stdout.conf
```

After look at the Fluentd output, check the configuration files used on each command, what are the main differences ?

## Step 2: Extend Tags with File names

Tags are the core functionality for filtering and routing to multiple destinations in Fluentd. On this exercise, edit the configuration file **02\_tail\_stdout.conf **and replace:

```
Tag webserver
```

by

```
Tag webserver.*
```

Then run the modified configuration file:

```
$ docker run -v $PWD:/kelw kelw/fluentd:0.12 fluentd -c /kelw/config/02_tail_stdout.conf
```

What's different now in Fluentd output records ?

## Step 3: Files position \(aka POS file\)

In the real world log files gets data appended constantly, 



