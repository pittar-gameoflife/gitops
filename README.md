# Conway's Game of Life - GitOps Resources

## About This Repository

This repository contains everything you need to spin up the infrastructure, builds and apps - either with `kubectl` or `oc`, or with Argo CD.

## Using kubectl or oc

If you don't have Argo CD installed in your cluster, you can spin up everything with a few commands:

```
oc apply -k overlays/01-cluster/01-operators
oc apply -k overlays/01-cluster/01-cicd-tools

# Wait for Nexus to deploy in the "cicd-tools" namespace.
oc apply -k overlays/02-environments/01-cicd
oc apply -k overlays/02-environments/02-dev
oc apply -k overlays/02-environments/03-test

# Kick off the initial buils.
oc apply -k argocd/00-bootstrap/03-first-builds
```

## Using Argo CD

```
# First, setup core cluster infrastructure.
oc apply -k argocd/00-bootstrap/01-cluster

# Wait for Nexus to be deployed in "cicd-tools" project, then:
oc apply -k argocd/00-bootsrap/02-gameoflife

# Once the "Pipelines" appear in gameofile-cicd, you can kick off first builds with:
oc apply -k argocd/00-bootstrap/03-first-builds
```