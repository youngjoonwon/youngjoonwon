### Trying k9s

k9s: convenient Kubernetes CLI, managing clusters (https://k9scli.io/)

install k9s https://k9scli.io/topics/install/ for mac, linux, windows

for example, using mac homebrew

```shell
$ brew install derailed/k9s/k9s
```

see available Pods

```
$ k9s -c pod
```

e.g.)

```

```

here are other k9s commands:

https://k9scli.io/topics/commands/



### Create a new service: Expose app publicly (giving IP)

```shell
$ kubectl get pods
$ kubectl get services
$ kubectl expose deployment/kubernetes-bootcamp --type="NodePort" --port 8080
$ kubectl get services
$ kubectl describe services/kubernetes-bootcamp

$ export NODE_PORT="$(kubectl get services/kubernetes-bootcamp -o go-template='{{(index .spec.ports 0).nodePort}}')"
$ echo "NODE_PORT=$NODE_PORT"

$ curl http://"$(minikube ip):$NODE_PORT"

#deleting a service
$ kubectl delete service -l app=kubernetes-bootcamp
$ kubectl get services
$ curl http://"$(minikube ip):$NODE_PORT"
$ kubectl exec -ti $POD_NAME -- curl http://localhost:8080
```

