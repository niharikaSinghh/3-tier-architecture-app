# 🏗️ AWS 3-Tier Web Application

<p align="center">
  <strong>Production-Style Full-Stack Application Deployed on AWS</strong>
</p>

<p align="center">
  EC2 • Nginx • React • Node.js • Application Load Balancer • Auto Scaling • Aurora/MySQL
</p>

<p align="center">

<a href="https://github.com/niharikaSinghh/3-tier-architecture-app">
<img src="https://img.shields.io/badge/GitHub-Repository-181717?style=for-the-badge&logo=github"/>
</a>

<a href="https://github.com/niharikaSinghh">
<img src="https://img.shields.io/badge/GitHub-Profile-181717?style=for-the-badge&logo=github"/>
</a>

</p>

---

# 📌 Project Overview

The **AWS 3-Tier Web Application** is a full-stack application designed and deployed using a layered cloud architecture on AWS.

The project separates the application into three independent tiers:

```text
                    🌐 INTERNET
                         │
                         ▼
              ┌─────────────────────┐
              │      WEB TIER       │
              │                     │
              │    Amazon EC2       │
              │       Nginx         │
              │   React Frontend    │
              └──────────┬──────────┘
                         │
                         │ HTTP / API
                         ▼
              ┌─────────────────────┐
              │  APPLICATION TIER   │
              │                     │
              │    Amazon EC2       │
              │   Node.js/Express   │
              │                     │
              │ Internal ALB        │
              │   Auto Scaling      │
              └──────────┬──────────┘
                         │
                         │ Database Connection
                         ▼
              ┌─────────────────────┐
              │    DATABASE TIER    │
              │                     │
              │   Amazon Aurora     │
              │  MySQL-Compatible   │
              └─────────────────────┘
