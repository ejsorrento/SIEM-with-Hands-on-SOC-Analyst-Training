# SIEM-with-Hands-on-SOC-Analyst-Training![siem-image-wp](https://github.com/user-attachments/assets/ad692c7d-fce2-4e56-8fbb-2e54d3268fbd)

The overall goal of this lab was to gain experience pushing Nmap scan data up to a SIEM through an agent attached to a virtual machine. The SIEM is built through Elastic and the virtual machine is built with a Kali Linux ISO file. Then finally to attach alerts to each Nmap scan that will send an alert to email.

**Overview of tasks:**

-Set up a free trial of Elastic account.

-Install the Kali Linux VM.

-Configure the Elastic Agent on the Linux VM to collect the logs and forward them to the SIEM.

-Generate security events on the Kali VM.

-Query to find the security events in the Elastic SIEM.

-Create a Dashboard to visualize security events.

-Create email alerts for security events.

**Step 1: Set up an Elastic account**
In order to begin, we'll need to set upa free account to set up a cloud Elastic instance to run the SIEM on.

1. Sign up for free trial of Elastic Cloud - https://cloud.elastic.co/registration
2. Log into Elastic Cloud console - https://cloud.elastic.co.
3. "Click "Start your free trial."
4. Click “Create Deployment”, then “Elasticsearch” as the deployment type.
5. Choose a region and deployment size that fits your needs and click on “Create Deployment.”
6. Wait for the configuration to complete.
7. Once the deployment is ready, click “continue.”

**Step 2: Setting up the Kali Linux VM**

Next, we'll need to set up the Kali Linux VM. You can use any Linux OS and virtualization software for this, but I’ll be using Kali Linux and Oracle VirtualBox.

**Set up instructions:**

1. Go to official Kali website and download Kali Linux VM file - https://www.kali.org/get-kali/#kali-virtual-machines.
2. Create a new virtual machine in input the Kali VM file in either VirtualBox or VMware. For the purposes of this writeup, I will be utilizing VirtualBox.
3. Start the VM and follow the prompts to set up Kali Linux.
4. Upon landing at the credentials screen, log using "kali" for both the username and password.

If you encounter trouble during this step, utilize YouTube for "creating a virtual machine using VirtualBox/VMware with a Kali Linux VM file"

**Step 3: Setting up the Elastic Agent to Collect Logs**

Brief overview of an agent: An agent is a software program that is installed on a device, such a server or an endpoint, to collect and send data to a centralized system for analysis and monitoring. In the context of Elastic SIEM, an agent is used to collect and forward security-related events from your endpoints to your Elastic SIEM instance.

**Steps to set up agent to collect logs from Kali VM and forward them to your Elastic SIEM instance:**

1. Elastic SIEM instance and navigate to the Integrations page by clicking on the Kibana main menu bar on the top left, then selecting "integrations" at the bottom.

![1_OFaFyshfXVJkheFmGEsuwg](https://github.com/user-attachments/assets/9a052f5e-0f94-4797-9d8f-2e8936d434a1)


2. Search for “Elastic Defend” and click on it to open the integration page.

![2_StUpb5eGGZ5SzIbURBqCLA](https://github.com/user-attachments/assets/13978a48-88c0-40ba-8cb4-54c96e970abc)

3. Click on “Install Elastic Defend” and follow the instructions provided on the integration page to install the agent on your Kali VM.

![3_5sbyyzQSDj0y5oOQEgTUSQ](https://github.com/user-attachments/assets/1645d209-592b-465c-ac88-2359895267f5)

![4_AMG0J_a1m1R7LGCjrFtIZw](https://github.com/user-attachments/assets/e7ab77e6-551f-4caa-a73b-a764b76379f6)
