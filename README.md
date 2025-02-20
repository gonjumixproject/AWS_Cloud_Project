# 🚀 AWS Projects with Well-Architected Framework

Welcome to the **AWS Projects** repository! 🎯 This repository documents step-by-step AWS projects aligned with the **AWS Well-Architected Framework**, providing detailed guides, infrastructure-as-code (IaC), and best practices.

---

## 📚 Project Roadmap

1. 🔽 **Project 1: S3 Static Website Hosting**  
<details>
<summary><strong>Project Overview</strong></summary>

### 🚀 **Project Overview**
In this project, we build a **static website** hosted on **Amazon S3**, accessible via a public endpoint.

---

### 📝 **1.1 Create Your S3 Static Website**
*Reference: [Enabling website hosting](https://docs.aws.amazon.com/AmazonS3/latest/userguide/EnableWebsiteHosting.html).*

1. **Access the S3 Console**
   - Sign in to the [AWS Management Console](https://console.aws.amazon.com/s3/).
   - In the left navigation pane, choose **General purpose buckets**.

2. **Create Your Bucket**
   - Give your bucket a unique name and create it with **Default** values. Do not change anything for now.

3. **Enable Static Website Hosting**
   - Go to the **Properties** tab of the bucket.
   - Under **Static website hosting**, choose **Edit**.
   - Select **Use this bucket to host a website**.
   - Under **Static website hosting**, toggle **Enable**.

4. **Configure Index and Error Documents**
   - **Index Document:** Enter the file name of the index document, typically `index.html`.  
   - **Error Document (Optional):** Enter the name of your custom error page, typically `error.html`.

5. **Upload Your Website Files**
   - Upload your `index.html` and `error.html` files into the bucket.
   - Example files: [Configuring an index document](https://docs.aws.amazon.com/AmazonS3/latest/userguide/IndexDocumentSupport.html).

---

### 🔐 **1.2 Setting Permissions for Website Access**
*Reference: [Blocking public access to S3 storage](https://docs.aws.amazon.com/AmazonS3/latest/userguide/access-control-block-public-access.html).*

By default, Amazon S3 blocks public access to your account and buckets. To host a static website, you must adjust these settings:

1. Sign in to the [Amazon S3 console](https://console.aws.amazon.com/s3/).
2. In the **Buckets** list, select the bucket configured for static website hosting.
3. Go to the **Permissions** tab.
4. Under **Block public access (bucket settings)**, click **Edit**.
5. Uncheck **Block all public access** and choose **Save changes**.

⚠️ **Warning:**  
Disabling Block Public Access allows anyone on the internet to access your bucket. Make sure you understand the security implications before proceeding.

---

### 📜 **1.3 Add a Bucket Policy for Public Access**

To make the objects in your bucket publicly readable, you need to apply a bucket policy that grants `s3:GetObject` permission.

1. In the **S3 console**, navigate to the **Permissions** tab of your bucket.
2. Under **Bucket Policy**, click **Edit**.
3. Paste the following bucket policy, replacing `your-bucket-name` with your actual bucket name:

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
```

### 📜 **Step 3: Click the URL**
   - Your website URL is under the **Proporties** tab of your S3 Bucket under **Static Website**  
---
</details>
1. 🔽 **Project 2: Secure S3 Static Website Hosting with CloudFront**
<details>
<summary><strong>Project Overview</strong></summary>
   
### 📝 **1.1 Create Your S3 Static Website**
*Reference: [Enabling website hosting](https://docs.aws.amazon.com/AmazonS3/latest/userguide/EnableWebsiteHosting.html).*

1. **Access the S3 Console**
   - Sign in to the [AWS Management Console](https://console.aws.amazon.com/s3/).
   - In the left navigation pane, choose **General purpose buckets**.

2. **Create Your Bucket**
   - Give your bucket a unique name and create it with **Default** values. Do not change anything for now.

3. **Enable Static Website Hosting**
   - Go to the **Properties** tab of the bucket.
   - Under **Static website hosting**, choose **Edit**.
   - Select **Use this bucket to host a website**.
   - Under **Static website hosting**, toggle **Enable**.

4. **Configure Index and Error Documents**
   - **Index Document:** Enter the file name of the index document, typically `index.html`.  
   - **Error Document (Optional):** Enter the name of your custom error page, typically `error.html`.

5. **Upload Your Website Files**
   - Upload your `index.html` and `error.html` files into the bucket.
   - Example files: [Configuring an index document](https://docs.aws.amazon.com/AmazonS3/latest/userguide/IndexDocumentSupport.html).
### 📝 **1.2 Go to the CloudFront and Create a Distributaion**
   - Select your **Origin domain** as your S3 bucket
   - Select **Origin access** as **Origin access control settings (recommended)**
   - Click **Create New OAC**
      - Create a new OAC with default values.
   - Go under **Web Application Firewall (WAF)**, and **Do not enable security protections** since this is only educational purpose.
   - Go under **Settings** and set your **Default root object - optional** as **index.html**
   - **Create** your distribution.
   - **Copy Policy** for The S3 bucket policy. 

### 📝 **1.3 Go to the S3 Bucket Policy**
   - **Edit bucket policy**
   - Paste the provided policy, and **Save Changes**
     
### 📝 **1.4 Test your Access**
   - Go Under CloudFront **Distributions**
   - Type your **Distribution domain name** into the browser, either only Distribution domain name or Distribution domain name/index.html should work.
   - Go Under S3 Bucket, and see that does not work
