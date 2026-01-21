# CloudWatch CPU Utilization Visualization (By Environment)

In this lab I created a way to visualize CPU utilization for EC2 instances in an AWS account. I used CloudWatch to build a dashboard and then used Metric Explorer to filter and aggregate CPU utilization by environment.

---

## Steps Performed

### **1. Create the CloudWatch Dashboard**

- Open **CloudWatch → Dashboards**
- Click **Create dashboard**
- Enter the dashboard name used in the lab: `my-ec2-dashboard`
- Click **Create dashboard**
- When prompted to add a widget, skip this step for now

---

### **2. Open Metric Explorer**

- From the left navigation panel select:
  - **Metrics → Explorer**

---

### **3. Select CPU Utilization Metric and Apply Environment Tag Filter**

- In the **Metrics** search bar type:
  - `CPUUtilization`
- Choose:
  - **EC2 Instance: CPUUtilization**
- Under **From**, choose a tag and select:
  - `Environment = Prod`

---

### **4. Aggregate CPU Utilization Using Average**

- Under **Aggregate by**
- Select:
  - **Average**
- This combines CPU utilization from all EC2 instances tagged with `Environment = Prod`

---

### **5. Configure Graph Layout Settings**

- Under **Graph options**
- Set:
  - **Layout:** `1 column × 1 row`

---

### **6. Add to Dashboard**

- Click **Add to dashboard**
- Select the dashboard created in Step 1
- Confirm the widget appears on the dashboard

---

## Result

I successfully visualized CPU utilization for EC2 instances by environment. Using Metric Explorer I:

- Queried the CPUUtilization metric for EC2
- Filtered by `Environment = Prod`
- Aggregated values using the **Average** statistic
- Configured a **1×1 layout**
- Added the resulting graph to my CloudWatch dashboard

This produced a single widget showing the average CPU utilization trend for all production EC2 instances, making it easier to monitor performance at an environment level.

---

## Screenshot

`CW–EC2–explorer–metric.png`


