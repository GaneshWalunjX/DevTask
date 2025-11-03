# DevTask — Fullstack Kanban with DevOps Automation

## Project Description
DevTask is a fullstack Kanban task management application designed to demonstrate **end‑to‑end DevOps practices**.  
It showcases how modern applications can be **built, containerized, tested, and deployed** using CI/CD pipelines, Kubernetes, Ansible, and Infrastructure as Code.  

---


## Project Info / Features

- **Frontend**: React + Vite SPA  
- **Backend**: Java (Spring Boot REST API)  
- **Database**: MongoDB  
- **CI/CD**: GitLab pipelines with build → test → deploy  
- **Containerization**: Docker images tagged with `$CI_COMMIT_SHORT_SHA` + `latest`  
- **Orchestration**: Kubernetes deployments in `devtask` namespace  
- **Registry**: GitLab Container Registry (private)  
- **Automation**: **Ansible** for provisioning and deployment tasks  
- **Security**: `imagePullSecrets` for private image pulls  
- **Scalability**: Resource requests/limits defined for pods  

---

## Run & Deploy

**Clone the repository**
git clone <https://github.com/GaneshWalunjX/DevTask.git>
cd stackbridge


**Frontend**
```bash
cd frontend
npm install
npm run dev
```

**Backend (Java Spring Boot)**
```bash
cd backend
./mvnw spring-boot:run
```

**MongoDB (local via Docker)**
```bash
docker run -d -p 27017:27017 --name mongo mongo
```

---

### Docker Build & Run
**Frontend**
```bash
docker build -t devtask-frontend:local ./frontend
docker run -p 3000:3000 devtask-frontend:local
```

**Backend**
```bash
docker build -t devtask-backend:local ./backend
docker run -p 8080:8080 -e MONGO_URL=mongodb://host.docker.internal:27017/devtask devtask-backend:local
```

---

### Kubernetes Deployment
1. Create namespace:
```bash
kubectl apply -f k8s/namespace.yaml

```

2. Create registry secret:
```bash
kubectl create secret docker-registry gitlab-registry-secret \
  --docker-server=registry.gitlab.com \
  --docker-username=<gitlab-username> \
  --docker-password=<personal-access-token> \
  --docker-email=<email> \
  -n devtask
```

3. Apply manifests:
```bash
kubectl apply -f k8s/ -n devtask
```

---

## Tools & Technologies

- **Languages**: Java (Spring Boot), JavaScript (React)  
- **Containers**: Docker  
- **Orchestration**: Kubernetes  
- **CI/CD**: GitLab CI/CD  
- **Registry**: GitLab Container Registry  
- **Database**: MongoDB  
- **Automation**: Ansible  
- **IaC (planned)**: Terraform  

---
