# Datadog Admission Controller

This repo is intended to try out the [Datadog Admission Controller](https://docs.datadoghq.com/containers/cluster_agent/admission_controller/) for Datadog Library injection from the agent and other stuff.

## Applications

It's composed of two applications `hello-node` running with Node.js and `hello-python` running with Python. Traffic to both is balanced when possible.

## Deployments

We go through 3 deployments types:
* Host where the applications and agent are installed directly on the host.
* Containers where everything is containerized with Docker and deployed through `docker-compose`
* Containers through `kubernetes` with instrumented applications
* Containers through `kubernetes` with library injection

## Build the apps

The applications are build locally using Docker then made available on the DockerHub registry. You might want to update your username in the following commands.

```shell
# Build the node app with tracer
$ docker build --no-cache --tag hello-node ./0-app/hello-node
$ docker tag hello-node leopaillier/hello-node:1.0
$ docker push leopaillier/hello-node:1.0

# Build the node app without tracer
$ docker build --no-cache --tag hello-node-no-tracer ./0-app/hello-node-no-tracer
$ docker tag hello-node leopaillier/hello-node-no-tracer:1.0
$ docker push leopaillier/hello-node-no-tracer:1.0

# Build the python app with tracer
$ docker build --no-cache --tag hello-python ./0-app/hello-python
$ docker tag hello-python leopaillier/hello-python:1.0
$ docker push leopaillier/hello-python:1.0

# Build the python app without tracer
$ docker build --no-cache --tag hello-python-no-tracer ./0-app/hello-python-no-tracer
$ docker tag hello-python leopaillier/hello-python-no-tracer:1.0
$ docker push leopaillier/hello-python-no-tracer:1.0
```