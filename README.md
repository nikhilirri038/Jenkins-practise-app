# Jenkins CI Practice Project 🚀

A hands-on DevOps practice project demonstrating a basic CI pipeline setup using **AWS EC2**, **Jenkins**, and **GitHub**.

## 📌 Project Overview

This project simulates a simple Continuous Integration (CI) workflow:

1. A sample static website (`index.html` + `style.css`) is hosted on GitHub.
2. Jenkins, self-hosted on an AWS EC2 instance, pulls the code from this repository.
3. Every build checks out the latest code and runs verification steps.
4. A GitHub webhook triggers Jenkins automatically whenever new code is pushed.

This project was built to understand the fundamentals of CI/CD tooling — setting up a Jenkins server from scratch, connecting it to source control, and triggering automated builds.

## 🛠️ Tech Stack

- **AWS EC2** (Ubuntu) — hosting the Jenkins server
- **Jenkins** — CI automation server
- **GitHub** — source code repository & webhook trigger
- **HTML/CSS** — sample application being built

## ⚙️ Architecture

```
Developer → git push → GitHub Repository
                              │
                              ▼ (webhook trigger)
                    Jenkins Server (AWS EC2)
                              │
                              ▼
                    Freestyle Build Job
                (checkout code → verify files → run build steps)
                              │
                              ▼
                      Console Output / Build Status
```

## 🔧 Setup Steps

### 1. Provisioned AWS Infrastructure
- Launched an Ubuntu EC2 instance
- Configured security group rules:
  - Port 22 (SSH) restricted to my IP
  - Port 8080 (Jenkins UI) open for webhook access

### 2. Installed Jenkins
- Installed Java (OpenJDK)
- Added the official Jenkins APT repository and signing key
- Installed and started the Jenkins service via `systemctl`

### 3. Configured Jenkins
- Unlocked Jenkins using the initial admin password
- Installed suggested plugins
- Created an admin user

### 4. Connected to GitHub
- Created this public repository containing the sample website
- Added the repository URL under Jenkins' **Source Code Management**
- Configured a **GitHub webhook** pointing to:
  ```
  http://<jenkins-server-ip>:8080/github-webhook/
  ```
- Enabled **"GitHub hook trigger for GITScm polling"** in the job configuration

### 5. Created a Freestyle Build Job
- Job pulls the latest code from GitHub on every trigger
- Executes shell build steps to verify the files and simulate a build process

## ✅ What I Practiced

- Setting up a Jenkins server manually on a cloud VM
- Resolving real-world server issues (e.g., GPG signing key rotation/expiry during `apt` installs)
- Connecting Jenkins to a GitHub repository
- Configuring webhooks for automatic build triggers
- Running and monitoring builds via Jenkins' console output
- Understanding the basic building blocks of a CI pipeline

## 📂 Repository Contents

| File | Description |
|------|--------------|
| `index.html` | Sample webpage used as the build artifact |
| `style.css` | Styling for the sample webpage |
| `README.md` | Project documentation (this file) |

## 🔭 Next Steps / Future Improvements

- Add a `Jenkinsfile` to convert this into a scripted/declarative Pipeline job
- Add automated deployment of the site to an S3 bucket or a web server
- Add build notifications (Slack/Email) on failure
- Add parameterized builds and multi-branch pipeline support

---
*This project was built as a personal learning exercise to understand Jenkins CI fundamentals using free-tier AWS infrastructure.*
