---
title: "Overview and Objectives"
linkTitle: "5.1. Introduction"
weight: 1
---


## Overview

CloudLibrary is a containerized full-stack web application consisting of:

- **Frontend:** React, Vite, and Nginx.
- **Backend:** Python Flask, Flask-SQLAlchemy, and Gunicorn.
- **Database:** PostgreSQL.
- **Containers:** Docker and Docker Compose.
- **Source control:** GitHub.
- **CI/CD:** GitHub Actions.
- **Registry:** Amazon ECR.
- **Deployment:** AWS Elastic Beanstalk.
- **Monitoring:** Amazon CloudWatch.

{{< report-figure src="images/cloudlibrary-interface.png" alt="CloudLibrary administration dashboard" caption="The CloudLibrary system dashboard." >}}

## Workshop objectives

After completing the workshop, the reader can:

1. Verify the project structure and run the system with Docker Compose.
2. Run Flask backend tests and build the React frontend.
3. Configure GitHub OIDC and an IAM role for CI/CD.
4. Build and push Docker images to Amazon ECR.
5. Create a deployment bundle and application version.
6. Deploy, verify, monitor, and roll back on Elastic Beanstalk.
7. Investigate failures using GitHub Actions, Elastic Beanstalk, and CloudWatch.

## Automation flow

A new commit on `develop_2.0` triggers the pipeline. It validates the backend, builds the frontend, builds and pushes two Docker images, creates the deployment package, updates Elastic Beanstalk, and verifies the running version and health.
