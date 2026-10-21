# Project Requirements

Design a security solution for a two-tier web application deployed in AWS across two Availability Zones. The web application consists of an auto-scaled fleet of EC2 instances, in public subnets, behind an Application Load Balancer. The solution must enhance the application’s security posture and minimize the impact of internet generated attacks, including DDoS attacks. The solution must be very cost-effective in achieving the required with the least ongoing overhead.

### Extended Requirements (Based on Architecture Design):
- **WAF Integration:** Implement AWS WAF on CloudFront to protect against common vulnerabilities.
- **Rate Limiting:** Implement WAF Rate Limit rules to prevent DDoS and HTTP flood attacks.
- **Strict Network Security:** Ensure EC2 instances only accept traffic from the ALB (Security Groups) and implement strict NACLs.
- **Automated Incident Response:** Send CloudFront logs to S3, trigger a Lambda function to parse logs, and automatically update WAF/NACL rules to block malicious IPs.