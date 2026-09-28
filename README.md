# AWS S3 + CloudFront Static Website

![AWS](https://img.shields.io/badge/AWS-Cloud-blue?logo=amazonaws)
![Amazon S3](https://img.shields.io/badge/Amazon-S3-orange?logo=amazons3)
![CloudFront](https://img.shields.io/badge/Amazon-CloudFront-purple?logo=amazoncloudfront)
![HTML](https://img.shields.io/badge/HTML5-Website-orange?logo=html5)
![CSS](https://img.shields.io/badge/CSS3-Styling-blue?logo=css3)

## 📌 Project Overview

This project demonstrates how I deployed a **static website on Amazon S3 and delivered it globally using Amazon CloudFront**.

The website is a space-themed static website containing multiple HTML pages, CSS stylesheets, JavaScript, fonts, and images.

The main objective of this project was to understand how AWS can be used to host and distribute a static website without requiring an EC2 server.

### Architecture

```text
                    ┌─────────────────────┐
                    │       User          │
                    │     Web Browser     │
                    └──────────┬──────────┘
                               │
                               │ HTTPS
                               ▼
                    ┌─────────────────────┐
                    │    CloudFront       │
                    │       CDN           │
                    └──────────┬──────────┘
                               │
                               │ Origin Access Control
                               ▼
                    ┌─────────────────────┐
                    │     Amazon S3       │
                    │   Static Website    │
                    │                     │
                    │ HTML / CSS / JS     │
                    │ Images / Fonts      │
                    └─────────────────────┘
☁️ AWS Services Used
Service	Purpose
Amazon S3	Stores the static website files
Amazon CloudFront	Provides global content delivery
CloudFront OAC	Secures access between CloudFront and S3
IAM / AWS Policies	Controls access to S3 objects
🏗️ Project Architecture

The website files are stored in an Amazon S3 bucket.

CloudFront is configured as the distribution layer in front of S3.

Users access the website through the CloudFront distribution instead of directly accessing the S3 bucket.

Request Flow
User
  │
  │ HTTPS Request
  ▼
CloudFront Distribution
  │
  │ OAC Authentication
  ▼
Amazon S3 Bucket
  │
  ├── HTML
  ├── CSS
  ├── JavaScript
  ├── Images
  └── Fonts
📁 Project Structure
AWS-S3-CLOUDFRONT-STATIC-WEBSITE/
│
├── css/
│   ├── mobile.css
│   └── style.css
│
├── fonts/
│   ├── audiowide-regular-webfont.eot
│   ├── audiowide-regular-webfont.svg
│   ├── audiowide-regular-webfont.ttf
│   └── audiowide-regular-webfont.woff
│
├── images/
│   ├── alien-life.jpg
│   ├── astronaut.jpg
│   ├── bg-about.jpg
│   ├── bg-home.jpg
│   ├── curious-rover.jpg
│   ├── earth-satellite.jpg
│   ├── galaxy.jpg
│   ├── mars-rover.jpg
│   └── ...
│
├── js/
│   └── mobile.js
│
├── screenshots/
│   ├── 01-s3-bucket-objects.png
│   ├── 02-cloudfront-access-denied.png
│   ├── 03-s3-bucket-policy-oac.png
│   ├── 04-cloudfront-distribution-settings.png
│   ├── 05-home-page.png
│   ├── 06-about-page.png
│   ├── 07-contact-page.png
│   └── 08-blog-page.png
│
├── about.html
├── blog.html
├── contact.html
├── index.html
├── proj1.html
├── projects.html
├── singlepost.html
└── README.md
🚀 Implementation
Step 1 – Created the Static Website

I used a static HTML website containing multiple pages:

Home
About
Projects
Blog
Contact
Project details
Single blog post

The website also contains supporting CSS, JavaScript, images and font files.

🪣 Step 2 – Created Amazon S3 Bucket

I created an Amazon S3 bucket to store the website files.

The bucket contains:

HTML files
CSS files
JavaScript files
Images
Fonts
S3 Bucket Objects

The following screenshot shows the website files uploaded to Amazon S3.

🔐 Step 3 – Configured CloudFront Access

I created an Amazon CloudFront distribution with the S3 bucket configured as the origin.

The CloudFront distribution is responsible for delivering the website content to users.

Initially, accessing the CloudFront distribution returned an Access Denied response because CloudFront did not yet have the required permission to retrieve objects from the private S3 bucket.

Initial Access Denied

This helped me understand that the issue was related to the permissions between CloudFront and S3.

🔑 Step 4 – Configured Origin Access Control

I configured Origin Access Control (OAC) for the CloudFront distribution.

OAC allows CloudFront to securely access objects stored in the S3 bucket.

Instead of making the S3 bucket publicly accessible, CloudFront is granted permission to retrieve the required objects.

S3 Bucket Policy with CloudFront OAC

The bucket policy allows the CloudFront service principal to perform:

s3:GetObject

on the objects required by the CloudFront distribution.

🌐 Step 5 – CloudFront Distribution Configuration

The CloudFront distribution was configured with the S3 bucket as its origin.

The distribution provides:

Global content delivery
HTTPS access
Edge caching
Secure S3 origin access
Improved website performance
CloudFront Distribution Settings

🖥️ Step 6 – Tested the Website

After configuring S3 and CloudFront, I tested the website through the CloudFront distribution domain.

The website successfully loaded through CloudFront.

CloudFront Distribution:

https://d200lls7xh3st.cloudfront.net

Note: The CloudFront domain is included as a reference to the deployment used during this project.

📸 Website Screenshots
🏠 Home Page

The home page contains the main space-themed landing page with the website navigation and featured content.

🌍 About Page

The About page contains information about the website and its content.

📩 Contact Page

The Contact page contains the website contact form.

📝 Blog Page

The Blog page contains featured and recent posts.

🧪 Testing Performed

The following tests were performed during the deployment:

S3 Testing
Uploaded website files to S3
Verified HTML files
Verified images
Verified CSS files
Verified JavaScript files
Verified font files
CloudFront Testing
Created CloudFront distribution
Configured S3 as the origin
Configured Origin Access Control
Updated S3 bucket policy
Tested CloudFront URL
Verified website pages
Verified images and CSS loading
⚠️ Troubleshooting
Access Denied from CloudFront

During the implementation, the CloudFront URL initially returned:

AccessDenied
Cause

CloudFront did not have the required permission to retrieve objects from the S3 bucket.

Resolution

I configured:

CloudFront
     │
     │ Origin Access Control
     ▼
Amazon S3
     │
     │ Bucket Policy
     ▼
Allow s3:GetObject

After configuring the appropriate S3 bucket policy for the CloudFront distribution, the website became accessible through CloudFront.

This troubleshooting step helped me understand the relationship between:

S3 bucket permissions
CloudFront
Origin Access Control
IAM-style resource policies
🔒 Security Configuration

The project uses CloudFront Origin Access Control instead of relying on direct public access to the S3 bucket.

The intended architecture is:

Internet
   │
   ▼
CloudFront
   │
   │ Authorized Origin Access
   ▼
S3 Bucket

This allows CloudFront to retrieve website content while keeping the S3 origin controlled by an S3 bucket policy.

📚 What I Learned

Through this project, I gained practical experience with:

Amazon S3
Creating S3 buckets
Uploading objects
Organizing website files
Understanding S3 object access
Understanding bucket policies
Amazon CloudFront
Creating CloudFront distributions
Configuring S3 origins
Understanding CDN architecture
Testing CloudFront distributions
Understanding caching and content delivery
Origin Access Control
Creating OAC
Connecting CloudFront with S3
Understanding CloudFront-to-S3 authorization
Configuring S3 bucket policies
Troubleshooting
Diagnosing CloudFront Access Denied errors
Checking S3 permissions
Validating CloudFront configuration
Testing static website resources
💡 Key AWS Concepts Demonstrated
Amazon S3
   │
   │ Object Storage
   ▼
Website Files
   │
   ▼
CloudFront Origin
   │
   │ OAC
   ▼
CloudFront Distribution
   │
   ▼
End Users

This project demonstrates a common AWS pattern for hosting and distributing static content.

🔮 Future Improvements

The project can be extended with:

Custom domain using Route 53
HTTPS certificate using AWS Certificate Manager
Route 53 DNS configuration
CloudFront custom domain
CloudFront cache invalidations
CI/CD deployment using GitHub Actions
Automated S3 deployment
AWS WAF integration
CloudWatch monitoring
Access logging
Infrastructure as Code using Terraform or AWS CloudFormation
🎯 Project Outcome

Successfully deployed a multi-page static website using:

Amazon S3
      +
Amazon CloudFront
      +
Origin Access Control
      +
S3 Bucket Policy

The project demonstrates practical experience with AWS object storage, CDN delivery, access control and troubleshooting.

👨‍💻 Author

Abhinay Kumar

AWS / Cloud Learning Projects

GitHub:

https://github.com/abhinay17644

⭐ Project Highlights
✅ Static website hosted on Amazon S3
✅ Amazon CloudFront distribution
✅ CloudFront Origin Access Control
✅ S3 bucket policy configuration
✅ HTTPS content delivery
✅ Multi-page HTML website
✅ CSS, JavaScript, images and fonts
✅ CloudFront Access Denied troubleshooting
✅ End-to-end AWS deployment
