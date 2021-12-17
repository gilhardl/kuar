# Pods

> This folder is the chapter **5 - Pods** workspace.
>
> Each `.yaml` file is a Kubernetes resource manifest used in this chapter, sorted by their appearance order in the book.

## Cheatsheet

A **pod** represents a collection of application containers and volumes running in the same environment.

### Create a pod

Create a pod named `kuard` using the `kuard-amd64` image
```
kubectl run kuard --image=gcr.io/kuar-demo/kuard-amd64:1
```

Run a pod from a manifest
```
kubectl apply -f 01-kuard-pod.yaml
```

### View a pod

View a pod state
```
kubectl get pods kuard
```
> Change the output format using `-o` option (`-o wide`, `-o json`, `-o yaml` for example)

View detailled pod informations
```
kubectl describe pods kuard
```

### Delete a pod

Delete a pod
```
kubectl delete pods kuard
```

Delete a pod from its manifest
```
kubectl delete -f 01-kuard-pod.yaml
```

### Access a pod

Redirect a pod's port to localhost (pod `8080` to localhost `1234`)
```
kubectl port-forward kuard 8080:1234
```

Get a pod's logs
```
kubectl logs kuard
```

Run a command inside a pod
```
kubectl exec -it kuard date
```

Run an interactive shell inside a pod
```
kubectl exec -it kuard sh
```

Copy files from / to a pod
```
kubectl cp kuard:/path/to/file/inside/pod ./path/to/local/machine

kubectl cp ./path/to/local/machine kuard:/path/to/file/inside/pod
```

### Probes

#### `httpGet` probe

Make an HTTP call and succeed if the request returns with a status code between 200 and 400.

#### `tcpSocket` probe

Open a TCP socket and succeed if the socket connexion succeeds.

#### `exec` probe

Run a script and succeed if the script exit code is equal to 0.

### Volumes

#### `hostPath` volume

Mount a directory from the host pod inside a container.

#### `emptyDir` volume

An empty directory which depends on the pod lifecycle and could be shared by multiple containers.

#### Network volumes

A network storage could be mounted inside a container, in order to persist data. This network volumes could use common protocols like `nfs`, `isci`, or even services from major cloud providers.
