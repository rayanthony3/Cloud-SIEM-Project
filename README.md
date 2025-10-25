Project summary

Windows SIEM lab using Elastic Cloud and a Windows VM on Azure. Collects Windows Security logs and endpoint telemetry. Includes KQL detections for failed logon spikes, local Administrators membership changes, and suspicious PowerShell. Ships a ready to import dashboard and sample queries.

How to import the dashboard

Kibana → Stack Management → Saved Objects.

Click Import.

Select dashboards/windows-siem-lab.ndjson.

Choose Create new objects.

Open Analytics → Dashboards and select Windows SIEM Lab.

Reproduce the lab (short)

Create Elastic Cloud deployment and Windows VM.

In Kibana, create an agent policy with Windows and Elastic Defend.

Enroll the VM with Elastic Agent via Fleet (MSI).

Enable auditing:

auditpol /set /subcategory:"Process Creation" /success:enable /failure:enable
auditpol /set /subcategory:"Security Group Management" /success:enable /failure:enable
auditpol /set /subcategory:"User Account Management" /success:enable /failure:enable
reg add "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System" /v ProcessCreationIncludeCmdLine_Enabled /t REG_DWORD /d 1 /f


Create the three detections using the queries in queries/KQL.txt.
