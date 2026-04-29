# The Lands Between Network Topology / Elden Ring Cybersecurity Lab

This is a personal student cybersecurity and networking project. It is used to simulate a multi-VLAN enterprise corporate network mapped to the lore of Elden Ring. This project was made to practice implementing secure network architecture, Active Directory management and threat auditing.

## Topology
<img width="2516" height="2144" alt="topology" src="https://github.com/user-attachments/assets/2e9e65f8-6f74-4bfb-81a8-bc27c449954a" />

## Features
* **VLAN Segmentation:** Uses pfSense to strictly isolate subnets.
* **Active Directory Domain:** A Windows Server 2022 Primary Domain Controller complete with Enterprise Admins and GPOs.
* **Shadow IT Exploitation:** Simulates a real-world breach by finding and compromising a forgotten, legacy Ubuntu server.
* **Credential Harvesting & Pivoting:** Demonstrates theoretical lateral movement by acquiring plaintext Domain Admin credentials to bypass internal firewalls via WinRM.
* **SIEM & Vulnerability Scanning:** Utilizes Wazuh to ingest network logs and Nessus for continuous vulnerability auditing within an isolated SOC network.

## Motivation
I thought of making this lab while studying network architecture and wondered if I could map enterprise security concepts to the map of one of my favorite games, Elden Ring. I always found learning more engaging when I gamify the experience. I find networking the hardest part of IT, and wanted a project where I can practice my skills while immersing myself in the lore of Elden Ring.

## Use case
I recommend using this topology as a blueprint if you want to practice building realistic corporate environments. Building out the Active Directory and pfSense rules takes trial and error, so it is mostly a framework for learning Blue Team defense (segmentation, logging) and Red Team offense (credential harvesting, pivoting).

## Disclaimer
Cybersecurity lab environments should never be bridged directly to your home network or the public internet without strict protections. The vulnerable nodes like Limgrave and Liurnia are intentionally flawed.

## Video
[![Elden Ring but It Is My Cybersecurity Lab Project](https://img.youtube.com/vi/O9OWs27ZRmE/0.jpg)](https://youtu.be/O9OWs27ZRmE)

## Topology & Subnet Breakdown

**1. Limgrave DMZ (10.0.10.0/24)**

**Components:** Stormveil Castle (Ubuntu Jump Server) acting as the external-facing entry point with vulnerable SSH/FTP access.

**What it taught me:** Setting up public-facing Demilitarized Zones (DMZs) and configuring basic firewall ingress rules to allow specific traffic (Ports 21 & 22). It demonstrated the importance of isolating external-facing assets so that an attacker cannot easily pivot directly into the internal network.

**2. Liurnia of the Lakes DMZ (10.0.15.0/24)**

**Components:** Raya Lucaria Academy (Dockerized Ubuntu Web Server) and Rennala (SQL Database).

**What it taught me:** Containerization using Docker and deploying multi-tier web applications. It also served as a playground for understanding web-layer vulnerabilities, specifically how SQL Injection can be used to extract data from backend databases.

**3. Caelid Malware Sandbox (10.0.30.0/24)**

**Components:** Redmane Castle (Windows 10 Victim Machine), Great Horned Tragoth (Flare-VM Hardening), Castellan Jerren (REMnux Gateway), Blaidd (Wireshark), and Iron Fist Alexander (Procmon).

**What it taught me:** Safe malware detonation and analysis. Setting up this completely isolated subnet taught me how to use Flare-VM and REMnux to analyze network traffic and host behavior while safely executing payloads (Scarlet Rot Ransomware) without infecting the rest of the lab.

**4. Mt. Gelmir / Volcano Manor (10.0.66.0/24)**

**Components:** Legacy Ubuntu Server acting as a Shadow IT VLAN, housing Rykard (Compromised Domain Admin Account).

**What it taught me:** The severe risks of Shadow IT and forgotten infrastructure. Setting this up taught me how to establish reverse shells to bypass perimeter firewalls and how attackers perform local enumeration to harvest plaintext credentials (creds.txt).

*Note: Originally, I wanted to set up a custom C2 beacon here for persistence, but I dropped it.*

**5. Altus Plateau / Leyndell (10.0.1.0/24)**

**Components:** The Erdtree (Windows Server 2022 Primary Domain Controller).

**What it taught me:** This was primarily for learning Blue Team defense and enterprise administration. It taught me how to build an Active Directory forest from scratch, manage Enterprise Admins, and configure Group Policy Objects (GPOs) and LDAP. On the networking side, it taught me how to configure pfSense to enforce strict internal segmentation, routing, and conditional access policies like VPN and MFA requirements.

**6. Roundtable Hold (10.0.99.0/24)**

**Components:** Management/SOC VLAN containing the Table of Lost Grace (Wazuh SIEM) and Gideon Ofnir (Nessus).

**What it taught me:** Setting up a dedicated Security Operations Center (SOC) network. This area was strictly Blue Team focused, teaching me how to deploy a Wazuh SIEM to ingest logs from across the various subnets and how to use Nessus to run automated vulnerability scans to actively audit the network's security posture.

**7. The Central Firewalls (pfSense)**

**Components:** Central Firewall (Edge Router) & Draconic Tree Sentinel (Internal Segmentation).

**What it taught me:** This was the routing backbone of the entire lab. Setting this up taught me how to configure and distribute DHCP across multiple isolated VLANs. I also gained hands-on experience managing NAT and port forwarding rules to correctly route traffic to specific subnets, as well as building strict, stateful firewall rules to control exactly which segments of the network are allowed to communicate.
