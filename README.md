# AWS S3 + CloudFront Static Website

## 📌 Project Overview

This project demonstrates how to host a static website using **Amazon S3** and deliver the website globally using **Amazon CloudFront**.

The website is created using HTML and CSS. The files are stored in an Amazon S3 bucket, while CloudFront acts as a Content Delivery Network (CDN) to provide faster and secure content delivery.

## 🏗️ Architecture

```text
                         Internet Users
                               │
                               ▼
                    ┌─────────────────────┐
                    │     CloudFront      │
                    │        CDN          │
                    │                     │
                    │  Edge Locations     │
                    └──────────┬──────────┘
                               │
                       Secure Access
                               │
                               ▼
                    ┌─────────────────────┐
                    │     Amazon S3       │
                    │                     │
                    │    index.html      │
                    │    style.css       │
                    └─────────────────────┘
```

## 🛠️ Technologies Used

* Amazon S3
* Amazon CloudFront
* AWS IAM
* HTML
* CSS

## 🎯 Project Objectives

* Host a static website using Amazon S3.
* Upload HTML and CSS files to S3.
* Configure secure access between CloudFront and S3.
* Create a CloudFront distribution.
* Configure `index.html` as the default root object.
* Deliver website content using CloudFront.
* Test website accessibility through the CloudFront URL.

## 🚀 Implementation Steps

### 1. Create the Website

Created a simple static website using:

```text
website/
├── index.html
└── style.css
```

The `index.html` file contains the website structure, while `style.css` provides the styling.

### 2. Create an S3 Bucket

Created an Amazon S3 bucket to store the website files.

Example:

```text
aws-s3-cloudfront-static-website
```

The bucket was configured to store:

```text
index.html
style.css
```

### 3. Upload Website Files

Uploaded the HTML and CSS files to the S3 bucket.

```text
S3 Bucket
│
├── index.html
└── style.css
```

### 4. Configure S3 Access

The S3 bucket was kept private and configured to allow CloudFront to securely access the objects.

This prevents users from directly accessing the S3 bucket.

### 5. Create CloudFront Distribution

Created an Amazon CloudFront distribution.

The S3 bucket was configured as the CloudFront origin.

```text
CloudFront
     │
     ▼
S3 Bucket
```

### 6. Configure Origin Access Control

Configured **Origin Access Control (OAC)** so CloudFront can securely retrieve files from the private S3 bucket.

The flow becomes:

```text
User
 │
 ▼
CloudFront
 │
 │ Secure Access
 ▼
S3
```

### 7. Configure Default Root Object

Configured:

```text
index.html
```

as the CloudFront default root object.

Therefore, when a user opens the CloudFront domain, CloudFront serves the `index.html` file.

### 8. Deploy CloudFront

After creating the distribution, waited for CloudFront to finish deployment.

The CloudFront distribution provides a domain similar to:

```text
https://xxxxxxxx.cloudfront.net
```

### 9. Test the Website

Opened the CloudFront domain in a web browser.

The website was successfully displayed through CloudFront.

## 🔄 Request Flow

When a user requests the website:

```text
1. User requests website
          │
          ▼
2. CloudFront receives request
          │
          ▼
3. CloudFront checks its cache
          │
       ┌──┴──┐
       │     │
      HIT   MISS
       │     │
       │     ▼
       │    S3
       │     │
       │     ▼
       │ CloudFront
       │     │
       └──┬──┘
          ▼
      User receives
       website
```

## 🔐 Security

The project uses CloudFront Origin Access Control to provide secure access to the S3 bucket.

Instead of making the S3 bucket publicly accessible:

```text
User → S3
```

the architecture uses:

```text
User → CloudFront → S3
```

This provides better control over how the website content is accessed.

## ⚡ Benefits of CloudFront

CloudFront provides:

* Faster content delivery
* Edge caching
* Reduced latency
* HTTPS support
* Global content delivery
* Secure access to S3
* Reduced direct traffic to the S3 origin

## 📸 Screenshots

Screenshots demonstrating the project are stored in:

```text
screenshots/
```

Recommended screenshots:

1. S3 bucket creation
2. Website files uploaded to S3
3. CloudFront distribution
4. CloudFront configuration
5. Website running successfully

## 📁 Project Structure

```text
aws-s3-cloudfront-static-website/
│
├── README.md
│
├── website/
│   ├── index.html
│   └── style.css
│
├── architecture/
│   └── architecture-diagram.png
│
└── screenshots/
    ├── s3-bucket.png
    ├── s3-files.png
    ├── cloudfront.png
    └── website.png
```

## 💡 Key Learnings

Through this project, I learned:

* How Amazon S3 stores static website files.
* How to create and configure an S3 bucket.
* How to upload HTML and CSS files to S3.
* How Amazon CloudFront works as a CDN.
* How to configure an S3 origin in CloudFront.
* How Origin Access Control provides secure S3 access.
* How CloudFront caching improves content delivery.
* How to test a website using a CloudFront distribution URL.
* Basic AWS IAM and security concepts.

## 🎤 Interview Explanation

> I developed a static website using HTML and CSS and hosted the website files in Amazon S3. I created a CloudFront distribution with S3 as the origin and configured Origin Access Control to securely allow CloudFront to access the private S3 bucket. I configured `index.html` as the default root object and tested the website using the CloudFront distribution URL. This project helped me understand S3 static content storage, CDN-based content delivery, caching, and AWS security.

## ❓ Interview Questions

### 1. Why did you use S3?

Amazon S3 is used to store the static website files such as HTML, CSS, JavaScript, and images.

### 2. Why did you use CloudFront?

CloudFront is a CDN that caches and delivers content from AWS edge locations, helping reduce latency for users.

### 3. What is the origin in CloudFront?

The origin is the location from which CloudFront retrieves content.

In this project:

```text
Origin = Amazon S3
```

### 4. What is Origin Access Control?

Origin Access Control allows CloudFront to securely access an S3 bucket without requiring the bucket to be publicly accessible.

### 5. What is the default root object?

The default root object is the file CloudFront returns when a user requests the root of the distribution.

In this project:

```text
index.html
```

### 6. What happens when a user opens the CloudFront URL?

The request goes to CloudFront. If the requested content is cached, CloudFront can return it from its cache. Otherwise, CloudFront retrieves it from S3 and returns it to the user.

### 7. What is the difference between S3 and CloudFront?

**S3** stores the website files.

**CloudFront** delivers those files to users through its CDN and edge locations.

### 8. Why keep the S3 bucket private?

Keeping the bucket private provides better security and allows CloudFront to control access to the S3 origin.

## 📌 Future Improvements

Possible improvements include:

* Add a custom domain using Amazon Route 53.
* Configure an SSL/TLS certificate using AWS Certificate Manager.
* Add HTTPS-only access.
* Add JavaScript functionality.
* Configure CloudFront cache policies.
* Add CI/CD deployment using GitHub Actions.
* Add monitoring using Amazon CloudWatch.

## 👨‍💻 Author

**Bhuvan Chander**

AWS Cloud / DevOps Enthusiast

## ⭐ Project Summary

```text
HTML/CSS
   │
   ▼
Amazon S3
   │
   │ Origin
   ▼
Amazon CloudFront
   │
   ▼
Internet Users
```

This project demonstrates a basic **AWS static website hosting and content delivery architecture using Amazon S3 and CloudFront**.
