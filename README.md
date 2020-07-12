# Kubernetes_Docker
### Kubernetes cheat sheet 

  - kubectl create -f deployment-definition.yaml
  
> Pod Example

```
apiVersion: v1
kind: Pod
metadata:
  name: postgres
  labels:
    tier: db-tier
spec:
  containers:
    - name: postgres
      image: postgres
      env:
        - name: POSTGRES_PASSWORD
          value: mysecretpassword
```

> ReplicaSet Example

```
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: frontend
  labels:
    app: mywebsite
    tier: frontend
spec:
  replicas: 4
  template:
    metadata:
      name: myapp-pod
      labels:
        app: myapp
    spec:
      containers:
        - name: nginx
          image: nginx
  selector:
    matchLabels:
      app: myapp
```

> Deployment Example

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: frontend
  labels:
    app: mywebsite
    tier: frontend
spec:
  replicas: 4
  template:
    metadata:
      name: myapp-pod
      labels:
        app: myapp
    spec:
      containers:
        - name: nginx
          image: nginx
  selector:
    matchLabels:
        app: myapp
```


  - kubectl get deployments
  - kubectl apply -f deployment-definition.yaml
  - kubectl set image <deployment_name> nginx=nginx:9.1.0
  - kubectl rollout status <deployment_name>
  - kubectl rollout history <deployment_name>
  - kubectl rollour undo <deployment_name>
