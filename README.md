# Local Network Port Scanning — Nmap Lab

## Objective
Discover open ports and services on devices in my local network to understand network exposure and provide remediation suggestions.

## Tools used
- Nmap 7.98
- (Optional) Wireshark for packet capture

## Scans performed
- Host discovery: `nmap -sn 192.168.158.0/24`
- TCP SYN + service scan: `nmap -sS -sV 192.168.158.0/24`
- Full port scan (single host): `nmap -p- 192.168.158.59`
- UDP scan: `sudo nmap -sU 192.168.158.59`

## Key findings (summary)
- Live host: `192.168.158.59`
- Important open ports: `135/tcp`, `139/tcp`, `445/tcp`, `5357/tcp`, multiple ephemeral RPC ports; several UDP discovery ports.
- The host appears to be a Windows machine with SMB and RPC services enabled.

## Recommendations
- Patch the host and disable SMBv1.
- Restrict SMB and RPC access with firewall rules.
- Disable UPnP and unnecessary discovery services if not required.
- Use network segmentation for IoT or guest devices.

## Files included
- `results/scan-results.nmap`
- `results/scan-allports.nmap`
- `results/scan-udp.nmap`
- `host_summary.md`
- `interview_answers.md`
- `pcaps/`

## How to reproduce (only on your own network)
1. Identify your local CIDR using `ipconfig` / `ip addr`.
2. Run `nmap -sn <cidr>` to list live hosts.
3. Run `sudo nmap -sS -sV <cidr> -oA results/full-scan` to discover services.
4. For deep dive on a host, run `sudo nmap -p- <ip> -oN results/allports.nmap` and `sudo nmap -sU <ip> -oN results/udp.nmap`.

**DO NOT** run scans on networks you do not own or have permission to test.
