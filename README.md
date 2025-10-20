# CyberSecurity-Task1-PortScan

Task 1 - Local Network Port Scanning & Analysis

Author: Shivangi
GitHub: Shivangi07-bee
Device scanned: <REDACTED_IP>
Network range: <REDACTED_NET>

Objective
Identify active hosts and analyze open TCP ports and running services on my local host using Nmap, and capture SYN scan packets with Wireshark as evidence of scanning activity.

Repository Structure (for reference)
.
├── README.md
├── scans/
│ ├── hosts_scan.txt # Host discovery output (sanitized if public)
│ ├── mydevice_full_ports_sanitized.txt # Full port scan (sanitized for public)
│ ├── mydevice_scan.nmap # Nmap standard output (sanitized if public)
│ └── mydevice_scan.gnmap # Greppable Nmap output (sanitized if public)
└── captures/
├── syn_summary_redacted.csv # Redacted SYN packet summary (no private IPs)

Note: Raw .pcap/.pcapng files and exact service-version strings are not included here for public safety. If reviewers require raw files, share them privately.

Tools Used

Nmap (network scanner)

Wireshark / TShark (packet capture and analysis)

Windows: cmd / PowerShell for command execution

Commands (exact commands used)

Host discovery (find live hosts)
nmap -sn <REDACTED_NET> -oN scans/hosts_scan.txt

Full port scan (all TCP ports) on the target device
nmap -p- -sS -sV <REDACTED_IP> -oN scans/mydevice_full_ports.txt

Standard scan with service/version and OS detection
nmap -sS -sV -O <REDACTED_IP> -oA scans/mydevice_scan

Wireshark display filter used to show probe packets (SYN only)
tcp.flags.syn == 1 && tcp.flags.ack == 0

(Optional) Capture only SYN packets with tshark (example)
tshark -i "Wi-Fi" -f "tcp[13] & 0x02 != 0 and tcp[13] & 0x10 == 0" -w captures/mydevice_syn_scan_only.pcapng
(If publishing publicly, do not upload the .pcapng; instead create captures/syn_summary_redacted.csv.)

How to reproduce locally

Install Nmap and Wireshark on your machine.

Start Wireshark and select the appropriate network adapter (run as admin if needed).

(Optional) Set a capture filter to record only SYNs:
tcp[13] & 0x02 != 0 and tcp[13] & 0x10 == 0

Run the host discovery and port scan commands above, replacing <REDACTED_IP> / <REDACTED_NET> with your target values.

Stop the capture, apply the display filter (tcp.flags.syn == 1 && tcp.flags.ack == 0) and export Displayed packets. If sharing publicly, transform the capture into a redacted summary CSV (no private IPs) before upload.

Findings (summary)
(Example — replace with sanitized lines from your sanitized scan file)

Open/Listening ports found (example):

22/tcp — ssh — service version redacted — risk: brute-force if weak credentials

80/tcp — http — service type only — risk: outdated web app vulnerabilities

443/tcp — https — service type only — risk: misconfigured TLS or outdated web services

Evidence: captures/syn_summary_redacted.csv contains a timestamped summary of SYN probe packets with private IPs redacted.

Risk assessment & recommendations

Close or firewall any unnecessary ports.

For required services (SSH/RDP/HTTP):

Enforce strong authentication (use key-based SSH).

Use rate-limiting and fail2ban-style protections for exposed services.

Keep services and OS up to date with security patches.

Move remote access services behind a VPN where possible.

Notes & submission

Do not commit installers (e.g., nmap-setup.exe, Wireshark-Installer.exe) or raw packet captures to a public repository.

This repository is prepared for submission to the internship portal. Paste the repo link into the submission form. Raw files are available to reviewers upon request via a private channel.

Submitted by: Shivangi — Shivangi07-bee
