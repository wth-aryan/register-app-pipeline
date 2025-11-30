# register-app-pipeline
🚀 CI/CD Pipeline Architecture
This project utilizes a GitOps approach for automated deployment. Below is the architectural flow used to deploy the application from development to the EKS production cluster.

<div align="center"> <img src="C:\Users\Aryan\Desktop\register-app-devsecops\docs\JobPipeline.png" alt="CI/CD Flow" width="100%"> </div>

🛠️ Tech Stack
Version Control: GitHub

CI Server: Jenkins

Build Tool: Maven

Code Quality: SonarQube

Containerization: Docker & Docker Hub

Security: Trivy (Image Scanning)

CD / GitOps: Argo CD

Orchestration: Amazon EKS (Kubernetes)

Notifications: Slack

🔄 Workflow Description
Code Push: Developer pushes code to the Application Repo.

CI Trigger: Jenkins detects changes and triggers the build.

Build & Test: Maven compiles the code and runs unit tests.

Analysis: SonarQube performs static code analysis.

Dockerize: Jenkins builds the Docker image and pushes it to Docker Hub.

Security Scan: Trivy scans the Docker image for vulnerabilities.

Update Manifest: The CI pipeline updates the Kubernetes manifest repository with the new build tag.

Sync: Argo CD detects the change in the manifest repo.

Deploy: Argo CD synchronizes the state and deploys to the EKS Cluster.

Notify: A notification is sent to Slack regarding the deployment status.
