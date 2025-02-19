# 🚀 AWS Projects with Well-Architected Framework

Welcome to the **AWS Projects** repository! 🎯 This repository documents step-by-step AWS projects aligned with the **AWS Well-Architected Framework**, providing detailed guides, infrastructure-as-code (IaC), and best practices.

---

## 📚 Project Roadmap

1. ✅ **Project 1: S3 Static Website Hosting**  
2. 🚧 **Project 2: CI/CD Pipeline for Website Deployment (Coming Soon!)**  
3. 🚧 **Project 3: CloudFront for Content Delivery (Coming Soon!)**  
4. 🚧 **More projects are on the way!**

---

## 🌐 Project 1: Create an S3 Bucket for Static Website Hosting

In this project, we build a **static website** hosted on **Amazon S3**, accessible via a public endpoint.

### 📦 **Project Highlights**
1. **S3 Bucket:** Created for hosting website files.  
2. **Static Website Hosting:** Enabled through S3.  
3. **Public Access:** Configured with a bucket policy.  
4. **Terraform Automation:** Infrastructure-as-Code (IaC).  
5. **Website Upload:** HTML and error pages.  

### 📄 **Project Steps**
1. **Create an S3 Bucket:** Store website files.  
2. **Enable Static Hosting:** Configure website endpoint.  
3. **Set Bucket Policy:** Allow public read access.  
4. **Upload Website Files:** `index.html` and `error.html`.  
5. **Test the Website:** Access through the S3 endpoint.

---

📜 Project Resources
📖 AWS S3 Static Website Hosting Documentation
🌍 Terraform AWS Provider Documentation
🔑 AWS IAM Bucket Policy Generator
💡 Follow this repository for updates as we expand projects covering compute, databases, networking, and security!

📬 Contributions and feedback are welcome! If you have any questions, feel free to open an issue.



## ⚙️ **Infrastructure Setup (Terraform)**

This project uses **Terraform** to provision AWS resources. Find the code in the `/terraform` directory.

**Main commands:**

```bash
# Initialize Terraform
terraform init

# Preview the infrastructure changes
terraform plan

# Deploy the infrastructure
terraform apply

# Destroy resources (if needed)
terraform destroy
