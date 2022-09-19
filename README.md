# Kubernetes learning

STEPS: 

1. Install Docker desktop for MacOS https://docs.docker.com/desktop/install/mac-install/. Pods can contain multiple clusters but for the convenience always use one container in one pod. Services are the connection points between pods with static IP addresses.Pods will find each other through labels. Kubernetes STATE is saved at `etcd`. Core of distributed systems. Pod is aabstraction on top of container.

2. Install Kubernetes engine Minikube. Minikube runs inside a Docker container. `brew install minikube`. 

3. Initialise cluster `minikube start --driver docker`. Check cluster status `minikube status`. 

4. `kubectl get node` which is minikube dependency will show control plane and worker nodes. Each pod has a unique name, they can have common labels. 

5. Make sure all yaml files are correct to retrieve attributes and values from other files. Then type `kubectl apply -f mongo-config.yaml` also for other mongo files `kubectl apply -f mongo-secrets.yaml` and `kubectl apply -f mongo.yaml`, `kubectl apply -f webapp.yaml`.

6. Issue `kubectl get all` for all components,  `kubectl get node -o wide` for control plane, `kubectl get svc -o wide` for user plane. `kubectl describe service/webapp-service` `kubectl describe service/mongo-service` to find out more about the pods in detail, `minikube service webapp-service` to see pod in browser.

8. Helm: Package manager for Kubernetes.
9. Ingress: Route traffic to cluster
9. Service: Connection point between pods.
10. ConfigMap: external configuration of the app. DB_URL=mongo-db
11. Secret: used to store secret data. Stored base64 encoded.
12. Volumes: storage on local machine, for data persisence.
13. Stateful services:DB can not be replicated easily as it has its state for data persistency.


14. Worker nodes have multiple pods. 
	3 main processes: 
		- container runtime(docker) need to be installed in every node.
		- kubelet (interface with container runtime and node.
		- services (catches the request and forwards to respective pod)
		- kubeproxy (intelligent forward logic)

15. Kube master nodes:
	- API server: Cluster gateway,authentication, validation
	- Scheduler: Decides on which pod the new application will be deployed
	- Controller manager: Detects the dead node and recover 
	- etcd: key-value store. Cluster brain

16. Test on local env: To prevent cluster creating overhead. Minikube is used to demonstrate. Master and worker processes are installed in one docker container.

17. Kubectl: Service, Secret, ConfigMap, Node, API Server(UI, API, CLI). Kubectl create, delete components interact with the cluster.

Deployment manages a replicaset, replicaset manages pods.

18. Between pods the connectivity is established with labels and selectors.

19. Code blueprint nginx. `kubectl get deployment nginx-deployment -o yaml > nginx-deployment-result.yaml`
