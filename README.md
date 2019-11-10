# trucos-kubernetes

```
mv k8s-1-16-2-do-0-sfo2-1571222951-kubeconfig.yaml .kube/config
```

```
kubectl get nodes
```


# Creando un Namespace

```
nano 00-namespace.yaml
```

```
kind: Namespace
apiVersion: v1
metadata:
  name: testing
```

```
kubectl apply -f 00-namespace.yaml
```

# Listar Namespace
```
kubectl get ns
```

# Creamos un servicio
```
kind: Service
apiVersion: v1
metadata:
  name: wordpress
spec:
  type: NodePort
  ports:
  - port: 80
    targetPort: 80
    nodePort: 30001
  selector:
    role: wordpress
```

```
kubectl -n testing  apply -f 01-wordpress-service.yaml
```

# Saber los servicios
```
kubectl -n testing get svc
```


# Creamos un ReplicationController
```

kind: ReplicationController
apiVersion: v1
metadata:
  name: wordpress
spec:
  replicas: 1
  template:
    metadata:
        labels:
            role: wordpress
    spec:
        containers:
        - name: wordpress
          image: wordpress:php7.1-apache
          imagePullPolicy: IfNotPresent
          ports:
            - containerPort: 80
```

```
kubectl -n testing  apply -f 02-wordpress-service.yaml
```

# Obtenemos pods
```
kubectl -n testing get pods
```

# Borrar el pods
```
kubectl -n testing delete pod wordpress-h7x2h
```

# Obtenemos el IP publico
```
kubectl get nodes -o wide
```

# Creamos un LoadBalancer
```
kind: Service
apiVersion: v1
metadata:
  name: wordpress-lb
spec:
  type: LoadBalancer
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
      name: http
  selector:
    role: wordpress
```

```
kubectl -n testing apply -f 03-wordpress-service.yaml
```





