# Cloud-Soc
Building a SOC + Honeynet in Azure (Live Traffic)
<img width="960" height="540" alt="image" src="https://github.com/user-attachments/assets/3f724405-2ad4-4df4-a95c-76b2a94ee941" />

Cloud Honeynet / SOC

Introduction
In this project, I build a mini honeynet in Azure and ingest log sources from various resources into a Log Analytics workspace, which is then used by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. I measured some security metrics in the insecure environment for 24 hours, apply some security controls to harden the environment, measure metrics for another 24 hours, then show the results below. The metrics we will show are:

SecurityEvent (Windows Event Logs)
Syslog (Linux Event Logs)
SecurityAlert (Log Analytics Alerts Triggered)
SecurityIncident (Incidents created by Sentinel)
AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)
Architecture Before Hardening / Security Controls
<img width="960" height="540" alt="image" src="https://github.com/user-attachments/assets/0818d8e6-77e8-4379-b3b0-d6ed0f9ce325" />

Architecture Diagram

Architecture After Hardening / Security Controls
<img width="960" height="540" alt="image" src="https://github.com/user-attachments/assets/9a70ff62-aa90-45c3-a2a2-9af8249797d7" />

Architecture Diagram

The architecture of the mini honeynet in Azure consists of the following components:

Virtual Network (VNet)
Network Security Group (NSG)
Virtual Machines (2 windows, 1 linux)
Log Analytics Workspace
Azure Key Vault
Azure Storage Account
Microsoft Sentinel
For the "BEFORE" metrics, all resources were originally deployed, exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources are deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint

Attack Maps Before Hardening / Security Controls
<img width="1140" height="685" alt="image" src="https://github.com/user-attachments/assets/b2e1b6b1-dfde-47b0-9f60-dd4f26b8b2ab" />

nsg-malicious-allowed-in
linux-ssh-auth-fail
<img width="1198" height="657" alt="image" src="https://github.com/user-attachments/assets/b3f44f9d-71d4-4a30-9483-1bc2df49fe4a" />

windows-rdp-auth-fail
<img width="1133" height="643" alt="image" src="https://github.com/user-attachments/assets/6e481954-6023-4c3c-908b-418777fa18c1" />

mssql-auth-fail
<img width="1202" height="679" alt="image" src="https://github.com/user-attachments/assets/5389f26d-b312-415f-b618-4afff7ce1ece" />

Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours: Start Time 2024-12-31 19:00:13 Stop Time 2024-12-31 19:00:13
environment for 24 hours: Start Time 2024-12-31 19:00:13 Stop Time 2024-12-31 19:00:13

<img width="288" height="224" alt="image" src="https://github.com/user-attachments/assets/78d2a415-cdde-4c9c-b943-7a91531972ed" />


Attack Maps Before Hardening / Security Controls
All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.


Metrics After Hardening / Security Controls
The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls: Start Time 2025-01-02 01:52:31 Stop Time 2025-01-02 00:52:31
<img width="287" height="221" alt="image" src="https://github.com/user-attachments/assets/4892ad64-50b1-4983-8e00-03cc02f23287" />

Metric	Count
SecurityEvent	9548
Syslog	1
SecurityAlert	0
SecurityIncident	0
AzureNetworkAnalytics_CL	0

Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.
