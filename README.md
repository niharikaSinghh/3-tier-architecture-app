# 🏗️ AWS 3-Tier Web Application

<p align="center">
  <strong>Production-Style Full-Stack Application Deployed on AWS</strong>
</p>

<p align="center">
  EC2 • Nginx • React • Node.js • Application Load Balancer • Auto Scaling • Aurora/MySQL
</p>

<p align="center">

[![AWS](https://img.shields.io/badge/AWS-Cloud-232F3E?style=for-the-badge&logo=amazonaws&logoColor=white)](https://aws.amazon.com/)
[![EC2](https://img.shields.io/badge/Amazon_EC2-FF9900?style=for-the-badge&logo=amazonec2&logoColor=white)](https://aws.amazon.com/ec2/)
[![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)](https://react.dev/)
[![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)](https://nodejs.org/)
[![Express](https://img.shields.io/badge/Express.js-000000?style=for-the-badge&logo=express&logoColor=white)](https://expressjs.com/)
[![Nginx](https://img.shields.io/badge/Nginx-009639?style=for-the-badge&logo=nginx&logoColor=white)](https://nginx.org/)
[![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)](https://www.mysql.com/)
[![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)](https://git-scm.com/)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/)

</p>

<p align="center">

[![GitHub](https://img.shields.io/badge/GITHUB-REPOSITORY-181717?style=for-the-badge&logo=github)](https://github.com/niharikaSinghh/3-tier-architecture-app)
[![GitHub](https://img.shields.io/badge/GITHUB-PROFILE-181717?style=for-the-badge&logo=github)](https://github.com/niharikaSinghh)

</p>

---

# 📌 Project Overview

The **AWS 3-Tier Web Application** is a full-stack application designed and deployed using a layered cloud architecture on AWS.

The project separates the application into three independent layers:

- 🌐 **Web Tier** — React frontend served using Nginx
- ⚙️ **Application Tier** — Node.js / Express backend
- 🗄️ **Database Tier** — Amazon Aurora / MySQL-compatible database

This architecture demonstrates how a traditional full-stack application can be transformed into a **scalable, maintainable, and production-style cloud deployment**.

The application provides a simple transaction-management interface where users can:

- ➕ Add transactions
- 👀 View transactions
- 🗑️ Delete transactions

---

# 🎯 Project Objectives

The main objectives of this project are:

- Understand AWS 3-Tier Architecture
- Deploy a React frontend on Amazon EC2
- Configure Nginx as a web server
- Deploy a Node.js / Express backend
- Configure an Application Load Balancer
- Understand EC2 Auto Scaling
- Connect the backend with Aurora / MySQL
- Implement separation between application layers
- Understand cloud networking and security concepts
- Build a scalable full-stack cloud application

---

# 🏗️ System Architecture

The application follows a standard three-tier architecture.

```text
                              🌐 INTERNET
                                   |
                                   |
                                   v
                         +-------------------+
                         |     WEB TIER      |
                         |                   |
                         |    Amazon EC2     |
                         |       Nginx       |
                         |  React Frontend   |
                         +---------+---------+
                                   |
                                   |
                              HTTP / API
                                   |
                                   v
                         +-------------------+
                         | APPLICATION TIER  |
                         |                   |
                         | Application Load  |
                         |     Balancer      |
                         |         |         |
                         |    Auto Scaling   |
                         |         |         |
                         |   +-----+-----+   |
                         |   |           |   |
                         |   v           v   |
                         |  EC2         EC2  |
                         | Node.js     Node.js|
                         | Express     Express|
                         +---------+---------+
                                   |
                                   |
                                  SQL
                                   |
                                   v
                         +-------------------+
                         |   DATABASE TIER   |
                         |                   |
                         | Amazon Aurora /   |
                         |      MySQL        |
                         |                   |
                         | Persistent Data   |
                         +-------------------+
