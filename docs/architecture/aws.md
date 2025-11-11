# AWS Specific Architecture

This section explains the AWS specific architecture for **Kya Saabzi** and why this architecture is chosen.

---

![AWS architecture](../assets/aws-architecture.png)
/// caption
AWS specific architecture
///

---

| AWS Component / Tool | Purpose in this architecture |
|----------------------|------------------------------|
| **Client / Internet** | End user using the PWA in a browser or mobile; accesses frontend over the public internet. |
| **Amazon S3 (Frontend)** | Hosts the built static PWA assets. Provides durable, low-cost static hosting for the app bundle. |
| **Virtual Private Cloud (VPC)** | Network boundary that contains the compute and database resources (subnet layout shown in diagram). |
| **Public Subnet** | The public subnet inside the VPC where internet-facing resources (as drawn) can be placed and receive traffic. |
| **Amazon EC2 (Backend)** | Runs the FastAPI backend application. Handles API requests, business logic, and talks to the database and SES. |
| **Amazon RDS (Database)** | Managed PostgreSQL instance that stores `users`, `dishes`, and `cooklogs`. Provides durable, backed-up relational storage for the app. |
| **Amazon SES (Authentication / Email)** | Used by the backend to send authentication emails, OTPs, and other transactional messages (as shown). |
| **GitHub Actions (CI/CD)** | Continuous integration / deployment pipeline that builds and deploys the backend and frontend to the AWS environment. |