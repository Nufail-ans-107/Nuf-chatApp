[![Fork Button](https://img.shields.io/github/forks/iemafzalhassan/full-stack_chatApp?style=social)](https://github.com/iemafzalhassan/full-stack_chatApp/fork)


# Real-Time Chat Application
This project is forked from [original repo link].
Changes I made:
- Added Kubernetes manifests
- Improved authentication logic
- Fixed deployment scripts


Welcome to the **Full Stack Realtime Chat App** project, where we're building a scalable and secure real-time chat experience using the latest technologies. Whether you're a seasoned developer or a beginner, we invite you to contribute and be a part of this exciting journey!

https://streamable.com/n3l8ur  - This is my Project deployment screen recording (Minikube cluster)


Architecture---
<img width="1529" height="413" alt="diagram-export-14-09-2025-01_27_57" src="https://github.com/user-attachments/assets/614c32af-1e00-47cf-81cc-48617718de66" />


## Table of Contents
* [Introduction](#introduction)
* [Features](#features)
* [Tech Stack](#tech-stack)
* [Getting Started](#getting-started)
* [Building the Backend](#building-the-backend)
* [Running the Application](#running-the-application)
* [Contributing](#contributing)
* [Future Plans](#future-plans)
* [License](#license)

## 📝 Introduction

This project aims to provide a real-time chat experience that's both scalable and secure. With a focus on modern technologies, we're building an application that's easy to use and maintain.

## ✨ Features


* **Real-time Messaging**: Send and receive messages instantly using Socket.io 
* **User Authentication & Authorization**: Securely manage user access with JWT 
* **Scalable & Secure Architecture**: Built to handle large volumes of traffic and data 
* **Modern UI Design**: A user-friendly interface crafted with React and TailwindCSS 
* **Profile Management**: Users can upload and update their profile pictures 
* **Online Status**: View real-time online/offline status of users 


## 🛠️ Tech Stack


* **Backend:** Node.js, Express, MongoDB, Socket.io
* **Frontend:** React, TailwindCSS
* **Containerization:** Docker
* **Orchestration:** Kubernetes (planned)
* **Web Server:** Nginx
* **State Management:** Zustand
* **Authentication:** JWT
* **Styling Components:** DaisyUI


### 🔧 Prerequisites


* **[Node.js](https://nodejs.org/)** (v14 or higher)
* **[Docker](https://www.docker.com/get-started)** (for containerizing the app)
* **[Git](https://git-scm.com/downloads)** (to clone the repository)


### 📝 Environment Configuration

Create a `.env` file in the root directory with the following configuration:

```env
# Database Configuration
MONGODB_URI=mongodb://root:admin@mongo:27017/chatApp?authSource=admin&retryWrites=true&w=majority

# JWT Configuration
JWT_SECRET=your_jwt_secret_key

# Server Configuration
PORT=5001
NODE_ENV=production
```

> **Note:** 
> - Replace `your_jwt_secret_key` with a strong secret key
> - For local development without Docker, change `MONGODB_URI` to `mongodb://localhost:27017/chatApp`
> - You can use command ```echo "Text what you want" | base64

### Clone the Repository

```bash
git clone https://github.com/iemafzalhassan/full-stack_chatApp.git
```

🏗️ Build and Run the Application

Follow these steps to build and run the application:

1. Build & Run the Containers:

```bash
cd full-stack_chatApp
```
```bash
docker-compose up -d --build
```

2. Access the application in your browser:

```
http://localhost
```
---

## 🛠️ Getting Started

Follow these simple steps to get the project up and running on your local Host using docker.

```bash
git clone https://github.com/iemafzalhassan/full-stack_chatApp.git
```

```bash
cd full-stack_chatApp
```
## Create a Docker network:

```bash
docker network create full-stack
```

## 🛠️ Building the Frontend

```bash
cd frontend
```

```bash
docker build -t full-stack_frontend .
```

### Run the Frontend container:

```bash
docker run -d --network=full-stack  -p 5173:5173 --name frontend full-stack_frontend:latest
```
#### The frontend will now be accessible on port 5173.


## Run the MongoDB Container:

```bash
docker run -d -p 27017:27017 --name mongo mongo:latest
```
---

## 🛠️ Building the Backend

```bash
cd backend
```

### Build the Backend image:

```bash
docker build -t full-stack_backend .
```

### Run the Backend container:

```bash
docker run -d --network=full-stack --add-host=host.docker.internal:host-gateway -p 5001:5001 --env-file .env full-stack_backend
```
#### This will build and run the backend container, exposing the backendAPI on port 5001.

`Backend API: http://localhost:5001`

### To Verify the conncetion between backend and databse:
```bash
docker-compose logs -f
```

### Once the backend and frontend containers are running, you can access the application in your browser:

`Frontend: http://localhost`


You can now interact with the real-time chat app and start messaging!

---



### 🤝 Contributing
I have added k8s files and deploy on minikube cluster....Below are the SS and screen recording of application




## 📚 Project Snapshots:

![Settings](frontend/public/settings.png)

![chat](frontend/public/chat.png)

![logout](/frontend/public/logout.png)

![Login](/frontend/public/login.png)

https://streamable.com/n3l8ur



## 📜 License


This project is licensed under the MIT License. See the LICENSE file for more details.


















