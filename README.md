# Securing a mini honeynet in Azure
![Cloud Honeynet / SOC](https://i.imgur.com/ZWxe03e.jpg)

## Introduction

In this project, I built a mini honeynet in Azure. I was able to collect logs from various sources and view them in the Log Analytics Workspace. With those logs, Microsoft Sentinel was able to build attack maps, trigger alerts, and create incidents. I opened those virtual machines to the internet and viewed security metrics for 24 hours before and after I applied security controls and hardened the environment. Some of the metrics I measured were:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Before Hardening
![Architecture Diagram](https://i.imgur.com/aBDwnKb.jpg)

For the "BEFORE" metrics, all resources were deployed and exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources are deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

## After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/YQNa9Pp.jpg)

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint

The architecture of the mini honeynet in Azure consists of the following:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel


## Attack Maps Before Hardening / Security Controls
![NSG Allowed Inbound Malicious Flows]()<br>
![Linux Syslog Auth Failures](https://imgur.com/a/Gc8sKzk)<br>
![Windows RDP/SMB Auth Failures](https://imgur.com/a/baX3c9Z)<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 5/25/2023, 7:31:03 PM
Stop Time 5/26/2023, 7:31:03 PM

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 101688
| Syslog                   | 7144
| SecurityAlert            | 1
| SecurityIncident         | 342
| AzureNetworkAnalytics_CL | 643

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 6/2/2023, 5:14:31 PM
Stop Time	6/3/2023, 5:14:31 PM

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 519
| Syslog                   | 24
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0
