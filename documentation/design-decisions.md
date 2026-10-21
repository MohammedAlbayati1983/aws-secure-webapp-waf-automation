# Design Decisions & Security Architecture

This document outlines the architectural choices made to secure the two-tier web application, including automation logic and cost optimizations.

## 1. Layered Security Approach
- **Edge (CloudFront + WAF):** AWS WAF is integrated with CloudFront to filter malicious traffic (Layer 7) before it even reaches the AWS Region. This protects against SQLi, XSS, and DDoS (via Rate Limiting).
- **Network (NACLs):** A custom Network ACL was created to allow only HTTP/HTTPS and Ephemeral ports, blocking all other traffic at the subnet level.
- **Compute (Security Groups):** The `EC2-SG` was configured to allow HTTP traffic **only** from the `ALB-SG`. This ensures that no one can bypass the Load Balancer and access the instances directly.

## 2. DDoS Mitigation
- **AWS Shield Standard:** Automatically protects CloudFront and Route 53 against common Layer 3/4 DDoS attacks at no extra cost.
- **WAF Rate Limiting:** A custom WAF rule was created to block any IP address that exceeds 100 requests in a 5-minute window. This was tested and proven effective against HTTP flood attacks.

## 3. Automated Incident Response (SOAR)
- **Logging:** CloudFront access logs are delivered to an S3 bucket.
- **Trigger:** An S3 Event Notification triggers the `Security-Automation-Lambda` function whenever a new log file is created.
- **Lambda Logic:** The Python function reads the gzipped log file, parses the JSON data, and identifies IPs that received a `403 Forbidden` status. 
- *Future State:* In production, this Lambda would use `boto3` to push the malicious IPs into a WAF IP Set and NACL Deny rules for permanent blocking.

## 4. Cost Optimization
- **No WAF Advanced Shield:** AWS Shield Advanced ($3000/month) was omitted. Basic WAF + Shield Standard is sufficient for this lab.
- **Lambda:** Serverless, meaning we only pay for the milliseconds it takes to process the logs.
- **EC2:** Used `t3.micro` instances within the Free Tier.

## 5. Infrastructure as Code
- **Current State:** Manual provisioning via Console.
- **Future Enhancement:** Terraform implementation is planned.