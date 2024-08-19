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

_Note: Select and copy above command onto clipboard._

4. Paste command into the Kali terminal.
<img width="1280" alt="Screen Shot 2024-05-02 at 1 14 27 PM" src="https://github.com/user-attachments/assets/6ca7f6e2-dbef-4ee9-8be9-e6087fd0b3fd">

5. Agent installation can take a few minutes, upon completion, you’ll see a message that says “Elastic Agent has been successfully installed.” It will automatically start collecting and forwarding logs to your Elastic SIEM instance, although it might take a few minutes for the logs to appear in the SIEM.

![5_UEF1sm6RNxXbMrCw_3eNkQ](https://github.com/user-attachments/assets/9e99cb4e-f56f-47ba-b7a9-3a6374987f46)

Verify that the agent has been installed correctly by running this command: sudo systemctl status elastic-agent.service

<img width="603" alt="Screen Shot 2024-05-02 at 1 14 46 PM" src="https://github.com/user-attachments/assets/8ae0248b-b4db-4f10-bd95-261bf6c8eaa5">

_To troubleshoot an error with installing the agent, test that Kali is connected to the internet by pinging google.com_

**Step 4: Generating Security Events on Kali Linux VM**

We'll now verify that the agent is working correctly by generating some security-related events on the Kali VM. In order to do this, we will use Nmap (Network Mapper). Nmap is a free, open-source utility used for network exploration, management, and security auditing. It is designed to discover hosts and services on a computer network, thus creating a “map” of the network. Nmap can be used to scan hosts for open ports, determine the operating system and software running on the target system, and gather other information about the network.

**Follow these steps in order to run Nmap:**

1. Nmap comes pre-installed into Kali Linux, therefore, it is unneccessary to install. If you are not utilizing Kali, open a new Terminal and run this command to install it: sudo apt-get install nmap.

2. Run a scan on Kali machine by running the command: sudo nmap <vm-ip>. You can also run a scan of your host machine if you place your Kali VM on a “bridged” network.

![6_g9YjaeWzuZDCFTMQ_wzQhQ](https://github.com/user-attachments/assets/35af6009-7bf8-4769-ab3f-3131eed49409)

_Nmap scan of my host machine._

3. This scan generates several security events, such as the detection of open ports and the identification of services running on those ports. Run a few more Nmap scans (“nmap -sS <ip address>”, “nmap -sT <ip address>”, “nmap -p- <ip address>”etc..”

<img width="527" alt="Screen Shot 2024-05-02 at 1 15 26 PM" src="https://github.com/user-attachments/assets/1b6e2e21-d098-450d-a165-4dca11b50a8b">

![7_6zTYVC4FAYskyfVgJO6bTQ](https://github.com/user-attachments/assets/06e25cea-d089-4c8e-9725-817660477d8f)

**Step 5: Querying for Security Events in Elastic SIEM**

Now with the forwarded data to the SIEM from the Kali VM, we can begin querying and analyzing the SIEM logs.

**Follow these steps:**

1. In the Elastic Deployment, click the hamburger menu in the top left, then click "Logs" under "Observability"to view the logs from the Kali VM.

![8_AHJpiV6UBsbz9BNnQptTkA](https://github.com/user-attachments/assets/38e60984-216b-4ed4-bc52-3e8f69754da2)

2. In the search bar, enter a search query to filter the logs. For example, to search for all logs related to Nmap scans, enter the query: event.action:
“nmap_scan” or process.args: “sudo”. Execute the search query. Note that it could take a bit of time for the queries populate within the SIEM.

3. The query results will be displayed in the table. Click the three dots next to each event to see more details.

![9_uCQQRrAFde7b-qg27415hA](https://github.com/user-attachments/assets/34d851d5-7721-45e4-95f1-2224fce13610)

![10_Hyf_7WS1lV6JSX02w69iEg](https://github.com/user-attachments/assets/bfe7ec23-1962-4310-a636-13b1f0ae0f1e)

By generating and analyzing different types of security events in Elastic SIEM like the one above, or generating authentication failures by typing in the wrong password for a user or attempting SSH logins an incorrect password, you can gain a better understanding of how security incidents are detected, investigated, and responded to in real-world environments.

**Step 6: Create a Dashboard to Visualize the Events**

Visualizations and Dashboards in the SIEM app can be used analyze the logs and identify patterns or anomalies in the data. For example, you can create a simple dashboard that shows a count of security events over time.

This is done by:

1. Navigating to the Elastic web portal - https://cloud.elastic.co/.
2. Click on the hamburger menu, then "Analytics", the click on "Dashboards".

![11_xnDZLOaAgmHSzT8Fr5vgSw](https://github.com/user-attachments/assets/9cf36b4d-041b-4384-a68a-9cb9b222331d)

3. Click the “Create dashboard” button on the top right to create a new dashboard.

4. Click the "Create Visualization" button to add a new visualization to the dashboard

5. Select the visualization type of either "Area" or "Line", based on your preference. This will create a chart that shows the count of events over time.

![12_SHUc8PSWdr_19z6n73QF0A](https://github.com/user-attachments/assets/f54a0a9d-019f-408c-8917-d8795f0b823a)

6. On the right of the visualization editor, locate a "Metrics" dropdown menu and select "Timestamp" for the horizontal field and "Count" for the vertical field. Each instance or event will now be counted.

![13_ZBJ3X5M94mo8rQoTZqu-6w](https://github.com/user-attachments/assets/a98e9b63-b473-4261-8114-9c31999aa3f5)

![14_Esjo2Aljf2vbhsgS3mNXRw](https://github.com/user-attachments/assets/d89b36a2-e1f9-4928-8041-903190499f3f)

![15_odXMlW_xItFgVUU2XEDTGQ](https://github.com/user-attachments/assets/1fa0eeff-e5fe-4ed6-8214-5c3718e39b2f)
_Make sure to click "close" to save changes_

7. Click the "Save and return" button in the top right to complete the rest of the settings

![16_N3rTTklO-Nlu4mksJbMX3w](https://github.com/user-attachments/assets/ef205a98-aeba-48a5-b2da-3518c59eab94)

**Step 7: Create an Alert**

SIEM alerts are a critical component in detecting security incidents and responding to them in a timely manner Alerts can be configured based on predefined rules and customer quieries, and can be configured to trigger specific actions when certain conditions are met. We will walk through the steps in creating alerts in the Elastic SIEM instance in order to detect Nmap scans. You will be able to create an alert that monitors logs for Nmap scan events and then generate a notification, in this case we will choose an email.

1. Click on the hamburger menu in the top left, then "Security, and then "Alerts".

2. Next, click "Manage rules" in the top right

![17_fo_0LV1O9EdRkKTdPLIotw](https://github.com/user-attachments/assets/b5abef59-0462-49cd-b093-5739c15c2dd9)

3. Click the "Create a new rule" button in the top right.

4. Navigate to the "Define rule" sections and select "Custom query" from the dropdown menu.

5. Set the conditions for the rule under "Custom query". The following query can be used to detect Nmap scan events.

![18_k_pLOknQWj9n91d3ep0IRA](https://github.com/user-attachments/assets/e970ad69-93be-408a-8570-b11f47c837d6)

_This query will match all events with the action “nmap_scan.” Then click “Continue.”_

6. Give the rule a name and a description under the "About Rule section. Choose something for both that gives another person a clear understanding of the purpose of this rule, for example, "Nmap Scan Detection", "This rule exists to generate a notification for each time an Nmap scan is detected.".

7. Remeber to set the severity level for the alert in order to aid in the prioritzation of alerts based on their importance. Disregard all other default settings for the time being under "Schedule rule" and click "Continue".

![19_F5tRVabgbkE0IWSyWyRaIQ](https://github.com/user-attachments/assets/9b40c704-0d7d-49f9-9ea0-c167ec695220)

8. Navigate the "Actions" section and select the action you're looking for when the rule is triggered. In this case, we'll be setting up email notification, other options include a notification by Slack message or to trigger a custom webhook.

9. Finish creating the alert by clicking the "Create and enable rule" button.


![20_duyt56mJ__eBne9eSVsVsg](https://github.com/user-attachments/assets/f3279b9e-3849-4b49-936e-12868711da26)

Now that this alert has been created, it will monitor your logs for Nmap scan events. Once an Nmap scan event is identified, the alert will be triggered and an email notification will be sent. Manage alerts under the "Alerts" section under "Security".

**Epilogue**
We've successfuly set up a home lab utilizing Elastic SIEM and a Kali Linux VM. We then transmitted data from the Kali VM to the SIEM using the Elastic Beats agent, generating security events from the Kali VM using Nmap, then queried and analyzed the logs in the SIEM using the Elastic web interface. Then we also created a dashboard to visualize security events and created an alert to detect security events.

This lab provides a beneficial place for learning and practicing the necessary skills for effective security monitoring and incident response using Elastic SIEM. By following these steps, you gain hands-on experience with a SIEM and improve your security monitoring skills in order to become a successful security analyst.

**Moving Forward**
• Attempt to generate differetn types of security events on your new Kali Linux VM and the querying into the Elastic SIEM.

• Test the alert that you created by generating Nmap scans on the Kali VM.

•Explore different analysis and visualization tools provided by Elastic SIEM to better understand and analyze your security logs. The more practice with these tools, the efficient you can become at detecting and responding to security threats.

•Dive into different types of integrations and data sources available for Elastic SIEM, such as integrating with cloud providers like AWS or Azure, and collecting data from different log sources like Windows event logs or syslogs. As you continue learning, your knowledge of Elastic SIEM will continue to grow.

Thank you for taking the time to read this write up of my homelab project.
