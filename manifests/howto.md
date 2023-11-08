# StabilityStudio container deployment
This document explains how to build and deploy StabilityStudio on Openshift
Container Platform


## Deployment
First, let's build the image for our Openshift Cluster. Open
`manifests/openshift/build-config.yaml` file and replace `spec.source.git.uri`
by your fork url. After that, create the buildConfig object for building the
image and store it in Openshift internal registry, as a ImageStream object.
```sh
export NS="stability-studio"
oc new-project $NS


oc apply -f manifests/openshift/build-config.yaml

oc start-build stability-studio
```

Now, deploy the application
```sh
oc apply -f manifests/openshift/stability-studio.yaml
```

Wait until every pod is on Running, and check the routes to find the HTTPS
endpoint

```sh
oc get routes
```
