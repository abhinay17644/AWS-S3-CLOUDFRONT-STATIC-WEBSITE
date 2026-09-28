# AWS S3 + CloudFront Static Website

A static website hosted on **Amazon S3** and delivered globally using **Amazon CloudFront**. This project demonstrates how to deploy a static HTML/CSS/JavaScript website to AWS and use CloudFront as a content delivery layer.

## Project Overview

In this project, a static website was deployed using Amazon S3 and Amazon CloudFront.

The website files, including HTML, CSS, JavaScript, images, and fonts, are stored in an Amazon S3 bucket. Amazon CloudFront is configured in front of the S3 bucket to provide fast content delivery and HTTPS access.

### AWS Architecture

```text
                         Internet
                            |
                            |
                            v
                  +-------------------+
                  |   Amazon CloudFront |
                  |   CDN Distribution |
                  +-------------------+
                            |
                            | Origin Access
                            | Control (OAC)
                            v
                  +-------------------+
                  |    Amazon S3       |
                  |   Static Website   |
                  +-------------------+
                            |
             +--------------+--------------+
             |              |              |
             v              v              v
        index.html       CSS/JS        Images/Fonts
AWS Services Used
AWS Service	Purpose
Amazon S3	Stores the static website files
Amazon CloudFront	Delivers website content globally
CloudFront OAC	Provides secure access from CloudFront to S3
AWS IAM	Controls access between AWS services
Website Components

The website contains:

HTML pages
CSS stylesheets
JavaScript
Images
Web fonts
Responsive/mobile assets
Project Structure
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
│   └── mobile/
│       ├── mobile-close.png
│       ├── mobile-collapse.png
│       ├── mobile-expand.png
│       └── mobile-menu.png
│
└── js/
    └── mobile.js
Implementation
1. Prepare the Static Website

The website was prepared using static HTML, CSS, and JavaScript files.

The main entry point of the website is:

index.html

Additional pages include:

about.html
blog.html
contact.html
proj1.html
projects.html
singlepost.html

The required CSS, JavaScript, images, and font files were organized into separate directories.

2. Create an Amazon S3 Bucket

An Amazon S3 bucket was created to store the static website files.

The website files were uploaded to the root of the S3 bucket.

The bucket contains:

index.html
css/
fonts/
images/
js/
Main Website File
index.html

The index.html file is used as the default entry point for the website.

3. Upload Website Files to S3

The complete website structure was uploaded to the S3 bucket.

Example:

S3 Bucket
│
├── index.html
├── about.html
├── blog.html
├── contact.html
├── projects.html
│
├── css/
├── fonts/
├── images/
└── js/

Maintaining the correct directory structure is important because the HTML files reference CSS, JavaScript, images, and fonts using relative paths.

For example:

<link rel="stylesheet" href="css/style.css">

Therefore, the following file must exist:

css/style.css
4. Configure Amazon CloudFront

An Amazon CloudFront distribution was created to deliver the website through a CDN.

CloudFront uses the S3 bucket as its origin.

CloudFront Configuration

The main configuration includes:

Origin:
Amazon S3 bucket

Default Root Object:
index.html

Protocol:
HTTPS

Distribution:
CloudFront

The CloudFront distribution provides a public HTTPS endpoint for accessing the website.

5. Configure Origin Access Control

CloudFront Origin Access Control (OAC) was configured to allow CloudFront to securely retrieve objects from the S3 bucket.

The architecture is:

User
 |
 v
CloudFront
 |
 | OAC
 v
S3 Bucket

This allows the S3 bucket to be accessed through CloudFront while controlling direct access to the S3 objects.

The S3 bucket policy allows the CloudFront distribution to retrieve the required website objects.

6. Configure Default Root Object

The CloudFront distribution was configured with:

Default Root Object:
index.html

This allows users to access:

https://d200lls7xh3st.cloudfront.net/

and CloudFront automatically serves:

index.html

without requiring the user to manually enter:

/index.html
7. CloudFront Cache Invalidation

CloudFront caches website content at edge locations.

When website files are updated, CloudFront may continue serving an older cached version.

A cache invalidation can be created using:

/*

This requests CloudFront to refresh the cached content.

Cache invalidation is useful after updating:

HTML files
CSS files
JavaScript
Images
Other website assets
Deployment Architecture

The final deployment follows this architecture:

                         Users
                           |
                           v
                +---------------------+
                |   Amazon CloudFront |
                |       HTTPS / CDN   |
                +---------------------+
                           |
                           | OAC
                           v
                +---------------------+
                |      Amazon S3      |
                |    Website Bucket   |
                +---------------------+
                           |
          +----------------+----------------+
          |                |                |
          v                v                v
       HTML Files       CSS / JS       Images / Fonts
CloudFront Distribution

The deployed website is available through the CloudFront distribution:

CloudFront URL:

https://d200lls7xh3st.cloudfront.net/

Note: The CloudFront URL may change if the distribution is replaced or a different distribution is created.

Testing

The website was tested through the CloudFront distribution.

The following areas were verified:

Website homepage loading
index.html delivery
CSS loading
JavaScript loading
Images loading
Fonts loading
Navigation between HTML pages
CloudFront HTTPS access
Website Pages

The project contains the following pages:

Page	File
Home	index.html
About	about.html
Blog	blog.html
Contact	contact.html
Project	proj1.html
Projects	projects.html
Single Post	singlepost.html
Troubleshooting

During deployment, several common issues were considered.

CSS Not Loading

If the website loads without styling, verify that:

css/style.css

exists in the correct location and that index.html references it correctly.

Example:

<link rel="stylesheet" href="css/style.css">
Index Page Not Loading

CloudFront should have:

Default Root Object:
index.html

The index.html file should also exist in the root of the S3 bucket.

AccessDenied Error

An AccessDenied error can occur when CloudFront does not have permission to retrieve objects from the S3 bucket.

The following areas should be checked:

CloudFront Origin
Origin Access Control
S3 bucket policy
Object permissions
CloudFront distribution configuration
Old Website Version Appearing

If an older version of the website is displayed after uploading updated files, create a CloudFront invalidation:

/*

Then wait for the invalidation to complete before testing again.

Security Considerations

The project uses CloudFront as the public access layer and S3 as the origin.

Important security practices include:

Avoid exposing AWS access keys in the repository.
Do not upload secret keys or credentials to GitHub.
Use CloudFront Origin Access Control when appropriate.
Keep sensitive configuration outside the website source code.
Use HTTPS through CloudFront.
Follow the principle of least privilege for AWS permissions.
GitHub Repository

The complete website source code is available in this repository:

AWS-S3-CLOUDFRONT-STATIC-WEBSITE

The repository contains the HTML, CSS, JavaScript, images, and font files required for the static website.

Skills Demonstrated

This project demonstrates practical experience with:

Amazon S3
Amazon CloudFront
CloudFront Origin Access Control
Static website hosting
CDN configuration
AWS IAM permissions
S3 bucket policies
HTTPS delivery
Cache invalidation
HTML
CSS
JavaScript
Website deployment
AWS troubleshooting
Key Learnings

Through this project, I gained practical experience in:

Hosting static website files using Amazon S3.
Configuring Amazon CloudFront as a CDN.
Connecting CloudFront to an S3 origin.
Understanding Origin Access Control.
Configuring the CloudFront default root object.
Troubleshooting S3 AccessDenied errors.
Troubleshooting missing CSS and static assets.
Understanding CloudFront caching and invalidation.
Maintaining website directory structures.
Deploying a website using AWS services.
Future Improvements

The project can be further improved by implementing:

Custom domain using Amazon Route 53
SSL/TLS certificate using AWS Certificate Manager
HTTPS with a custom domain
AWS WAF for additional web security
CloudWatch monitoring
CloudFront access logging
Automated deployment using GitHub Actions
Infrastructure as Code using AWS CloudFormation or Terraform
Separate development and production environments
CI/CD pipeline for automatic website deployment
Conclusion

This project demonstrates the deployment of a static website using Amazon S3 and Amazon CloudFront.

Amazon S3 provides reliable object storage for the website files, while CloudFront provides CDN-based content delivery and HTTPS access.

The project also provided hands-on experience with AWS permissions, Origin Access Control, CloudFront configuration, cache invalidation, and troubleshooting static website deployment issues.

The final architecture provides a foundation that can be extended with a custom domain, SSL/TLS, monitoring, security controls, and automated CI/CD deployment.

Author

Abhinay

GitHub: abhinay17644

Project Status

Completed

Static website successfully deployed using:

Amazon S3
     +
Amazon CloudFront
     +
Origin Access Control

### One small change before you paste it

At the bottom, I included a GitHub Markdown link for your profile. Since you're putting this **inside GitHub's README**, that's perfectly fine.

For your **project screenshots**, I recommend adding them later under a section like:

```markdown
# Screenshots

## S3 Bucket

![S3 Bucket](screenshots/s3-bucket.png)

## CloudFront Distribution

![CloudFront](screenshots/cloudfront.png)

## Website

![Website](screenshots/website.png)
