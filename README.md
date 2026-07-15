# Project Title
End-to-end AWS deployment of the DevBoard Node.js application using Terraform, Docker Compose, and GitHub Actions CI/CD.

*******************************************************************************************************************************************************************

## Assignment Overview
This project demonstrates a complete CI/CD deployment pipeline for a containerized full-stack application. The infrastructure is provisioned using Terraform, the application is deployed on an Amazon EC2 instance using Docker Compose, and GitHub Actions automates the build and deployment process without requiring SSH access to the server.

*******************************************************************************************************************************************************************

### Objectives
- Provision AWS infrastructure using Terraform.
- Deploy a Node.js/Express backend.
- Deploy a Vite/React frontend application.
- Deploy PostgreSQL using Docker Compose.
- Store application assets in Amazon S3.
- Implement least-privilege IAM policies.
- Automate deployments with GitHub Actions.
- Eliminate the need for SSH by using EC2 User Data and AWS Systems Manager.

*******************************************************************************************************************************************************************

#### Architecture Diagram

                        Source Code
                             │ (Git Push)
                             ▼
                    GitHub Repository
                             │ (Event Trigger)
                             ▼
                  GitHub Actions CI/CD
                             │ (Build Docker Image & Push Image)
                             ▼
                        Amazon ECR
                             │ (Deploy via AWS SSM)
                             ▼
                        EC2 Instance 
                             │ (Pulls Image & Runs Docker Compose)
        ┌────────────────────┼────────────────────┐
        │                    │                    │
        ▼                    ▼                    ▼
    Frontend              Backend             PostgreSQL 
    Container             Container           Container    
        │                    │ (SQL)
        ▼                    ├──────────────► PostgreSQL
     Browser                 │ (HTTPS AWS SDK / S3 API)
                             └──────────────► Amazon S3

*******************************************************************************************************************************************************************

##### Deployment Flow

push source code to github

↓

GitHub Actions starts

↓

Backend Docker image is built

↓

Frontend Docker image is built

↓

Images are pushed to Amazon ECR

↓

GitHub Actions invokes AWS Systems Manager

↓

EC2 pulls the newest images

↓

Docker Compose updates the running containers

↓

Application becomes available on Port 80

*******************************************************************************************************************************************************************

###### Technology Stack

Component	                      Technology
Backend	              ->        Node.js + Express
Frontend	            ->        React + vite
Database	            ->        PostgreSQL
Infrastructure	      ->        Terraform
Containerization	    ->        Docker
Orchestration	        ->        Docker Compose
CI/CD	                ->        GitHub Actions
Registry	            ->        Amazon ECR
Cloud	                ->        AWS EC2
Storage	              ->        Amazon S3
Remote Management	    ->        AWS Systems Manager

*******************************************************************************************************************************************************************

###### Repository Structure

.
├── backend/
├── frontend/
├── terraform/
├── .github/
│   └── workflows/
├── docker-compose.yml
├── README.md
└── .gitignore

*******************************************************************************************************************************************************************

###### Deployment Stages

* Create GitHub repository
* Containerize the backend
* Containerize the frontend
* Write Docker Compose
* Provision AWS resources using Terraform
* Configure IAM roles
* Configure S3
* Configure EC2 User Data
* Configure GitHub Actions
* Deploy automatically

  *******************************************************************************************************************************************************************

###### Security Considerations

- SSH access is disabled.
- Only HTTP (port 80) is exposed publicly.
- Docker containers communicate over a private Docker network.
- The backend accesses Amazon S3 using an EC2 IAM role with least-privilege permissions.
- GitHub Actions authenticates to AWS using OpenID Connect (OIDC), avoiding long-lived AWS access keys.
- Database credentials are retrieved securely from AWS Systems Manager Parameter Store.

  *******************************************************************************************************************************************************************

###### Deliverables

- Terraform configuration
- EC2 User Data script
- Docker Compose configuration
- GitHub Actions workflow
- Amazon S3 configuration
- IAM configuration
- Source code
- GitHub repository





