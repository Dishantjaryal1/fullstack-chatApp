# 💬 Chatty - Real-Time Chat Application

Chatty is a full-stack real-time chat application built using the **MERN** stack (MongoDB, Express, React, Node.js) and **WebSockets (Socket.IO)**. It supports instant messaging, image sharing, authentication, and user presence tracking.

---


## 🔗 Live Demo 
[![Live Demo](https://img.shields.io/badge/Live-Demo-blue?style=for-the-badge&logo=vercel)](https://fullstack-chatapp-w70e.onrender.com/)

---

## 🚀 Features

- 🔐 User Authentication (Signup / Login with JWT)
- 🧑‍🤝‍🧑 Realtime 1:1 chat using **Socket.IO**
- 🖼️ Image sharing in messages (via Cloudinary)
- 🟢 Online/Offline user status indicator
- 🧭 Persistent message history (MongoDB)
- 💾 Profile picture upload
- 🪶 Responsive, minimal UI (Tailwind CSS + Lucide icons)

---

## 🛠️ Tech Stack

| Frontend          | Backend             | Real-time        | Storage           |
|-------------------|---------------------|------------------|--------------------|
| React + Vite      | Node.js + Express   | Socket.IO        | MongoDB (Mongoose) |
| Zustand (state)   | JWT Auth Middleware | WebSocket Server | Cloudinary (images) |
| Tailwind CSS      | REST API            |                  |                    |

---

## 📁 Project Structure

```bash
chatty/
├── frontend/             # React frontend (Vite)
│   └── src/
│       ├── components/
│       ├── pages/
│       ├── store/      # Zustand stores
│       └── App.jsx
├── backend/             # Express backend
│   ├── controllers/
│   ├── models/
│   ├── routes/
│   ├── lib/            # Cloudinary, socket setup, etc.
│   └── index.js
└── README.md
```

## ⚙️ Installation & Setup

### 🧩 Prerequisites

- **Node.js** >= 18
- **MongoDB** (local or [MongoDB Atlas](https://www.mongodb.com/cloud/atlas))
- **Cloudinary** account (for image uploads)

---

## 🔧 Backend Setup

```bash
cd backend
npm install

Create a .env file inside the server/ directory:

PORT=5001
MONGO_URI=your_mongodb_uri
JWT_SECRET=your_jwt_secret
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret

Start the backend:

npm run dev
```

## 💻 Frontend Setup
```
cd frontend
npm install
npm run dev
```

The frontend will run on http://localhost:5173 by default.
Make sure the backend is running on http://localhost:5001.

---

## 🚀 CI/CD Workflow

This project uses GitHub Actions for CI/CD automation and Render for deployment.

  ### ✅ CI/CD Pipeline Includes:

  - Automatic Testing before deploy (npm test)

  - Linting for code quality (npm run lint)

  - Deployment to Render only if all checks pass

  - triggered on: every push to the main branch

🛠️ GitHub Actions Workflow
```
      name: CI/CD Pipeline
      
      on:
        push:
          branches: [ main ]
        workflow_dispatch:
      
      jobs:
        build-and-test:
          runs-on: ubuntu-latest
          steps:
            - name: 📦 Checkout Code
              uses: actions/checkout@v3
      
            - name: 📥 Setup Node.js
              uses: actions/setup-node@v3
              with:
                node-version: 18
      
            - name: 📦 Install Dependencies
              run: npm install
              working-directory: ./client
      
            - name: ✅ Run Tests
              run: npm test
              working-directory: ./client
      
            - name: 💅 Run Linter
              run: npm run lint
              working-directory: ./client
      
        deploy:
          needs: build-and-test
          runs-on: ubuntu-latest
          if: success()
          steps:
            - name: 🚀 Trigger Render Deployment
              run: curl -X POST ${{ secrets.RENDER_DEPLOY_HOOK }}
```
---
ℹ️ Your Render deploy hook must be stored securely in GitHub secrets as RENDER_DEPLOY_HOOK.
