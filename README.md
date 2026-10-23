# AWS Secure Web App with WAF Automation

## 📌 Overview
A production-grade security architecture for a two-tier web application hosted on AWS. This project demonstrates how to enhance the security posture of a web application, mitigate DDoS attacks, and implement an automated incident response system using AWS WAF, CloudFront, and Lambda.

## 🏗️ Architecture Diagram
![Architecture Diagram](./architecture/architecture-diagram.png)

## 🎯 Requirements Covered
1. **Two-Tier Web App:** Auto-scaled fleet of EC2 instances (in public subnets) behind an Application Load Balancer (ALB) across two Availability Zones.
2. **Enhanced Security:** Implementation of AWS WAF (Web Application Firewall) integrated with CloudFront to protect against common web vulnerabilities (Layer 7).
3. **DDoS Mitigation:** Utilization of AWS Shield Standard (automatic) and WAF Rate Limiting rules to minimize the impact of internet-generated attacks.
4. **Layer 4 Security:** Restricting EC2 Security Groups to accept traffic **only** from the ALB, and implementing strict Network ACLs.
5. **Automated Incident Response (SOAR):** CloudFront Access Logs are sent to S3, triggering a Lambda function that parses the logs, detects blocked IPs, and is designed to automatically update WAF/NACL rules to block malicious actors.
6. **Cost-Effective:** Used only necessary resources to minimize ongoing overhead in the lab environment.

## 🔧 AWS Services Used
| Service | Purpose |
|---------|---------|
| Amazon VPC | Network isolation (2 Public Subnets, IGW, Route Tables) |
| Amazon EC2 (ASG) | Web/App compute tier (Auto Scaling Group) |
| Application Load Balancer | Traffic distribution across AZs |
| Amazon CloudFront | CDN and entry point for WAF protection |
| AWS WAF | Web Application Firewall (Rate limiting, Geo-blocking) |
| Amazon S3 | Storage for CloudFront Access Logs |
| AWS Lambda | Serverless automation for log parsing and security response |
| AWS IAM | Access control for Lambda automation |

## 📂 Repository Structure
```text
.
├── architecture/          # Architecture diagrams
├── screenshots/           # AWS Console screenshots (proof of implementation)
├── documentation/         # Requirements & design decisions
├── testing/               # Connectivity & validation tests
└── infrastructure-as-code/ # (Planned) Terraform implementation# AWS Secure Web App with WAF Automation
```
