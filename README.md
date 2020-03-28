# Kubernetes Ingress Test

This is a test project for using an Ingress Controller. I used the Contour
Ingress Controller in this test.

## Requirements

Requirements for this test project are:

* Minikube 1.8+
* Docker

For local usage you need to add some lines to the `/etc/hosts` file:

```
127.0.0.1 foo.cwansart.de
127.0.0.1 bar.cwansart.de
```

## How to start

Start Docker and a Kubernetes cluster in Minikube:

```
$ minikube start --driver=docker --container-runtime=docker
$ eval $(minikube docker-env)
$ docker build -t cwansart.de-foo:latest foo
$ docker build -t cwansart.de-bar:latest bar
$ kubectl apply -f config
```

Open in a different terminal window the tunnel command:

```
$ minikube tunnel
```

Now open up one of the pages:

* http://foo.cwansart.de
* http://bar.cwansart.de

## Structure of this repository

The repository contains 2 small test projects, _foo_ and _bar_. Each have an `index.html` pointing to each other, via
the defined domains foo.cwansart.de and bar.cwansart.de. They also contain a Dockerfile that copies the index.html file
into a nginx webserver.

The _config_ folder contains the Kubernetes manifests to start the Contour Ingress Controller, its Ingress definitions
and the Deployments of the _foo_ and _bar_ applications.

## Links

* https://minikube.sigs.k8s.io/docs/tasks/docker_daemon/
* https://projectcontour.io/getting-started/