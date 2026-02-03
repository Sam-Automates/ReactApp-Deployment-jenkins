# ReactApp-Deployment-jenkins
🛠️ Real-world DevOps CI/CD pipeline for React apps featuring zero downtime, environment-based deployments, and secure SSH automation using Jenkins.


## 🧠 About This Repository

This repository showcases a **real-world Jenkins CI/CD pipeline** for deploying a **React application** with **zero downtime**.

No demo tricks.  
No fake examples.  
**Same approach used in production environments.** 💪

---

## ✨ Key Features

- 🚀 Zero Downtime Deployment
- 🧩 Jenkins Declarative Pipeline
- 🌍 Staging & Production Environments
- 🔐 Secure SSH-based Deployment
- 🔁 Atomic Build Swap
- 🧹 Automatic Jenkins Workspace Cleanup
- 🏗️ Production-Ready Pipeline Structure

---

## 🚦 Branch & Environment Strategy

| Branch | Environment | Description |
|------|------------|-------------|
| `staging` | 🧪 Staging | Testing & QA |
| `main` | 🚀 Production | Live Users |

---

## 🔄 Pipeline Flow (Step-by-Step)

```text
Code Push
   ↓
Jenkins Trigger
   ↓
Environment Selection
   ↓
Secure SSH Login
   ↓
Git Sync
   ↓
npm install
   ↓
npm run build
   ↓
Build Validation
   ↓
Atomic Swap (Zero Downtime)
   ↓
Jenkins Workspace Cleanup
   ↓
🎉 Application Live

Zero Downtime Strategy Explained

✔ Current build stays live
✔ New build created separately
✔ Build validation before switch
✔ Atomic directory swap
✔ No server restart
✔ No user impact

Users never feel the deployment. 😎

🧹 Workspace Cleanup (Best Practice)

After every pipeline run, Jenkins cleans its workspace using:

cleanWs()

Prevents disk space issues

Ensures fresh builds

Recommended for long-running Jenkins servers

Small step.
Big DevOps mindset. 💡

🔐 Jenkins Credentials (Example)

All secrets are stored securely in Jenkins Credentials Manager.

🖥️ Server Access

PROD_HOST → Production server IP / domain

PROD_USER → SSH username

PROD_SSH_KEY → SSH private key

STAGING_HOST

STAGING_USER

STAGING_SSH_KEY

🔑 GitHub Access

GH_USERNAME

GH_PAT → GitHub Personal Access Token

⚠️ No secrets are committed to the repository. Security first.

🛠️ Tech Stack

🐧 Linux (Ubuntu)

⚛️ React

🧩 Jenkins

🔐 SSH

📦 Node.js & npm

🌐 Nginx / Apache

☁️ AWS / Any VPS
