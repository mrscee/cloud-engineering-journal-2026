## 🛡️ Section 2: Security, Compliance, and Governance

### **Security: The Bigger Picture**
- Security is shared responsibility
- AWS protects infrastructure; customer protects usage
- Misconfig is the #1 cause of breaches (not AWS failure)

### **What Do We Need to Secure on AWS?**
- Data (at rest + in transit)
- Identities & access
- Network boundaries
- Application layers
- Visibility + logging + auditing

### **Principle of Least Privilege**
- Default stance: “deny everything”
- Then grant only what is required
- IAM roles > IAM users for workload access

### **What is IAM?**
- Central identity + permissions control plane
- Core primitives:
  - **Users** = human credentials
  - **Roles** = temporary access w/ STS
  - **Groups** = permission aggregation
  - **Policies** = JSON documents that evaluate ALLOW/DENY

### **Troubleshooting IAM on EC2**
- Common failure path:
  - EC2 needs role → role needs policy → service must support STS → trust relationship must match
- “AccessDenied” ≠ AWS broken → permissions gap

### **Keeping Secrets Safe**
- Secrets should not be stored:
  - in AMIs
  - in user data
  - in code repos
- Preferred:
  - AWS Secrets Manager
  - Parameter Store (SSM)

### **Network Security Services**
- VPC = boundary
- SG = stateful per-instance firewall
- NACL = stateless subnet boundary (rarely changed)
- Private subnets = reduce public exposure
- Endpoints = private connectivity to AWS services

### **Security Hub**
- Aggregates security findings from AWS services:
  - GuardDuty
  - Inspector
  - IAM Access Analyzer
  - Config
- Normalizes results to industry frameworks (CIS, PCI, etc.)

### **Responding to Security Events**
- Key pipeline:
  1. Detect (GuardDuty)
  2. Log (CloudTrail/CloudWatch)
  3. Alert (SNS/EventBridge)
  4. Act (manual or Lambda automation)

### **Growing Security Muscles**
- Best learning pattern:
  - Threat modeling
  - Log interpretation
  - IAM drill-down
  - Hands-on triage

### **Governing Multiple Accounts**
- Organizations + SCPs = governance at scale
- Multi-account = better blast radius control
- Root account should never hold workloads

### **Compliance on AWS**
- Compliance != security (but they overlap)
- AWS gives tooling (not compliance guarantees)
- Customer ensures actual implementation

---
