### Stateless application deployment

create a local, empty (default) cluster

```
$ minikube start
$ kubectl get po -A
```

e.g.)

```
young-ultra] kubectl get po -A
NAMESPACE     NAME                               READY   STATUS    RESTARTS   AGE
kube-system   coredns-7db6d8ff4d-dz22r           0/1     Running   0          13s
kube-system   etcd-minikube                      1/1     Running   0          28s
kube-system   kube-apiserver-minikube            1/1     Running   0          27s
kube-system   kube-controller-manager-minikube   1/1     Running   0          27s
kube-system   kube-proxy-tpbxw                   1/1     Running   0          13s
kube-system   kube-scheduler-minikube            1/1     Running   0          27s
kube-system   storage-provisioner                1/1     Running   0          26s
```

create **deployment.yaml** file

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 2 # tells deployment to run 2 pods matching the template
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```

create a Deployment to the above (default) cluster using yaml

```shell
$ kubectl apply -f deployment.yaml
$ kubectl describe deployment nginx-deployment
```

e.g.)

```
young-ultra] kubectl apply -f deployment.yaml
deployment.apps/nginx-deployment created

young-ultra] kubectl describe deployment nginx-deployment
Name:                   nginx-deployment
Namespace:              default
CreationTimestamp:      
Labels:                 <none>
Annotations:            deployment.kubernetes.io/revision: 1
Selector:               app=nginx
Replicas:               2 desired | 2 updated | 2 total | 2 available | 0 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:  app=nginx
  Containers:
   nginx:
    Image:         nginx:1.14.2
    Port:          80/TCP
    Host Port:     0/TCP
    Environment:   <none>
    Mounts:        <none>
  Volumes:         <none>
  Node-Selectors:  <none>
  Tolerations:     <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Available      True    MinimumReplicasAvailable
  Progressing    True    NewReplicaSetAvailable
OldReplicaSets:  <none>
NewReplicaSet:   nginx-deployment-77d8468669 (2/2 replicas created)
Events:
  Type    Reason             Age   From                   Message
  ----    ------             ----  ----                   -------
  Normal  ScalingReplicaSet  24s   deployment-controller  Scaled up replica set nginx-deployment-77d8468669 to 2
```

list the Pods created by the deployment:

```
$ kubectl get pods -l app=nginx
```

create **deployment-update.yaml** file, now "replicas = 4", increasing from 2 to 4 Pods

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 4
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.16.1 #nginx from 1.14.2 to 1.16.1
        ports:
        - containerPort: 80
```

apply the new yaml file

```shell
$ kubectl apply -f deployment-update.yaml
$ kubectl get pods -l app=nginx
```

when you done, let's delete the deployment

```shell
$ kubectl delete deployment nginx-deployment
```
