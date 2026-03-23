☁️ Microsoft Sentinel: Cloud SOC & Detection Engineering
Azure Security | Kusto Query Language (KQL) | Threat Response

This repository is a dedicated portfolio of Microsoft Sentinel labs. It focuses on cloud-native security operations, including log ingestion, detection rule engineering, and incident response within the Azure ecosystem.

🔬 Active Detection Labs (Lab Name - Primary Focus - Key Outcome - Status)
RDP Brute Force Detection - External Attack Surface - Automated Incident Generation (4625/4740) - Compelete
Persistence MonitoringInternal Registry/Task Changes - Custom Azure Workbook Visualization - Complete


🛠️ Microsoft Sentinel Technical Stack
SIEM/SOAR: Microsoft Sentinel (Incidents, Automation, Hunting).
Logs: Log Analytics Workspaces (LAW), Data Collection Rules (DCR).
Analytics: Kusto Query Language (KQL) for detection logic.
XDR Integration: Microsoft Defender for Cloud & Microsoft Defender for Endpoint.
Visualization: Azure Workbooks and Sentinel Dashboards.

🧠 Core Methodology
In every lab within this repository, I follow the Detection Engineering Lifecycle:
Simulation: Executing real-world attacks (Hydra, PowerShell Empire, etc.).
Analysis: Hunting through raw logs to identify high-fidelity telemetry.
Engineering: Authoring KQL rules to minimize False Positives.
Validation: Testing the alert to ensure an Incident is triggered for the SOC.

📁 Repository Structure
/Brute-Force-Lab: Sentinel detection for RDP brute-force attacks.
/Persistence-Workbook-Lab: Visualizing system persistence with Azure Workbooks.
/.....

Featured Logic: Brute Force DetectionOne of the most frequent cloud attacks is RDP credential stuffing. I developed the following KQL logic to alert on sustained attacks while ignoring occasional user typos:Code snippetSecurityEvent
| where EventID == 4625
| summarize FailureCount = count() by IpAddress, Computer, bin(TimeGenerated, 5m)
| where FailureCount >= 10
| project TimeGenerated, IpAddress, Computer, FailureCount
