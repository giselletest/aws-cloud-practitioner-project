# S3 Static Website Hosting Setup Guide

## Overview
This guide documents the process of setting up static website hosting using Amazon S3. This implementation demonstrates key concepts from the AWS Cloud Practitioner certification while creating a practical, working example.

## Prerequisites
- AWS Account
- AWS CLI configured
- Basic understanding of HTML and S3 concepts

## Step-by-Step Setup Process

### 1. Create S3 Bucket
1. Log into AWS Console
2. Navigate to S3 service
3. Click "Create bucket"
4. Configure bucket:
   - Name: `[your-unique-bucket-name]`
   - Region: Choose your preferred region
   - Uncheck "Block all public access"
   - Acknowledge the warning about public access
   - Keep other settings as default
   - Click "Create bucket"

### 2. Enable Static Website Hosting
1. Select your newly created bucket
2. Go to "Properties" tab
3. Scroll to "Static website hosting"
4. Click "Edit"
5. Select "Enable"
6. Set "Index document" to `index.html`
7. Save changes

### 3. Configure Bucket Policy
1. Go to "Permissions" tab
2. Click "Bucket Policy"
3. Add the following policy (replace `[your-bucket-name]`):
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::[your-bucket-name]/*"
        }
    ]
}
```

### 4. Upload Website Files
1. Go to "Objects" tab
2. Click "Upload"
3. Upload your `index.html` file
4. Click "Upload"

### 5. Access Your Website
- Find your website URL under Properties > Static website hosting
- URL format: `http://[bucket-name].s3-website-[region].amazonaws.com`

## Security Considerations
- The bucket is publicly accessible (required for website hosting)
- Only upload content meant to be public
- Consider using CloudFront for added security and performance

## Cost Considerations
- S3 costs are based on storage, requests, and data transfer
- Static website hosting has no additional cost
- Monitor usage through AWS Cost Explorer

## Validation Checklist
- [ ] Bucket created successfully
- [ ] Static website hosting enabled
- [ ] Bucket policy configured
- [ ] Website files uploaded
- [ ] Website accessible via S3 endpoint

## Troubleshooting
1. If website is not accessible:
   - Verify bucket policy is correct
   - Confirm static website hosting is enabled
   - Check if index.html is in the root of the bucket
   - Ensure file permissions are correct

2. If getting 403 errors:
   - Check bucket policy
   - Verify public access settings

## Next Steps
1. Consider adding:
   - Custom error page
   - CSS styling
   - JavaScript functionality
   - CloudFront distribution
