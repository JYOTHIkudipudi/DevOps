# MicroK8s Nginx Deployment Guide

Today, I successfully deployed an Nginx page using Kubernetes on MicroK8s with the following commands. This experience allowed me to deepen my understanding of Kubernetes deployment, scaling, and using YAML files for configuration. Below are the detailed steps I followed to set up and manage the deployment.

---

## Prerequisites

- **Windows 10/11** with WSL installed
- **MicroK8s** installed
- **Basic Kubernetes knowledge**
- **kubectl installed**

---

## Steps

### Step 1: Install WSL

1. Open **PowerShell** as Administrator.
2. Run the following command to install WSL:

```bash
wsl --install
```
3. Launch WSL and install MicroK8s:

```bash
sudo snap install microk8s --classic
```

---

## Step 2: Set Up MicroK8s

1. Start MicroK8s:

```bash
microk8s start
```

2. Check node status:

```bash
microk8s kubectl get nodes
```
- The status should show "Ready".

3. Alias kubectl to simplify commands:

```bash
alias kubectl="microk8s kubectl"
```

4. Verify node details:

```bash
kubectl get nodes -o wide
```

---

## Step 3: Enable Kubernetes Dashboard

1. Enable the dashboard:

```bash
microk8s enable dashboard
```

2. Start the dashboard proxy:

```bash
microk8s dashboard-proxy
```

- Copy the IP address from the output and paste it into a browser.
- Use the token provided to log in.

---

## Step 4: Deploy Nginx Application

1. Create a deployment using the Nginx image:

```bash
kubectl create deployment my-nginx --image=nginx
```

2. Check the deployment status:

```bash
kubectl get deployments -o wide
```

3. Verify pod status:

```bash
kubectl get pods
```
- The status should be **Running**.

4. Delete the deployment (if needed):

```bash
kubectl delete deployment my-nginx
```

---

## Step 5: Inspect and Edit the Deployment

1. Check pod details:

```bash
kubectl get pods -o wide
```

2. Check ReplicaSets:

```bash
kubectl get replicaset -o wide
```

3. Describe the deployment:

```bash
kubectl describe deployment my-nginx
```

4. Describe a specific pod:

```bash
kubectl describe pod <pod-name>
```

---

## Step 6: Update Deployment Version

1. Edit the deployment:

```bash
kubectl edit deployment my-nginx
```

- Change the image to `nginx:1.26`, save, and exit.

2. Verify pod updates:

```bash
kubectl get pods
```

---

## Step 7: Scale the Deployment

1. Edit the deployment and change replicas to `2`:

```bash
kubectl edit deployment my-nginx
```

2. Verify updated pods:

```bash
kubectl get pods
kubectl get replicaset
```

---

## Step 8: Interact with the Pod

1. Access the pod:

```bash
kubectl exec -it <pod-name> -- /bin/bash
```

2. View environment variables:

```bash
env
```

3. Exit the pod:

```bash
exit
```

---

## Step 9: Use YAML Files for Configuration

1. Navigate to the directory where the YAML files are stored:

```bash
cd /mnt/c/Users/your-folder
ls
```

2. Apply the deployment configuration:

```bash
kubectl apply -f my-app-deployment.yaml
```

3. Apply the service configuration:

```bash
kubectl apply -f my-app-service.yaml
```

4. Apply the ingress configuration:

```bash
kubectl apply -f my-app-ingress.yaml
```

5. Verify the configurations:

```bash
kubectl get deployments
kubectl get pods
kubectl get service
kubectl get ingress
```

---

## Step 10: Expose the Application

1. Copy the internal IP address from the node description:

```bash
kubectl describe node
```

2. Get the external port:

```bash
kubectl get service
```

3. Open the application in a browser using:

```
<internal-ip>:<port-number>
```

---

## Conclusion

This guide demonstrates how to deploy, scale, and manage an Nginx application using MicroK8s and Kubernetes. By following these steps, you can efficiently configure and expose your application while utilizing YAML files for better automation and management.
