# Week-1 Microservices

## Project Overview
This folder contains the implementation of deploying a WordPress website using a microservices architecture on AWS. The architecture separates the web server and database server for modularity and scalability.

### Goals
- Launch two EC2 instances:
  - One for WordPress + Apache + PHP (Web Server)
  - One for MySQL (Database)
- Use Ubuntu 22.04 AMI with t2.micro instance type
- Configure appropriate Security Groups
- Create a Welcome Page as the WordPress homepage
- Secure the WordPress site with HTTPS (SSL Certificate)

### Architecture Overview
```
Internet
↓
Route 53 (DNS / Domain)
↓
EC2 Instance (WordPress Server)
  Apache + PHP + WP Site
  Public IP + Elastic IP
↓
RDS MySQL Database (Private Subnet)
```

### Security Group Configuration
#### EC2 WordPress Instance (Web Server)
| Type  | Protocol | Port Range | Source         |
|-------|----------|------------|----------------|
| SSH   | TCP      | 22         | My IP          |
| HTTP  | TCP      | 80         | 0.0.0.0/0      |
| HTTPS | TCP      | 443        | 0.0.0.0/0      |

#### RDS MySQL Instance
| Type         | Protocol | Port Range | Source                     |
|--------------|----------|------------|----------------------------|
| MySQL/Aurora | TCP      | 3306       | EC2 Instance’s Security Group |

### Step-by-Step Implementation
1. **Launch EC2 for WordPress**
   - Use Ubuntu Server 22.04 LTS AMI and t2.micro instance type.
   - Configure networking and security groups.
   - Optionally assign an Elastic IP.

2. **Create RDS Instance (MySQL)**
   - Use MySQL with Standard Create.
   - Configure instance class, username, password, and security groups.

3. **Configure LAMP Stack on EC2**
   - Install Apache, PHP, and required PHP modules.

4. **Apache Virtual Host Setup**
   - Configure and enable a virtual host for the WordPress site.

5. **Connect to MySQL (RDS)**
   - Install MySQL client and connect to the RDS instance.
   - Create a database for WordPress.

6. **Download and Configure WordPress**
   - Download WordPress and set up file permissions.

7. **WordPress Web Setup**
   - Complete the WordPress setup through the browser.

8. **Setup SSL Certificate (HTTPS)**
   - Use Certbot to install and configure SSL.

### Final Outcome
- WordPress deployed successfully on EC2 with Apache and PHP.
- MySQL database hosted on RDS securely.
- Welcome Page configured as homepage.
- HTTPS SSL enabled with Let’s Encrypt.
