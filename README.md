# Dummy-k8s-scheduler

## Build Binary

Build server and client binaries and prepare to be packed into docker image. This is built with Linux Arch so it cannot be executed directly on Mac OS.
```
bash build-binary
```

## Build Docker Image

This creates the docker image and pushed to local repo, named `cheersyang/dummy-scheduler:0.1.0`
```
bash build-docker-image
```

## Deploy on k8s

Once k8s is running locally on Mac (via Minikube or docker-desktop). First deploy a nginx app to k8s, as its spec defines the scheduler name as `schedulerName: unified-scheduler`, it will be at pending state.
```
kubectl create -f nginx.yaml
```
Deploy the scheduler
```
kubectl create -f scheduler.yaml
```
the dummy scheduler will run in a pod, with 3 containers,

1. k8s-scheduler: a dummy k8s scheduler
2. dummy-scheduler: a dummy unified scheduler implementation
3. kubectl: used to access API server

After this pod is running, previous nginx pod will be scheduled. 

