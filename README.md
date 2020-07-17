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
  - kubectl scale --replicas=2 rs/replica-set
  
  # CKAD Exam Tips
  
  - Certified Kubernetes Application Developer: https://www.cncf.io/certification/ckad/
  - Candidate Handbook: https://www.cncf.io/certification/candidate-handbook
  - Exam Tips: https://www2.thelinuxfoundation.org/ckad-tips
  - Keep the code - DEVOPS15 - handy while registering for the CKA or CKAD exams at Linux Foundation to get a 15% discount
  
  # Kubernetes Command Line 
  - kubectl run hello-world
  - kubectl cluster-info
  - kubectl get nodes
  - kubectl get pods
  
  # Kubernetes Labs
  - https://kodekloud.com/courses/kubernetes-certification-course-labs/lectures/12039428
  - https://kodekloud.com/courses/kubernetes-certification-course-labs/lectures/12039434
  - https://kodekloud.com/courses/kubernetes-certification-course-labs/lectures/12039431
  
  #Imperative Commands
   In kubernetes you can use imperative commands as well, and using Kubectl you can generate Yaml file from it, Rather than writing it from scratch.
   
    ## Create a Pod
      `kubectl run nginx --image=nginx -o yaml > pod-definition.yaml`
   
