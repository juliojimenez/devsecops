<sub><sup><a href="index.html">Hogar</a> > <a href="kubernetes.html">Kubernetes</a> > kubectl</sup></sub>

# kubectl

- [cluster-info](#cluster-info)
- [create deployment](#create-deployment)
- [describe](#describe)
- [exec](#exec)
- [expose](#expose)
- [get](#get)
- [logs](#logs)
- [proxy](#proxy)
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

## describe

- [describe pods](#describe-pods)
- [describe services](#describe-services)

### describe pods

```shell
$ kubectl describe pods
Name:         kubernetes-bootcamp-765bf4c7b4-krkbp
Namespace:    default
Priority:     0
Node:         minikube/172.17.0.21
Start Time:   Tue, 09 Feb 2021 00:21:14 +0000
Labels:       pod-template-hash=765bf4c7b4
              run=kubernetes-bootcamp
Annotations:  <none>
Status:       Running
IP:           172.18.0.5
IPs:
  IP:           172.18.0.5
Controlled By:  ReplicaSet/kubernetes-bootcamp-765bf4c7b4
Containers:
  kubernetes-bootcamp:
    Container ID:   docker://a17c399ba870418509c208cd2ecf87d4b67ddb1611170dfbf8275c2cb7a111ff
    Image:          gcr.io/google-samples/kubernetes-bootcamp:v1
    Image ID:       docker-pullable://jocatalin/kubernetes-bootcamp@sha256:0d6b8ee63bb57c5f5b6156f446b3bc3b3c143d233037f3a2f00e279c8fcc64af
    Port:           8080/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Tue, 09 Feb 2021 00:21:17 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-gwdjs (ro)
Conditions:
  Type              Status
  Initialized       True 
  Ready             True 
  ContainersReady   True 
  PodScheduled      True 
Volumes:
  default-token-gwdjs:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-gwdjs
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type     Reason            Age                    From               Message
  ----     ------            ----                   ----               -------
  Warning  FailedScheduling  3m14s (x2 over 3m14s)  default-scheduler  0/1 nodes are available: 1 node(s) had taints that the pod didn't tolerate.
  Normal   Scheduled         3m6s                   default-scheduler  Successfully assigned default/kubernetes-bootcamp-765bf4c7b4-krkbp to minikube
  Normal   Pulled            3m3s                   kubelet, minikube  Container image "gcr.io/google-samples/kubernetes-bootcamp:v1" already present on machine
  Normal   Created           3m3s                   kubelet, minikube  Created container kubernetes-bootcamp
  Normal   Started           3m3s                   kubelet, minikube  Started container kubernetes-bootcamp
```

### describe services

```shell
$ kubectl describe services/kubernetes-bootcamp
Name:                     kubernetes-bootcamp
Namespace:                default
Labels:                   run=kubernetes-bootcamp
Annotations:              <none>
Selector:                 run=kubernetes-bootcamp
Type:                     NodePort
IP:                       10.104.47.177
Port:                     <unset>  8080/TCP
TargetPort:               8080/TCP
NodePort:                 <unset>  31218/TCP
Endpoints:                172.18.0.6:8080
Session Affinity:         None
External Traffic Policy:  Cluster
Events:                   <none>
```

## exec

- [bash](#bash)
- [env](#env)

### bash

```shell
$ kubectl exec -ti $POD_NAME bash
root@kubernetes-bootcamp-765bf4c7b4-ncrpz:/#
```

### env

```shell
$ kubectl exec $POD_NAME env
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
HOSTNAME=kubernetes-bootcamp-765bf4c7b4-ncrpz
KUBERNETES_PORT_443_TCP_PORT=443
KUBERNETES_PORT_443_TCP_ADDR=10.96.0.1
KUBERNETES_SERVICE_HOST=10.96.0.1
KUBERNETES_SERVICE_PORT=443
KUBERNETES_SERVICE_PORT_HTTPS=443
KUBERNETES_PORT=tcp://10.96.0.1:443
KUBERNETES_PORT_443_TCP=tcp://10.96.0.1:443
KUBERNETES_PORT_443_TCP_PROTO=tcp
NPM_CONFIG_LOGLEVEL=info
NODE_VERSION=6.3.1
HOME=/root
```

## expose

```shell
$ kubectl expose deployment/kubernetes-bootcamp --type="NodePort" --port 8080
service/kubernetes-bootcamp exposed
```

## get

- [get deployments](#get-deployments)
- [get nodes](#get-nodes)
- [get pods](#get-pods)
- [get services](#get-services)

### get deployments

```shell
$ kubectl get deployments
NAME                  READY   UP-TO-DATE   AVAILABLE   AGE
kubernetes-bootcamp   1/1     1            1           94s
```

### get nodes

```shell
$ kubectl get nodes
NAME       STATUS   ROLES    AGE     VERSION
minikube   Ready    master   3m55s   v1.17.3
```

### get pods

```shell
$ kubectl get pods
NAME                                   READY   STATUS    RESTARTS   AGE
kubernetes-bootcamp-765bf4c7b4-krkbp   1/1     Running   0          27s
```

### get services

```shell
$ kubectl get services
NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   44s
```

## logs

```shell
$ kubectl logs $POD_NAME
Kubernetes Bootcamp App Started At: 2021-02-09T02:35:44.983Z | Running On:  kubernetes-bootcamp-765bf4c7b4-4jlwb 

Running On: kubernetes-bootcamp-765bf4c7b4-4jlwb | Total Requests: 1 | App Uptime: 298.038 seconds | Log Time: 2021-02-09T02:40:43.022Z
```

[Get Pod Name](notes.md#get-pod-name)

## proxy

```shell
$ kubectl proxy
Starting to serve on 127.0.0.1:8001
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