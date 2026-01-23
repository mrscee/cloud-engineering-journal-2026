# Week 3 — Section 1  
## Auditing, Monitoring, Logging & Operational Visibility on AWS

---

## 🎯 Objective
Section 1 introduces how AWS provides **observability**, **accountability**, and **operational visibility** across cloud workloads. The goal is to answer:

1. **What is happening?** (Monitoring)
2. **Who did what?** (Auditing)
3. **Is it configured correctly?** (Compliance)
4. **Is AWS itself healthy?** (Platform Health)
5. **Are we following best practices?** (Assessment)

These concerns show up constantly in real production environments.

---

# 🧱 Part 1 — Core Observability Services (High Priority)

These are the core primitives used by Cloud, DevOps, SRE, and Platform Engineering teams.

---

## 🟦 **Amazon CloudWatch**
Provides **performance visibility** into AWS resources and applications.

Core capabilities:
- **Metrics** → CPU, memory, network, usage, custom metrics
- **Logs** → application & system log ingestion
- **Alarms** → notify or trigger actions when thresholds are hit
- **Dashboards** → visualize metrics in real-time
- **Events** → event routing to other AWS services
- **Insights** → SQL-like log querying

> **Mental Model:**  
> CloudWatch = “What is happening right now?”

**Terraform relevance:**
Common Terraform resources:
- `aws_cloudwatch_dashboard`
- `aws_cloudwatch_log_group`
- `aws_cloudwatch_metric_alarm`
- `aws_cloudwatch_event_rule`

---

## 🟩 **AWS CloudTrail**
Tracks **API activity** for auditing and forensic visibility.

CloudTrail answers:
- Who did it?
- When did they do it?
- From where?
- Using what identity?
- Against which resource?

CloudTrail integrates with:
- S3
- Athena
- GuardDuty
- SIEM tools

> **Mental Model:**  
> CloudTrail = “Who touched what and when?”

---

### **CloudWatch vs CloudTrail Summary**

| Category | CloudWatch | CloudTrail |
|---|---|---|
| Purpose | Monitoring | Auditing |
| Focus | Performance & Logs | Identity & API Activity |
| Visibility | System behavior | User behavior |
| Output | Metrics, alarms, dashboards | Audit logs |
| Primary User | SRE + Ops | SecOps + Compliance |

---

## 🟨 **AWS Systems Manager (SSM)**

Provides centralized **operational control** across fleets of resources.

Capabilities:
- resource grouping
- patching & automation
- commands across resources
- operational data aggregation
- secure parameter storage (Parameter Store)

Parameter Store is used for secrets such as:
- passwords
- DB connection strings
- API keys
- license keys

---

## 🟥 **AWS Health Dashboard & AWS Health API**

Provides visibility into **AWS platform health**:

- **Health Dashboard**  
  Shows service status relevant to your account + region.

- **AWS Health API**  
  Used for custom observability integrations.

---

## 🟪 **Trusted Advisor**

Automated best practice checks across pillars:

- Security
- Cost Optimization
- Performance
- Operational Excellence
- Fault Tolerance
- Service Limits

**Free checks include:**
- root user MFA
- open security groups
- IAM user usage
- service limit warnings

**Business/Enterprise tier adds:**
- public RDS snapshots
- public EBS snapshots
- public S3 buckets
- idle resources cost leaks

---

# 🧱 Part 2 — Tagging for Cost, Ownership & Observability

Tagging enables:
- cost allocation
- chargeback/showback
- resource ownership
- environment separation
- metric filtering

Common enterprise tags:
- `Environment`
- `Application`
- `Owner`
- `CostCenter`
- `Team`
- `Criticality`

CloudWatch metrics can be **aggregated by tags**, making tagging foundational for monitoring.

---

# 🧱 Part 3 — Business & End-User Services (Awareness Level)

These services are consumed by business users rather than cloud engineers.

### **Amazon Connect**
Cloud contact center:
- telephony + IVR + support workflows

### **Amazon WorkSpaces**
Virtual desktop (VDI):
- full remote desktop environment (Win/Linux)

### **Amazon AppStream 2.0**
Application streaming:
- streams specific apps without a full desktop

