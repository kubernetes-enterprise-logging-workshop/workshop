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

Docker containers can have access to files located in the host system through _volumes. _The kelw repository project contains two main directories that are used along the laboratory:

* config/: several configuration files for Fluentd
* data/: files used as samples for several configurations



docker run -v $PWD/data:/kelw/data -v $PWD/config:/kelw/config/ kelw/fluentd:0.12 fluentd -c /kelw/config/01\_tail\_stdout.conf

## Step 3: Run Fluentd with Configuration Files

The following command will mount a volume with Fluentd configuration files and run Fluentd using the most basic file:

```
$ docker run -v /some/some kelw/fluentd:0.12 -c /
```

> COMMENT: above config files should contain:
>
> * sample of apache log files
> * sample of syslog log files
> * basic config with in\_tail to consume above files and write them down to JSON output files



