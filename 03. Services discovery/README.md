# Services discovery

> This folder is the chapter **7 - Labels and annotations** workspace.
>
> Each `.yaml` file is a Kubernetes resource manifest used in this chapter, sorted by their appearance order in the book.

## Cheatsheet

A **service** is a resource used to name a labels selector.

### Create a service

Create a service for the `alpaca-prod` deployment

```
kubectl expose deployment alpaca-prod
```

### DNS

Kubernetes provide a DNS service exposed to running pods. This DNS service attribute domain names to cluster services to facilitate service discovery inside the cluster. Here is the `alpaca-prod` service's domain name :

```
alpaca-prod.default.svc.cluster.local
```

- `alpaca-prod` is the service's name
- `default` is the service's namespace
- `svc` is Kubernetes resource designated by the domain name, here it's a service
- `cluster.local` is the cluster's base domain name

> - Referencing a service in the same namespace could be done directly with the service's name, here `alpaca-prod`
> - Referencing a service in another namespace could be done with the service's name and namespace, here `alpaca-prod.default`
> - A service can also be referenced by its full domain name

### Service endpoints

View a service's endpoints
```
kubectl get endpoints alpaca-prod
```

Watch a Kubernetes resource
```
kubectl get endpoints alpaca-prod --watch
```

### Expose a service outside cluster

By default, a service is exposed inside the cluster due to its `ClusterIP` type. The type can be changed to `NodePort` in order to expose the service outside the cluster throught a specific port.

```
kubectl expose deployment alpaca-prod --type=NodePort
```