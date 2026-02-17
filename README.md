# MEAN Stack CRUD Application - DevOps Deployment

Full-stack MEAN (MongoDB, Express, Angular, Node.js) application deployed on AWS EC2 with Docker containerization and CI/CD pipeline.

## 🚀 Live Application

**URL:** http://13.232.185.205

## 🏗️ Architecture
```
Browser → Nginx (Port 80) → Angular Frontend (Port 4200)
                          → Node.js Backend (Port 8080) → MongoDB (Port 27017)
```

## 🛠️ Technology Stack

- **Frontend:** Angular 15
- **Backend:** Node.js, Express.js
- **Database:** MongoDB 6
- **Containerization:** Docker, Docker Compose
- **Cloud Platform:** AWS EC2 (Ubuntu 22.04)
- **Web Server:** Nginx (Reverse Proxy)
- **CI/CD:** Jenkins
- **Version Control:** Git, GitHub

## 📁 Project Structure
```
mean-crud-devops/
├── backend/
│   ├── Dockerfile
│   ├── app/
│   │   ├── config/
│   │   │   └── db.config.js
│   │   ├── controllers/
│   │   ├── models/
│   │   └── routes/
│   └── server.js
├── frontend/
│   ├── Dockerfile
│   ├── nginx.conf
│   └── src/
├── nginx/
│   └── nginx.conf
├── docker-compose.yml
└── screenshots/
```

## 🐋 Docker Configuration

### docker-compose.yml

Orchestrates 4 services:
- **MongoDB:** Database on port 27017
- **Backend:** Node.js API on port 8080
- **Frontend:** Angular app on port 4200 (internal port 80)
- **Nginx:** Reverse proxy on port 80

### Key Configuration

**Frontend Port Mapping:**
```yaml
frontend:
  ports:
    - "4200:80"  # Maps host 4200 to container 80
```

**Backend Database Connection:**
```yaml
backend:
  environment:
    - MONGODB_URI=mongodb://mongo:27017/mean-crud
  volumes:
    - ./db.config.js:/app/app/config/db.config.js
```

## 🚀 Deployment Steps

### 1. Clone Repository
```bash
git clone https://github.com/MuruganM09/mean-crud-devops.git
cd mean-crud-devops
```

### 2. Build Docker Images
```bash
# Backend
cd backend
docker build -t murugan29/mean-backend:latest .
docker push murugan29/mean-backend:latest

# Frontend
cd ../frontend
docker build -t murugan29/mean-frontend:latest .
docker push murugan29/mean-frontend:latest
```

### 3. AWS EC2 Setup

- **Instance Type:** t2.micro
- **OS:** Ubuntu 22.04 LTS
- **Security Group Ports:**
  - 22 (SSH)
  - 80 (HTTP)
  - 8080 (Backend API)
  - 8081 (Jenkins)

**Install Docker:**
```bash
sudo apt update
sudo apt install -y docker.io docker-compose
sudo usermod -aG docker ubuntu
```

### 4. Deploy Application
```bash
cd ~/mean-app
docker-compose up -d
```

### 5. Verify Deployment
```bash
docker-compose ps
# All containers should show "Up"
```

## 📸 Screenshots

### Application Interface

#### Homepage - Tutorials List
![App Homepage](./screenshots/app-homepage.png)

#### Create Tutorial Form
![Create Tutorial](./screenshots/create-tutorial.png)

#### Tutorials Management
![Tutorials List](./screenshots/tutorials-list.png)

---

### Infrastructure & Deployment

#### Docker Containers Running
![Docker Compose](./screenshots/docker-compose-ps.png)

#### Docker Hub Repositories
![Docker Hub](./screenshots/dockerhub-images.png)

---

### AWS Infrastructure

#### EC2 Instance Details
![EC2 Instance](./screenshots/ec2-instance.png)

#### Security Group Configuration
![Security Groups](./screenshots/security-groups.png)

---

### CI/CD Pipeline

#### Jenkins Dashboard
![Jenkins Dashboard](./screenshots/jenkins-dashboard.png)

---

### Source Code Repository

#### GitHub Repository
![GitHub Repo](./screenshots/github-repo.png)

## 🔧 Key Features

- ✅ Full CRUD operations (Create, Read, Update, Delete)
- ✅ RESTful API architecture
- ✅ Responsive Angular frontend
- ✅ Containerized microservices
- ✅ Nginx reverse proxy
- ✅ Persistent MongoDB storage
- ✅ Docker Compose orchestration
- ✅ AWS cloud deployment
- ✅ Jenkins CI/CD pipeline

## 🌐 API Endpoints

- `GET /api/tutorials` - Get all tutorials
- `GET /api/tutorials/:id` - Get tutorial by ID
- `POST /api/tutorials` - Create new tutorial
- `PUT /api/tutorials/:id` - Update tutorial
- `DELETE /api/tutorials/:id` - Delete tutorial
- `DELETE /api/tutorials` - Delete all tutorials

## 🔐 Configuration

### Frontend API Configuration
Location: `frontend/src/app/services/tutorial.service.ts`
```typescript
const baseUrl = '/api/tutorials';  // Proxied through Nginx
```

### Nginx Reverse Proxy
Location: `nginx/nginx.conf`
- Routes `/` to frontend
- Routes `/api/` to backend

### Database Connection
Location: `backend/app/config/db.config.js`
```javascript
module.exports = {
  url: process.env.MONGODB_URI || "mongodb://mongo:27017/mean-crud"
};
```

## 🎯 Deployment Commands Reference

**Start Application:**
```bash
docker-compose up -d
```

**Stop Application:**
```bash
docker-compose down
```

**View Logs:**
```bash
docker-compose logs -f
```

**Restart Service:**
```bash
docker-compose restart [service-name]
```

**Pull Latest Images:**
```bash
docker-compose pull
```

## 🐛 Troubleshooting

**Backend can't connect to MongoDB:**
- Check MONGODB_URI environment variable
- Verify mongo container is running
- Check db.config.js override

**Frontend shows connection errors:**
- Verify API endpoint is `/api/tutorials` (not `localhost:8080`)
- Check nginx proxy configuration
- Clear browser cache

**Port conflicts:**
- Backend uses port 8080
- Frontend internal port 80, mapped to host 4200
- Nginx uses port 80
- Jenkins uses port 8081

## 👨‍💻 Author

**Murugan M**
- GitHub: [@MuruganM09](https://github.com/MuruganM09)
- Repository: [mean-crud-devops](https://github.com/MuruganM09/mean-crud-devops)

## 📄 License

This project is for educational purposes as part of a DevOps assessment.

## 🎓 Project Highlights

- Complete containerization of a full-stack application
- Multi-container orchestration with Docker Compose
- Cloud deployment on AWS EC2
- Reverse proxy configuration with Nginx
- CI/CD pipeline setup with Jenkins
- Production-grade configuration management
- Comprehensive documentation with visual evidence

---

**Project Status:** ✅ Deployed and Running

**Last Updated:** February 17, 2026
