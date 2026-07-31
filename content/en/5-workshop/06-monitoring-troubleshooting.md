---
title: "Monitoring and Troubleshooting"
linkTitle: "5.6. Monitoring and Troubleshooting"
weight: 6
---


## Monitored signals

Amazon CloudWatch monitors:

- EC2 CPU and memory.
- HTTP request count.
- Backend p95 latency.
- HTTP 4xx/5xx responses.
- Elastic Beanstalk environment health.
- Flask/Gunicorn, Nginx, Docker, and deployment logs.

{{< report-figure src="images/cloudwatch-monitoring.png" alt="CloudLibrary CloudWatch dashboard" caption="Dashboard widgets for CPU/memory, environment health, traffic, p95 latency, and HTTP 5xx." >}}

## Troubleshooting data sources

- GitHub Actions job logs.
- Elastic Beanstalk Events and Enhanced Health.
- Deployment log bundles.
- `/var/log/eb-engine.log`.
- Docker container logs.
- CloudWatch Logs.

Request a log bundle:

```bash
aws elasticbeanstalk request-environment-info \
  --environment-name Aws-library-system-env \
  --info-type bundle \
  --region ap-southeast-2
```

## Real incident: inconsistent PostgreSQL credentials

The backend previously used a hard-coded password in `DATABASE_URL`, while the PostgreSQL container used the password from Elastic Beanstalk environment properties.

```text
Credential mismatch
→ backend connection failure
→ backend health-check failure
→ frontend not started
→ Elastic Beanstalk deployment failure
```

The solution was to construct `DATABASE_URL` from the same variables:

```text
POSTGRES_USER
POSTGRES_PASSWORD
POSTGRES_DB
```

{{< report-figure src="images/deployment-error.png" alt="GitHub Actions deployment error" caption="The workflow stops during version and health verification while the environment is Red/Degraded." >}}

## Rollback

```text
Elastic Beanstalk
→ Application versions
→ Select a stable version
→ Deploy
```

Rollback restores service while the failed version is investigated.

## Resource cleanup

- Remove old ECR images.
- Remove unused application versions and S3 bundles.
- Adjust log retention.
- Remove IAM policies and roles that are no longer required.
- Never delete resources used by the current environment.
