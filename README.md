# AWS S3 + CloudFront Static Website Project

## Project Overview

This project demonstrates the deployment of a static website using Amazon S3 and Amazon CloudFront.

The website files, including HTML, CSS, JavaScript, fonts, and images, are stored in an Amazon S3 bucket. Amazon CloudFront is used as the Content Delivery Network (CDN) to distribute the website content globally.

CloudFront is configured to securely access the private S3 bucket using Origin Access Control (OAC). This allows the S3 bucket to remain private while CloudFront serves the website to users.

The implementation covers S3 bucket creation, static website file upload, CloudFront distribution configuration, Origin Access Control, S3 bucket policy configuration, website deployment, and application verification.

---

## Project Objectives

The main objectives of this project were:

- Create an Amazon S3 bucket for static website hosting.
- Upload website files to Amazon S3.
- Organize website assets such as CSS, JavaScript, images, and fonts.
- Configure Amazon CloudFront as a CDN.
- Configure CloudFront to use the S3 bucket as the origin.
- Configure Origin Access Control (OAC).
- Secure the S3 bucket using a bucket policy.
- Prevent direct public access to the S3 bucket.
- Configure CloudFront to serve the website.
- Verify the website through the CloudFront distribution.
- Verify multiple website pages through CloudFront.

---

# Project Architecture

The deployment consists of the following AWS components:

- Amazon S3 – Stores the static website files.
- Amazon CloudFront – Distributes website content globally.
- Origin Access Control (OAC) – Allows CloudFront to securely access the S3 bucket.
- S3 Bucket Policy – Grants CloudFront permission to access the bucket.

### Architecture Flow

Internet

↓

Amazon CloudFront

↓

Origin Access Control (OAC)

↓

Amazon S3 Bucket

↓

Static Website Files

The user accesses the website through the CloudFront distribution. CloudFront retrieves the required files from the S3 bucket and delivers them to the user.

---

# Step 1: Create Amazon S3 Bucket

An Amazon S3 bucket was created to store the static website files.

The S3 bucket contains the HTML pages along with the CSS, JavaScript, image, and font files required by the website.

The website files were uploaded to the S3 bucket while maintaining the required directory structure.

### Website Files

The project contains:

- HTML files
- CSS files
- JavaScript files
- Images
- Fonts

### Screenshot

![S3 Bucket Objects](./screenshots/01-s3-bucket-objects.png)

The screenshot shows the website objects stored inside the Amazon S3 bucket.

---

# Step 2: Verify CloudFront Access

Amazon CloudFront was configured to distribute the content stored in the S3 bucket.

During the initial configuration, access to the S3 origin was tested.

The initial access-denied response demonstrated that CloudFront required the appropriate permissions to access the private S3 bucket.

### Screenshot

![CloudFront Access Denied](./screenshots/02-cloudfront-access-denied.png)

This helped verify that the S3 bucket was not simply exposed for unrestricted public access.

---

# Step 3: Configure Origin Access Control

Origin Access Control (OAC) was configured for the CloudFront distribution.

OAC allows CloudFront to securely access objects stored in the S3 bucket.

Instead of making the S3 bucket publicly accessible, CloudFront is given permission to retrieve the required objects.

### Security Flow

User

↓

CloudFront

↓

OAC

↓

S3 Bucket

### Screenshot

![S3 Bucket Policy and OAC](./screenshots/03-s3-bucket-policy-oac.png)

The screenshot shows the S3 bucket policy and CloudFront Origin Access Control configuration.

---

# Step 4: Configure CloudFront Distribution

A CloudFront distribution was configured with the S3 bucket as its origin.

The distribution provides a CloudFront domain name that users can use to access the static website.

The CloudFront distribution was configured to retrieve website content from the S3 origin.

### CloudFront Configuration

The configuration includes:

- S3 origin
- CloudFront distribution
- Origin Access Control
- Default root object
- Distribution domain name
- HTTPS access

### Screenshot

![CloudFront Distribution Settings](./screenshots/04-cloudfront-distribution-settings.png)

The screenshot shows the CloudFront distribution configuration.

---

# Step 5: Access the Website Through CloudFront

After configuring the CloudFront distribution and S3 permissions, the website was accessed using the CloudFront distribution domain.

CloudFront retrieved the website files from the S3 bucket and delivered them to the browser.

This confirmed that the S3 origin and CloudFront distribution were communicating successfully.

### Screenshot

![CloudFront Home Page](./screenshots/05-home-page.png)

The screenshot shows the website home page successfully loading through CloudFront.

---

# Step 6: Verify About Page

The About page was accessed through the CloudFront distribution.

This verified that CloudFront was able to retrieve the required HTML and supporting static assets from the S3 origin.

### Screenshot

![About Page](./screenshots/06-about-page.png)

The screenshot shows the About page successfully loading through CloudFront.

---

# Step 7: Verify Contact Page

The Contact page was accessed through the CloudFront distribution.

