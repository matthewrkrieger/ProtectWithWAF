Pre-requisites
==============

- A computer with Chrome
- An RDP Client
- An AWS EC2 Key Pair
- Optional - git

Lab Prep -- Launch Cloudformation Stacks Setup
==============================================

(Estimated completion time -- 35 minutes)

Lab preparation will take some time to complete, so we recommend that
you initiate this and let it complete in the background.

Web Carter & Attacker workstation setup
---------------------------------------

1.  Open the Cloudformation console

![](.//media/image10.png)    

2.  Create a new stack

![](.//media/image11.png)

3.  Upload stack template **template/webcarter-attacker-template.yaml**

![](.//media/image12.png)

4.  Enter a stack name -- e.g. "WAF-Lab-WebCarter"

![](.//media/image13.png)

5.  Get your IP from Amazon checkip -> http://checkip.amazonaws.com/.

![](.//media/image7.png)


6.  Enter the environmental configurations for the stack

    a.  Your IP address from above

    b.  An SSH in your inventory from EC2

    c.  An environment tag (e.g. DEV or TEST or PROD)

![](.//media/image14.png)

7.  Enter passwords for the following credentials. Passwords should be at least 8 characters long:

    d.  RDS instance master password

    e.  RDS database password

    f.  Admin password

    g.  Test user password

Scroll to the bottom of the page and hit **Next**

![](.//media/image15.png)

8.  Scroll to the bottom of the page and hit **Next** on *Configure
    stack options* page

9.  Scroll to the bottom of the page and check **I acknowledge that AWS
    CloudFormation might create IAM resources.**, the click **Create**

![](.//media/image16.png)

10.  The stack will eventually turn to CREATE\_COMPLETE.

11. Go to the stack’s "Output" and copy value of the webCarterALBAccessLogBucket. It will be used as a parameter in the next CloudFormation stack:

![](.//media/image17.png)


WAF Automation And Dashboard Setup
----------------------------------

This Cloudformation stack will stand up the automation for managing WAF
and the dashboards.

1.  Open the CloudFormation console

![](.//media/image1.png)    

2.  Create a new stack

![](.//media/image2.png)

3.  Upload the template

`template/aws-waf-security-automations-template.yaml`

![](.//media/image3.png)

4.  Enter a new stack name in **all lowercase** -- e.g. waf-lab

![](.//media/image4.png)

5.  Update Scanner & Probe Protection to "yes -- Amazon Athena log parser":

![](.//media/image5.png)

6.  Enter the S3 bucket name saved in the Web Carter and Attaker stack's output (webCarterALBAccessLogBucket):

![](.//media/image6.png)

7.  Enter your IP + "/32" for the attacker's allowed ingress IP address in the Cloudformation form. Please replace 0.0.0.0/0 in these instructions with your IP address:

![](.//media/image8.png)    

8.  Scroll to the bottom of the page and hit **Next**.

9. Hit **Next** on "Configure stack options"

10. Scroll to the bottom of the page. Check **I acknowledge that AWS CloudFormation might create IAM resources with custom names.** and **I acknowledge that AWS Cloudformation might require the following capability: CAPABILITY\_AUTO\_EXPAND**, then click "Create"

![](.//media/image9.png)

11. The stack will eventually turn to CREATE\_COMPLETE.

