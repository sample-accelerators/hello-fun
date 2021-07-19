## Deploying to Kubernetes as a Knative Service

![Knative Logo](https://avatars.githubusercontent.com/u/35583233?s=200&v=4)

You can containerize this template app and deploy it as a Knative Service.
See the [Hello World - Spring Boot Java](https://knative.dev/docs/serving/samples/hello-world/helloworld-java-spring/) sample for details.

You need to have Knative Service installed on your cluster. See https://knative.dev/docs/install/ for instructions.

We have included a `skaffold.yaml` file to make it easier to deploy the function app to a local cluster like [minikube](https://minikube.sigs.k8s.io/) or [kind](https://kind.sigs.k8s.io/).

You can install Skaffold by following these instructions: https://skaffold.dev/docs/install/

### Deploying to local cluster using Skaffold

To build and deploy the app run:

```
skaffold run -p local --default-repo dev.local
```

To uninstall the app run:

```
skaffold delete
```

### Deploying as a native image to local cluster using Skaffold

> **NOTE:** The native image compilation is resource intensive and takes several minutes.

See the [System Requirements](https://docs.spring.io/spring-native/docs/current/reference/htmlsingle/#getting-started-buildpacks-system-requirements) note in the Spring Native documentation for suggestions on Docker configuration.

To build and deploy the app run:

```
skaffold run -p local -p native --default-repo dev.local
```

To uninstall the app run:

```
skaffold delete
```


### Accessing the app deployed to local cluster

If you don't have `curl` installed it can be installed using downloads here: https://curl.se/download.html

You need to look up the Ingress endpoint for the Knative Serving install. See the [Install a networking layer](https://knative.dev/docs/install/install-serving-with-yaml/#install-a-networking-layer) and [Configure DNS](https://knative.dev/docs/install/install-serving-with-yaml/#configure-dns) sections for instructions for the different netwoking layers.

For _Kourier_ we can simply run the following port-forward command:

```
kubectl port-forward --namespace kourier-system service/kourier 8080:80
```

For _Contour_ we can simply run the following port-forward command:

```
kubectl port-forward --namespace contour-external service/envoy 8080:80
```

To invoke the deployed function run the following `curl` command in another terminal window:

```
curl localhost:8080 -w'\n' -H 'Content-Type: text/plain' -H 'Host: hello-fun.default.example.com' -d Fun
```
