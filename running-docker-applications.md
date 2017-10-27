# Running Docker applications

Docker is a fundamental piece in the CloudNative ecosystem, the following steps will guide you to learn and run packaged applications as Docker images.

All images used in this article are public and available in our Docker Hub Organization called [KELW](https://hub.docker.com/u/kelw/)

## Step 1: Verify that Docker is running

```bash
$ docker version
Client:
 Version:      17.09.0-ce
 API version:  1.32
 Go version:   go1.8.3
 Git commit:   afdb6d4
 Built:        Tue Sep 26 22:42:45 2017
 OS/Arch:      linux/amd64
Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?
```

If the command shows an output similar to the one above, means that your Docker service is running

## **Step 2: Run our hello-world image from the Public Registry**

To get familiar with public images from the registry, run our hello-world image  located at kelw/hello-world:

```bash
$ docker run kewl/hello-world
```

The above command will lookup the image locally, if it's not found, it will pull it and then run it.

## Step 3: Checkout a different version of hello-world image

Docker images have the concept of tags, which is commonly used to associate specific versions to an image. So an image repository might have different versions available:

```
$ docker run kewl/hello-world:v2
```



