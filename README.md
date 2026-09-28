# AWS S3 + CloudFront Static Website

## 📌 Project Overview

This project demonstrates how to deploy a **static website on Amazon S3** and distribute it globally using **Amazon CloudFront**.

The website contains multiple HTML pages along with CSS, JavaScript, images, and web fonts. The website files are stored in an Amazon S3 bucket, while Amazon CloudFront is configured as the CDN layer to provide fast and secure access to the website.

This project also includes hands-on configuration of **CloudFront Origin Access Control (OAC)** to securely connect CloudFront with the S3 bucket.

---

# 🏗️ Architecture

```text
                         Users
                           |
                           |
                           v
                +----------------------+
                |   Amazon CloudFront  |
                |       CDN            |
                |      HTTPS            |
                +----------------------+
                           |
                           |
                    Origin Access
                      Control
                           |
                           v
                +----------------------+
                |      Amazon S3       |
                |   Static Website     |
                +----------------------+
                           |
              +------------+-------------+
              |            |             |
              v            v             v
           HTML          CSS/JS      Images/Fonts
Architecture Flow
User sends a request to the CloudFront distribution.
CloudFront receives the request.
CloudFront checks its cache for the requested content.
If the content is not available in cache, CloudFront requests it from Amazon S3.
CloudFront uses Origin Access Control (OAC) to access the S3 bucket.
S3 returns the requested website files.
CloudFront delivers the content to the user over HTTPS.
☁️ AWS Services Used
AWS Service	Purpose
Amazon S3	Stores static website files
Amazon CloudFront	CDN and global content delivery
CloudFront OAC	Secure access between CloudFront and S3
AWS IAM	Access and permission management
🌐 Project Website
CloudFront Distribution
https://d200lls7xh3st.cloudfront.net/

The website is accessed through the CloudFront distribution instead of directly accessing the S3 bucket.

📂 Project Structure
AWS-S3-CLOUDFRONT-STATIC-WEBSITE/
│
├── index.html
├── about.html
├── blog.html
├── contact.html
├── proj1.html
├── projects.html
├── singlepost.html
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
│   ├── bg-transparent1.png
│   ├── curious-rover.jpg
│   ├── earth-satellite.jpg
│   ├── finding-planet.jpg
│   ├── galaxy.jpg
│   ├── icons.png
│   ├── logo.png
│   ├── mars-rover.jpg
│   ├── martianrover-journey.jpg
│   ├── moon-landing.jpg
│   ├── moon-satellite.jpg
│   ├── new-satellitedish.jpg
│   ├── project-image1.jpg
│   ├── project-image2.jpg
│   ├── project-image3.jpg
│   ├── project-image4.jpg
│   ├── satellite-dish.jpg
│   ├── satellite.png
│   ├── space-shuttle.png
│   ├── space-station.jpg
│   │
│   └── mobile/
│       ├── mobile-close.png
│       ├── mobile-collapse.png
│       ├── mobile-expand.png
│       └── mobile-menu.png
│
└── js/
    └── mobile.js
🚀 Implementation
Step 1: Prepare the Static Website

The static website was prepared using:

HTML
CSS
JavaScript
Images
Web fonts

The main website entry point is:

index.html

Additional pages include:

about.html
blog.html
contact.html
proj1.html
projects.html
singlepost.html

The website assets were organized into separate directories:

css/
js/
images/
fonts/

Maintaining the correct directory structure is important because the HTML files reference these assets using relative paths.

For example:

<link rel="stylesheet" href="css/style.css">
Step 2: Create Amazon S3 Bucket

An Amazon S3 bucket was created to store the static website files.

The website files were uploaded into the S3 bucket.

The bucket structure looks like:

S3 Bucket
│
├── index.html
├── about.html
├── blog.html
├── contact.html
├── projects.html
│
├── css/
├── js/
├── images/
└── fonts/
S3 Configuration

The bucket was configured to store the static website content.

The index.html file was placed in the root of the bucket.

Step 3: Upload Website Files

The complete website files were uploaded to the S3 bucket.

The following files and folders were uploaded:

index.html
about.html
blog.html
contact.html
proj1.html
projects.html
singlepost.html

css/
js/
images/
fonts/

After uploading, the S3 bucket contained the complete website structure.

Step 4: Configure CloudFront

An Amazon CloudFront distribution was created.

The S3 bucket was configured as the CloudFront origin.

CloudFront Configuration
Origin:
Amazon S3 Bucket

Default Root Object:
index.html

Protocol:
HTTPS

The CloudFront distribution provides the public URL:

https://d200lls7xh3st.cloudfront.net/
Step 5: Configure Origin Access Control (OAC)

CloudFront Origin Access Control was configured to securely access the S3 bucket.

The request flow is:

User
  |
  v
CloudFront
  |
  | OAC
  |
  v
S3 Bucket

OAC allows CloudFront to retrieve objects from the S3 bucket without requiring the S3 objects to be publicly accessible.

The S3 bucket policy was configured to allow the CloudFront distribution to retrieve objects.

Step 6: Configure Default Root Object

The CloudFront distribution was configured with:

Default Root Object:
index.html

This allows the user to open:

https://d200lls7xh3st.cloudfront.net/

instead of manually entering:

https://d200lls7xh3st.cloudfront.net/index.html

CloudFront automatically serves:

index.html

when the root URL is requested.

Step 7: Test the Website

The CloudFront URL was tested after completing the configuration.

Website URL
https://d200lls7xh3st.cloudfront.net/

The following components were tested:

Homepage
HTML pages
CSS
JavaScript
Images
Fonts
Website navigation
🔧 Troubleshooting

During the deployment, some issues were encountered and resolved.

Issue 1: AccessDenied Error

Initially, accessing the website resulted in an:

AccessDenied

error.

Cause

CloudFront did not have the required permission to retrieve the objects from the S3 bucket.

Resolution

The CloudFront origin and Origin Access Control configuration were checked.

The S3 bucket policy was configured to allow CloudFront to retrieve objects.

The request flow became:

CloudFront
     |
     | OAC
     v
S3 Bucket
     |
     v
Website Files
Issue 2: index.html Not Loading

The CloudFront URL was not automatically displaying the homepage.

Cause

The CloudFront distribution did not have the correct default root object configured.

Resolution

The CloudFront distribution was configured with:

Default Root Object:
index.html

After the configuration, opening:

https://d200lls7xh3st.cloudfront.net/

loads:

index.html

automatically.

Issue 3: CSS Not Loading

The website was initially displayed without proper styling.

Cause

The CSS file was not being retrieved correctly through the CloudFront/S3 configuration.

The website uses:

css/style.css

and:

css/mobile.css
Resolution

The S3 object structure was checked to ensure the CSS files existed in the correct location.

The correct structure is:

S3 Bucket
│
├── index.html
│
└── css/
    ├── style.css
    └── mobile.css

The HTML references the stylesheet using:

<link rel="stylesheet" href="css/style.css">
Issue 4: CloudFront Cache

After making configuration or website changes, CloudFront could continue serving previously cached content.

Resolution

A CloudFront invalidation was created using:

/*

This forces CloudFront to request updated content from the origin when required.

🔄 Complete Request Flow

The complete website request flow is:

                     User
                       |
                       |
                       v
              CloudFront URL
                       |
                       v
              CloudFront Edge
                       |
                       |
                  Cache Check
                  /          \
                Hit          Miss
                |              |
                |              v
                |       Origin Request
                |              |
                |              v
                |         OAC Authentication
                |              |
                |              v
                |          S3 Bucket
                |              |
                |              v
                |        Website Files
                |              |
                +--------------+
                       |
                       v
                    User
📸 Screenshots

Screenshots can be added to document the implementation.

1. S3 Bucket

Screenshot showing the uploaded website files.

screenshots/s3-bucket.png
2. S3 Website Files

Screenshot showing:

index.html
css/
images/
fonts/
js/
screenshots/s3-files.png
3. CloudFront Distribution

Screenshot showing the CloudFront distribution.

screenshots/cloudfront-distribution.png
4. CloudFront Origin

Screenshot showing the S3 origin and OAC configuration.

screenshots/cloudfront-origin.png
5. CloudFront Default Root Object

Screenshot showing:

index.html
screenshots/default-root-object.png
6. Working Website

Screenshot showing the website successfully loading through CloudFront.

screenshots/website.png
🔐 Security Considerations

The project uses CloudFront as the public delivery layer and S3 as the origin.

Security practices used in this project include:

CloudFront Origin Access Control
S3 bucket policy
HTTPS through CloudFront
Controlled access between CloudFront and S3
No AWS credentials stored in the GitHub repository

AWS access keys, secret keys, passwords, and other sensitive credentials should never be committed to GitHub.

📚 Key Learnings

Through this project, I gained hands-on experience with:

Amazon S3
Creating an S3 bucket
Uploading static website files
Organizing website objects
Understanding S3 permissions
Understanding S3 bucket policies
Amazon CloudFront
Creating a CloudFront distribution
Configuring an S3 origin
Configuring the default root object
Understanding CDN caching
Creating cache invalidations
Accessing a website through CloudFront
Origin Access Control
Understanding CloudFront OAC
Connecting CloudFront securely to S3
Configuring S3 permissions for CloudFront
Troubleshooting
Troubleshooting AccessDenied
Troubleshooting missing index.html
Troubleshooting CSS loading issues
Troubleshooting CloudFront cached content
Verifying website asset paths
💡 Future Improvements

The project can be extended with:

Custom domain using Amazon Route 53
SSL certificate using AWS Certificate Manager
AWS WAF
CloudWatch monitoring
CloudFront access logging
GitHub Actions CI/CD
Automatic deployment from GitHub to S3
Infrastructure as Code using Terraform
Infrastructure as Code using AWS CloudFormation
Future Architecture
Developer
    |
    v
GitHub
    |
    | CI/CD
    v
Amazon S3
    |
    v
CloudFront
    |
    v
Route 53
    |
    v
Custom Domain
    |
    v
Users
🛠️ Technologies Used
Frontend
HTML5
CSS3
JavaScript
AWS
Amazon S3
Amazon CloudFront
CloudFront Origin Access Control
AWS IAM
Version Control
Git
GitHub
📊 Project Summary
Component	Implementation
Website Type	Static Website
Frontend	HTML, CSS, JavaScript
Storage	Amazon S3
CDN	Amazon CloudFront
Origin Security	CloudFront OAC
Default Page	index.html
Protocol	HTTPS
Version Control	GitHub
Deployment	AWS S3 + CloudFront
🎯 Conclusion

This project demonstrates a complete deployment of a static website using Amazon S3 and Amazon CloudFront.

The project started with a static HTML/CSS/JavaScript website and was deployed to Amazon S3. CloudFront was then configured as the CDN layer with Origin Access Control to securely retrieve content from S3.

During the implementation, practical troubleshooting was performed for:

S3 AccessDenied
CloudFront origin configuration
Default root object
Missing CSS
Static asset paths
CloudFront caching

The final solution provides a simple, scalable, and secure foundation for hosting a static website on AWS.

👨‍💻 Author

Abhinay Kumar

GitHub:
https://github.com/abhinay17644

📌 Project Status

Completed ✅

Amazon S3
     |
     | Secure Origin
     v
CloudFront OAC
     |
     v
HTTPS Website
     |
     v
Users

This version is much closer to the **project-documentation style** we used for your WordPress/LAMP project: it documents **your actual implementation and troubleshooting**, rather than just describing what S3 and CloudFront are. 

### What I recommend you do now

Since your GitHub repository already has the website files, go to:

**Add file → Create new file**

Name:

```text
README.md