This provided another verification that the static website pages were correctly stored in S3 and distributed through CloudFront.

### Screenshot

![Contact Page](./screenshots/07-contact-page.png)

The screenshot shows the Contact page successfully loading through CloudFront.

---

# Step 8: Verify Blog Page

The Blog page was accessed through the CloudFront distribution.

This confirmed that multiple pages of the static website were available through the CloudFront distribution.

### Screenshot

![Blog Page](./screenshots/08-blog-page.png)

The screenshot shows the Blog page successfully loading through CloudFront.

---

# S3 Bucket Configuration

The Amazon S3 bucket is used as the origin for the CloudFront distribution.

The bucket contains the static website files required by the application.

The website structure includes:

```text
AWS-S3-CLOUDFRONT-STATIC-WEBSITE/
│
├── css/
├── fonts/
├── images/
├── js/
├── screenshots/
│
├── index.html
├── about.html
├── blog.html
├── contact.html
├── projects.html
├── proj1.html
└── singlepost.html

The screenshots directory is maintained in the GitHub repository for project documentation and does not need to be uploaded to the S3 website unless it is required by the actual website.

CloudFront Configuration

Amazon CloudFront acts as the CDN layer between users and the S3 bucket.

The CloudFront distribution provides:

Global content delivery
HTTPS access
Caching
S3 origin integration
Origin Access Control
Secure access to the S3 bucket

The CloudFront domain is used to access the deployed website.

Security Configuration

The S3 bucket is protected by allowing CloudFront to access the required objects through Origin Access Control.

The architecture avoids relying on unrestricted public access to the S3 bucket.

Security Flow
Internet User
      |
      v
Amazon CloudFront
      |
      v
Origin Access Control
      |
      v
Amazon S3

This provides a more secure architecture compared with directly exposing the S3 bucket to the internet.

Website Verification

The following components were verified:

S3 bucket was created successfully.
Website files were uploaded successfully.
HTML pages were accessible.
CSS files were available.
JavaScript files were available.
Images and fonts were stored in the required directories.
CloudFront distribution was created.
S3 was configured as the CloudFront origin.
Origin Access Control was configured.
S3 bucket policy was configured.
CloudFront successfully retrieved website content.
Home page was accessible.
About page was accessible.
Contact page was accessible.
Blog page was accessible.
Key Learning Outcomes

This project provided practical experience with:

Amazon S3
Amazon CloudFront
Origin Access Control
S3 Bucket Policies
Static Website Hosting
CDN Architecture
HTTPS
CloudFront caching
AWS security concepts
AWS content delivery
Static website deployment
GitHub project documentation

The project also provided practical understanding of how Amazon S3 and CloudFront can be combined to deploy and distribute static websites.

Project Benefits

Using Amazon S3 together with CloudFront provides a scalable architecture for static websites.

Amazon S3 provides durable storage for website files, while CloudFront provides content delivery and caching closer to end users.

The use of Origin Access Control also allows the S3 origin to remain protected while CloudFront serves the website.

Future Improvements

The current deployment can be enhanced further by introducing the following AWS services and features:

Amazon Route 53 for DNS management
Custom domain name
HTTPS using AWS Certificate Manager
CloudFront cache optimization
CloudFront response headers policies
AWS WAF for web application protection
CloudWatch monitoring
CloudFront access logs
S3 versioning
S3 lifecycle policies
CI/CD deployment using GitHub Actions
Infrastructure as Code using AWS CloudFormation or Terraform

A future version of this project can use a custom domain such as:

www.example.com

with Route 53 pointing the domain to the CloudFront distribution.

Project Architecture Diagram
                    Internet Users
                          |
                          v
                 +------------------+
                 | Amazon CloudFront|
                 |      CDN         |
                 +------------------+
                          |
                          v
                +-------------------+
                | Origin Access     |
                | Control (OAC)     |
                +-------------------+
                          |
                          v
                 +------------------+
                 |   Amazon S3      |
                 |   Static Website  |
                 +------------------+
                          |
              +-----------+-----------+
              |           |           |
              v           v           v
           HTML/CSS    JavaScript   Images
Repository Structure
AWS-S3-CLOUDFRONT-STATIC-WEBSITE/
│
├── css/
├── fonts/
├── images/
├── js/
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
├── index.html
├── about.html
├── blog.html
├── contact.html
├── proj1.html
├── projects.html
├── singlepost.html
└── README.md
Conclusion

This project demonstrates the deployment of a static website using Amazon S3 and Amazon CloudFront.

Amazon S3 provides storage for the website files, while Amazon CloudFront provides global content delivery and caching.

Origin Access Control was configured to allow CloudFront to securely retrieve objects from the S3 bucket without requiring unrestricted public access.

The implementation covered S3 bucket configuration, website file upload, CloudFront distribution creation, Origin Access Control, S3 bucket policy configuration, and website verification.

The project provides practical experience with AWS static website hosting, CDN architecture, security configuration, and cloud-based content delivery.
