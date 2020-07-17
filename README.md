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
  
    
  # Imperative Commands
 
        - POD
        Create an NGINX Pod

        kubectl run nginx --image=nginx



        Generate POD Manifest YAML file (-o yaml). Don't create it(--dry-run)

        kubectl run nginx --image=nginx  --dry-run=client -o yaml



        - Deployment
        Create a deployment

        kubectl create deployment --image=nginx nginx



        Generate Deployment YAML file (-o yaml). Don't create it(--dry-run)

        kubectl create deployment --image=nginx nginx --dry-run=client -o yaml



        IMPORTANT:

        kubectl create deployment does not have a --replicas option. You could first create it and then scale it using the kubectl scale command.



        Save it to a file - (If you need to modify or add some other details)

        kubectl create deployment --image=nginx nginx --dry-run=client -o yaml > nginx-deployment.yaml

        You can then update the YAML file with the replicas or any other field before creating the deployment.



        - Service
        Create a Service named redis-service of type ClusterIP to expose pod redis on port 6379

        kubectl expose pod redis --port=6379 --name redis-service --dry-run=client -o yaml

        (This will automatically use the pod's labels as selectors)

        Or

        kubectl create service clusterip redis --tcp=6379:6379 --dry-run=client -o yaml  (This will not use the pods labels as selectors, instead it will assume selectors as app=redis. You cannot pass in selectors as an option. So it does not work very well if your pod has a different label set. So generate the file and modify the selectors before creating the service)



        Create a Service named nginx of type NodePort to expose pod nginx's port 80 on port 30080 on the nodes:

        kubectl expose pod nginx --port=80 --name nginx-service --type=NodePort --dry-run=client -o yaml

        (This will automatically use the pod's labels as selectors, but you cannot specify the node port. You have to generate a definition file and then add the node port in manually before creating the service with the pod.)

        Or

        kubectl create service nodeport nginx --tcp=80:80 --node-port=30080 --dry-run=client -o yaml

        (This will not use the pods labels as selectors)

        Both the above commands have their own challenges. While one of it cannot accept a selector the other cannot accept a node port. I would recommend going with the `kubectl expose` command. If you need to specify a node port, generate a definition file using the same command and manually input the nodeport before creating the service.



        Reference:

        https://kubernetes.io/docs/reference/kubectl/conventions/
   
