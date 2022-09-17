# Kubernetes learning directory

STEPS: 

1. Install Docker desktop for MacOS https://docs.docker.com/desktop/install/mac-install/. Pods can contain multiple clusters but for the convenience always use one container in one pod. Services are the connection points between pods with static IP addresses.Pods will find each other through labels. Kubernetes STATE is saved at `etcd`. Core of distributed systems.

2. Install Kubernetes engine Minikube. Minikube runs inside a Docker container. `brew install minikube`. 

3. Initialise cluster `minikube start --driver docker`. Check cluster status `minikube status`. 

4. `kubectl get node` which is minikube dependency will show control plane and worker nodes. Each pod has a unique name, they can have common labels. 

5. Make sure all yaml files are correct to retrieve attributes and values from other files. Then type `kubectl apply -f mongo-config.yaml` also for other mongo files `kubectl apply -f mongo-secrets.yaml` and `kubectl apply -f mongo.yaml`, `kubectl apply -f webapp.yaml`.

6. `kubectl get all` to list all cluster components. `kubectl describe service/webapp-service` `kubectl describe service/mongo-service` to find out more about the pods in detail.



