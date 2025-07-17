# 🚀 DevOps CI/CD Pipeline with Jenkins, Docker & AWS EC2

This project demonstrates a full CI/CD pipeline using **Jenkins**, **Docker**, and **AWS EC2**, deploying a simple **Node.js web application**.

> ✅ Built from scratch to showcase real-world DevOps practices. Featured on my resume and LinkedIn.

---

## 📦 Technologies Used

- **Node.js** – Lightweight backend application
- **Docker** – Containerization
- **Jenkins** – CI/CD automation
- **GitHub** – Source code repository
- **AWS EC2 (Ubuntu)** – Hosting environment
- **Shell scripting** – Deployment automation

---

## 🌐 Live Deployment

After every push to GitHub, Jenkins:
- Pulls the latest code
- Builds a Docker image
- Runs the container on EC2
- App is accessible at:  
  👉 `http://44.248.40.23:3000`

---

## 📁 Project Structure

```
ci-cd-demo/
├── app.js
├── Dockerfile
├── Jenkinsfile
├── package.json
└── README.md
```

---

## 🛠️ Setup Instructions

### 1. 🚀 Launch EC2 Instance & Open Ports
- Use Ubuntu 22.04 LTS
- Open ports: **22**, **8080**, **3000**

### 2. ⚙️ Install Jenkins on EC2

```bash
sudo apt update
sudo apt install openjdk-17-jdk -y
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt update
sudo apt install jenkins -y
sudo systemctl start jenkins
sudo systemctl enable jenkins
```

Access Jenkins at: `http://<your-ec2-ip>:8080`

### 3. 🔓 Setup Jenkins Admin

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Install suggested plugins and create admin user.

### 4. 🐳 Install Docker & Configure Jenkins Access

```bash
sudo apt install docker.io -y
sudo usermod -aG docker jenkins
sudo systemctl enable docker
sudo systemctl start docker
sudo reboot
```

### 5. 📂 Clone & Push Node.js App

```bash
git clone https://github.com/Anjan854/ci-cd-demo.git
cd ci-cd-demo
git add .
git commit -m "Initial CI/CD project commit"
git push origin main
```

---

## 📝 Jenkinsfile

```groovy
pipeline {
  agent any

  stages {
    stage('Build Docker Image') {
      steps {
        sh 'docker build -t ci-cd-demo .'
      }
    }

    stage('Run Docker Container') {
      steps {
        sh '''
          docker stop demo || true
          docker rm demo || true
          docker run -d -p 3000:3000 --name demo ci-cd-demo
        '''
      }
    }
  }

  post {
    success {
      echo '✅ Deployment Successful!'
    }
    failure {
      echo '❌ Build or Deploy Failed!'
    }
  }
}
```

---

## 🧪 Jenkins Pipeline Setup

- Go to Jenkins → **New Item** → **Pipeline**
- Set GitHub repo: `https://github.com/Anjan854/ci-cd-demo.git`
- Branch: `*/main`
- Script path: `Jenkinsfile`
- Save & click **Build Now**

---

## ✅ Results

- CI/CD pipeline triggered on every GitHub push
- Dockerized app deployed live on EC2
- Full automation with zero manual steps

---

## 📌 Author

**Md Ashraf Mahmud Anjan**  
[GitHub](https://github.com/Anjan854) | [LinkedIn](https://www.linkedin.com/in/your-profile)

---

> ⭐ Star this repo if you found it helpful or want to use it as a DevOps reference project.
