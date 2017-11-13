## Installing and Running Fluentd

> Estimated Time: 10 - 15 minutes

Fluentd can be installed from sources or through  pre-built packages that exists for different operating systems and Linux Distributions.  For the Cloud Native space we strongly recommend to use our official Docker images since they are validated, secured and supported by Fluentd core maintainers.

Official images of Fluentd for production usage are available at [fluent/fluentd](https://hub.docker.com/r/fluent/fluentd/) repository, for this laboratory we will use the images we have prepared on [KELW](https://hub.docker.com/r/kelw) Docker Hub Organization.

## Step 1: Pull Fluentd Image and Run it

Run the last version of Fluentd v0.12 series:

```
$ docker run kelw/fluentd:0.12 fluentd --version
```

the above command will pull the image and override it default command, instead the command will print out the full version of Fluentd that is running.

> COMMENT: this image musy have the following addons:
>
> * Monitor / Debug Plugin
> * Prometheus plugins

## Step 2: Volumes

Docker containers can have access to files located in the host system through _volumes_. The kelw repository project contains two main directories that are used along the laboratory:

| Directory | Description |
| :--- | :--- |
| config/ | configuration files for Fluentd |
| data/ | data sample files used for different setups |

to get started join into the KELW labs 2.2 directory:

```
$ cd kelw/labs/2.2
```

then mount the kelw current lab in Docker as a mounted volume:

```
$ docker run -v $PWD:/kelw kelw/fluentd:0.12 ls -l /kelw
```

> the current directory labs/2.2/ content will be visible from /kelw

## Step 3: Run Fluentd with Configuration Files

The following command will mount a volume with Fluentd configuration files and run it using the 01\_tail\_stdout.conf configuration file:

```
<source>
  type tail
  path /kelw/data/simple.txt
  tag  raw
  format none
  read_from_head true
</source>

<match **>
  type stdout
</match>
```

Command:

```
$ docker run -v $PWD:/kelw kelw/fluentd:0.12 fluentd -c /kelw/config/01_tail_stdout.conf
```



