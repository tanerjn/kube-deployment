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
11. Secret: used to store secret data. Stored base64 encoded. do `echo -n 'username' | base64 `. `echo -n 'password' | base64`
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

17. Kubectl: Service, Secret, ConfigMap, Node, API Server(UI, API, CLI). Kubectl create, delete components interact with the cluster. `kubectl get pod` `kubectl describe pod <pod>`

Deployment manages a replicaset, replicaset manages pods.

18. Between pods the connectivity is established with labels and selectors. name: mongo-config key: mongodb-password

19. `minikube service mongo-express-service` will give a publicly accesible mongo db.

19. Code blueprint nginx. `kubectl get deployment nginx-deployment -o yaml > nginx-deployment-result.yaml`

21. Namespaces help divide cluster: Ingress-NGINX, DB, ElasticStack, Monitoring. Don't use namespaces up to 10 users. Namespaces create for 2 diff teams. Use namespace attribute in config file. metadata: name: namespace:

22. `brew install kubectx` will install kubens tool. 

23. Kube-ingress: app, service, ingress component with internal service. ingress is to let pod deliver service with domain name. service will only let you use ip addresses. define host. `minikube addons enable ingress`. `kubectl get ns` `kubetctl get all` dashboard name to host. 

24. Forward from dashboard.com to kubernetes-dashboard service.`kubectl get ingress -n kubernetes-dashboard` find the IP, open `/etc/hosts/` add correspoinding IP for resolving for dashboard.com.

25. Ingress service: Multipath for same hosts. Google: Calendar, Search, Gmail.. path/analytics port:nnn path/shopping port:nnn

or using subdomains. analytics.google.com shopping.google.com. Subdomains analytics service -> analytics pod.

26. Define TLS attribute. SecretName: TLS  TLS can also get injected into domain over ingress service.

27. HELM is tha package manager for Kubertnets. One place to see Statefull sets, configMap, secret, user permissions, services. Helm charts available for monitoring, elastic search, database apps, mysql existing ones as well as custom. `helm search <>` public registries, private registries. 

28. HELM charts have templating engine for multi service cluster. `values.yaml`. similat to creating environmental vars file. Also useful, same application at different environemtns. `development`, `staging`, `produtcion`.

29. HELM Release management. `helm install ...` send from client to server(tiller). Tiller has Kubernets cluster to install helm charts. `helm upgrade .. `, `helm rollback ..`

30. Persistent volume by YAML for Google Cloud. Volume seperation. What type of storage will needed. Storage provisioner works like the Terraform. Persistent Volume Claim(PVC)

31. Stateful: MySQL, Mongo, ElasticSearch. Storage must be available in all nodes. 

32.  `kubectl get ingress <your-ingress-name>` && `kubectl describe ingress <your-ingress-name>`

33. with `helm install --values=values.yaml <chartname> values can be overridden on the fly.

34. Volume mounts for data, secret, config. Provisioner kubernetes/aws
35. steteful servicesdeployed with stateful component. One master and 2 slaves, whenever master updates slaves update themselves.

36. 4 main services: ClusterIP, Headless, NodePort, LoadBalancer. ClusterIP: Ingress: Selector: Service Endpoint. Headless and ClusterIP goes in hand.

37. Two container in the same pod. Second pod is mongo-exporter for prometheus. Name the second port accordingly. Headless pod-to-pod communication. Load Balancer for cloud native load balancer connections.

38. External dockerhub: Nexus. EKS management: Kibana. Docker orhectration: Swarm/KNS. Monitoring: Nagios/Prometheus. Infrastructure provisioning: Terraform. Configuration management: Ansible

![alt text](https://github.com/tanerjn/kube_demo/blob/master/blocks.png?raw=true)
