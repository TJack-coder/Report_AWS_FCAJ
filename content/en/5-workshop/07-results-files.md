---
title: "Results and Attached Files"
linkTitle: "5.7. Results and Attached Files"
weight: 7
---


## Results

- The frontend and backend are packaged as separate Docker images.
- Images are stored in private Amazon ECR repositories.
- GitHub Actions automatically tests, builds, and deploys.
- GitHub Actions authenticates to AWS through OIDC.
- A push to `develop_2.0` triggers deployment.
- Elastic Beanstalk manages the Docker environment and application versions.
- CloudWatch collects logs, metrics, health data, and alarms.
- Failed deployments can be investigated and rolled back.

{{< report-figure src="images/cloudlibrary-production.png" alt="CloudLibrary production book catalog" caption="Final result: the book catalog running in the deployment environment." >}}

## Attached implementation files

The files below were extracted from the source code and **sanitized by replacing the AWS account ID with a placeholder** before publication.

{{< download path="files/attachments/docker-compose.yml" label="docker-compose.yml" meta="Local integration: db, backend, frontend" >}}
{{< download path="files/attachments/backend.Dockerfile" label="Backend Dockerfile" meta="Flask + Gunicorn image" >}}
{{< download path="files/attachments/frontend.Dockerfile" label="Frontend Dockerfile" meta="React build + Nginx runtime" >}}
{{< download path="files/attachments/beanstalk-compose.template.yml" label="Beanstalk Compose template" meta="Production deployment bundle template" >}}
{{< download path="files/attachments/ci.yml" label="GitHub Actions CI" meta="Backend tests and frontend build" >}}
{{< download path="files/attachments/deploy.yml" label="GitHub Actions deployment" meta="ECR, S3, and Elastic Beanstalk pipeline" >}}
{{< download path="files/attachments/setup-github-oidc.example.sh" label="GitHub OIDC setup script" meta="Sanitized AWS IAM configuration" >}}
{{< download path="files/attachments/setup-cloudwatch.sh" label="CloudWatch setup script" meta="Dashboard, metrics, and alarms" >}}
{{< download path="files/attachments/env.example" label="Environment example" meta="Placeholder values only" >}}

## Workshop conclusion

The delivery pipeline transformed CloudLibrary from a locally running full-stack application into an AWS system that can be tested, packaged, released, monitored, and recovered through one consistent process. The key result is a deployment process that is **repeatable, traceable, and mostly automated**.
