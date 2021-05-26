# Kubernetes Beginners Workshop

[Slides](https://docs.google.com/presentation/d/1_UQWk4VRxfT7Iml62Ja-55YXqbf_vh3spX4B_4AV104/edit?usp=sharing)

## Prerequisites 

- `kubectl` is installed (https://kubernetes.io/docs/tasks/tools/)

- Kubernetes Cluster
    - [minikube](https://minikube.sigs.k8s.io/)
    - [microk8s](https://microk8s.io/)
    - Vendevio Dev Cluster [rancher-dev](https://cluster.vendev.io)

## Cheat Sheet

    kubectl get all -n <namespace>

    kubectl get <kind> <name>

    kubectl describe <kind>/<name>

    kubectl logs -f <pod-name>

    kubectl port-forward pod/<pod-name> 8080:80

    kubectl exec -ti <pod-name> -- /bin/bash

    kubectl apply -f config.yml

    kubectl delete -f config.yml


## Exercises

### 01 - Namespaces

    kubectl create namespace <first-name>

    kubectl delete namespace <first-name>

    kubectl apply -f namespace.yml

### 02 - Deployment

    =>  Deployment Name
    =>  Image: nginxdemos/hello:0.1

    kubectl apply -n <first-name> -f Exercises/02-Deployment/deployment.yml 

    =>  replicas: 3

    => nginxdemos/hello:0.2

    kubectl get pods -n <first-name>
    kubectl port-forward -n <first-name> pod/<pod-name> 8080:80

### 03 - Services

    kubectl port-forward -n <first-name> service/<service-name> 8080:80

### 04 - Ingress

    => Host + Service Name

    kubectl apply -n <first-name> -f Exercises/04-Ingress/ingress.yml 

    kubectl apply -n <first-name> -f Exercises/04-Ingress/ingress-tls.yml 

### 05 - Persistence

    kubectl apply -n <first-name> -f Exercises/05-Persistence/postgres-pvc.yml

    kubectl apply -n <first-name> -f Exercises/05-Persistence/postgres.yml 

    # Postgres

    kubectl port-forward -n <first-name> service/postgres 5432:5432

    kubectl exec -ti -n <namespace> <postgres-pod> -- /bin/bash
    psql -U postgres
    exit

    kubectl exec -n <first-name> <postgres-pod> -- pg_dump -U postgres

### 06 - Config

    kubectl apply -n <first-name> -f Exercises/06-Config/postgres-secret.yml

    kubectl apply -n <first-name> -f Exercises/06-Config/postgres.yml

### 07 - Jobs

    kubectl apply -n <first-name> -f Exercises/07-Jobs/postgres-secret.yml

    kubectl describe -n tobias <job-name>

    kubectl get pods -n tobias

    kubectl logs -f -n tobias <job-pod-name>