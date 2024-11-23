# SOC Automation Project

This project involves automating the Security Operations Center (SOC) environment using **Wazuh**, **Shuffle**, and **TheHive**.

---

## Project Overview

The goal of this project is to enhance SOC efficiency by integrating and automating critical processes through open-source tools. By leveraging Wazuh for threat detection, Shuffle for workflow automation, and TheHive for incident response, this setup aims to create a streamlined and responsive SOC environment.

---

## Tools Used

### Wazuh  

<img width="1680" alt="Screenshot 2024-11-18 at 18 58 57" src="https://github.com/user-attachments/assets/9be455fe-535b-4407-b3f2-cc2a69371be0">

**Wazuh** is a free, open-source security platform that unifies Extended Detection and Response (XDR) and Security Information and Event Management (SIEM) capabilities.  
Key Features:  
- **Threat Detection**: Identifies potential security threats across systems.  
- **Compliance**: Helps organizations meet regulatory and security compliance requirements.  
- **Incident Handling**: Aids in managing and responding to security incidents.  
- **Integrity Monitoring**: Tracks and monitors file and system integrity.  
- **Regulatory Compliance**: Ensures alignment with various regulatory frameworks.

---

### Shuffle  
<img width="1680" alt="Screenshot 2024-11-18 at 19 03 49" src="https://github.com/user-attachments/assets/f49a1e5d-5a96-40b1-b75a-6ea9a2579f81">

**Shuffle Automation** is an open-source platform designed to automate security processes and workflows.  
Key Features:  
- Allows the definition of automated workflows to improve infrastructure security.  
- Integrates with REST APIs of security tools, enabling seamless communication and action between them.  
- Enhances efficiency by automating repetitive tasks.

---

### TheHive  
<img width="1680" alt="Screenshot 2024-11-18 at 19 02 28" src="https://github.com/user-attachments/assets/e200e5c0-e50f-4992-9647-7c50fa0607f1">

**TheHive** is a free, open-source Security Incident Response Platform (SIRP) used for investigating and managing security incidents.  
Key Features:  
- Enables analysts to add observables to cases and use tags for categorization.  
- Facilitates the identification of Indicators of Compromise (IOCs).  
- Supports collaborative investigation and documentation of security incidents.  

---

## System Architecture  

Below is a diagrammatic representation of the intended setup:
<img width="1000" alt="Screenshot 2024-11-18 at 07 38 30" src="https://github.com/user-attachments/assets/85b663b8-bb2d-442e-afd4-4c95023e5699">



## Workflow

1. Event Collection
Wazuh Agents (installed on endpoints) continuously monitor systems for events.
Wazuh Agents send collected events to the Wazuh Manager.

<br>
<br>

2. Event Processing
The Wazuh Manager processes the received events.
If an event matches predefined rules or thresholds, the Wazuh Manager generates an alert.

<br>
<br>

3. Alert Forwarding
The Wazuh Manager forwards the alert to Shuffle for further processing.

<br>
<br>

4. Alert Enrichment
Shuffle receives the alert and performs enrichment, such as querying external threat intelligence sources to enrich Indicators of Compromise (IOCs).

<br>
<br>

5. Incident Management
Shuffle sends enriched alerts to TheHive, where they are categorized and managed as part of incident response workflows.

<br>
<br>

6. Analyst Notification
Shuffle sends a notification email to the Security Analyst, providing details of the alert.
<br>
<br>

7. Analyst Review and Response
The Security Analyst reviews the alert details and determines the appropriate response action.
The Security Analyst sends the response action to Shuffle.

<br>
<br>

9. Response Execution
Shuffle forwards the response action to the Wazuh Manager.
The Wazuh Manager executes the response action via the Wazuh Agents on the affected Windows clients.


### Setting Up the Environment

To begin the SOC automation project, the first step was to set up a virtualized Windows environment. Below are the steps taken:

---

