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

<br />

## Steps to create Golden AMI:
***


##### Step-1: Go to AWS System Manager: 
![Patching Architecture](/images/ssm-1.png)
<br />
<br />

##### Step-2: Scroll down to Automation

<br />

![Patching Architecture](/images/ssm-2.png)
<br />
<br />

##### Step-3: Scroll down to Automation

<br />

![Patching Architecture](/images/ssm-2.png)
<br />
<br />

##### Step-4: Scroll down to Automation

<br />

![Patching Architecture](/images/ssm-2.png)
<br />
<br />

##### Step-5: Scroll down to Automation

<br />

![Patching Architecture](/images/ssm-2.png)
<br />
<br />

##### Step-6: Scroll down to Automation

<br />

![Patching Architecture](/images/ssm-2.png)
<br />
<br />

##### Step-7: Scroll down to Automation

<br />

![Patching Architecture](/images/ssm-2.png)
<br />
<br />

##### Step-8: Scroll down to Automation

<br />

![Patching Architecture](/images/ssm-2.png)
<br />
<br />

##### Step-9: Scroll down to Automation

<br />

![Patching Architecture](/images/ssm-2.png)
<br />
<br />

##### Step-10: Scroll down to Automation

<br />

![Patching Architecture](/images/ssm-2.png)
<br />
<br />

##### Step-11: Scroll down to Automation

<br />

![Patching Architecture](/images/ssm-2.png)
<br />
<br />




### FAQ: 

1. Why Patching is needed?
2. What types of Patches we will intall into the server?
3. Is Patching mandatory for all the MSP Customers?
4. How to initiate Patcing for any customer?
5. Is Patchig Calendar should be maintained?
6. Is Downtime there in the Patching process?
7. How is the Approval Flow of Patching?
8. Are Pre and Post Patching Validation necessary?
9. Does Patching invlolve costing?











