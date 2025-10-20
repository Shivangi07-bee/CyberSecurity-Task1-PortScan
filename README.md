# CyberSecurity-Task1-PortScan


Task 1 - Local Network Port Scanning & Analysis

Author: Shivangi
GitHub: Shivangi07-bee
Device scanned: 192.168.31.180
Network range: 192.168.31.0/24

Objective
Identify active hosts and analyze open TCP ports and running services on my local host using Nmap, and capture SYN scan packets with Wireshark as evidence of scanning activity.

Repository Structure (for reference)
.
├── README.md
├── scans/
│ ├── hosts_scan.txt # Host discovery output
│ ├── mydevice_full_ports.txt # Full port scan (all ports) - text
│ ├── mydevice_scan.nmap # Nmap standard output
│ └── mydevice_scan.gnmap # Greppable Nmap output
└── captures/
├── mydevice_scan.pcapng # Full Wireshark capture (raw)
└── mydevice_syn_scan_only.pcapng # Filtered: only SYN packets (evidence)

Tools Used

Nmap (network scanner)

Wireshark / TShark (packet capture and analysis)

Windows: cmd / PowerShell for command execution

Commands (exact commands used)

Host discovery (find live hosts)
nmap -sn 192.168.31.0/24 -oN scans/hosts_scan.txt

Full port scan (all TCP ports) on the target device
nmap -p- -sS -sV 192.168.31.180 -oN scans/mydevice_full_ports.txt

Standard scan with service/version and OS detection (produces .nmap/.xml/.gnmap)
nmap -sS -sV -O 192.168.31.180 -oA scans/mydevice_scan

Wireshark display filter used to show probe packets (SYN only)
tcp.flags.syn == 1 && tcp.flags.ack == 0

(Optional) Capture only SYN packets with tshark (example)
tshark -i "Wi-Fi" -f "tcp[13] & 0x02 != 0 and tcp[13] & 0x10 == 0" -w captures/mydevice_syn_scan_only.pcapng

How to reproduce locally

Install Nmap and Wireshark on your machine.

Start Wireshark and select the appropriate network adapter (run as admin if needed).

(Optional) Set a capture filter to record only SYNs:
tcp[13] & 0x02 != 0 and tcp[13] & 0x10 == 0

Run host discovery and port scan commands.

Stop the capture, apply the display filter (tcp.flags.syn == 1 && tcp.flags.ack == 0) and export Displayed packets to captures/mydevice_syn_scan_only.pcapng.

Findings (summary)


Open/Listening ports found (example):

22/tcp — ssh — OpenSSH 7.x — risk: brute-force if weak credentials

80/tcp — http — Apache/ — risk: outdated web app vulnerabilities

443/tcp — https — TLS — risk: misconfigured TLS or outdated web services

Evidence: captures/mydevice_syn_scan_only.pcapng contains the SYN probes matching the Nmap scan.

Risk assessment & recommendations

Close or firewall any unnecessary ports.

For required services (SSH/RDP/HTTP):

Enforce strong authentication (use key-based SSH).

Use rate-limiting and fail2ban-style protections for exposed services.

Keep services and OS up to date with security patches.

Move remote access services behind a VPN where possible.

Notes & submission

Do not commit installers (e.g., nmap-setup.exe, Wireshark-Installer.exe) — only include scan outputs and captures.

This repository is prepared for submission to the internship portal. Paste the repo link into the submission form.

Submitted by: Shivangi — Shivangi07-bee
