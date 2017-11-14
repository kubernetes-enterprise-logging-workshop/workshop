# Processing Data / Log Files

> Estimated Time: 20 - 25 minutes

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

In the real world log files gets data appended constantly so it's ideal that Fluentd can remember the last position of the file that it was processed in case something goes wrong \(system outage\).

* Check the content of **03\_tail\_stdout.conf** configuration file
* Check the path set for **pos\_file **variable

Start Fluentd with the new configuration file:

```
$ docker run -v $PWD:/kelw kelw/fluentd:0.12 fluentd -c /kelw/config/03_tail_stdout.conf
```

Open the **pos\_file** generated and see it content. What does it represents ?

## Step 4: Append more data

Using the same configuration from **Step 3, **start the container:

```
$ docker run -v $PWD:/kelw kelw/fluentd:0.12 fluentd -c /kelw/config/03_tail_stdout.conf
```

From a different termina,l now append data to the monitored apache log file and see how Fluentd output changes. Then re-check it **pos\_file **content:

```
$ cat apache.append >> apache.log
```

## **Step 5: Files Rotation**

Log rotation is a common administration task which is done usually through a third party utility like logrotate. Fluentd as a log processor have to deal with such scenarios and the proper configuration to detect these changes is fundamental.

* Check the content of **04\_tail\_stdout.conf** configuration file
* Check the value of **refresh\_interval** variable

Start Fluentd container with the following command:

```
$ docker run -v $PWD:/kelw kelw/fluentd:0.12 fluentd -c /kelw/config/04_tail_stdout.conf
```

now from a different terminal, simulate a log rotation:

```
$ mv apache.log apache.log.1
```

pay attention to Fluentd container logs, what does it say ?

Re-create a new apache.log file using the _apache.append_ file sample:

```
$ cp apache.append apache.log
```

Question: what is **rotate\_wait** ? hint: [https://docs.fluentd.org/v0.12/articles/in\_tail.](https://docs.fluentd.org/v0.12/articles/in_tail)

