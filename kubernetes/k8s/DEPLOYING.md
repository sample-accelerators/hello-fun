## Deploying to Kubernetes using Kubernetes Deployment and Service

<img src="https://kubernetes.io/images/kubernetes-horizontal-color.png"
     alt="Kubernetes" width="400" />

You can containerize this template app and deploy it as a Deployment and Service on Kubernetes.
See the [Spring Boot Kubernetes](https://spring.io/guides/gs/spring-boot-kubernetes/) Guide for details.

We have included both `skaffold.yaml` and `Tiltfile` files to make this easier when deploying to a local cluster like [minikube](https://minikube.sigs.k8s.io/) or [kind](https://kind.sigs.k8s.io/).

You can install Skaffold by following these instructions: https://skaffold.dev/docs/install/

### Deploying to local cluster using Tilt

You can install Tilt by following these instructions: https://docs.tilt.dev/install.html

You also need to have `pack` from Cloud Native Buildpacks installed, see: https://buildpacks.io/docs/tools/pack/

To build and deploy the app run:

```
tilt up
```

and follow the instructions (hitting space bar brings up the Tilt interface in your browser).

To uninstall the app run:

```
tilt down
```

### Deploying to a cluster using Skaffold

You need to specify the `default-repo` which is the registry prefix for the image that is being built. For Docker Hub the prefix would be your Docker ID, for other registries it would typically be the registry URL plus your project.

> **NOTE**: You must specify a registry prefix where you have permission to push images.

You can do this globally by running:

```bash
skaffold config set --global default-repo ${REGISTRY_PREFIX}
```

Or, you can set it for the current Kubernetes context:

```bash
skaffold config set default-repo ${REGISTRY_PREFIX}
```

Finally, you can specify it as part of the `run` command:

```bash
skaffold run --default-repo ${REGISTRY_PREFIX} --port-forward --tail
```

#### Local cluster deployment

To build and deploy the app to a local cluster run:

```
skaffold run -p local --default-repo ${REGISTRY_PREFIX} --port-forward
```

#### Remote cluster deployment

To build and deploy the app to a remote cluster run:

```
skaffold run --default-repo ${REGISTRY_PREFIX} --port-forward
```

To uninstall the app run:

```
skaffold delete
```

### Deploying as a native image to a cluster using Skaffold

> **NOTE:** The native image compilation is resource intensive and takes several minutes.

See the [System Requirements](https://docs.spring.io/spring-native/docs/current/reference/htmlsingle/#getting-started-buildpacks-system-requirements) note in the Spring Native documentation for suggestions on Docker configuration.

To build and deploy the app as a native image to a local cluster run:

```
skaffold run -p local -p native --default-repo dev.local --port-forward
```

To build and deploy the app as a native image to a remote cluster run:

```
skaffold run -p native --default-repo <your-docker-id> --port-forward
```

To uninstall the app run:

```
skaffold delete
```

### Accessing the app deployed to your cluster

If you don't have `curl` installed it can be installed using downloads here: https://curl.se/download.html

To invoke the deployed function run the following `curl` command in another terminal window:

```
curl localhost:8080 -w'\n' -H 'Content-Type: text/plain' -d Fun
```
