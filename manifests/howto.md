# StabilityStudio container deployment
This document explains how to build and deploy StabilityStudio on Openshift
Container Platform


## Building
Use the following commands to build and push a container image for StabilityStudio

```sh
# Building image
podman build -t stability-studio:v0.1.0 -f ./manifests/Containerfile .

# Tagging image
IMAGE_SERVER="<your-container-image-server-url>" # (quay.io, hub.docker...)
IMAGE_REPO="<your-repo-name>" # (username on image server)
IMAGE_TAG="<desired-image-tag>" # (v0.1.0, rc-XX, latest...)

podman tag localhost/stability-studio:v0.1.0 $IMAGE_SERVER/$IMAGE_REPO/stability-studio:$IMAGE_TAG
podman tag localhost/stability-studio:v0.1.0 $IMAGE_SERVER/$IMAGE_REPO/stability-studio:latest

# Pushing to repo
podman push $IMAGE_SERVER/$IMAGE_REPO/stability-studio:$IMAGE_TAG
podman push $IMAGE_SERVER/$IMAGE_REPO/stability-studio:latest
```
