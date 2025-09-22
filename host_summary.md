# Host summary — Local Network Scan
**Scan date:** 2025-09-22

## Network scanned
CIDR: `192.168.158.0/24`  
Discovered live hosts: `192.168.158.59`

---

## 192.168.158.59
- **Host is up** (low latency).
- **Open TCP ports found**:
  - `135/tcp` — msrpc (Microsoft RPC)
  - `139/tcp` — netbios-ssn (NetBIOS session service)
  - `445/tcp` — microsoft-ds (SMB / Windows file sharing)
  - `5040/tcp` — unknown (service not identified by Nmap)
  - `5357/tcp` — wsdapi (Web Services for Devices API)
  - `49664-49670/tcp` — unknown high ephemeral ports (likely RPC/Win services)
- **Open/filtered UDP ports found**:
  - `137/udp` — netbios-ns (NetBIOS name service) (open|filtered)
  - `138/udp` — netbios-dgm (open|filtered)
  - `1900/udp` — upnp (open|filtered)
  - `3702/udp` — ws-discovery (open|filtered)
  - `4500/udp` — nat-t-ike (open|filtered)
  - `5050/udp` — mmcc (open|filtered)
  - `5353/udp` — zeroconf / mDNS (open|filtered)
  - `5355/udp` — llmnr (open|filtered)

### Likely device / service context
This looks like a **Windows host** (SMB, MSRPC, NetBIOS and WSD indicate a Windows machine — possibly a desktop, a server, or an IoT device running Windows services).

### Risk assessment (quick)
- **High**: `445/tcp` (SMB) and `139/tcp` — SMB exposure can lead to information disclosure and, in some cases, remote code execution if exposed and vulnerable.
- **Medium**: `135/tcp` (RPC) — can be used for service enumeration; targeted exploits exist for misconfigured or unpatched systems.
- **Medium**: WSD/UPnP/mDNS (`5357`, `1900`, `5353`) — useful for local service discovery; UPnP misconfigurations can expose services externally if router wrongly configured.
- **Low/Medium**: high ephemeral ports (49664–49670) — likely dynamic RPC ports; they are normal but should be firewalled if not needed.

### Recommendations
1. **If this is your machine**:
   - Ensure Windows Update is up-to-date (patch SMB, RPC and other services).
   - Disable SMBv1 if still enabled: `Disable-WindowsOptionalFeature -Online -FeatureName smb1protocol` (or via Windows Features).
   - Turn on Windows Firewall and restrict SMB/RPC to local subnet or specific management IPs only.
   - Use strong local passwords and enable account lockout policies.
   - If remote admin access is required, use VPN or SSH tunnel, not direct internet exposure.

2. **If this is another device you control (e.g., IoT or NAS)**:
   - Disable unneeded services (file sharing, WSD, UPnP) if not used.
   - Change default credentials.
   - Place the device on a guest VLAN / network segment if possible.

3. **If you find port forwarding on router that exposes these to the internet**:
   - Remove unnecessary forwards.
   - Use NAT firewall policies to limit access to known safe IPs.

---

