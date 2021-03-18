# Conway's Game of Life - GitOps Resources

## About This Repository

This repository contains everything you need to spin up the infrastructure, builds and apps - either with `kubectl` or `oc`, or with Argo CD.

## Prerequisites

There is some base infrastructure that needs to be in place for this demo:

1. Nexus 2
2. OpenShift Pipelines Operator(v1.3.1)
3. AMQ Streams Operator (v1.6.2)

If you don't already have these in place, run the following to add them:

```
# Create a CICD Tools project and install Nexus 2.
oc new-project cicd-tools
oc project cicd-tools
oc apply -k https://github.com/redhat-canada-gitops/catalog/nexus2/base?ref=master

## Install OpenShift Pipelines and AMQ Streams Operators for all namespaces.
oc apply -k https://github.com/redhat-canada-gitops/catalog/openshift-pipelines-operator/overlays/stable?ref=master
oc apply -k https://github.com/redhat-canada-gitops/catalog/amq-streams-operator/overlays/stable?ref=master
```

This should only take a few minutes to install everything.

## Using kubectl or oc

If you don't have Argo CD installed in your cluster, you can spin up everything with a few commands:

```
# Once Nexus, OpenShift Pipelines and AMQ Streams Operator are installed...
oc apply -k overlays/01-cicd
oc apply -k overlays/02-dev
oc apply -k overlays/03-test

# Kick off the initial buils.
oc create -f first-builds
```

## Using Argo CD

```
# Once Nexus, OpenShift Pipelines and AMQ Streams Operator are installed...
oc apply -k argocd/00-bootstrap
```