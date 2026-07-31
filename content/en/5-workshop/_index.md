---
title: "Workshop: Deploying CloudLibrary to AWS"
linkTitle: "5. Workshop"
weight: 5
---


This workshop documents the complete process of moving CloudLibrary from development to AWS. The content is divided into independent, sequential sections and satisfies the mandatory requirements for **bilingual content, screenshots, an architecture diagram, code snippets, and downloadable files**.

{{< report-figure src="images/cloudlibrary-production.png" alt="CloudLibrary book catalog in the production environment" caption="CloudLibrary running in the public deployment environment." >}}

{{< notice type="warning" title="Database architecture note" >}}
The current source code runs PostgreSQL as the `db` container in Docker Compose on Elastic Beanstalk/EC2. Amazon RDS is treated only as a future enhancement.
{{< /notice >}}


### Contents
- [5.1. Introduction](01-introduction/)
- [5.2. Prerequisites](02-prerequisites/)
- [5.3. Deployment Architecture](03-architecture/)
- [5.4. Local Testing and Validation](04-local-validation/)
- [5.5. CI/CD and AWS Deployment](05-cicd-deployment/)
- [5.6. Monitoring and Troubleshooting](06-monitoring-troubleshooting/)
- [5.7. Results and Attached Files](07-results-files/)
