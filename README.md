# Task 2: Kubernetes Deployment
**Author: Utpal Raj**  
**Date: October 20, 2025**

## Project Overview
This repository contains the Kubernetes deployment configuration for the Task Management application from Task 1. The deployment includes containerization of the Spring Boot application and MongoDB database with proper persistence and environment configuration.

## Requirements Completed
✅ Create Dockerfile for backend  
✅ Build Docker image  
✅ Create Kubernetes manifests  
✅ Deploy MongoDB in separate pod  
✅ Use environment variables  
✅ Expose app from host machine  
✅ Persistent volume for MongoDB  
✅ Modify PUT /execute with k8s API  
✅ Create pods programmatically  

## Implementation Details

### 1. Docker Configuration
- Backend Dockerfile created with multi-stage build
- Application built using Maven and JDK 11
- Runtime optimized with JRE-only image

### 2. Kubernetes Manifests
- `backend.yaml`: Spring Boot application deployment
- `mongo.yaml`: MongoDB StatefulSet with persistence
- Environment variables for configuration
- NodePort service for external access

### 3. Storage Configuration
- Persistent Volume Claims for MongoDB
- Data persistence across pod restarts
- Proper volume mounts configured

### 4. Environment Variables
```yaml
environment:
  - MONGODB_URI=mongodb://mongo:27017/tasks
  - EXECUTION_MODE=kubernetes
```

### 5. K8s Integration
- Added K8sExecService.java for pod management
- Busybox container for command execution
- Proper RBAC configuration

## Deployment Steps

1. Start Kubernetes cluster (Docker Desktop/Minikube)
```bash
# Verify cluster is running
kubectl cluster-info
```

2. Deploy MongoDB
```bash
kubectl apply -f k8s/mongo.yaml
```

3. Deploy Backend Application
```bash
kubectl apply -f k8s/backend.yaml
```

4. Verify Deployment
```bash
kubectl get pods
kubectl get services
```

## Directory Structure
```
kaiburr-task-2/
├── k8s/
│   ├── backend.yaml
│   └── mongo.yaml
├── screenshots/
│   ├── docker-status.png
│   ├── pods-running.png
│   └── api-test.png
├── src/
│   └── main/
│       └── java/
│           └── com/
│               └── kaiburr/
│                   └── tasks/
│                       └── service/
│                           └── K8sExecService.java
└── README.md
```

## Implementation Screenshots

### Docker Desktop Status
![Docker Status](screenshots/docker-status.png)
*Docker Desktop running with Kubernetes enabled - October 20, 2025*

### Kubernetes Pods Running
![Pods Running](screenshots/pods-running.png)
*All pods running successfully with MongoDB persistence - October 20, 2025*

### API Test with K8s Integration
![API Test](screenshots/api-test.png)
*Task execution in Kubernetes pod - October 20, 2025*

## Technical Details

### MongoDB StatefulSet
- Replica count: 1
- Persistent volume: 1GB
- Port: 27017

### Backend Service
- Type: NodePort
- Port: 8080
- Target Port: 8080
- Node Port: 30007

### Container Resources
```yaml
resources:
  limits:
    memory: "512Mi"
    cpu: "500m"
  requests:
    memory: "256Mi"
    cpu: "250m"
```

## Verification Steps
1. ✅ MongoDB pod running with persistence
2. ✅ Backend pod connected to MongoDB
3. ✅ Service accessible from host machine
4. ✅ Tasks executing in separate pods
5. ✅ Data persisting across restarts

## Author
**Utpal Raj**
- Date: October 20, 2025
- Assessment: Kaiburr Technical Assessment Task 2

## License
This project is open source and available under the MIT License.