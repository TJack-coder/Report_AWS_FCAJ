---
title: "Deployment Architecture"
linkTitle: "5.3. Deployment Architecture"
weight: 3
---


## Current architecture

{{< report-figure src="images/architecture-current.svg" alt="Current CloudLibrary architecture" caption="GitHub Actions builds and pushes images, creates an S3 bundle, and deploys frontend, backend, and PostgreSQL containers on Elastic Beanstalk." >}}

## Component responsibilities

- **GitHub:** stores source code and produces push/pull-request events.
- **GitHub Actions:** tests, builds the frontend, builds/pushes Docker images, and deploys.
- **Amazon ECR:** stores private frontend/backend images.
- **Amazon S3:** stores Elastic Beanstalk deployment bundles.
- **Elastic Beanstalk:** manages EC2, application versions, deployment, and health.
- **Frontend container:** Nginx serves React and reverse-proxies `/api`.
- **Backend container:** Flask/Gunicorn handles JWT, business logic, and database access.
- **PostgreSQL container:** stores application data in the current implementation.
- **CloudWatch:** collects logs, metrics, dashboards, and alarms.
- **CloudShell:** runs AWS CLI and supports operations.

## Runtime communication

```text
User → Nginx frontend → /api → Flask backend → PostgreSQL
                           ↓
                     JWT authorization
```

## Traceability

Docker images are tagged from the Git commit. Elastic Beanstalk versions use a format such as:

```text
gh-<commit-sha>-<workflow-run-id>-<attempt>
```

This links the running environment to the source commit and workflow execution that produced it.
