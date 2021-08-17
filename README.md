### Horizontal Pod Autoscaler
The Horizontal Pod Autoscaler automatically scales the number of Pods in a replication controller, deployment, replica set or stateful set based on observed ```CPU utilization and Memory``` (or, with custom metrics support, on some other application-provided metrics).


### Prerequisites
  - Kubernetes Cluster (I tested with v.1.21.2 on Digital Ocean)
  - Metric Server Installed
  - Resource limit in deployment

### Setup Metric Server
Latest Metrics Server release can be installed by running:
```console
$ kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```

### Verify
  - The pod metric server is running
  - The output of the metric server in a pod (CPU and memory)

### Setup Deployment & HPA

  1. Clone this repo 
     ```console
     $ git clone https://github.com/armansaa/HPA-K8s.git
     ```
  2. Go to HPA-K8s directory
     ```console
     $ cd HPA-K8s/
      ```
  3. Apply `my-deployment` file
     ```console
     $ kubectl apply -f my-deployment.yaml
     ```
  4. Check pod status : 
     ```console
     $ kubectl get pod
     ```
  5. We can retrieve a lot more information about pod using : 
     ```console
     $ kubectl describe pod hello-xxx-xxx
     ```
  6. Create HPA using this command : 
     ```console
     $ kubectl apply -f hpa-metrics.yaml
     ```
  7. Check HPA status :
     ```console
     $ kubectl get hpa
     ```

### Testing autoscale 
  1. Stress testing using load generator : 
     ```console
     $ kubectl apply -f load-generator.yaml
     ```
  2. After load generator runs, check the status of HPA : 
     ```console
     $ kubectl get hpa
     ```
  3. Wait for a few minutes, HPA starts scheduling more pods
  4. You can check the number of pods using : 
     ```console
     $ kubectl get pod
     ```
  

