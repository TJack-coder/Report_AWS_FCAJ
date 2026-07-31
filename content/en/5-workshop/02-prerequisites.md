---
title: "Prerequisites"
linkTitle: "5.2. Prerequisites"
weight: 2
---


## Tools and accounts

- An AWS account with access to IAM, ECR, S3, EC2, Elastic Beanstalk, and CloudWatch.
- A GitHub repository containing the CloudLibrary source code.
- Git, Docker Desktop, and Docker Compose.
- Python 3, `pip`, Node.js, and `npm`.
- AWS CLI or AWS CloudShell.
- A GitHub Actions IAM role configured through OpenID Connect.

## Project resources

| Resource | Value |
|---|---|
| AWS Region | `ap-southeast-2` |
| Backend ECR repository | `aws-library-backend` |
| Frontend ECR repository | `aws-library-frontend` |
| Elastic Beanstalk application | `aws-library-system` |
| Elastic Beanstalk environment | `Aws-library-system-env` |
| GitHub deployment role | `aws-library-github-deploy` |
| EC2 instance role | `aws-elasticbeanstalk-ec2-role` |
| Deployment branch | `develop_2.0` |

## Project structure

```text
.github/workflows/
.platform/hooks/
aws/
backend/
cloudwatch/
deploy/
frontend/
docker-compose.yml
.env.example
```

## Security rules

- Do not commit `.env`, access keys, session tokens, or passwords.
- Use GitHub OIDC instead of long-term AWS access keys.
- Configure secrets through Elastic Beanstalk environment properties and GitHub variables.
- Replace account IDs with placeholders before publishing technical files.
