🧠 Overview

This architecture is designed to meet PCI-DSS requirements by enforcing strong network isolation, least-privilege access, runtime security, and comprehensive audit logging. The goal is to minimize the Cardholder Data Environment (CDE) scope while ensuring full traceability and protection.

🌐 Network Segmentation Model
Design:
VPC divided into:
Public Subnets (ALB, WAF entry)
Private Subnets (EKS workloads)
Isolated Subnets (RDS – no internet access)
Controls:
Strict Security Groups and NACLs
No direct internet access to workloads
Use of NAT Gateway for outbound traffic
Private endpoints for AWS services

PCI Alignment:

Segmentation reduces scope of CDE and limits lateral movement.

🔐 IAM Least Privilege Strategy
Approach:
Role-based access using IAM
Fine-grained permissions per service
No hardcoded credentials
Implementation:
IAM Roles for Service Accounts (IRSA) in EKS
Temporary credentials via STS
Separate roles for dev, staging, and prod
Controls:
Deny-by-default policy
MFA enforced for privileged users

PCI Alignment:

Ensures restricted access to cardholder data and critical systems.

🛡️ Web Application Firewall (WAF)
Setup:
AWS WAF integrated with ALB / CloudFront
Protections:
SQL Injection
Cross-Site Scripting (XSS)
Rate limiting (DDoS mitigation)
Geo-blocking (if needed)
Additional:
AWS Shield for DDoS protection

PCI Alignment:

Protects web-facing applications from common vulnerabilities.

🐳 Container Runtime Security Model
Controls:
Image scanning (ECR scan / tools like Trivy)
Only signed/approved images deployed
Read-only root file systems
Non-root containers
Runtime Security:
Kubernetes Pod Security Policies / OPA
Network policies to restrict communication
No privileged containers
Secrets:
Injected via AWS Secrets Manager (not in code)

PCI Alignment:

Ensures secure processing environment for applications handling sensitive data.

📊 Audit Logging Framework
Logging Sources:
AWS CloudTrail → API activity
CloudWatch Logs → application logs
VPC Flow Logs → network activity
EKS audit logs
Centralization:
Logs aggregated into a shared logging account
Security:
Logs are immutable (S3 + versioning + encryption)
Retention policies enforced
Monitoring:
Alerts via CloudWatch / SNS

PCI Alignment:

Enables traceability, auditing, and incident investigation.

🧾 PCI Audit Readiness – How It Will Be Presented

During a PCI audit, the architecture will be demonstrated using the following approach:

1. Architecture Diagram
Show segmented network (CDE vs non-CDE)
Highlight security layers (WAF, IAM, encryption)
2. Access Control Evidence
IAM policies
Role mappings (IRSA)
MFA enforcement proof
3. Data Protection
Encryption at rest (KMS)
Encryption in transit (TLS)
4. Logging & Monitoring Proof
CloudTrail logs
Access logs
Alert configurations
5. Vulnerability Management
Image scan reports
Patch management strategy
6. Change Management
CI/CD pipeline approvals
Deployment logs
Key Statement:

“The system enforces strict access control, network segmentation, encryption, and centralized logging, ensuring full compliance with PCI-DSS requirements.”

🎯 Conclusion

This security blueprint ensures a defense-in-depth strategy, combining network isolation, identity security, runtime protection, and audit visibility. It minimizes risk while maintaining compliance with PCI standards.