#### 1. Installing VirtualBox  
VirtualBox was chosen as the virtualization platform due to its flexibility and ease of use.  
Steps:  
1. Downloaded the latest version of VirtualBox from the [official website](https://www.virtualbox.org/).  
2. Installed VirtualBox on the host machine by following the installation wizard.  

---

#### 2. Downloading the Windows 10 ISO  
To create a virtual machine, a Windows 10 ISO file was required.  
Steps:  
1. Downloaded the Windows 10 ISO file directly from the [Microsoft website](https://www.microsoft.com/en-us/software-download/windows10ISO).  
2. Verified the ISO file checksum to ensure integrity and authenticity.  

---

#### 3. Installing the Windows 10 Operating System  
Once VirtualBox and the Windows 10 ISO were ready, the next step was to install the operating system.  
Steps:  
1. Created a new virtual machine in VirtualBox and configured the following:  
   - **Name**: Win10
   - **Operating System Type**: Microsoft Windows  
   - **Version**: Windows 10 (64-bit)  
   - **Memory Allocation**: 4 GB (or adjusted based on system capacity)  
   - **Storage**: 50 GB dynamically allocated virtual hard disk.  
2. Mounted the downloaded Windows 10 ISO as the virtual machine's bootable media.  
3. Started the virtual machine and followed the Windows 10 installation wizard to complete the setup.

---

<img width="1009" alt="Screenshot 2024-11-18 at 10 54 34" src="https://github.com/user-attachments/assets/89dd10e4-5ec1-479c-992d-93182fea2e03">

#### Next, I downloaded and installed sysmon on the windows 10 using the Olaf Hartong configuration file.

<img width="1023" alt="Screenshot 2024-11-18 at 13 24 13" src="https://github.com/user-attachments/assets/98822163-2fa7-4c41-987b-a6ee4f631064">

#### After that I deploy the remaining virtual servers in the cloud using Digital Ocean

<img width="1680" alt="Screenshot 2024-11-18 at 18 47 37" src="https://github.com/user-attachments/assets/cf19ea34-2626-4eae-ac9d-928aa21b1085">
i deployed a  Ubuntu 22.04 (LTS) x64
Size
2 vCPUs
8GB / 160GB Disk




<br>
<br>

### Configuring Firewall Rules on the Ubuntu server

To secure the Ubuntu  virtual machine and limit access to trusted sources, new **Inbound Firewall Rules** were created to allow connections only from a specific IP address. This ensures that only authorized devices can connect to the server.
 

<br>
<br>
<img width="1680" alt="Screenshot 2024-11-18 at 18 40 18" src="https://github.com/user-attachments/assets/8da610aa-96cd-4789-a07b-c7d1faefd667">
<br>
<br>

I also added the Wazuh server to the firewall 

<img width="1680" alt="Screenshot 2024-11-18 at 19 31 54" src="https://github.com/user-attachments/assets/7d7a7664-1177-4999-921f-95029c2a211b">



Next, I SSH into the server using my terminal and updated all the Ubuntu

<img width="807" alt="Screenshot 2024-11-18 at 22 23 52" src="https://github.com/user-attachments/assets/2863556e-fd7b-49c1-b9f9-2fed723378a5">


After that, I install Wazuh on the Ubuntu Server
<img width="934" alt="Screenshot 2024-11-18 at 22 35 26" src="https://github.com/user-attachments/assets/b91dfbf7-34ea-40bd-a0c1-35ce4ab3bb50">


<br>
<br>
<img width="1680" alt="Screenshot 2024-11-18 at 22 47 56" src="https://github.com/user-attachments/assets/cb60104c-f596-45e7-8da0-ac62794fa852">



<br>
<br><br>
<br><br>
<br>

I also created another virtual server for the Thehive and added firewall rules
<img width="1675" alt="Screenshot 2024-11-20 at 08 04 15" src="https://github.com/user-attachments/assets/fdc5ac90-c944-42be-bdb4-f9b3046a9e92">


<img width="1626" alt="Screenshot 2024-11-20 at 08 13 51" src="https://github.com/user-attachments/assets/ee980b11-5aef-4bd7-b8ed-d6a1aef75716">



Next, I SSH into thehive virtual machine to install all the Prerequisites (Java, Cassandra and Elasticsearch) to get thehive up and running 

## Configurations 
After editing various configuration files in Elasticsearch, Cassandra and Thehive. I was finally able to get thehive up and running.
<img width="1680" alt="Screenshot 2024-11-20 at 10 05 07" src="https://github.com/user-attachments/assets/f0d29a45-faf3-4d1a-bd3e-35039934fce8">
<br><br>
<br><br><img width="1680" alt="Screenshot 2024-11-20 at 09 52 05" src="https://github.com/user-attachments/assets/8ad3ab76-437f-4ff5-97cb-2c74335cb994">




## Installing the Wazuh agent on the Windows 10 virtual machine  

<img width="1680" alt="Screenshot 2024-11-20 at 10 09 06" src="https://github.com/user-attachments/assets/493e2663-4030-47c6-aed3-be0abf5fbe42">

<img width="1680" alt="Screenshot 2024-11-20 at 10 21 40" src="https://github.com/user-attachments/assets/5dbf574a-0864-4c1e-b1e7-d6c069c6dd8d">





## Next I edited the ossec.conf file in Windows 10 where the wazuh agent was installed to enable me to INGEST SYSMON logs from Windows 10 to wazuh 

<img width="1037" alt="Screenshot 2024-11-21 at 19 13 19" src="https://github.com/user-attachments/assets/c4dc8ec0-edca-4270-9211-60eac568d709">



<br><br>
<br><br>
## Next I will try to detect MIMIKATZ  usage on Windows 10 using WAZUH, I downloaded mimikatz on the Win10 machine and had to exclude the download folder on the Windows Security cause by default windows security would not allow me to download a known malicious tool. 



<img width="1021" alt="Screenshot 2024-11-23 at 22 19 53" src="https://github.com/user-attachments/assets/3ced3113-ca76-45e7-b89c-99e89e7ab366">
<img width="1021" alt="Screenshot 2024-11-23 at 22 20 48" src="https://github.com/user-attachments/assets/bc87d863-e02e-402c-8eaf-091b5ef8c755">
<img width="1023" alt="Screenshot 2024-11-23 at 22 22 06" src="https://github.com/user-attachments/assets/80b58d34-772e-431d-8bae-9303cbab6513">
<br><br>
<br><br>

## By default Wazuh doesn't log everything so I had to make some changes to Wazuh manager's "ossec.conf" file so i logs everthing which will be saved in "archives.json".. On opeing the "archives.json" using the grep command i found the mimikatz process (after several hours of troubleshooting and restarting the wazuh-manager.service) 

<img width="1680" alt="Screenshot 2024-11-23 at 22 34 56" src="https://github.com/user-attachments/assets/1039d6ce-0950-4819-8266-7b56fc92f554">
<img width="1676" alt="Screenshot 2024-11-23 at 22 40 00" src="https://github.com/user-attachments/assets/3d8c8972-d754-4bbb-aa46-7a0a77db3a3e">
<img width="1680" alt="Screenshot 2024-11-23 at 22 43 14" src="https://github.com/user-attachments/assets/98dab445-7eb3-4b26-94ab-cf4b5bee2000">

## Conclusion 


This SOC automation project showcases the integration of powerful open-source tools to create a more efficient and scalable security environment. By automating workflows and incident response, the SOC can better handle modern cyber threats while reducing manual overhead.









