# How L.U. Corp Standardized Remote Access in AWS
### Use Case: Secure Remote Access via SSH and RDP
_By Comfort Benton — Cloud DevOps Engineer_

---

## CASE OVERVIEW — Secure Remote Access for EC2 Administration

L.U. Corp, a mid-sized tech company, operates a growing portfolio of applications across Amazon Web Services (AWS), running a mix of Linux and Windows workloads on Amazon EC2. With development and operations teams distributed across regions, the company needed a reliable way for engineers to administer servers, perform maintenance tasks, and troubleshoot issues in real time.

However, the organization lacked a standardized, secure, and direct remote administration path into its EC2 instances. This gap made even routine operations slower than necessary, increased downtime during incidents, and created unnecessary friction for IT personnel working across time zones.

---

## BUSINESS PROBLEM

Without direct remote access to the operating system, troubleshooting often required escalation between multiple teams. In some cases, the IT staff relied on indirect or delayed methods to diagnose issues, such as:

- relaying commands through another engineer,
- relying solely on application-level monitoring tools,
- using slow ticket queues for operational changes, or
- depending on shared documentation instead of real access.

These makeshift approaches are not uncommon in enterprises transitioning to cloud-first environments, but they restrict visibility and reduce operational control. They also introduce ambiguity in ownership during outages, particularly when multiple teams support the same workload.

Without standardized secure remote access, even simple tasks like restarting a failed service or inspecting system logs would take too long to diagnose, which would increase downtime, hurt productivity, and possibly raise security concerns among leadership.

---

## PROPOSED SOLUTION

To address the bottleneck, L.U. Corp standardized the foundational layer of remote administration by adopting:

- For Linux EC2 instances, use **SSH**
- For Windows EC2 instances, use **RDP**

Both protocols provide secure, encrypted channels for remote login and are widely supported across enterprise tooling, credentials, and workflows. This solution also sets the stage for more advanced access models in the future, such as AWS Systems Manager, IAM-managed permissions, or bastion host architectures.

---

## IMPLEMENTATION — SSH FOR LINUX EC2

### Step 1 — Launch Linux Instance

1. Launch Amazon Linux instance type. After naming it what you want, then:
   a. Create a new key pair with type `RSA` and format `.pem`  
   b. Click **Edit** to change the Network settings  
   c. Create a security group with name and description  
   d. Choose type `ssh` (port 22)  
   e. Choose **My IP** as source type for single-source admin connection  
   f. Launch the instance  

![SSH Step 1](./assets/B_ssh-step-1.png)
---

### Step 2 — Connect via SSH

2. Go to your instance page, then:
   a. Select the instance you want to connect to  
   b. Click **Connect**  
   c. In the Connect screen (SSH tab), follow the steps to connect to your EC2  
   d. Copy the provided command to your SSH client (PowerShell)  
   e. Navigate to the folder with the key pair and execute the command  

**Screenshot:**  
`assets/C_connect-step-2.png`

---

## IMPLEMENTATION — RDP FOR WINDOWS EC2

### Step 1 — Launch Windows Instance

1. Launch Windows Server instance type:
   a. Create a new key pair with type `RSA` and format `.pem`  
   b. Click **Edit** to change the Network settings  
   c. Create a security group with name and description  
   d. Choose type `rdp` (port 3389)  
   e. Choose **My IP** as source type  
   f. Launch the instance

---

### Step 2 — Connect Workflow

2. Go to your instance page, then:
   a. Select the instance  
   b. Click **Connect**  
   c. Under **RDP client**, click **Get password**

**Screenshot:**  
`assets/E_rdp-get-pw.png`

---

### Step 3 — Retrieve Admin Password

3. Obtain password by decrypting key pair:
   a. Upload the key pair  
   b. Click **Decrypt password**  
   c. Capture username and password for RDP client  

**Screenshot:**  
`assets/D_rdp-connect-pw.png`

---

### Step 4 — Connect via RDP Client

4. Connect using RDP client:
   a. Open the RDP client  
   b. Enter obtained credentials  
   c. Accept certificate prompt and continue  

**Screenshot:**  
`assets/F_rdp-screens-to-desktop.png`

---

## OUTCOME

By modernizing remote administration, L.U. Corp moved from slow, indirect troubleshooting to secure, real-time access. Outages resolved faster, engineers stayed productive, and operations scaled more gracefully as the environment grew.

Key operational benefits included:

- Faster incident response
- Security improvements
- Reduced downtime
- Higher productivity
- Scalability

Together, these improvements increased operational velocity, strengthened security posture, and aligned teams around a consistent and cloud-appropriate access pattern.

---

## FUTURE ENHANCEMENTS

L.U. Corp could further mature its remote administration strategy through:

- AWS Systems Manager (SSM)
- IAM-based authorization for least-privilege control
- Session Manager for audit logging
- Bastion hosts for private network access
- Zero Trust workforce models

These enhancements would reduce credential sprawl, improve auditability, and standardize access across larger footprints.

---

## KEY TAKEAWAYS

- Secure remote access is foundational for distributed cloud operations
- SSH (Linux) and RDP (Windows) are practical, lightweight, and widely adopted
- Standardization reduces friction during outages and maintenance
- Indirect operational models increase downtime
- Foundational improvements enable advanced access patterns

---

## TAGS

`AWS` `EC2` `SSH` `RDP` `Remote Administration` `DevOps` `Cloud Engineering`


