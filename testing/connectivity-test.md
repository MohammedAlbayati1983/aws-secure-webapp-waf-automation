# Security & Connectivity Tests

The following tests were performed to validate the security posture and automation of the architecture.

| # | Test Description | Expected Result | Status |
|---|------------------|-----------------|--------|
| 1 | Direct access to EC2 Public IP | Timeout (Blocked by EC2-SG) | ✅ Passed |
| 2 | Access via ALB DNS | Returns "Secure Web App is Running" | ✅ Passed |
| 3 | Access via CloudFront URL | Returns "Secure Web App is Running" | ✅ Passed |
| 4 | WAF Rate Limit Test (Simulated DDoS) | Returns 403 Forbidden after 100 requests | ✅ Passed |
| 5 | S3 Log Delivery | CloudFront logs appear in S3 Bucket | ✅ Passed |
| 6 | Lambda Trigger | Lambda is invoked when a new log arrives in S3 | ✅ Passed |
| 7 | Lambda Execution | Lambda successfully parses logs without errors | ✅ Passed |