**Mental Model:**
> WorkSpaces = Desktop  
> AppStream = Application  
> Connect = Contact Center

---

# 🧱 Part 4 — Auditing & Compliance Tooling (Context Priority)

These services support compliance frameworks but do not enforce them.

---

## 🔎 **AWS Config**
Backbone of configuration auditing.

Tracks:
- resource configuration
- configuration drift
- compliance against rules

Important note:
> Config **detects & alerts**, it does **not enforce**

Used for rules such as:
- S3 encryption required
- security groups not open to 0.0.0.0/0
- IAM password policies
- EBS encryption required

---

## 📋 **AWS Audit Manager**
Aggregates audit evidence for frameworks such as:
- HIPAA
- NIST Cybersecurity
- SOC 2
- ISO 27001
- AWS Best Practices

Audit Manager allows teams to:
- collect evidence
- generate reports
- reduce manual effort

> **Mental Model:** Audit Manager = “Show evidence to auditors.”

---

## 🧰 **AWS Well-Architected Tool**
Assesses workloads against the 6 AWS pillars:

1. Security
2. Cost Optimization
3. Performance Efficiency
4. Operational Excellence
5. Reliability
6. Sustainability

Outputs:
- risks (HRIs = High Risk Issues)
- remediation guidance
- action plans

---

# 🧱 Part 5 — Enforcement vs Auditing vs Assessment (Clarification)

AWS splits responsibilities into three domains:

| Category | Example | Purpose |
|---|---|---|
| **Monitoring** | CloudWatch | observe performance |
| **Auditing** | CloudTrail / Config | observe configuration & actions |
| **Assessment** | Audit Manager / Well-Architected | prove alignment |
| **Enforcement** | IAM / SCP / Config Remediation | prevent violations |

Production workflow often looks like:

Enforce → Detect → Audit → Assess → Improve


Example mapping:

- IAM/SCP = prevent
- Config = detect
- CloudTrail = record
- Audit Manager = prove
- Well-Architected = improve

---

# 🧱 Part 6 — Well-Architected Framework Integration

Observability supports multiple pillars:

- **Security** → track actions across resources
- **Cost Optimization** → metrics support rightsizing
- **Performance Efficiency** → find bottlenecks
- **Operational Excellence** → dashboards + logs
- **Reliability** → uptime & availability metrics
- **Sustainability** → utilization informs energy consumption

---

# 🧪 Part 7 — Units of Capability (Resume + Interview Mappable)

Completion of Section 1 grants the following capability units:

- **UC-1:** Monitor AWS workloads via CloudWatch metrics
- **UC-2:** Query logs via CloudWatch Logs/Insights
- **UC-3:** Build dashboards for operational visibility
- **UC-4:** Audit IAM/API actions via CloudTrail
- **UC-5:** Apply tagging standards for cost + ownership
- **UC-6:** Use Trusted Advisor for automated checks
- **UC-7:** Leverage SSM for operational management
- **UC-8:** Assess platform health via Health Dashboard/API
- **UC-9:** Interpret compliance vs best practice tooling

---

# 🧩 Part 8 — Terraform Opportunity (For Portfolio Add-On)

High-value Terraform targets:

- CloudTrail → S3 → KMS
- CloudWatch Log Groups
- CloudWatch Dashboard
- Metric Alarms
- Tagging Standards
- Event Rules (for automation)
- Parameter Store (for secrets)

This can be added to the “Level Up Bank” project as:

> **Observability + Compliance Add-On**

---

# 🧩 Part 9 — Final Section Summary (Executive View)

Operational visibility on AWS is composed of:

| Concern | AWS Mechanism |
|---|---|
| Performance | CloudWatch Metrics + Dashboards |
| Logs | CloudWatch Logs + Insights |
| Audit | CloudTrail |
| Configuration | AWS Config |
| Compliance Evidence | Audit Manager |
| Best Practices | Well-Architected |
| Cost/Ownership | Tagging |
| Platform Health | Health Dashboard / API |
| Automated Checks | Trusted Advisor |
| Operations | Systems Manager |
| Business Consumption | Connect / WorkSpaces / AppStream |

Together, these provide the ability to see, prove, and improve cloud workloads at scale.

---

