# Welcome to Kya Saabzi Documentation

**Kya Saabzi** is a simple dish recommendation app that aims to solve your everyday problem of  
> *"Aaj kya banau?"*  

Click here to get started on how to use this app and download this for yourself from this link.

---

| Project Name | Project Manager | Start Date   | Duration        |
|--------------|-----------------|--------------|-----------------|
| Kya Saabzi   |                 | 6th Nov, 2025| 2 Weeks         |

---

## Executive Summary 

### Problem Statement

One of the major confusion in everyday life of many households is *What should I cook today?* and this dilemma often leads to dishes being repeated too soon. Certain disliked dishes cooked repeatedly are often wasted or people lean towards ordering food *(junk usually)* which is also a major source for health related issues.

### Solution

Kya Saabzi addresses this everyday problem through personalized, data-driven dish recommendations.

The app will:

- Recommend dishes intelligently based on a user’s past cooking history.

- Learn from others’ patterns, suggesting popular dishes across households.

- Track when each dish was last cooked, helping you avoid repetition.

- Allow you to delete cook logs for a dish.

- Continuously improve recommendations as more users log data.

With these features, Kya Saabzi brings structure and simplicity to meal planning, encouraging variety and mindful eating habits.

### Technical Overview

| **Component** | **AWS Service** | **Purpose / Description** |
|----------------|------------------|-----------------------------|
| **Frontend (React + Vite PWA)** | **Amazon S3 + CloudFront** | Hosts the static frontend files (HTML, JS, CSS, icons). CloudFront provides global CDN delivery and HTTPS. |
| **Backend (FastAPI API)** | **EC2** | Runs the containerized FastAPI backend. EC2 is suitable for smaller self-managed deployments. |
| **Database (PostgreSQL)** | **Amazon RDS (PostgreSQL)** | Managed relational database for user data, cook logs, and dishes. Automated backups and scaling supported. |
| **Environment Configuration** | **AWS Systems Manager Parameter Store** | Centralized storage for environment variables (e.g., `DATABASE_URL`, `API_BASE_URL`). |
| **Networking** | **VPC + Application Load Balancer (ALB)** | Securely connects EC2 tasks and RDS within a private network. ALB distributes API traffic to running containers. |
| **CI/CD Pipeline** | **AWS CodePipeline + CodeBuild** | Automates the build, test, and deployment process for both backend and frontend. |
| **Container Registry** | **Amazon ECR (Elastic Container Registry)** | Stores and versions the Docker images for the backend. |
| **DNS & Domains** | **Amazon Route 53** | Manages custom domains and integrates with CloudFront and ALB. |
| **Documentation Hosting** | **GitHub Pages** | Hosts MkDocs-generated static documentation for public or internal access. |

---

## Future Enhancements

- Family based recommendations
- Weekly meal planner integration
- Community-driven recipes and ratings
- Push notifications or reminders and new dish ideas

---
