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
