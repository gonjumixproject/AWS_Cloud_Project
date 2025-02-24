# 🚀 AWS Projects with Well-Architected Framework

Welcome to the **AWS Projects** repository! 🎯 This repository documents step-by-step AWS projects aligned with the **AWS Well-Architected Framework**, providing detailed guides, infrastructure-as-code (IaC), and best practices.

---

## 📚 Project Roadmap

 🔽 **Project 1: S3 Static Website Hosting**  
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

 🔽 **Project 2: Secure S3 Static Website Hosting with CloudFront**
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
</details>

🔽 **Project 3: Connect your GitHub Actions with AWS using OIDC**  
<details>
<summary><strong>Project Overview</strong></summary>

*Reference:[AWS: Use IAM roles to connect GitHub Actions][https://aws.amazon.com/blogs/security/use-iam-roles-to-connect-github-actions-to-actions-in-aws/]*


### 1. Create an OIDC Identity Provider in AWS
1. Sign in to the AWS Management Console.
2. Open the **IAM** service.
3. In the left navigation pane, choose **Identity Providers**.
4. Select **Add Provider** and set the following:
   - **Provider Type:** OpenID Connect
   - **Provider URL:** `https://token.actions.githubusercontent.com`
   - **Audience:** `sts.amazonaws.com`
5. Click **Add Provider**.

### 2. Create an IAM Role for GitHub Actions
1. Go to the **IAM** > **Identity providers** > **token.actions.githubusercontent.com**
2. Click **Assing Role** and choose **Create a new Role** .
3. Select **Web Identity**. 
4. Select the identity provider created earlier.
5. Under **Audience**, choose `sts.amazonaws.com`.
6. Select your **GitHub organization**.
7. Select your **GitHub repository** if you want.
8. Attach policies required for your GitHub Actions workflow, for this example I will create a S3 static website, so I will give **AmazonS3FullAccess**.
9. Give a **Role name** to this role. 
10. AWS will create a **Trust policy** for that role, so you do not need to update that information. 

### 3. Update GitHub Actions Workflow
1. Create a GitHub repository, and make sure it matches with the **GitHub repository** that provided in the AWS IAM. 
2. In your GitHub repository, click **Action**.
3. Click **Configure** under **Simple workflow**.
4. It will create a **.github/workflows/blank.yml** file automaticly, you can create your own workflows folder, and yaml file as well.
5. Change the **blank.yml** to **main.yml**
6. Add the following permissions and AWS credentials setup in your workflow YAML:

```yaml
# This is a basic workflow to help you get started with Actions
name:  Connect to an AWS role from a GitHub repository

# Controls when the action will run. Invokes the workflow on push events but only for the main branch
on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

env:
  
  AWS_REGION : <"us-east-1"> #Change to reflect your Region

# Permission can be added at job level or workflow level    
permissions:
      id-token: write   # This is required for requesting the JWT
      contents: read    # This is required for actions/checkout
jobs:
  AssumeRoleAndCallIdentity:
    runs-on: ubuntu-latest
    steps:
      - name: Git clone the repository
        uses: actions/checkout@v3
      - name: configure aws credentials
        uses: aws-actions/configure-aws-credentials@v1.7.0
        with:
          role-to-assume: <arn:aws:iam::111122223333:role/GitHubAction-AssumeRoleWithAction> #change to reflect your IAM role’s ARN
          role-session-name: GitHub_to_AWS_via_FederatedOIDC
          aws-region: ${{ env.AWS_REGION }}
      # Hello from AWS: WhoAmI
      - name: Sts GetCallerIdentity
        run: |
          aws sts get-caller-identity
```

AWS_REGION: Enter the AWS Region for your AWS resources.
role-to-assume: Replace the ARN with the ARN of the AWS GitHubAction role that you created previously.

### 4. Run your workflow
</details>

🔽 **Project 4:Create your first CI/CD pipeline to automate deployment on EC2 - Soon**  
<details>
<summary><strong>Project Overview</strong></summary>
</details>
