“From On-Prem to the Cloud”
An S3 Static Website Use Case:
![Screenshot with article graphic](./assets/articlepic2.jpeg)

By Comfort Benton | Cloud DevOps Engineer
Press enter or click to view image in full size

🟦 CASE OVERVIEW | Migrating a Static Website to AWS S3

I’ve been asked to migrate the marketing website for Level Up Bank, a fictional online financial institution, from on-premises to the cloud. The original website lived on a physical server that the company had to maintain, patch, and pay for itself. That setup works in the beginning, but over time, it becomes expensive, harder to scale, and slower for customers visiting the site from different regions.

The website itself was informational. It did not include login features, custom dashboards, or any server-side processing. In cloud terms, that makes it a static website, meaning it can be delivered as plain files without needing servers or databases running in the background.

My goal for this project was to move the site into AWS in a way that would reduce cost, improve availability, enhance performance, and require less ongoing maintenance. I also wanted to explore how global content delivery and secure access could be achieved without complicating the architecture.

🟦 PROJECT PHASES

This deployment can be broken down into three stages, each one building on the last:

Foundational — Host the static website using Amazon S3
Performance — Add CloudFront for global delivery and HTTPS
Security — Block direct S3 access and enforce CloudFront as the entry point

🟦 FOUNDATIONAL — Host the Website Using Amazon S3

Create the bucket

1. In the AWS Console, search S3

2. On the landing page, click Create bucket

3. Enter a unique “Bucket name,” with no spaces. For example, I chose lubank-website-s3

4. Leave all other defaulted items as is and click Create bucket the bottom

Upload file to bucket

5. Select your newly created bucket to then upload

the static website index.html file provided. You can click Add files

or you can drag-and-drop the file, click Upload, and close.

Modify bucket to host a static website

6. On the new bucket page, select the “Properties” tab, look for “Static website hosting” and click Edit to Enable


7. On that page, specify your uploaded .html file as the “Index document” and click Save changes

8. At the bottom of the page you will see you now have, although still blocked, a link to the page.

Press enter or click to view image in full size

Enable public access

9. Go back to the top of the new bucket page, select the “Permissions” tab. In “Block public access (bucket settings)” click Edit to deselect “Block all public access” and click Save changes

10. Just below is “Bucket Policy”, where I added code written in JSON to grant public read access to the bucket using the bucket ARN in code and Save Changes. Various bucket policies can be found with a quick online search.

Press enter or click to view image in full size

{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::lubank-website-s3/*"
        }
    ]
}

11. Now, under the “Properties” tab, our endpoint link can be seen by the public:

Press enter or click to view image in full size

Press enter or click to view image in full size

🟦 FOUNDATIONAL WRAP-UP

With the foundational work completed, the Level Up Bank website was officially live on the public internet using nothing more than S3’s built-in static hosting feature. There were no servers to manage, no auto-scaling groups to configure, and no operating systems to patch or maintain. AWS handled the storage, durability, and availability of the website without requiring any additional infrastructure.

This established the baseline experience. The site was hosted, reachable, and served over HTTP without any compute resources involved. With the site now operational, the next engineering focus becomes performance and security hardening through CloudFront and HTTPS.

***
