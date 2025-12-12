# Cricket Academy - Kubernetes Application

A full-stack Cricket Academy management application deployed on Kubernetes with Minikube. This project demonstrates a microservices architecture with a Flask frontend, Spring Boot backend, and PostgreSQL database.

## 🏗️ Architecture

- **Frontend**: Python Flask application (port 5000)
- **Backend**: Java Spring Boot REST API service (port 8080)
- **Database**: PostgreSQL 16 with persistent storage
- **Orchestration**: Kubernetes resources including ConfigMap, Secret, PVC, Deployments, and Services

## 🚀 Getting Started

### Prerequisites

- Docker
- Minikube
- kubectl

### Source

***For the latest updates and more information, visit the [GitHub repository](https://github.com/Thamaraikannan00011/Cricket-Academy-Project.git).***

## 📦 Deployment

### 1. Start Minikube
```bash
minikube start
```

### 2. Deploy All Resources

Assuming your manifest file is named `cricket-compose.yml`:
```bash
kubectl create -f cricket-compose.yml
```

### 3. Verify Deployment

Check that all pods are running:
```bash
kubectl get pods -A
kubectl get svc -A
```

**Expected output:**

**Pods:**
- `cricket-db` - Running
- `cricket-backend` - Running
- `cricket-frontend` - Running

**Services:**
- `cricket-db` (ClusterIP, port 5432)
- `cricket-backend` (ClusterIP, port 8080)
- `cricket-frontend` (NodePort, nodePort 30001)

## 🔌 Network Configuration

### Port Mappings

| Component | Container Port | Service Port | Node Port | Type |
|-----------|---------------|--------------|-----------|------|
| PostgreSQL | 5432 | 5432 | - | ClusterIP |
| Backend | 8080 | 8080 | - | ClusterIP |
| Frontend | 5000 | 80 | 30001 | NodePort |

### Connection Details

- **Database Connection**: 
```
  jdbc:postgresql://cricket-db:5432/cricket_academy
```

- **Backend API**: 
```
  http://cricket-backend:8080/api
```

- **Frontend Access**: 
```
  NodePort 30001 → Service port 80 → Pod port 5000
```

### Traffic Flow
```
Browser → NodePort 30001 → Service (port 80) → Frontend Pod (port 5000) 
         → Backend Service (port 8080) → Database Service (port 5432)
```

## 🌐 Accessing the Application

### Get the Service URL

When using the Docker driver on Linux, use the Minikube service helper:
```bash
minikube service cricket-frontend --url
```

This will example output a URL like:
```
http://127.0.0.1:37387
```

**Important:** Keep this terminal window open while using the application.

### Open in Browser

1. Copy the printed URL (e.g., `http://127.0.0.1:37387`)
2. Paste it into your browser's address bar
3. Press Enter
4. You should see the Cricket Academy frontend

## ⚡ Quick Start Summary
```bash
# 1. Start Minikube cluster
minikube start --driver=docker

# 2. Deploy all Kubernetes resources
kubectl create -f cricket-compose.yml

# 3. Get the application URL
minikube service cricket-frontend --url

# 4. Copy the URL and open it in your browser
```

## 🛠️ Useful Commands

### View logs
```bash
# Frontend logs
kubectl logs -l app=cricket-frontend

# Backend logs
kubectl logs -l app=cricket-backend

# Database logs
kubectl logs -l app=cricket-db
```

### Delete resources
```bash
kubectl delete -f cricket-compose.yml
```

### Stop Minikube
```bash
minikube stop
```

## 📝 Project Structure
```
Cricket-Academy-Project/
├── cricket-compose.yml    # Kubernetes manifests
├── frontend/              # Flask application
├── backend/               # Spring Boot application
└── README.md             # This file
```
