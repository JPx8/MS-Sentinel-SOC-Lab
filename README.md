MS-Sentinel-SOC-Lab
Microsoft Sentinel lab

Overview

This repository is a collection of hands-on cybersecurity projects focused on Detection Engineering, Cloud SIEM Operations, and Threat Hunting.

The environment consists of a Windows endpoint (managed via Azure Arc) streaming high-fidelity Sysmon telemetry into Microsoft Sentinel. The goal of this lab is to simulate real-world attack vectors and engineer the necessary ingestion pipelines, KQL parsers, and visual dashboards to detect them.

Technical Stack:

SIEM: Microsoft Sentinel Agent: Azure Monitor Agent (AMA) Log Sources: Sysmon (Event IDs 1, 11, 12, 13, etc, Heartbeat, WindowsEvent Languages: Kusto Query Language (KQL), JavaScript Object Notation(JSON) Automation: Data Collection Rules (DCR), Analytics Rules

Project Modules

Each folder below contains a specific lab module, including the attack methodology, KQL queries, and proof-of-concept screenshots.

Module 01: Brute-Force-Lab / Credential Access (Brute Force)

Focus: Identity security and high-volume authentication failures. Tools: Hydra (Kali Linux).

Module 02: Persistence-Workbook-Lab/ Persistence & Monitoring

Focus: Registry/Task persistence and real-time health dashboards. Feature: Custom Sentinel Workbook with conditional formatting.

(More modules added as the lab expands...)
