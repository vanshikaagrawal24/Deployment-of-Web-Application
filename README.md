Deploying and Managing a Scalable Web Application Using Kubernetes

INTRODUCTION:
This project demonstrates the deployment and management of a scalable web application using Kubernetes. 
The application is containerized using Docker and deployed on Minikube, with features like auto-scaling, 
rolling updates, self-healing, persistent storage, and logging.

SETUP INSTRUCTIONS:

1. PREREQUISITES:
   - Install Docker
   - Install Minikube
   - Install Kubectl
   - Install Node.js

2. START MINIKUBE & VERIFY CLUSTER:
   - Run: minikube start
   - Verify nodes: kubectl get nodes

3. BUILD & PUSH DOCKER IMAGE:
   - Build image: docker build -t my-portfolio:v1 .
   - Verify image: docker images
   - (Optional) Push to Docker Hub:
     docker tag my-portfolio:v1 <dockerhub-username>/my-portfolio:v1
     docker push <dockerhub-username>/my-portfolio:v1

4. DEPLOY APPLICATION TO KUBERNETES:
   - Apply configurations: kubectl apply -f deployment.yaml
   - Apply service: kubectl apply -f service.yaml
   - Check running pods: kubectl get pods

5. EXPOSE THE APPLICATION:
   - Get the service URL: minikube service portfolio --url
   - Open the URL in a browser to verify it is running.

6. AUTO-SCALING (HPA):
   - Apply HPA configuration: kubectl apply -f hpa.yaml
   - Check status: kubectl get hpa
   - To simulate high CPU usage and trigger auto-scaling:
     kubectl run --rm -it --image=busybox stress-test -- /bin/sh
     while true; do wget -q -O- http://<SERVICE-IP>:<PORT>; done
   - Verify scaling: kubectl get pods -w

7. ROLLING UPDATES & ROLLBACKS:
   - Perform update: kubectl set image deployment/portfolio portfolio=newimage:v2
   - Rollback if needed: kubectl rollout undo deployment/portfolio

8. SELF-HEALING TEST:
   - Delete a pod: kubectl delete pod <POD_NAME>
   - Kubernetes should automatically recreate the pod.

9. PERSISTENT STORAGE TEST:
   - Apply persistent storage: kubectl apply -f pvc.yaml
   - Delete pod and verify data persistence: kubectl delete pod <POD_NAME>

10. LOGGING & PORT FORWARDING:
    - View logs: kubectl logs <POD_NAME>
    - Forward port: kubectl port-forward service/portfolio 3000:3000
    - Open browser and access application on port 3000.

KEY FEATURES:
- Minikube Cluster for local Kubernetes deployment
- Dockerized Node.js Application
- Kubernetes Deployment with scaling
- Auto-scaling using HPA (Horizontal Pod Autoscaler)
- Rolling Updates & Rollbacks for zero downtime
- Self-Healing Mechanism to automatically recreate pods
- Persistent Storage (PV & PVC) for data retention
- Logging & Monitoring for application activity

CONCLUSION:
This project successfully deploys and manages a scalable web application in Kubernetes using Minikube. 
It covers cluster setup, application deployment, scaling, updates, self-healing, persistent storage, and logging.

