# Development, Messaging, and Deployment Services — My Takeaways

This week introduced several foundational AWS services that support modern application development, deployment, and communication. The lesson content covered the tooling around how applications get built, deployed, and decoupled across cloud environments.

---

## What I Worked Through

- CI/CD concepts and workflows
- AWS development tools (CloudShell, CLI, Cloud9, CodeArtifact)
- Application decoupling approaches
- Messaging & notification services (SNS, SQS, SES)
- Event-driven routing with EventBridge
- Orchestration with Step Functions

---

## Key Concepts in Plain Language

### CI/CD
- **CI** automates building and testing
- **CD** automates deployment
- Reduces manual steps and human error during releases
- AWS Development tools:
  
**CodeCommit** — *Source & Version Control*  
Managed Git-based source control service for teams to collaborate on code, scripts, HTML pages, images, and binaries.

**CodeBuild** — *Automated Build*  
Compiles source code, runs automated tests, and produces build artifacts/packages that are ready to deploy.

**CodeDeploy** — *Automated Deployment*  
Automates code deployments to EC2, Lambda, and on-premises servers with support for blue/green and rolling updates.

**CodePipeline** — *Manages the Workflow*  

End-to-end CI/CD orchestration that automatically builds, tests, and deploys application changes whenever code updates occur.

### AWS Development Tools
- **CloudShell / AWS CLI** — command-line interaction with AWS
- **Cloud9** — browser-based IDE for cloud development without local setup
- **CodeArtifact** — internal package repository for sharing libraries

### Decoupling Applications
- Services don’t call each other directly
- Improves scalability, reliability, and failure isolation

### Amazon SNS (Simple Notification Service)
- Publish/subscribe (pub/sub) messaging
- One message can fan out to multiple subscribers
- Often used for notifications and system fan-out

### Amazon SQS (Simple Queue Service)
- Durable message queue for work distribution
- Consumers poll queues and process at their own pace
- Supports Standard + FIFO queues
- All for decoupling components of applications

### Polling
- **Short Polling** — quick checks for messages
- **Long Polling** — waits for messages and reduces empty receives

### Amazon SES (Simple Email Service)
- Used for transactional and bulk email from applications
- Examples: password resets, receipts, confirmations

### Amazon EventBridge
- Event routing + filtering
- Enables event-driven architectures without tight coupling

### AWS Step Functions
- Orchestration + workflow engine
- Handles retries, wait states, branching, error handling

---

## Real-World Connections

These services support patterns commonly used in modern cloud-native systems:

- asynchronous processing
- microservices communication
- distributed workflows
- failure handling
- fan-out scenarios
- scalable deployments

The services in this section are the **building blocks** for how cloud applications talk, coordinate, notify, and scale.

---

## Personal Takeaway

The lesson content was straightforward, but the bigger value came from understanding how these services work together rather than in isolation. Messaging (SNS, SQS, SES), eventing (EventBridge), and orchestration (Step Functions) solve different parts of the communication story in a distributed application.

---

## Screenshots To Be Added

