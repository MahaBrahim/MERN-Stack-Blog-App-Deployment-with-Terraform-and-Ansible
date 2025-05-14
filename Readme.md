
MERN Stack Blog App Deployment - Infrastructure Bootcamp
This project demonstrates how to deploy a full-stack MERN blog application using modern DevOps tools on AWS. It was completed as part of the Infrastructure Engineering Bootcamp at the Saudi Digital Academy.
 
 Technologies Used
•	Terraform: Infrastructure provisioning
•	Ansible: Backend configuration automation
•	MongoDB Atlas: Managed NoSQL database
•	Amazon EC2: Hosting backend server
•	Amazon S3: Frontend static hosting and media storage
•	PM2: Node.js process manager
 
 Architecture Overview
The application consists of:
•	Frontend: Deployed on an S3 bucket with static website hosting enabled.
•	Backend: Runs on an EC2 instance (Ubuntu 22.04), configured with Ansible, and managed by PM2.
•	Database: Hosted on MongoDB Atlas, access restricted to the EC2 public IP.
•	Media Uploads: Stored in a separate S3 bucket, configured with IAM policies and CORS.
 
Deployment Steps
1. Terraform - Infrastructure Provisioning
Navigate to the Terraform folder and apply the configuration:
cd terraform/
terraform init
terraform apply
Terraform creates:
•	EC2 instance with a security group
•	Two S3 buckets (frontend + media)
•	IAM user with access policies
•	Key pair for SSH access
2. MongoDB Atlas Setup
•	Create a free cluster.
•	Add EC2 instance IP to IP Whitelist.
•	Create DB user.
•	Get the connection string for .env.
3. Backend Configuration with Ansible
cd ansible/
ansible-playbook -i inventory backend-playbook.yml
Ansible installs:
•	Node.js & PM2
•	Git clone of the backend repo
•	.env file from template
•	Runs pnpm install and starts app with PM2
 
Frontend Deployment
After building the frontend with:
pnpm run build
Sync it to the S3 bucket:
aws s3 sync dist/ s3://maha-blog-frontend-bucket1/
S3 static hosting URL can now serve the React app.
