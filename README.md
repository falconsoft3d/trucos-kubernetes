# trucos-kubernetes

```
mv k8s-1-16-2-do-0-sfo2-1571222951-kubeconfig.yaml .kube/config
```

```
kubectl get nodes
```


# Creando un Namespace

```
00-namespace.yaml
```

```
kind: Namespace
apiVersion: v1
metadata:
  name: testing
```


```
kubctl apply 00-namespace.yaml
```