- [Screenshot: Messaging Section Progress](#)
- [Screenshot: SNS Topic Creation](#)
- [Screenshot: SQS Queue View](#)

---




# DynamoDB + CloudFormation Lab — My Takeaways

For Week 02, I completed a short lab that used CloudFormation to provision a DynamoDB table for a fictitious pizza inventory application. The lab itself was simple, but it served as a clean introduction to what Infrastructure-as-Code feels like inside AWS.

---

## What I Did

- Reviewed the provided CloudFormation template in YAML
- Launched a CloudFormation stack to create the DynamoDB table
- Validated the table in the DynamoDB console
- Created my own manual test table (the **“Mom and Dad”** test table) to observe DynamoDB behavior outside the lab
- Compared **Provisioned** vs **On-Demand** billing modes
- Explored DynamoDB’s NoSQL storage characteristics and cost model through Q&A

---

## Key Observations

- CloudFormation is declarative: you describe the desired state and AWS provisions the infrastructure for you
- The template is not the deployment; the deployment becomes a **Stack** that AWS manages
- Templates can be reused across **dev/test/prod** with parameters rather than rewriting code
- DynamoDB is NoSQL and schema-flexible: only the primary key is enforced
- Lab table used **Provisioned throughput** (5 RCUs / 5 WCUs) which reserves capacity and bills whether used or not
- Manual test table defaulted to **On-Demand billing**, which only charges for actual reads/writes (my usage rounded down to $0)
- Small request volumes do not accumulate month-to-month; unused volume does not “roll over”
- Data is stored durably across multiple AZs in the region, not just visually in the UI
- Schema flexibility became obvious when adding different attributes to different items during the Mom & Dad test

---

## What This Lab Was Really Teaching

This lab wasn’t about pizza toppings or DynamoDB specifics. The real focus was the IaC workflow:

Template → Stack → Provision → Validate → Delete


The lab just provided the baseline; the deeper understanding came from asking questions about how DynamoDB works behind the scenes (schema, billing modes, storage, durability, and cost).

---

## Personal Takeaway

The lab scaffolded the exercise, but exploring DynamoDB’s behavior is what actually made it click. CloudFormation gave me something deployable; the Q&A gave me the “why” behind it.

---

## Topics Covered

- Infrastructure as Code (CloudFormation)
- Stack lifecycle
- Provisioned vs On-Demand billing models
- RCUs/WCUs and throughput
- NoSQL schema flexibility
- Multi-AZ durability
- Basic cloud cost awareness
- On-demand usage rounding and billing thresholds

---

## Assets & Screenshots

To be added:

- [Deployment Screenshot](#)  
- [DynamoDB Table Validation Screenshot](#)  
- [Mom-and-Dad Test Table Screenshot](#)

---
## Other Takeaways
### Elastic Beanstalk
Elastic Beanstalk is a managed platform-as-a-service (PaaS) that takes application code and automatically provisions the underlying infrastructure for you (EC2, autoscaling, load balancing, health checks, deployments, and monitoring) without requiring you to touch those pieces directly.

To deploy with Elastic Beanstalk, you:

1. Create a **service role** for Elastic Beanstalk to deploy services on your behalf  
2. Create an **EC2 instance role** to allow Elastic Beanstalk to administer AWS services such as EC2, RDS, S3, ELB, and Auto Scaling Groups on your behalf  
3. Upload your application code and let Beanstalk handle the rest

This enables a deployment experience where the application runs on AWS without the need to manually provision, configure, or maintain EC2 instances yourself.

### AWS X-Ray
X-Ray traces how requests move through distributed applications so engineers can find performance bottlenecks, errors, and latency. Applications must be instrumented for X-Ray to collect data, and companies pay for usage. It’s more common in modern DevOps/SRE work than in early-stage junior cloud roles.


## Snow Family (Bulk Data Transfer Appliances)

The Snow Family provides physical devices for bulk data migration when network transfer would be too slow or impractical:

- **Snowball** — Move 10+ TB of data to AWS.
- **Snowball Edge** — Move 10+ TB and also process data on the device before transfer.
- **Snowmobile** — Used for 10+ PB (petabyte-scale) migrations using a secure truck.
- **Snowcone** — Small, rugged, portable device supporting up to 14 TB.

**Use case:** Large offline data transfers into AWS when bandwidth is the bottleneck.


## Database Migration (DMS + SCT)

AWS provides tools for migrating and converting databases:

- **Database Migration Service (DMS)**  
  Migrates existing databases and analytics workloads from EC2, on-premises, or RDS into AWS with minimal downtime.

- **Schema Conversion Tool (SCT)**  
  Converts database schema and code from one engine to another, such as:
  - Oracle → Aurora MySQL
  - MySQL → RDS MySQL
  - SQL Server → Aurora PostgreSQL

**Key point:** DMS moves the data; SCT handles schema changes when engines differ.


## AWS Transfer Family (File Transfer Endpoints)

The AWS Transfer Family provides managed file transfer endpoints for external parties and clients:

- Supports file sharing and transfer in/out of AWS.
- Supports both download (SFTP GET) and upload (SFTP PUT).
- Works with multiple protocols including SFTP, FTPS, AS2, and FTP.
- Integrates directly with AWS storage (commonly S3).

**Use case:** Secure file transfer workflows with partners, vendors, or legacy clients. 


## AWS DataSync — My Takeaways

### 🧠 Mental Model

**DataSync is a high-throughput data transfer service** used to move large datasets (terabytes to petabytes) between:

- on-premises storage and AWS
- AWS storage services (S3, EFS, FSx)
- different cloud providers
- hybrid or multi-cloud environments

It handles:
✔ data validation  
✔ encryption  
✔ scheduling  
✔ bandwidth control  
✔ retries  
✔ storage protocol translation (NFS/SMB → S3/EFS/FSx)

---

### 🔧 How It Works (Simplified)

If the source is **on-prem**, an **agent** is deployed locally to access the file system and send data to AWS securely over the network.

If the source and destination are **both in AWS**, no agent is required.

Supported protocols:
- **NFS**
- **SMB**
- **Object stores**

Supported destinations:
- **S3**
- **EFS**
- **FSx** (for Windows and Lustre)

---

### 🎯 Primary Use Cases

From training + case examples:

- **Migrate** data to AWS storage
- **Replicate** data to low-cost storage
- **Archive** historical/long-lived datasets
- **Support hybrid & multi-cloud workflows**

This aligns with real enterprise needs such as:

- backup/retention modernization
- storage hardware refresh avoidance
- compliance-driven retention
- cloud onboarding

---

### 🏢 Real-World Autodesk Case Study (Memorable)

Autodesk had accumulated ~700 TB of backup data on-prem that needed to be retained for many years.

Using **AWS DataSync**, they:

- transferred ~700 TB over a **1.4 Gbps** link during low-usage hours
- landed data into **Amazon S3** first
- used **S3 lifecycle policies** to archive into **S3 Glacier** for long-term retention
- completed the project in **~2.5 months**

This demonstrates how enterprises combine:
1. **Migration** (DataSync)
2. **Storage landing** (S3)
3. **Archival economics** (Glacier)

---

### 🧩 After Migration — What Happens

Once data is in AWS:

- S3 becomes the **new system of record**
- Lifecycle policies automate tiering (e.g. S3 → Glacier → Deep Archive)
- On-prem storage can often be **retired and decommissioned**
- Retrieval is done through **AWS APIs/console**, not old file servers

This supports both:
- **A)** existing workload support, and  
- **C)** new cloud-native patterns  
(aligning with my A + C career trajectory)

---

### 🗄 Agent Clarification (Important)

Agent **required** when:
- source is on-prem
- source is NFS/SMB
- source is inside other clouds (Azure/GCP)

Agent **not required** when:
- transferring AWS → AWS (e.g., S3 ↔ EFS ↔ FSx)

Rule of thumb:
> If AWS cannot “reach” the file system directly, use the Agent.

---

### 💸 Economic Angle (Why Companies Care)

DataSync + S3 + Glacier helps enterprises reduce:

- storage hardware refresh cycles
- tape library systems
- power & cooling costs
- rack space costs
- vendor support contracts
- maintenance overhead
- CapEx-based storage planning

AWS model shifts this to predictable **OpEx** with pay-for-usage economics.

---

### 🛠 Practical Tasks for Cloud Engineers

A cloud engineer may be involved in:

- configuring DataSync agents
- throttling bandwidth
- defining transfer schedules
- validating checksums
- landing data into S3/EFS/FSx
- setting lifecycle rules for Glacier
- verifying cutover or archival success
- supporting retrieval workflows

This makes DataSync part of realistic cloud onboarding and modernization projects.

---

From the course visuals:

- **Securely migrate all your data to AWS**
- **Cost effectively replicate data using AWS Storage**
- **Archive historical data to low cost AWS Storage**
- **Support hybrid or multi-cloud workflows**

And summary slide:
> “Securely transfer TB of data to S3, EFS, FSx.  
Supports NFS, SMB, or object stores.  
Data can be on premises, in another cloud provider, or in AWS storage.  
Use cases: migration, replication to low cost storage, archiving, and hybrid or multi-cloud.”

---

### 🤝 Who Actually Performs the Migration?

Depending on the organization, migrations can be executed by:

- **AWS ProServe** — AWS’s own consulting arm for large/complex migrations.
- **AWS Partners (SI/MSP)** — consulting or managed service providers that run the project for the customer.
- **The Customer Themselves** — internal IT/cloud teams perform the transfer using AWS tools like DataSync.

---

### 🛠 Who Handles Maintenance After Migration?

After data lands in S3/Glacier, operational ownership typically falls into one of these models:

- **Customer-Owned Model** — customer manages access, retrieval, lifecycle, compliance, cost tuning, etc.
- **Partner-Managed MSP Model** — a managed service provider handles ongoing operational tasks on behalf of the customer.
- **AWS Enterprise Support / ProServe Engagements** — AWS advises and assists, but does not operate the customer's data day-to-day.

> Note: AWS provides the storage platform and support, but **does not function as a traditional MSP** for ongoing operations.

---

### 🏁 Personal Summary

DataSync is one of those AWS services where certification material doesn’t fully convey the real-world value — but once you see how companies use it to get rid of aging NAS/tape/backup infrastructure and modernize retention, it becomes a practical tool in migrations.

The Snow Family is about **physical data transport**, whereas DataSync is about **network-based sustained transfer**, and the Autodesk case made that distinction clear.

## AWS Application Discovery Service (ADS) — My Takeaways

**Mental Model:**  
Think of ADS as an **inventory + dependency scanner** for data centers. It surfaces what exists, what talks to what, and what needs to move together so you don’t break anything during migration.

**What it is:**  
A tool used to automatically identify and map on-premises applications, servers, and dependencies prior to migration.

**Why it exists (real-world):**  
Enterprises often have legacy environments with:
- tribal knowledge
- undocumented dependencies
- multiple data centers
- staff turnover
- acquired systems
- aging infrastructure

ADS helps answer practical migration questions such as:
- What applications are running?
- What systems depend on each other?
- What needs to move together?
- What can be retired or modernized?

This prevents migration failures caused by missing dependencies (e.g., moving a billing app but forgetting its SQL database or file share).

**Use Case Summary:**  
ADS reduces migration risk by replacing tribal knowledge with actual dependency mapping.


---

## AWS Application Migration Service (MGN) — My Takeaways

**Mental Model:**  
MGN is the **lift-and-shift conveyor belt** that moves applications as-is into AWS with minimal downtime, before anyone starts modernizing, refactoring, or containerizing them.

**What it is:**  
AWS’s managed **lift-and-shift (rehost)** migration service that moves applications to AWS **as-is**, without requiring code changes or refactoring.

**Why companies use it:**  
- least disruptive migration path
- lowest business risk
- supports legacy and monolithic systems
- avoids rewriting during migration
- maintains uptime during transfer phase

**How migration works conceptually:**
1. **Initial Sync** — copies full server image to AWS
2. **Continuous Replication** — streams deltas while users keep working
3. **Cutover Window** — short maintenance window for final sync + traffic switch
4. **Validation** — verify app behavior in AWS
5. **Decommission** — retire on-prem systems when safe

**Zero Downtime Note:**  
Users can continue using the application during replication; only the final cutover requires a brief coordinated window.

**Why modernization waits until after migration:**  
- reduces complexity and failure points
- isolates variables (move first, change later)
- respects compliance & business continuity
- enables CI/CD + DevOps practices once in AWS


---

## AWS Migration Hub — Quick Notes

**Mental Model:**  
Migration Hub is the **project dashboard** for migrations. It doesn’t perform the migration — it shows **status, progress, and inventory** across tools.

**What it does:**  
- tracks migration tasks across multiple tools
- aggregates inventory + status into one view
- helps coordinate cutovers and workload movement

**What it doesn’t do:**  
- does not move data
- does not run cutovers
- does not modernize workloads

**Who benefits from it:**  
- architects
- project managers
- cloud onboarding teams
- stakeholders who need visibility

Migration Hub is especially useful on multi-server or multi-app migration projects where coordination matters.


---

### Who Performs the Migration?

Depending on the customer, migrations may be executed by:
- **AWS ProServe** — for large/complex migrations
- **AWS Partners (SI/MSP)** — consulting or managed service providers
- **The Customer** — internal IT/cloud teams using AWS tooling


---

### Who Handles Post-Migration Maintenance?

Operational responsibility typically falls into:
- **Customer-Owned Model** — customer manages access, lifecycle, retrieval, compliance, etc.
- **Partner-Managed MSP Model** — MSP handles operational tasks on customer’s behalf
- **AWS Enterprise Support / ProServe** — advisory + support, but not day-to-day data operations

> Note: AWS provides the infrastructure platform, not traditional MSP-style operations.

## 🧩 Athena + Glue — Real-World Takeaways

### 1. S3 as the Data Lake Storage Layer
Companies store raw data in S3 because it is:
- cheap
- durable
- scalable
- schema-flexible

This creates a **data lake**, but raw data alone is not queryable.

---

### 2. Athena = SQL Over S3 (Without Loading Data)
Athena allows teams to query S3 data using **standard SQL** with:
- no clusters to manage
- no ingestion step
- no idle cost
- pay-per-query pricing

Athena uses **Schema-on-Read**, meaning the data stays raw and schema is applied at query time.

Common use cases:
- ad-hoc analysis
- exploration
- forensics
- “what’s in this data?” discovery
- early BI analytics

---

### 3. AWS Glue = Metadata + Discovery + Optional ETL
Glue provides the **Data Catalog** that describes:
- table names
- columns and types
- file formats (e.g. JSON, CSV, Parquet)
- S3 locations
- partitions (e.g. by date)

This allows Athena to interpret files correctly.

Glue also offers:
- **Crawlers** for schema detection
- **ETL jobs** (Spark-based) for format conversion and transformation

ETL is optional at this stage and often introduced later for optimization.

---

### 4. Common Serverless Data Lake Pattern

A very common real-world pipeline looks like:

S3 (raw data)
→ Glue Data Catalog (metadata)
→ Athena (SQL queries)
→ QuickSight (visualization)


This pattern enables analytics with minimal infrastructure overhead.

---

### 5. When Redshift Enters the Picture
As queries become:
- frequent
- scheduled
- aggregated
- multi-user
- dashboarded

companies often introduce **Redshift** as the data warehouse for heavier workloads.

High-level relationship:
- **Athena** → exploratory + ad-hoc
- **Redshift** → production + warehouse

---

### 6. Operational Benefits
This stack reduces:
- infrastructure provisioning
- ETL requirements
- schema friction
- upfront cost

And accelerates:
- experimentation
- insight discovery
- time-to-analysis

---

### 7. One-Sentence Explanation
> Athena lets teams query raw data in S3 using SQL without running databases or clusters. Glue provides the table metadata so Athena can interpret the files. This is ideal for early analytics and forensics before adopting a heavier warehouse like Redshift.


