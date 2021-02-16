<sub><sup><a href="index.html">Casa</a> > <a href="kubernetes.html">Kubernetes</a> > Notes</sup></sub>

# Notes

- [Connecting Applications With Services](#connecting-applications-with-services)
- [Get Node Port](#get-node-port)
- [Get Pod Name](#get-pod-name)
- [Host-Cluster Proxy](#host-cluster-proxy)
- [Labels And Selectors](#labels-and-selectors)
- [Pods](#pods)
- [Pod API URL](#pod-api-url)
- [Pod Lifecycle](#pod-lifecycle)
- [ReplicaSet](#replicaset)
- [Using Source IP](#using-source-ip)

## Connecting Applications With Services

[Connecting Applications With Services](https://kubernetes.io/docs/concepts/services-networking/connect-applications-service)

## Get Node Port

```shell
$ export NODE_PORT=$(kubectl get services/kubernetes-bootcamp -o go-template='{{(index .spec.ports 0).nodePort}}')
$ echo NODE_PORT=$NODE_PORT
NODE_PORT=31218
$ curl $(minikube ip):$NODE_PORT
Hello Kubernetes bootcamp! | Running on: kubernetes-bootcamp-765bf4c7b4-48g5h | v=1
```

## Get Pod Name

```shell
$ export POD_NAME=$(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}')
$ echo Name of the Pod: $POD_NAME
Name of the Pod: kubernetes-bootcamp-69fbc6f4cf-t98v9
```

## Host-Cluster Proxy

```
$ echo -e "\n\n\n\e[92mStarting Proxy. After starting it will not output a response. Please click the first Terminal Tab\n"; kubectl proxy
Starting Proxy. After starting it will not output a response. Please click the first Terminal Tab

$ kubectl proxy
Starting to serve on 127.0.0.1:8001
echo -e "\n\n\n\e[92mStarting Proxy. After starting it will not output a response. Please click the first Terminal Tab\n"; 
kubectl proxy
```

## Labels And Selectors

[Labels And Selectors](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels)

## Pods

[Pods](https://kubernetes.io/docs/concepts/workloads/pods/)
 
## Pod API URL

```shell
$ curl http://localhost:8001/api/v1/namespaces/default/pods/$POD_NAME/proxy/
Hello Kubernetes bootcamp! | Running on: kubernetes-bootcamp-765bf4c7b4-4jlwb | v=1
```

[Get Pod Name](#get-pod-name), [Host-Cluster Proxy](#host-cluster-proxy)

## Pod Lifecycle

[Pod Lifecycle](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

## ReplicaSet

[ReplicaSet](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/)

## Using Source IP

[Using Source IP](https://kubernetes.io/docs/tutorials/services/source-ip/)