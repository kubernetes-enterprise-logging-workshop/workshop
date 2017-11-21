# Docker and Application Logs

> Estimated Time: 15 minutes

The following laboraty aims to introduce the concepts of Logging from a Docker Container Engine perspective.

## Step 1: Understanding Streams

Run a Docker Container in foreground that generate random Apache Web Server logs

```
$ docker run kelw/apache-random
```

That container flushing the log entries to the standard output stream. Keep this container running since it's used in the following steps.

## Step 2: Read Log Streams using Docker Utilities

Without stop the running container from Step 1, open a new terminal and locate the Container ID associated:

```
$ docker ps
```

Using the Container ID run the Docker Logs command \(tail / follow mode\):

```
$ docker logs -f $CONTAINER_ID
```

> replace $CONTAINER\_ID with the proper value

## Step 3: Find stream logs into the file system

Using the Container ID obtained in Step 2, locate the stream log file generated into the file system:

```
$ docker inspect --format='{{.LogPath}}' $CONTAINER_ID
```

> replace $CONTAINER\_ID with the proper value



