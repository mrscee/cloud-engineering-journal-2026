



# Connect to an EC2 Instance Using AWS Systems Manager (No SSH)

This guide walks through launching an EC2 instance and connecting to it securely using **AWS Systems Manager Session Manager**, without opening SSH or managing key pairs.

---

## Prerequisites

- An AWS account
- Permissions to manage EC2 and IAM resources

---

## Step 1: Launch an EC2 Instance

1. Sign in to the **AWS Management Console** and navigate to **EC2**.
2. Click **Launch instance**.
3. Select **Amazon Linux** (Free Tier eligible).
4. Choose the instance type **t3.micro**.
5. Under **Key pair (login)**, select **No key pair**.
6. Expand **Network settings** and click **Edit**.
7. Create a **new security group**.
8. Add an inbound rule:
   - **Type:** SSH  
   - **Source:** Anywhere (0.0.0.0/0)  
   > This rule is temporary and will be removed later.
9. Click **Launch instance**.

---

## Step 2: Attempt to Connect Using Session Manager

1. Select your new **EC2 instance**.
2. Click **Connect**.
3. Choose **Session Manager**.

You will see an alert stating that the **SSM Agent is not online**.  
This is expected because **Session Manager requires an IAM instance profile** to be attached to the instance.

---

## Step 3: Create an IAM Role for the EC2 Instance

1. With the instance selected, click **Actions**.
2. Navigate to **Security** → **Modify IAM role**.
3. Click **Create new IAM role**.
4. In the **Roles** page, click **Create role**.

---

## Step 4: Configure the Trusted Entity

1. For **Trusted entity type**, select **AWS service**.
2. For **Use case**, select **EC2**.
3. Click **Next**.

---

## Step 5: Attach the Systems Manager Policy

1. On the **Policies** page, search for **SSM**.
2. Select the policy **AmazonSSMManagedInstanceCore**.
3. Click **Next**.

---

## Step 6: Name and Create the Role

1. Enter a **role name**.
2. Scroll to the bottom of the page.
3. Click **Create role**.

---

## Step 7: Verify the Role Permissions

1. Return to the **IAM Roles** page.
2. Search for the role you just created.
3. Click the role.
4. Verify that **AmazonSSMManagedInstanceCore** is attached.

---

## Step 8: Attach the Role to the EC2 Instance

1. Return to the **Modify IAM role** page for your EC2 instance.
2. From the **IAM role** dropdown, select the new role.
3. Click **Update IAM role**.

---

## Step 9: Wait for IAM Role Initialization

If you attempt to connect immediately, the connection may still fail.  
This is normal — it takes a few minutes for the **IAM role and SSM Agent** to initialize.

---

## Step 10: Remove SSH Access (Security Best Practice)

While waiting for initialization:

1. Navigate to the **Security Groups** attached to your EC2 instance.
2. Edit the **Inbound rules**.
3. Delete the **SSH (port 22)** rule.
4. Save the changes.

Removing SSH prevents inbound access over port 22 and improves overall security.

---

## Step 11: Connect Using Session Manager

1. Return to the EC2 instance **Connect** page.
2. Select **Session Manager**.
3. Click **Connect**.

You should now be able to connect successfully.

---

## Step 12: Confirm the Connection

Once connected, you will see a terminal prompt similar to:


