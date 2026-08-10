# AWS 3-Tier Web Application

A working AWS 3-Tier Web Application built and deployed using Amazon EC2, Nginx, Node.js, React, an Internal Application Load Balancer, Auto Scaling, and an Amazon Aurora/MySQL-compatible database.

This project demonstrates how a web application can be separated into three independent layers:

1. **Web Tier** — React frontend served by Nginx
2. **Application Tier** — Node.js/Express backend running on EC2
3. **Database Tier** — Amazon Aurora/MySQL-compatible database

The application provides a simple transaction-management interface that allows users to add, view, and delete transactions.

---

## 📌 Project Overview

This project was created to demonstrate a practical AWS 3-Tier Architecture and the deployment of a full-stack application on AWS.

Instead of placing the frontend, backend, and database on a single server, each layer is separated and communicates with the next layer through controlled network paths.

```text
                         INTERNET
                            |
                            v
                  +-------------------+
                  |     WEB TIER      |
                  |     Amazon EC2    |
                  |      Nginx        |
                  |   React Frontend  |
                  +---------+---------+
                            |
                            | HTTP / API
                            v
                  +-------------------+
                  |   INTERNAL ALB    |
                  | Application Load  |
                  |    Balancer       |
                  +---------+---------+
                            |
                  +---------+---------+
                  |                   |
                  v                   v
          +---------------+   +---------------+
          |    APP TIER   |   |    APP TIER   |
          |  EC2 Instance |   |  EC2 Instance |
          |    Node.js    |   |    Node.js    |
          |    Express    |   |    Express    |
          +-------+-------+   +-------+-------+
                  |                   |
                  +---------+---------+
                            |
                            | MySQL
                            v
                  +-------------------+
                  |  DATABASE TIER    |
                  | Amazon Aurora /   |
                  | MySQL-compatible  |
                  +-------------------+

The Application Tier can run behind an Internal Application Load Balancer and inside an Auto Scaling Group.

This allows multiple backend instances to serve requests while the database remains a separate persistent layer.

🏗️ Architecture
1. Web Tier

The Web Tier is responsible for serving the frontend application.

Technologies
React
Nginx
Amazon EC2

The React application is compiled into a production build.

Nginx serves the generated static files and acts as a reverse proxy for API requests.

The request flow is:

Browser
   |
   | HTTP
   v
Web Tier EC2
   |
   | Nginx
   |
   +----------------------+
   |                      |
   | Frontend request     | /api/*
   v                      v
React Build          Internal ALB
                          |
                          v
                       App Tier

The Web Tier is the public-facing layer of the application.

2. Application Tier

The Application Tier contains the backend API.

Technologies
Node.js
Express.js
MySQL2
CORS
Body Parser
Amazon EC2
PM2

The backend listens on:

Port 4000

The App Tier provides APIs for:

Health checks
Creating transactions
Retrieving all transactions
Retrieving a transaction by ID
Deleting all transactions
Deleting a transaction by ID

The App Tier is designed to run in private networking and receive requests through the Internal Application Load Balancer.

3. Database Tier

The Database Tier contains the application's persistent data.

The project uses an Amazon Aurora / MySQL-compatible database.

The Node.js backend connects to the database using the MySQL2 Node.js driver.

The database contains a table called:

transactions

The table contains:

id
amount
description

Example:

+----+----------+-------------+
| id | amount   | description |
+----+----------+-------------+
|  1 |   123.00 | Test        |
|  2 |   500.00 | Example     |
+----+----------+-------------+
🔄 Request Flow

A typical transaction request travels through the architecture as follows:

User Browser
     |
     v
Web Tier EC2
     |
     | Nginx
     |
     | /api/transaction
     v
Internal Application Load Balancer
     |
     v
App Tier EC2
     |
     | Node.js / Express
     v
TransactionService.js
     |
     | MySQL
     v
Aurora / MySQL Database

The response then travels back through the application layers.

This separation allows the different layers to be scaled and secured independently.

📁 Repository Structure

The repository is organized as follows:

3TierArchitectureApp/
│
├── application-code/
│   │
│   ├── app-tier/
│   │   ├── index.js
│   │   ├── TransactionService.js
│   │   ├── DbConfig.js
│   │   ├── package.json
│   │   ├── package-lock.json
│   │   └── README.md
│   │
│   └── web-tier/
│       ├── public/
│       ├── src/
│       ├── package.json
│       ├── package-lock.json
│       └── README.md
│
├── 3 Tier Architecture.png
├── Documentation.txt
├── nginx
├── nginx-Without-SSL
├── README.md
└── .gitignore

The exact Nginx configuration filenames may differ depending on the deployment version.

📂 App Tier

The App Tier contains:

app-tier/
│
├── index.js
├── TransactionService.js
├── DbConfig.js
├── package.json
├── package-lock.json
└── README.md
index.js

The main Express application.

Responsibilities include:

Creating the Express server
Parsing JSON requests
Enabling CORS
Defining API routes
Providing the health-check endpoint
Calling the transaction service
Starting the application on port 4000
TransactionService.js

Contains the database operations.

Responsibilities include:

Adding transactions
Retrieving all transactions
Finding a transaction by ID
Deleting all transactions
Deleting a transaction by ID

Keeping database operations separate from the Express routes makes the backend easier to understand and maintain.

DbConfig.js

Contains the database connection configuration.

Database credentials are supplied through environment variables rather than being hard-coded into the repository.

The application expects:

DB_HOST
DB_USER
DB_PWD
DB_DATABASE

Example:

DB_HOST=your-database-endpoint
DB_USER=your-database-user
DB_PWD=your-database-password
DB_DATABASE=your-database-name

Never commit real credentials to GitHub.

package.json

Contains the Node.js project metadata and dependencies.

Main dependencies include:

Express
MySQL2
CORS
Body Parser
Node Fetch
📂 Web Tier

The Web Tier contains the React frontend.

web-tier/
│
├── public/
│
├── src/
│   ├── App.js
│   ├── App.css
│   ├── global.js
│   ├── hooks.js
│   ├── index.js
│   ├── index.css
│   ├── theme.js
│   ├── assets/
│   │   ├── 1.png
│   │   └── 3TierArch.png
│   │
│   └── components/
│       ├── Burger/
│       ├── Menu/
│       ├── Home/
│       └── DatabaseDemo/
│
├── package.json
└── package-lock.json
🖥️ Frontend

The frontend currently contains two main views.

Home

The Home page displays:

Project title
AWS 3-Tier Architecture diagram
Database Demo

The Database Demo page provides a simple interface for interacting with the backend.

The current frontend allows users to:

Add a transaction
View transactions
Delete all transactions

The backend also contains endpoints for retrieving and deleting individual transactions by ID, although those operations are not currently exposed as separate controls in the frontend.

🧭 Frontend Routing

The application uses React Router with HashRouter.

Therefore, the Database Demo page is accessed using:

/#/db

rather than:

/db

The # portion is handled by the browser and therefore does not require Nginx to serve a separate frontend route.

🔌 API Endpoints

The backend provides the following API endpoints.

Health Check
GET /health

Used to verify that an App Tier instance is running.

Example response:

"This is the health check"

This endpoint can be configured as the health-check path for the Internal Application Load Balancer.

Get All Transactions
GET /transaction

Returns all transactions stored in the database.

Example response:

{
  "result": [
    {
      "id": 1,
      "amount": "123.00",
      "description": "Test transaction"
    }
  ]
}
Add Transaction
POST /transaction

Example request:

{
  "amount": "123.00",
  "desc": "Test transaction"
}
Delete All Transactions
DELETE /transaction

Deletes all transactions from the database.

This endpoint is included primarily for demonstration purposes.

Delete Transaction by ID
DELETE /transaction/id

Example request:

{
  "id": 1
}
Get Transaction by ID
GET /transaction/id

Example request:

{
  "id": 1
}
🚀 Running the Application Locally

The application can be run locally for development and testing.

Prerequisites

Install:

Node.js
npm
Git
A MySQL-compatible database

AWS is not required for local development if you provide your own MySQL-compatible database.

⚙️ App Tier Setup

Navigate to:

cd application-code/app-tier

Install dependencies:

npm install
🔑 Configure Database Environment Variables

The application reads database configuration from environment variables.

The following variables are required:

DB_HOST
DB_USER
DB_PWD
DB_DATABASE
Linux / macOS
export DB_HOST="your-database-endpoint"
export DB_USER="your-database-user"
export DB_PWD="your-database-password"
export DB_DATABASE="your-database-name"
Windows PowerShell
$env:DB_HOST="your-database-endpoint"
$env:DB_USER="your-database-user"
$env:DB_PWD="your-database-password"
$env:DB_DATABASE="your-database-name"

The current application does not use the dotenv package, so simply creating a .env file will not automatically load these values.

🗄️ Database Setup

Create a MySQL-compatible database.

Example:

CREATE DATABASE webappdb;

Select the database:

USE webappdb;

Create the transactions table:

CREATE TABLE transactions (
    id INT AUTO_INCREMENT PRIMARY KEY,
    amount DECIMAL(10,2),
    description VARCHAR(255)
);

Verify the table:

SELECT * FROM transactions;
▶️ Run the App Tier Locally

From the App Tier directory:

node index.js

The backend should listen on:

http://localhost:4000

Test the health endpoint:

http://localhost:4000/health
🌐 Web Tier Setup

Navigate to:

cd application-code/web-tier

Install dependencies:

npm install
🏗️ Build the React Application

Create a production build:

npm run build

This creates:

build/

The generated files are the production version of the React application.

🧪 Frontend Development Mode

For development:

npm start

The React development server normally runs on:

http://localhost:3000
☁️ AWS Deployment

The working deployment uses the following architecture:

                    INTERNET
                       |
                       v
              +----------------+
              |   WEB TIER     |
              | EC2 + Nginx    |
              | React Build    |
              +-------+--------+
                      |
                      | /api/*
                      v
              +----------------+
              |  INTERNAL ALB  |
              +-------+--------+
                      |
              +-------+-------+
              |               |
              v               v
        +-----------+   +-----------+
        | App EC2   |   | App EC2   |
        | Node.js   |   | Node.js   |
        | PM2       |   | PM2       |
        +-----+-----+   +-----+-----+
              |               |
              +-------+-------+
                      |
                      v
              +----------------+
              | Aurora / MySQL |
              +----------------+
🖥️ Web Tier Deployment

The Web Tier runs on an Amazon EC2 instance.

First build the React application:

npm run build

The resulting build/ directory contains the production frontend.

Nginx serves the contents of the build directory.

The deployment uses a directory similar to:

/home/ec2-user/web-tier/build
🔀 Nginx Configuration

Nginx performs two major functions.

1. Serve the React Application

Requests to:

/

are served from the React production build.

Nginx uses:

try_files $uri /index.html;

to allow the React application to handle frontend navigation.

2. Reverse Proxy API Requests

Requests beginning with:

/api/

are forwarded to the Internal Application Load Balancer.

For example:

Browser
   |
   | /api/transaction
   v
Nginx
   |
   | Internal HTTP
   v
Internal Application Load Balancer
   |
   v
App Tier

The Nginx configuration uses the trailing / in proxy_pass so that:

/api/transaction

is forwarded to the backend as:

/transaction

This matches the Express routes.

⚖️ Internal Application Load Balancer

The App Tier is placed behind an Internal Application Load Balancer.

The ALB:

Receives API requests from the Web Tier
Performs health checks
Routes traffic to healthy App Tier instances
Allows multiple backend instances to serve traffic
Provides the foundation for horizontal scaling

The App Tier does not need to be publicly accessible.

📈 Auto Scaling

The App Tier can run inside an Auto Scaling Group.

A simplified setup is:

             Internal ALB
                  |
          +-------+-------+
          |               |
          v               v
      App EC2          App EC2
      Instance         Instance
          |               |
          +-------+-------+
                  |
                  v
             Database

The Auto Scaling Group can launch or terminate App Tier instances according to the configured scaling policy.

This provides:

Horizontal scaling
High availability
Fault tolerance
Better handling of increased traffic

The working deployment was tested with Auto Scaling enabled.

🔄 Application Process Management

The App Tier deployment uses PM2 to keep the Node.js application running.

Example:

pm2 start index.js --name app-tier

Check the application:

pm2 status

View logs:

pm2 logs app-tier

Save the PM2 process list:

pm2 save

For automatic startup after reboot, configure PM2 startup according to the Linux distribution and Node.js installation being used.

🗄️ Database Deployment

The Database Tier uses an Amazon Aurora / MySQL-compatible database.

The database should be placed in private networking and should not be directly accessible from the public internet.

The App Tier communicates with the database over MySQL.

App Tier EC2
     |
     | MySQL
     v
Aurora / MySQL Database
🔐 Security Model

Each tier should only allow the communication it requires.

A simplified model is:

Internet
   |
   | HTTP / HTTPS
   v
Web Tier
   |
   | HTTP
   v
Internal ALB
   |
   | HTTP : 4000
   v
App Tier
   |
   | MySQL
   v
Database

Recommended security boundaries:

Internet
   |
   v
Web Tier Security Group
   |
   v
Internal ALB Security Group
   |
   v
App Tier Security Group
   |
   v
Database Security Group

The exact ports and security-group rules depend on the AWS deployment.

The important principle is that each layer should only accept traffic from the layer that needs to communicate with it.

🔑 Environment Variables

Database credentials are intentionally not stored directly in the source code.

The App Tier expects:

DB_HOST
DB_USER
DB_PWD
DB_DATABASE

Example:

DB_HOST=database-endpoint
DB_USER=database-user
DB_PWD=database-password
DB_DATABASE=webappdb

The actual values must be supplied by the person deploying the application.

🚨 Security Warning

Never commit the following to GitHub:

Database passwords
AWS access keys
AWS secret keys
Private SSH keys
API keys
Authentication tokens
Other secrets

The repository should contain only example configuration values.

If a secret is accidentally committed:

Remove it from the repository.
Immediately rotate or change the compromised credential.
Check Git history because removing the secret from the latest commit does not remove it from previous commits.
📋 Deployment Checklist
AWS Infrastructure
 AWS account
 VPC
 Public subnets
 Private subnets
 Internet Gateway
 Required route tables
 Security Groups
 Web Tier EC2
 App Tier EC2
 Internal Application Load Balancer
 Target Group
 Auto Scaling Group
 Aurora / MySQL-compatible database
App Tier
 Node.js installed
 Application files copied
 npm install completed
 Environment variables configured
 Database created
 Transactions table created
 Backend running on port 4000
 /health endpoint working
 PM2 configured
 App instances registered with the Target Group
 Internal ALB health checks passing
Web Tier
 Node.js installed
 Application files copied
 npm install completed
 React production build created
 Nginx installed
 Nginx configured
 React build served correctly
 /api/ forwarded to the Internal ALB
 Web Tier accessible from the internet
🧪 Testing the Deployment
Test 1 — Home Page

Open the public address of the Web Tier.

The Home page should load and display the project architecture.

Test 2 — Database Demo

Open:

/#/db

The Database Demo page should appear.

Test 3 — Add Transaction

Enter an amount and description.

Example:

Amount: 123
Description: Test

Click:

ADD

The transaction should appear in the table.

Test 4 — Verify Database

Connect to the database and run:

SELECT * FROM transactions;

The newly created transaction should be present.

Test 5 — Delete Transactions

Click:

DEL

The frontend should request:

DELETE /api/transaction

Nginx forwards the request to the Internal ALB, which sends it to the App Tier.

Verify the database:

SELECT * FROM transactions;
Test 6 — Health Check

The backend health endpoint is:

/health

The Internal Application Load Balancer can use this endpoint to determine whether an App Tier instance is healthy.

Test 7 — Auto Scaling

When Auto Scaling is enabled, verify:

Multiple App Tier instances can run.
The Target Group shows healthy instances.
The Internal ALB distributes requests.
Requests continue working when an App Tier instance becomes unavailable.
Scaling policies can launch additional instances when required.
🛠️ Troubleshooting
Application Does Not Start

Run:

node index.js

or check PM2:

pm2 status
pm2 logs app-tier

Look for errors related to:

Missing dependencies
Environment variables
Database connectivity
Port configuration
Database Connection Fails

Verify:

DB_HOST
DB_USER
DB_PWD
DB_DATABASE

Also verify that the database security rules allow MySQL traffic from the App Tier.

Frontend Loads but Database Demo Does Not Work

Check:

Browser developer console
Nginx configuration
/api/transaction request
Internal Application Load Balancer
Target Group health
App Tier application
Backend port 4000
Database connectivity
Load Balancer Marks App Tier Unhealthy

Check:

/health

Make sure:

Node.js is running.
The application listens on port 4000.
The Target Group uses the correct port.
The health-check path is /health.
Security Groups allow the ALB to reach the App Tier.
Nginx Is Not Serving the Frontend

Check that the React build exists:

ls -lh /home/ec2-user/web-tier/build

Check Nginx configuration:

sudo nginx -t

If the configuration is valid, reload Nginx:

sudo systemctl reload nginx

Check Nginx status:

sudo systemctl status nginx
📚 Learning Objectives

This project demonstrates practical experience with:

AWS
Amazon EC2
Application Load Balancer
Internal Application Load Balancer
Auto Scaling
VPC networking
Public and private subnets
Security Groups
Amazon Aurora / RDS
Backend
Node.js
Express.js
REST APIs
MySQL2
Database connectivity
CRUD operations
Frontend
React
React Router
Styled Components
Component-based architecture
API integration
Web Server
Nginx
Reverse proxying
Static file serving
Health checks
DevOps
Linux
EC2 deployment
PM2
Application logs
Git
GitHub
Load balancing
Auto Scaling
AWS networking
🧠 Why Use a 3-Tier Architecture?

A simple application could place the frontend, backend, and database on the same server.

While this is easy to build, it becomes harder to scale, secure, and maintain.

A 3-Tier Architecture separates responsibilities.

Web Tier

Responsible for:

User Interface
Static Files
Web Traffic
Application Tier

Responsible for:

Business Logic
API Requests
Application Processing
Database Requests
Database Tier

Responsible for:

Persistent Data
Queries
Transactions

This separation makes it easier to:

Scale individual layers
Improve security
Increase availability
Replace components independently
Monitor different layers
Maintain the application
📈 Future Improvements

The current repository represents the working deployed version of the project.

Possible future improvements include:

Infrastructure as Code using Terraform
CI/CD using GitHub Actions
Docker containers
HTTPS / TLS
AWS Certificate Manager
Route 53 custom domain
CloudWatch monitoring
Centralized logging
Better API validation
Parameterized SQL queries
Improved error handling
Authentication and authorization
AWS Secrets Manager
Automated testing
Database backup and recovery testing
More advanced Auto Scaling policies
Automated EC2 configuration
Infrastructure automation

These improvements can be introduced incrementally while keeping the same fundamental 3-Tier architecture.

💰 AWS Cost Considerations

AWS services used by this project may incur charges depending on the AWS account, region, configuration, and usage.

Potentially billable services include:

Amazon EC2
Application Load Balancer
Aurora / RDS
NAT Gateway
Data transfer
Other AWS services

Before recreating the project, check the current AWS pricing for the services you plan to use.

When the project is no longer required, terminate or delete resources that are no longer needed to avoid unnecessary charges.

📌 Project Status

Current Status: Working AWS Deployment

The project has been deployed and tested as a working 3-Tier architecture consisting of:

React Web Tier
Nginx
Node.js / Express App Tier
Internal Application Load Balancer
MySQL-compatible database
Amazon EC2
Auto Scaling

The application is functional and serves as the baseline version for future improvements.

👨‍💻 Author
Harshit Saharan

AWS 3-Tier Web Application demonstrating:

React
   +
Nginx
   +
Node.js / Express
   +
MySQL / Aurora
   +
Amazon EC2
   +
Application Load Balancer
   +
Auto Scaling
📜 Version History
v1.0.0 — Initial Working Deployment

Initial version of the AWS 3-Tier Web Application.

This version documents the working architecture and deployment.

Future changes and improvements will be tracked using Git commits, branches, and version tags.