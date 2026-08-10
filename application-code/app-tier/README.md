# \# App Tier — Node.js Backend

# 

# This directory contains the backend application for the AWS 3-Tier Web Application.

# 

# The App Tier runs a Node.js/Express API and communicates with the Amazon Aurora/MySQL-compatible database in the Database Tier.

# 

# \## Architecture

# 

# ```text

# Web Tier (React + Nginx)

# &#x20;       |

# &#x20;       | HTTP / API

# &#x20;       v

# Internal Application Load Balancer

# &#x20;       |

# &#x20;       v

# App Tier EC2 Instances

# (Node.js + Express)

# &#x20;       |

# &#x20;       | MySQL

# &#x20;       v

# Amazon Aurora / RDS

# ```

# 

# \## Technologies

# 

# \- Node.js

# \- Express.js

# \- MySQL2

# \- CORS

# \- Body Parser

# \- Amazon EC2

# \- Amazon Aurora / RDS

# 

# \## Files

# 

# | File | Purpose |

# |------|---------|

# | `index.js` | Express server and API routes |

# | `TransactionService.js` | Database operations |

# | `DbConfig.js` | Database connection configuration |

# | `package.json` | Node.js dependencies and project metadata |

# | `package-lock.json` | Locked dependency versions |

# 

# \## API Endpoints

# 

# \### Health Check

# 

# ```http

# GET /health

# ```

# 

# Used by the Application Load Balancer to verify that the application instance is healthy.

# 

# \### Get All Transactions

# 

# ```http

# GET /transaction

# ```

# 

# Returns all transactions from the database.

# 

# \### Add Transaction

# 

# ```http

# POST /transaction

# ```

# 

# Example request body:

# 

# ```json

# {

# &#x20; "amount": "123.00",

# &#x20; "desc": "Test transaction"

# }

# ```

# 

# \### Delete All Transactions

# 

# ```http

# DELETE /transaction

# ```

# 

# Deletes all transactions from the database.

# 

# \### Delete Transaction by ID

# 

# ```http

# DELETE /transaction/id

# ```

# 

# Example request body:

# 

# ```json

# {

# &#x20; "id": 1

# }

# ```

# 

# \### Get Transaction by ID

# 

# ```http

# GET /transaction/id

# ```

# 

# Example request body:

# 

# ```json

# {

# &#x20; "id": 1

# }

# ```

# 

# \## Local Setup

# 

# \### 1. Install dependencies

# 

# ```bash

# npm install

# ```

# 

# \### 2. Configure the database

# 

# Create or update `DbConfig.js` with the credentials for your own database.

# 

# \*\*Do not commit real database credentials to GitHub.\*\*

# 

# Example:

# 

# ```javascript

# module.exports = Object.freeze({

# &#x20;   DB\_HOST: 'your-database-endpoint',

# &#x20;   DB\_USER: 'your-database-user',

# &#x20;   DB\_PWD: 'your-database-password',

# &#x20;   DB\_DATABASE: 'your-database-name'

# });

# ```

# 

# \### 3. Start the application

# 

# ```bash

# node index.js

# ```

# 

# The backend listens on:

# 

# ```text

# http://localhost:4000

# ```

# 

# \## AWS Deployment

# 

# In the complete 3-tier architecture, the App Tier is deployed on EC2 instances inside private subnets.

# 

# An Internal Application Load Balancer distributes requests between App Tier instances.

# 

# The instances can be placed inside an Auto Scaling Group to provide:

# 

# \- High availability

# \- Automatic scaling

# \- Fault tolerance

# \- Load distribution

# 

# The App Tier does not need to be publicly accessible. Requests are received through the Internal Application Load Balancer from the Web Tier.

# 

# \## Database

# 

# The application connects to the database using MySQL2.

# 

# The database is hosted separately from the App Tier and is accessed through the private network.

# 

# \## Important

# 

# This project is designed as a demonstration of an AWS 3-Tier Architecture.

# 

# Before deploying the application yourself:

# 

# 1\. Create your own database.

# 2\. Configure your own database credentials.

# 3\. Update the database endpoint.

# 4\. Configure the required AWS networking and security groups.

# 5\. Configure the Internal Application Load Balancer.

# 6\. Deploy the App Tier EC2 instances.

# 7\. Configure the Web Tier to communicate with the Internal Load Balancer.

