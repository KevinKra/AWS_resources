# Creating an AWS Serverless Application w/ React

### Benefits of Serverless Architecture

- Don't need to install, manage, and secure an OS
- Designed to scale
- Use existing cloud technologies
- Are often less expensive than alternatives

### Technologies

#### General

- ReactJS
- HTML
- CSS
- Github

#### AWS

- Route53
- CloudFront
- IAM
- S3
- CodeBuild
- CodePipeline
- Lambda
- SNS

### Design Overview

#### Application Perspective

1. User visits website managed by **Route53**
2. **Route53** directs request to **CloudFront** which hosts and distributes app around the world
3. **CloudFront** gets app content from **S3** bucket

#### Developer Perspective

1. Develop app on local machine
2. Push changes to Github
3. When code is pushed to Github, **CodeBuild** gets it from Github, runs tests, then builds and packages code
4. **CodePipeline** will coordinate resources to build and deploy code to an **S3** bucket
5. **CodePipeline** then runs a **Lambda** function which deploys the code to the app's **S3** bucket
6. **SNS** informs you that the app has been deployed

---

## Setting up S3, Route53, CloudFront

- Use Route53 to purchase a domain
- Use S3 to set up a bucket to host website static resources
- Configuring Route53 and S3 to use purchased domain
- Acquire a HTTPS certification
- Setup CloudFront to distribute website and server certificate

### S3 Important Steps

- S3 Bucket will need to public
  > S3 > Permissions > Block Public Access > Off
- S3 Bucket will need Static Website Hosting enabled
  > S3 > Properties > Static Website Hosting > Use this bucket to host a website
- In order to use your domain you need to visit Route53
  > Route53 > Hosted zones > your domain > Create Record Set > Enter name (match S3 Bucket name) > Alias Yes > Select your bucket > click Yes

### Acquiring HTTPS certification

> This setup is tailored for those who created an domain through Route53

1. Acquire Certification
   > Services > Certificate Manager > Getting Started > enter \*.yourdomain > DNS Validation > Create Record in Route53
2. Use Certificate. Certification needs to be stored and served with our portfolio. See CloudFront.

### CloudFront

> Services > CloudFront > Create Distribution > Web

- Fill in Form
  - Origin Domain Name: Your Bucket
  - Viewer Protocol Policy: Redirect HTTP to HTTPS
  - Default TTL: 60 (seconds). Return back to 86400 later after app is completed
  - Alternate Domain Names: your website URL
  - Custom SSL Certificate: Select your cert.
  - Default Root Object: index.html

#### Resources:

https://docs.aws.amazon.com/acm/latest/userguide/gs-acm-validate-dns.html#dns-add-cname
https://medium.com/serverlessguru/deploy-reactjs-app-with-s3-static-hosting-f640cb49d7e6
https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html
https://github.com/backspace-academy/aws-nodejs-sample-codebuild/blob/master/buildspec.yml

> Provided better context for integration with create react app.
