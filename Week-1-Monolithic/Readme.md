# Week-1 Monolithic

## Project Overview
This folder contains the implementation of deploying a WordPress website using a monolithic architecture on AWS. Both the WordPress application and MySQL database are hosted on a single EC2 instance for simplicity.

### Goals
- Set up a monolithic server architecture using a single EC2 instance.
- Install and configure WordPress and MySQL on the same instance.
- Configure security groups to allow required ports.
- Design and set a Welcome Page as the homepage.

### Tools and Technologies Used
- AWS EC2 (t2.micro)
- Ubuntu 22.04 LTS
- CyberPanel with OpenLiteSpeed
- WordPress CMS
- MySQL (via CyberPanel)
- Dynu (Free DNS Service)
- Let’s Encrypt SSL
- Linux Terminal

### Infrastructure Setup
#### Step 1: Create EC2 Instance
- AMI: Ubuntu Server 22.04 LTS
- Instance Type: t2.micro (Free Tier eligible)
- Storage: 8 GB (default)
- Key Pair: Generated .pem file for SSH access
- Security Group (Ports Opened):
  - 22: SSH
  - 80: HTTP
  - 443: HTTPS
  - 3389: Reserved (optional)

#### Step 2: Assign Elastic IP
- Go to EC2 Dashboard > Elastic IPs.
- Allocate a new IP and associate it with the running instance.

#### Step 3: Install CyberPanel
- SSH into your EC2 instance:
  ```bash
  ssh -i "your-key.pem" ubuntu@<your-elastic-ip>
  ```
- Switch to root:
  ```bash
  sudo -i
  ```
- Download and run the CyberPanel installer:
  ```bash
  cd /root
  wget -O installer.sh https://cyberpanel.net/install.sh
  chmod +x installer.sh
  ./installer.sh
  ```
- During installation:
  - Select 1 → Install CyberPanel with OpenLiteSpeed
  - Choose 1 → Full installation
  - Set admin password
  - Enable PowerDNS, Postfix, Pure-FTPd as needed (optional)

#### Step 4: Access CyberPanel
- Visit:
  ```
  https://<your-elastic-ip>:8090
  ```
- Login:
  - Username: admin
  - Password: (as set during installation)

### Website Configuration
#### Step 5: Create a Website in CyberPanel
- Go to Websites > Create Website
- Enter:
  - Domain: your Dynu domain (e.g., yourdomain.dynu.com)
  - Email: valid email
  - PHP version: 8.1 or later
- Click Create Website

#### Step 6: Point Domain to EC2 IP
- Go to Dynu DNS
- Create a free account and add your domain.
- Set A record for @ and www to your Elastic IP.

#### Step 7: Install WordPress
- From CyberPanel dashboard:
  - Go to Websites → List Websites → Manage
  - Under Application Installer, click WordPress + LSCache
  - Enter:
    - Site title
    - Admin username/password
    - Email
  - Click Install Now

#### Step 8: Install SSL
- In the same site dashboard, scroll to SSL > Issue SSL
- CyberPanel automatically fetches SSL from Let’s Encrypt.
- Check:
  ```
  https://yourdomain.dynu.com
  ```

#### Step 9: Configure Welcome Homepage
- Login to WordPress Admin:
  ```
  https://yourdomain.dynu.com/wp-admin
  ```
- Create a new Page titled “Welcome.”
- Add your content (text, images, etc.).
- Go to Settings > Reading:
  - Set Homepage displays to “A static page”
  - Select the “Welcome” page as the homepage
  - Save Changes

#### Step 10: Migrate Existing Site (Optional)
- If migrating an old site:
  - Use All-in-One WP Migration plugin on the original site.
  - Export your site.
  - Install the same plugin on your new WordPress instance and import the site.

### Final Outcome
- WordPress deployed successfully on EC2 with CyberPanel and OpenLiteSpeed.
- Welcome Page configured as homepage.
- HTTPS SSL enabled with Let’s Encrypt.
- Domain resolution handled via Dynu DNS.
