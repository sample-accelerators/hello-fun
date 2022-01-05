allow_k8s_contexts(os.getenv("CURRENT_CONTEXT", default='kind-kind'))

NAMESPACE = os.getenv("NAMESPACE", default='default')

k8s_custom_deploy(
    'hello-fun',
    apply_cmd="tanzu apps workload apply -f config/workload.yaml " +
               " --namespace " + NAMESPACE +
               " --yes >/dev/null " +
              "&& kubectl get workload hello-fun --namespace " + NAMESPACE + " -o yaml",
    delete_cmd="tanzu apps workload delete -f config/workload.yaml --namespace " + NAMESPACE + " --yes",
    deps=['pom.xml', './target/classes'],
    container_selector='workload',
    live_update=[
      sync('./target/classes', '/workspace/BOOT-INF/classes')
    ]
)

k8s_resource('hello-fun', extra_pod_selectors=[{'serving.knative.dev/service': 'hello-fun'}])
