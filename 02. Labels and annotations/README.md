# Labels and annotations

> This folder is the chapter **6 - Labels and annotations** workspace.
>
> Each `.yaml` file is a Kubernetes resource manifest used in this chapter, sorted by their appearance order in the book.

## Cheatsheet

- **Labels** are used to define identification metadatas on resources, useful to gaher, exploit and display resources.
- **Annotations** are used store metadatas on resources, useful for tools and library consuming the cluster's API.

### Limitations

- **Label key** is a string composed of an optional prefix and a required name, separated by a `/`, using the following format :
  - The prefix should be a DNS subdomain, limited to 253 characters.
  - The name should start and end by an alphanumeric character and could include  `-`, `.` and `_` between alphanumeric characters, limited to 63 characters.
- **Label value** is a string limited to 63 characters, with the same format as the key.
- **Annotation key** use the same format as the label key.
- **Annotation value** is a string without limitation.

### Create labels

Create a pod with an `app` and an `env` labels
```
kubectl run kuard --image=gcr.io/kuar-demo/kuard-amd64:1 --labels="app=kuard,env=prod"
```

Add or update a label on a pod
```
kubectl label pods kuard ver=2
```

Remove a label on a pod
```
kubectl label pods kuard ver-
```

### View labels

View all pods with their labels
```
kubectl get pods --show-labels
```

View all pods with the `app` label as a column
```
kubectl get pods -L app
```

### Labels selectors

View pods with given labels (logical AND)
```
kubectl get pods --selector="env=prod,ver=2"
```

View pods having a label inside a given list of value (logical OR)
```
kubectl get pods --selector="env in (prod, test)"
```

View pods having a label with given key
```
kubectl get pods --selector="ver"
```

> Selectors can be used with other commands like `kubectl delete`.

#### Selectors operators

| Operator                     | Description                            |
|------------------------------|----------------------------------------|
| `key=value`                  | `key` equals `value`                   |
| `key!=value`                 | `key` not equals `value`               |
| `key in (value1, value2)`    | `key` equals `value1` or `value 2`     |
| `key notin (value1, value2)` | `key` not equals `value1` or `value 2` |
| `key`                        | `key` exists                           |
| !`key`                       | `key` not exists                       |
