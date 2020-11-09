# <center>Security Patching of EC2 Instances</center> 

### Aim:

The Aim is to do the Security Patching on EC2 Instances. The solution uses AWS SSM Patch Manager and AWS SSM Automation.

### Solution Architecture:

> Below is the high-level overview for the solution

<br />

![Patching Architecture](/images/patching-architecture.png)


### Solution Approach:

The approach for the Solution would be:

1. The admin installs the SSM agent on the EC2 Instance.
2. The admin creates a custom baseline where only Security Patches would get selected.
3. The admin patches the EC2 Instance using the Patch Manager in SSM. 


### Prerequisites:

1. SSM should be installed and running on the instances which need to be patched.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
[Click Here for AWS SSM Installation Documentation](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-manual-agent-install.html)
<br />

2. Custom Patch Baseline should be created where we define to use Security Patches only

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; [Click Here for AWS Custom Patch Baseline Documentation](https://docs.aws.amazon.com/systems-manager/latest/userguide/create-baseline-console-linux.html)

<br />
<br />

## Steps to setup the solution:
***


##### Step-1: Go to AWS System Manager: 
![Patching Architecture](/images/ssm-1.png)
<br />
<br />

##### Step-2: Scroll down to Patch Manager and click on Configure Patching:

<br />

![Patching Architecture](/images/ssm-2.png)
<br />
<br />

##### Step-3: Enter the Instance Tags that need to be patched and click on add:
<br />

![Patching Architecture](/images/ssm-3.png)
<br />
<br />

##### Step-4: Scroll down and Select “skip scheduling and patch instances now”, “Scan and install” and Configuring patching:
<br />

![Patching Architecture](/images/ssm-4.png)
<br />
<br />

## How to Patch an Auto Scaling Image (Golden Image Creation Process):
***

### Prerequisites for Creating Golden AMI:

1. The Source AMI ID
2. IamInstanceProfileName
3. IAM Role

## How to create IAM Instance Profile for Golden Image process:
1. Three policies are required to create IAMInstanceProfile
  - AmazonEC2RoleforSSM
  - AmazonSSMAutomationRole
  - Inline Policy "SSMAutomationServiceRolePolicy"

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": "iam:PassRole",
            "Resource": "arn:aws:iam::989033863264:role/SSMRoleForAutomation"
        }
    ]
}

``` 

2. In Trust Relationship, below access should be granted.

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "",
      "Effect": "Allow",
      "Principal": {
        "Service": [
          "ssm.amazonaws.com",
          "ec2.amazonaws.com"
        ]
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```


<br />



## Steps to create Golden AMI:
***


##### Step-1: Go to AWS System Manager: 
![Patching Architecture](/images/ssm-automation-1.png)
<br />
<br />

##### Step-2: Scroll down to Automation

<br />

![Patching Architecture](/images/ssm-automation-2.png)
<br />
<br />

##### Step-3: Click on Execute automation:

<br />

![Patching Architecture](/images/ssm-automation-3.png)
<br />
<br />

##### Step-4: In Automation document, seach for “Document name prefix : Equals : AWS-Update”

<br />

![Patching Architecture](/images/ssm-automation-4.png)
<br />
<br />

##### Step-5: Click on AWS-UpdateLinuxAmi

<br />

![Patching Architecture](/images/ssm-automation-5.png)
<br />
<br />

##### Step-6: Click on Execute automation:

<br />

![Patching Architecture](/images/ssm-automation-6.png)
<br />
<br />

##### Step-7: In Input parameters, fill SourceAmiId, IamInstanceProfileName and AutomationAssumeRole and click on Execute

<br />

![Patching Architecture](/images/ssm-automation-7.png)
<br />
<br />

##### Step-8: It will trigger all the Execution Steps and take a few minutes to get completed.

<br />

![Patching Architecture](/images/ssm-automation-8.png)
<br />
<br />

## Verification of the Golden AMI:

<br />
<br />

##### Step-9: Scroll down and click on createImage section

<br />

![Patching Architecture](/images/ssm-automation-9.png)
<br />
<br />

##### Step-10: Scroll down to the Ouputs Section and copy the AMI ID

<br />

![Patching Architecture](/images/ssm-automation-10.png)
<br />
<br />

##### Step-11: Search the AMI Id in the EC2-AMI section

<br />

![Patching Architecture](/images/ssm-automation-11.png)
<br />
<br />




### FAQ: 

1. **What is Patch Management:**<br>
Patch Management is the process by which businesses/IT procure, test, and install patches (changes in code or data) intended to upgrade, optimize, or secure existing software, computers, servers and technology systems to maintain operational efficacy or mitigate security vulnerabilities.

2. **Why Patching is needed?**<br>
Prompt patching is vital for cybersecurity. When a new patch is released, attackers use software that looks at the underlying vulnerability in the application being patched. This is something that hackers perform quickly, allowing them to release malware to exploit the vulnerability within hours of a patch release. Security patches prevent hackers and cybercriminals from exploiting vulnerabilities that could halt operations.

3. **What types of Patches we will be intalling into the server?**<br>
We will be installing only Security Patches as the other Patches installation might disrupt the application flow.

4. **Is Patching mandatory for all the MSP Customers?**<br>
Yes, but if the customer doesn't approve of this, then we can skip this process for that particular customer.

5. **How to initiate Patcing for any customer?**<br>
Patching initiation process includes 3 action/discussion points:
- Discussion with DEV Team.
- Discussion with Application Team.
- Discussion with Customer. 

6. **Is Patchig Calendar should be maintained?**<br>
Yes, It is good to have Patching Calendar in place.

7. **Is Downtime there in the Patching process?**<br>
Yes, Patching process requires rebooting the EC2 Instance and it will lead to a downtime.

8. **Are Pre and Post Patching Validation necessary?**<br>
Yes.

9. **Does Patching invlolve costing?**<br>
No, SSM Patch Manager and Automation are free AWS Services. 











