# 🏗️ AWS 3-Tier Web Application

<p align="center">
  <strong>Production-Style Full-Stack Application Deployed on AWS</strong>
</p>

<p align="center">
  EC2 • Nginx • React • Node.js • Application Load Balancer • Auto Scaling • Aurora/MySQL
</p>

<p align="center">

[![GitHub](https://img.shields.io/badge/GitHub-Repository-181717?style=for-the-badge&logo=github)](https://github.com/niharikaSinghh/3-tier-architecture-app)

[![GitHub](https://img.shields.io/badge/GitHub-Profile-181717?style=for-the-badge&logo=github)](https://github.com/niharikaSinghh)

</p>

---

# 📌 Project Overview

The **AWS 3-Tier Web Application** is a full-stack application designed and deployed using a layered cloud architecture on AWS.

The project separates the application into three independent tiers:

1. **🌐 Web Tier** — React frontend served through Nginx on Amazon EC2
2. **⚙️ Application Tier** — Node.js / Express backend running on EC2
3. **🗄️ Database Tier** — Amazon Aurora / MySQL-compatible database

This architecture improves **scalability, maintainability, security, and separation of responsibilities**.

---

# 🏗️ Architecture

```text
                         🌐 INTERNET
                              |
                              v
                 +-------------------------+
                 |        WEB TIER         |
                 |                         |
                 |      Amazon EC2         |
                 |        Nginx            |
                 |    React Frontend       |
                 +------------+------------+
                              |
                              | HTTP / API
                              v
                 +-------------------------+
                 |   APPLICATION TIER      |
                 |                         |
                 |    Application Load     |
                 |       Balancer          |
                 |            |            |
                 |       Auto Scaling      |
                 |            |            |
                 |      EC2 Instances      |
                 |    Node.js / Express    |
                 +------------+------------+
                              |
                              | SQL
                              v
                 +-------------------------+
                 |      DATABASE TIER       |
                 |                         |
                 |   Amazon Aurora /       |
                 |       MySQL             |
                 |                         |
                 |      Persistent Data    |
                 +-------------------------+
