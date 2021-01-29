# Conway's Game of Life

## Native Build
```
oc new-app quay.io/quarkus/ubi-quarkus-native-s2i:20.3-java11~https://github.com/pittar-sandbox/gameoflife-supervisor.git --name=gamoeoflife-supervisor-native
```

## Cluster build limits (RHPDS)

RHPDS clusters have pre-configured build limits.  You will need to delete them if you want to run a native build.

```
oc edit build.config.openshift.io/cluster
```

Then, change the `spec` to an empty object `{}`.