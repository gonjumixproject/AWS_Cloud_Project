# 🚀 AWS Projects with Well-Architected Framework

Welcome to the **AWS Projects** repository! 🎯 This repository documents step-by-step AWS projects aligned with the **AWS Well-Architected Framework**, providing detailed guides, infrastructure-as-code (IaC), and best practices.

---

## 📚 Project Roadmap

### 1. ✅ **Project 1: S3 Static Website Hosting**  

In this project, we build a **static website** hosted on **Amazon S3**, accessible via a public endpoint.

#### **1.1 Create your S3 Static Website**
*Reference [Enabling website hosting](https://docs.aws.amazon.com/AmazonS3/latest/userguide/EnableWebsiteHosting.html).*

1. **Access the S3 Console**
   - Sign in to the [AWS Management Console](https://console.aws.amazon.com/s3/).
   - In the left navigation pane, choose **General purpose buckets**.

2. **Create Your Bucket**
   - Give your bucket a uniq name and create it with **Default** values, do not change anything for now. 

3. **Once the bucket is created Enable Static Website Hosting**
   - Go to the **Properties** tab.
   - Under **Static website hosting**, choose **Edit**.
   - Select **Use this bucket to host a website**.
   - Under **Static website hosting**, toggle **Enable**.

4. **Configure Index and Error Documents**
   - **Index Document:** Enter the file name of the index document, typically `index.html`.  
   - **Error Document (Optional):** Enter the name of your custom error page, typically `error.html`.  

5. **Upload your Index file and Error file into your bucket**
   - *Example index.html, error.html file links [Configuring an index document](https://docs.aws.amazon.com/AmazonS3/latest/userguide/IndexDocumentSupport.htmll).*

#### **1.2 Setting permissions for website access**
*Reference [Blocking public access to S3 storage](https://docs.aws.amazon.com/AmazonS3/latest/userguide/access-control-block-public-access.html).*

By default, Amazon S3 blocks public access to your account and buckets. To host a static website, you must adjust these settings:

1. Sign in to the [Amazon S3 console](https://console.aws.amazon.com/s3/).
2. In the **Buckets** list, select the bucket configured for static website hosting.
3. Go to the **Permissions** tab.
4. Under **Block public access (bucket settings)**, click **Edit**.
5. Uncheck **Block all public access** and choose **Save changes**.

⚠️ **Warning:**  
Disabling Block Public Access allows anyone on the internet to access your bucket. Make sure you understand the security implications before proceeding. 
---

### 📜 **Step 2: Add a Bucket Policy for Public Access**

To make the objects in your bucket publicly readable, you need to apply a bucket policy that grants `s3:GetObject` permission.

1. In the **S3 console**, navigate to the **Permissions** tab of your bucket.
2. Under **Bucket Policy**, click **Edit**.
3. Paste the following bucket policy, replacing `Bucket-Name` with your actual bucket name:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::your-bucket-name/*"
            ]
        }
    ]
}


📄 **Example Endpoint:**  
### 📄 **Project Steps**
1. **Create an S3 Bucket:** Store website files.  
2. **Enable Static Hosting:** Configure website endpoint.  
3. **Set Bucket Policy:** Allow public read access.  
4. **Upload Website Files:** `index.html` and `error.html`.  
5. **Test the Website:** Access through the S3 endpoint.

---

## 📜 Project Resources

Here are the official AWS and Terraform resources used for this project:

### 🌐 **AWS Documentation**
1. 📖 [Amazon S3 Static Website Hosting](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html)  
   - Learn how to configure an S3 bucket for static website hosting.
   
2. 🔒 [AWS S3 Bucket Policies](https://docs.aws.amazon.com/AmazonS3/latest/userguide/example-bucket-policies.html)  
   - Explore how to set bucket policies for public access.

3. ⚙️ [AWS CLI for S3](https://docs.aws.amazon.com/cli/latest/reference/s3/index.html)  
   - Command-line interface for managing S3 resources.

4. 🛠️ [AWS IAM Policy Generator](https://awspolicygen.s3.amazonaws.com/policygen.html)  
   - Tool to generate bucket policies easily.

---

### 📦 **Terraform Documentation**
1. 📗 [Terraform AWS S3 Bucket Resource](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket)  
   - Understand how to create and manage an S3 bucket using Terraform.

2. 📝 [Terraform AWS Provider](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)  
   - Documentation for the AWS provider in Terraform.

3. 💡 [Terraform Official Documentation](https://developer.hashicorp.com/terraform)  
   - Learn Terraform best practices and commands.

---
