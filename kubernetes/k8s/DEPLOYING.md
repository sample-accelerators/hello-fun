## Deploying to Kubernetes using Kubernetes Deployment and Service

<img src="https://kubernetes.io/images/kubernetes-horizontal-color.png"
     alt="Kubernetes" width="400" />

You can containerize this template app and deploy it as a Deployment and Service on Kubernetes.
See the [Spring Boot Kubernetes](https://spring.io/guides/gs/spring-boot-kubernetes/) Guide for details.

We have included both `skaffold.yaml` and `Tiltfile` files to make this easier when deploying to a local cluster like [minikube](https://minikube.sigs.k8s.io/) or [kind](https://kind.sigs.k8s.io/).

### Deploying to local cluster using Tilt

You can install Tilt by following these instructions: https://docs.tilt.dev/install.html

You also need to have `pack` from Cloud Native Buildpacks installed, see: https://buildpacks.io/docs/tools/pack/

To deploy the app run:

```
tilt up
```

and follow the instructions (hitting space bar brings up the Tilt interface in your browser).

To uninstall the app run:

```
tilt down
```

### Deploying to local cluster using Skaffold

You can install Skaffold by following these instructions: https://skaffold.dev/docs/install/

To deploy the app run:

```
skaffold run -p local --port-forward
```

To uninstall the app run:

```
skaffold delete
```

### Accessing the app deployed to local cluster

If you don't have `curl` installed it can be installed using downloads here: https://curl.se/download.html

To invoke the deployed function run the following `curl` command in another terminal window:

```
curl localhost:8080 -w'\n' -H 'Content-Type: text/plain' -d Fun
```
