<sub><sup><a href="index.html">Hogar</a> > <a href="kubernetes.html">Kubernetes</a> > kubectl</sup></sub>

# kubectl

- [cluster-info](#cluster-info)
- [create deployment](#create-deployment)
- [get deployments](#get-deployments)
- [get nodes](#get-nodes)
- [Get Pod Name](#get-pod-name)
- [Host-Cluster Proxy](#host-cluster-proxy)
- [version](#version)
- [version With curl](#version-with-curl)

## cluster-info

```shell
$ kubectl cluster-info
Kubernetes master is running at https://172.17.0.31:8443
KubeDNS is running at https://172.17.0.31:8443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
```

## create deployment

```shell
$ kubectl create deployment kubernetes-bootcamp --image gcr.io/google-samples/kubernetes-bootcamp:v1
deployment.apps/kubernetes-bootcamp created
```

## get deployments

```shell
$ kubectl get deployments
NAME                  READY   UP-TO-DATE   AVAILABLE   AGE
kubernetes-bootcamp   1/1     1            1           94s
```

## get nodes

```shell
$ kubectl get nodes
NAME       STATUS   ROLES    AGE     VERSION
minikube   Ready    master   3m55s   v1.17.3
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

## version

```shell
$ kubectl version
Client Version: version.Info{Major:"1", Minor:"17", GitVersion:"v1.17.3", GitCommit:"06ad960bfd03b39c8310aaf92d1e7c12ce618213", GitTreeState:"clean", BuildDate:"2020-02-11T18:14:22Z", GoVersion:"go1.13.6", Compiler:"gc", Platform:"linux/amd64"}
Server Version: version.Info{Major:"1", Minor:"17", GitVersion:"v1.17.3", GitCommit:"06ad960bfd03b39c8310aaf92d1e7c12ce618213", GitTreeState:"clean", BuildDate:"2020-02-11T18:07:13Z", GoVersion:"go1.13.6", Compiler:"gc", Platform:"linux/amd64"}
```

## version With curl

Requires a [kubectl proxy](#host-cluster-proxy).

```shell
$ curl http://localhost:8001/version
{
  "major": "1",
  "minor": "17",
  "gitVersion": "v1.17.3",
  "gitCommit": "06ad960bfd03b39c8310aaf92d1e7c12ce618213",
  "gitTreeState": "clean",
  "buildDate": "2020-02-11T18:07:13Z",
  "goVersion": "go1.13.6",
  "compiler": "gc",
  "platform": "linux/amd64"
}
```