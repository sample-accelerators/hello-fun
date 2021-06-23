load('ext://pack', 'pack')

pack('hello-fun:latest')

k8s_yaml(['kubernetes/deployment.yaml', 'kubernetes/service.yaml'])
k8s_resource('hello-fun', port_forwards=8080)
