---
title: "CI/CD and AWS Deployment"
linkTitle: "5.5. CI/CD and AWS Deployment"
weight: 5
---


## Create Amazon ECR repositories

```bash
aws ecr create-repository \
  --repository-name aws-library-backend \
  --region ap-southeast-2

aws ecr create-repository \
  --repository-name aws-library-frontend \
  --region ap-southeast-2
```

{{< report-figure src="images/ecr-repositories.png" alt="Two Amazon ECR repositories" caption="Private repositories storing frontend and backend Docker images." >}}

## GitHub OIDC and IAM

The workflow requests `id-token: write`, then uses the `AWS_ROLE_ARN` GitHub repository variable to assume an IAM role. The trust policy is restricted by owner, repository, and the `develop_2.0` branch.

```yaml
permissions:
  contents: read
  id-token: write

- name: Configure AWS credentials
  uses: aws-actions/configure-aws-credentials@v6.2.0
  with:
    role-to-assume: ${{ vars.AWS_ROLE_ARN }}
    aws-region: ap-southeast-2
```

## Main workflow operations

1. Check out the source code.
2. Install Python dependencies and run tests.
3. Install Node dependencies and build React.
4. Assume the AWS role through OIDC.
5. Log in to ECR.
6. Build and push backend and frontend images.
7. Render the Docker Compose deployment template.
8. Zip the bundle and upload it to S3.
9. Create an Elastic Beanstalk application version.
10. Update the environment and wait for deployment.
11. Verify version, status, health, and the endpoint.

{{< report-figure src="images/github-actions-workflow.png" alt="GitHub Actions workflow runs" caption="Pipeline runs for develop_2.0, including failed and successful executions." >}}

## Trigger deployment

```bash
git switch develop_2.0
git add -A
git commit -m "feat: deploy CloudLibrary to AWS"
git push origin develop_2.0
```

## Application version

The deployment bundle contains the rendered Docker Compose file and `.ebextensions`/`.platform` configuration. It is uploaded to S3 and registered as an application version.

{{< report-figure src="images/beanstalk-application-version.png" alt="Elastic Beanstalk environment overview" caption="The Elastic Beanstalk environment reaches Health: Ok and runs a traceable application version." >}}

## Successful verification criteria

```text
Status: Ready
Health: Ok
Running version: gh-<new-version>
Public health endpoint: HTTP 200
```
