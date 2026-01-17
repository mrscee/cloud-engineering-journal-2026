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
