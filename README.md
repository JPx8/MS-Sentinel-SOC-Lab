# MS-Sentinel-SOC-Lab
Endpoint Persistence & Monitoring Dashboard

Endpoint Persistence & Monitoring Dashboard

Description
This module focuses on detecting common Persistence techniques (MITRE ATT&CK T1547.001) and visualizing endpoint health through a custom Microsoft Sentinel Workbook. The goal was to move beyond simple log collection and create an actionable, "at-a-glance" dashboard for a SOC analyst.

Attack Simulation
To test the detection pipeline, I manually simulated an attacker gaining persistence on the Windows endpoint:

Registry Run Key: Created a suspicious entry in HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run.

Telemetry Validation: Verified that Sysmon Event ID 13 (RegistryValueSet) captured the modification and successfully streamed it to the Log Analytics Workspace.

Detection Logic (KQL)
I used the following KQL query to monitor heartbeats and calculate a real-time "Online/Offline" status.

Code snippet:
Heartbeat
| summarize LastHeartbeat = max(TimeGenerated) by Computer, ComputerIP, OSType
| extend Status = iff(LastHeartbeat > ago(5m), "Online", "Offline")
| project Computer, ComputerIP, OSType, LastHeartbeat, Status

Visual Engineering (The JSON Mapping Fix)
A key challenge was getting the Workbook's conditional formatting to recognize the "Online/Offline" status. While the KQL was correct, the UI renderer was not applying the colors to the correct column.

The Issue: The "Thresholds" renderer was looking for a non-existent or mismatched column, resulting in no color status.

The "Pro" Fix: I accessed the Workbook Advanced Editor (JSON) to manually correct the column mapping.

Original Code: "columnMatch": "Colors"
Corrected Code: "columnMatch": "Status"

Result: By aligning the JSON logic with the KQL output, the "Thresholds" renderer successfully identified the Status column, enabling the green/red visual indicators.

Results
Process Timeline Spike
The chart below shows the vertical spikes in activity captured during the attack simulation.
<img width="1909" height="896" alt="image" src="https://github.com/user-attachments/assets/f36302d2-10f0-43bc-8c83-70b2b38ac2f4" />


Live Health Dashboard
The final dashboard showing the successfully configured "Online" status indicator after the JSON mapping fix.
<img width="1909" height="896" alt="image" src="https://github.com/user-attachments/assets/0066429b-49a8-4a83-af8a-47f11b02d0f9" />
