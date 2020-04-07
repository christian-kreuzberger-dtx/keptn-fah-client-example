# Keptn Folding at home example

This repository contains a Keptn Project for the Folding At Home Client. The Kubernetes Manifests are based on [richstokes/k8s-fah](https://github.com/richstokes/k8s-fah).

## Prerequesits

* Kubernetes Cluster (1.14, 1.15) with [Keptn 0.6.1](https://keptn.sh) installed
* Download (or clone) this repository

## Configuration options

Please find configuration options for the FAHClient in [fah-cpu/templates/deployment.yaml](fah-cpu/templates/deployment.yaml):

```
          command:
            - "/usr/bin/FAHClient"
            - "--allow=0/0:7396"
            - "--web-allow=0/0:7396"
            - "--user=Keptn" # auto generated for the cluster
            - "--team=259797" # Keptn Team ID
            - "--run-as"
            - "1234"
            - "--pid-file=/var/lib/fahclient/fahclient.pid"
            - "--power=full"
            - "--gpu=false"
```

## Setup

```console
keptn create project folding-at-home --shipyard=shipyard.yaml
keptn onboard service fah-cpu --project=folding-at-home --chart=./fah-cpu
keptn send event new-artifact --project=folding-at-home --service=fah-cpu --image=docker.io/richstokes20/fah-covid:latest
```

## Remove

```console
keptn delete project folding-at-home
kubectl delete namespace folding-at-home-prod
```