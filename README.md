# 🏗️ AWS 3-Tier Web Application

<p align="center">
  <strong>Production-Style Full-Stack Application Deployed on AWS</strong>
</p>

<p align="center">
  React • Node.js • Nginx • Amazon EC2 • Application Load Balancer • Auto Scaling • Aurora/MySQL
</p>

<p align="center">

[![AWS](https://img.shields.io/badge/AWS-Cloud-232F3E?style=for-the-badge&logo=amazonaws&logoColor=white)](https://aws.amazon.com/)
[![EC2](https://img.shields.io/badge/Amazon_EC2-FF9900?style=for-the-badge&logo=amazonec2&logoColor=white)](https://aws.amazon.com/ec2/)
[![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)](https://react.dev/)
[![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)](https://nodejs.org/)
[![Express](https://img.shields.io/badge/Express.js-000000?style=for-the-badge&logo=express&logoColor=white)](https://expressjs.com/)
[![Nginx](https://img.shields.io/badge/Nginx-009639?style=for-the-badge&logo=nginx&logoColor=white)](https://nginx.org/)
[![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)](https://www.mysql.com/)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/)

</p>

<p align="center">

[![Repository](https://img.shields.io/badge/GITHUB-REPOSITORY-181717?style=for-the-badge&logo=github)](https://github.com/niharikaSinghh/3-tier-architecture-app)

[![Profile](https://img.shields.io/badge/GITHUB-PROFILE-181717?style=for-the-badge&logo=github)](https://github.com/niharikaSinghh)

</p>

---

# 📑 Table of Contents

- [🎯 Overview](#-overview)
- [📊 Architecture](#-architecture)
- [⚡ Application Flow](#-application-flow)
- [☁️ AWS Services](#️-aws-services)
- [🌐 Web Tier](#-web-tier)
- [⚙️ Application Tier](#️-application-tier)
- [🗄️ Database Tier](#️-database-tier)
- [🔐 Security & Networking](#-security--networking)
- [📈 Scalability & Availability](#-scalability--availability)
- [🚀 Application Features](#-application-features)
- [🧰 Tech Stack](#-tech-stack)
- [📁 Project Structure](#-project-structure)
- [🔄 Deployment Workflow](#-deployment-workflow)
- [🧠 Key Engineering Concepts](#-key-engineering-concepts)
- [📚 What I Learned](#-what-i-learned)
- [🚀 Future Improvements](#-future-improvements)
- [⚡ Quick Start](#-quick-start)
- [👩‍💻 Author](#-author)

---

# 🎯 Overview

The **AWS 3-Tier Web Application** is a full-stack cloud project designed to demonstrate how a traditional web application can be deployed using a **layered AWS architecture**.

Instead of placing the frontend, backend, and database on a single server, the application separates them into independent tiers.

```text
                         🌐 INTERNET
                              |
                              v
                    ┌───────────────────┐
                    │      WEB TIER     │
                    │                   │
                    │    Amazon EC2     │
                    │      Nginx        │
                    │  React Frontend   │
                    └─────────┬─────────┘
                              |
                              | HTTP / API
                              v
                    ┌───────────────────┐
                    │ APPLICATION TIER  │
                    │                   │
                    │ Application Load  │
                    │     Balancer      │
                    │         |         │
                    │      Node.js      │
                    │      Express      │
                    └─────────┬─────────┘
                              |
                              | SQL
                              v
                    ┌───────────────────┐
                    │    DATABASE TIER  │
                    │                   │
                    │ Aurora / MySQL    │
                    │                   │
                    │ Persistent Data   │
                    └───────────────────┘
