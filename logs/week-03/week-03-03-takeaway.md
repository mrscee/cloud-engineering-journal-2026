
## 💰 Section 3: Pricing, Billing, and Support

### **Cloud Costs: The Bigger Picture**
- Cost optimization is continuous, not one-time
- Visibility → allocation → optimization

### **Compute Cost Model**
- EC2 billing drivers:
  - instance family (compute/cpu/gpu)
  - size (t3.micro vs m6i.8xlarge)
  - lifecycle: On-Demand > Reserved > Savings Plans > Spot

### **Data Storage Cost Model**
- S3 Storage Classes:
  - Standard
  - IA (Infrequent Access)
  - Glacier
  - Glacier Deep Archive
- Lifecycle transitions reduce cost automatically

### **Creating an S3 Storage Lifecycle**
- Lifecycle rules:
  - transition → change storage class
  - expiration → delete old data
  - version cleanup → reduce bloat

### **Data Transfer Cost Model**
- Key rule: **ingress = free; egress = not free**
- Big bills often come from:
  - cross-region data movement
  - inter-AZ traffic
  - outbound to Internet

### **Monitoring & Predicting Costs**
- Cost Explorer = historical trends
- Budgets = controlled guardrails
- CUR (Cost & Usage Report) = granular accounting

### **Budget Alerting**
- Budget alerts via:
  - Forecasted spend
  - Actual spend
  - SNS notifications

### **Multi-Account Cost Management**
- Organizations billing benefits:
  - Consolidated billing
  - Commitment sharing (RIs & Savings Plans)
  - Centralized budgeting

### **Support Models**
- Free → Developer → Business → Enterprise
- Support = not just break/fix; includes guidance

### **Other Sources of “Support”**
- AWS docs
- Re:Post
- Well-Architected Tool
- AWS Health Dashboard

### **Final Exam Tips from Section**
- Know the direction of data transfer charges
- Know key identity/security services
- Know how lifecycle rules reduce S3 spend
- Know that support plans cost money

---
