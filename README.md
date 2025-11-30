<div align="center">

![Jenkins](https://img.shields.io/badge/jenkins-%232C5263.svg?style=for-the-badge&logo=jenkins&logoColor=white)
![Maven](https://img.shields.io/badge/apache_maven-C71A36?style=for-the-badge&logo=apachemaven&logoColor=white)
![SonarQube](https://img.shields.io/badge/SonarQube-black?style=for-the-badge&logo=sonarqube&logoColor=4E9BCD)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![Argo CD](https://img.shields.io/badge/Argo%20CD-EF7B4D?style=for-the-badge&logo=argo&logoColor=white)
![Kubernetes](https://img.shields.io/badge/kubernetes-%23326ce5.svg?style=for-the-badge&logo=kubernetes&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=for-the-badge&logo=amazon-aws&logoColor=white)
![Slack](https://img.shields.io/badge/Slack-4A154B?style=for-the-badge&logo=slack&logoColor=white)

</div>

---
## 🚀 CI/CD Pipeline Architecture
This project utilizes a **GitOps** approach for automated deployment. Below is the architectural flow used to deploy the application from development to the EKS production cluster.

## 📂 Repository Structure
This project follows a strict **GitOps Architecture** by decoupling source code from configuration. We maintain two separate repositories to ensure security and clean workflow management.

| Repository | Type | Description |
| :--- | :--- | :--- |
| **[Main Repo](https://github.com/wth-aryan/register-app.git)** | 🏗️**Application** | Contains the Java Source Code, `Dockerfile`, and the CI Pipeline (`Jenkinsfile`). |
| **[Config Repo](https://github.com/wth-aryan/gitops-register-app)** | ⚙️**Manifests** | Contains Kubernetes configuration files (`deployment.yaml`, `service.yaml`) which are monitored by ArgoCD. |

### 🔗 How they connect
1. **Jenkins** builds the Docker image and pushes it to DockerHub.
2. **Jenkins** then automatically triggers a Git commit to the **Config Repo** to update the image tag.
3. **ArgoCD** detects the change in the Config Repo and syncs the live cluster.
---
<div align="center">
<img src="./Images/JobPipeline.png" alt="CI/CD Architecture" width="900"/>
</div>

### 🛠️ Tech Stack
* **Version Control:** GitHub
* **CI Server:** Jenkins
* **Build Tool:** Maven
* **Code Quality:** SonarQube
* **Containerization:** Docker & Docker Hub
* **Security:** Trivy (Image Scanning)
* **CD / GitOps:** Argo CD
* **Orchestration:** Amazon EKS (Kubernetes)
* **Notifications:** Slack

### 🔄 Workflow Description
1.  **Code Push:** Developer pushes code to the Application Repo.
2.  **CI Trigger:** Jenkins detects changes and triggers the build.
3.  **Build & Test:** Maven compiles the code and runs unit tests.
4.  **Analysis:** SonarQube performs static code analysis.
5.  **Dockerize:** Jenkins builds the Docker image and pushes it to Docker Hub.
6.  **Security Scan:** Trivy scans the Docker image for vulnerabilities.
7.  **Update Manifest:** The CI pipeline updates the Kubernetes manifest repository with the new build tag.
8.  **Sync:** Argo CD detects the change in the manifest repo.
9.  **Deploy:** Argo CD synchronizes the state and deploys to the EKS Cluster.
10. **Notify:** A notification is sent to Slack regarding the deployment status.
