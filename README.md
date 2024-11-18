# SOC Automation Project

This project involves automating the Security Operations Center (SOC) environment using **Wazuh**, **Shuffle**, and **TheHive**.

---

## Project Overview

The goal of this project is to enhance SOC efficiency by integrating and automating critical processes through open-source tools. By leveraging Wazuh for threat detection, Shuffle for workflow automation, and TheHive for incident response, this setup aims to create a streamlined and responsive SOC environment.

---

## Tools Used

### Wazuh  
**Wazuh** is a free, open-source security platform that unifies Extended Detection and Response (XDR) and Security Information and Event Management (SIEM) capabilities.  
Key Features:  
- **Threat Detection**: Identifies potential security threats across systems.  
- **Compliance**: Helps organizations meet regulatory and security compliance requirements.  
- **Incident Handling**: Aids in managing and responding to security incidents.  
- **Integrity Monitoring**: Tracks and monitors file and system integrity.  
- **Regulatory Compliance**: Ensures alignment with various regulatory frameworks.

---

### Shuffle  
**Shuffle Automation** is an open-source platform designed to automate security processes and workflows.  
Key Features:  
- Allows the definition of automated workflows to improve infrastructure security.  
- Integrates with REST APIs of security tools, enabling seamless communication and action between them.  
- Enhances efficiency by automating repetitive tasks.

---

### TheHive  
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



## Conclusion  

This SOC automation project showcases the integration of powerful open-source tools to create a more efficient and scalable security environment. By automating workflows and incident response, the SOC can better handle modern cyber threats while reducing manual overhead.









