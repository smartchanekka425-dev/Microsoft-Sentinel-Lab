# Microsoft-Sentinel-Lab
## Project Overview
This project demonstrates the deployment and configuration of a Microsoft Sentinel SIEM environment in Azure. A Windows Server 2022 virtual machine was deployed, onboarded with the Azure Monitor Agent (AMA), connected to Microsoft Sentinel, and configured to collect Windows Security Events. Custom analytics rules were created to detect failed login attempts and generate security incidents for investigation.

Technologies Used

Microsoft Sentinel
Azure Virtual Machines
Azure Monitor Agent (AMA)
Log Analytics Workspace
KQL (Kusto Query Language)
Windows Server 2022

## Architecture Diagram
This diagram illustrates the flow of security logs from the Windows VM through Azure Monitor Agent into Log Analytics and Microsoft Sentinel, where analytics rules generate security incidents.

Components

Windows Server 2022 VM
Azure Monitor Agent
Log Analytics Workspace
Microsoft Sentinel
Analytics Rule (Event ID 4625)
Security Incident

## VM Deployment
A Windows Server 2022 virtual machine was deployed in Azure to simulate a production endpoint and generate security events.

Configuration

VM Name: Sentinel-VM01
Operating System: Windows Server 2022
Region: East US 2
RDP Enabled
Public IP Assigned

## Azure Monitor Agent Installation
The Azure Monitor Agent (AMA) was installed on the Windows VM to collect security logs and send them to the Log Analytics workspace.

Tasks Completed

Installed Azure Monitor Agent
Verified agent deployment
Confirmed successful extension installation

## Windows Security Events Connector
The Windows Security Events via AMA connector was enabled in Microsoft Sentinel.

Tasks Completed

Installed Windows Security Events solution
Created Data Collection Rule (DCR)
Associated VM with DCR
Confirmed connector status as Connected

## Log Collection Verification
Security logs were successfully ingested into the Log Analytics workspace from the Windows VM.

Verification

SecurityEvent table populated
Events received from Sentinel-VM01
Logs visible in Log Analytics

SecurityEvent
| take 20

## Failed Log Detection Rule
A custom Scheduled Analytics Rule was created to detect failed Windows login attempts (Event ID 4625).

Rule Configuration

Rule Name: Failed Login Detection
Severity: Medium
Data Source: SecurityEvent
Event ID: 4625

SecurityEvent
| where EventID == 4625
| sort by TimeGenerated desc

## Incident Investigation
After generating failed login attempts, Microsoft Sentinel created a security incident for investigation.

Investigation Tasks

Reviewed incident details
Examined affected host
Identified source account
Analyzed event timeline
Reviewed Event ID 4625 logs

## KQL Queries
Failed Log in Events
--SecurityEvent
| where EventID == 4625
| sort by TimeGenerated desc

Successful Log in Events
SecurityEvent
| where EventID == 4624
| sort by TimeGenerated desc

Top Failed Login Accounts
SecurityEvent
| where EventID == 4625
| summarize Count=count() by Account
| order by Count desc

Events By Computer
SecurityEvent
| summarize Count=count() by Computer


## Lessons Learned
--Through this project I gained hands-on experience with:

Microsoft Sentinel deployment and configuration
Azure Monitor Agent (AMA)
Data Collection Rules (DCR)
Windows Security Event collection
KQL query development
Security incident detection and investigation
SIEM monitoring workflows
Azure security monitoring best practices

## Screenshots
