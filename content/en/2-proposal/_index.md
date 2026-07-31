---
title: "Proposal"
linkTitle: "2. Proposal"
weight: 2
---


## Project overview

CloudLibrary is a cloud-based library management web application supporting books, users, borrowing and returning, renewals, reservations, notifications, and administration. The system uses **React + Vite + Nginx** for the frontend, **Flask + Gunicorn** for the backend, and **PostgreSQL** for relational data.

The project aims not only to deliver a functional application but also to apply DevOps and cloud-native practices: containerization, CI/CD, image registry, managed deployment, and centralized monitoring.

## Objectives

- Build a web-based library borrowing and management system.
- Implement JWT authentication and Admin/User authorization.
- Provide CRUD, restore, import, and export operations for books.
- Support borrowing, returns, renewals, reservations, fines, and notifications.
- Containerize the frontend and backend.
- Automate CI/CD with GitHub Actions.
- Store images in Amazon ECR and deploy with Elastic Beanstalk.
- Observe logs, CPU, memory, latency, HTTP errors, and health in CloudWatch.

## Delivery phases

1. **Core application:** book lists, details, CRUD, database models, and APIs.
2. **Authentication and authorization:** login, registration, JWT, password reset, and role-based access.
3. **Library workflows:** borrowing, returning, renewals, reservations, fines, and notifications.
4. **Containerization and CI/CD:** Docker, Docker Compose, and GitHub Actions.
5. **AWS deployment and monitoring:** ECR, S3, Elastic Beanstalk, CloudWatch, and CloudShell.

## Technology stack

| Layer | Technology/Service |
|---|---|
| Frontend | React, Vite, Nginx |
| Backend | Flask, Flask-SQLAlchemy, Gunicorn |
| Authentication | JWT |
| Database | PostgreSQL |
| Containerization | Docker, Docker Compose |
| CI/CD | GitHub Actions |
| Container Registry | Amazon ECR |
| Deployment | AWS Elastic Beanstalk |
| Monitoring | Amazon CloudWatch |
| Cloud Operations | AWS CloudShell |

## Architecture and deployment flow

{{< report-figure src="images/architecture-current.svg" alt="Current CloudLibrary deployment architecture" caption="Current architecture: PostgreSQL runs as a container in the Elastic Beanstalk/EC2 environment; Amazon RDS is a future improvement." >}}

1. Developers push source code to GitHub.
2. GitHub Actions tests the application and builds frontend/backend Docker images.
3. Images are stored in Amazon ECR.
4. A deployment bundle is uploaded to S3 and registered as an Elastic Beanstalk application version.
5. Elastic Beanstalk runs `frontend`, `backend`, and `db` through Docker Compose.
6. CloudWatch collects logs, metrics, health data, and alarms.

## Security design

- GitHub Actions authenticates to AWS through OpenID Connect.
- IAM trust is restricted to the repository and deployment branch.
- Secrets are not stored in source code.
- JWT and role-based authorization protect backend APIs.
- `.env` files and access keys are excluded from Git.

## Scalability

The current version prioritizes simplicity and reproducibility. Future improvements may include Amazon RDS, S3/CloudFront for media, SES for email, HTTPS/custom domains, and ECS/EKS for advanced orchestration.

## Expected outcome

A full-stack library application that can be tested, packaged, deployed, and monitored through one consistent workflow, delivering both business functionality and practical AWS software-delivery experience.
