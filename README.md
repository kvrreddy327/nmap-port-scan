# nmap-port-scan
nmap SYN scan
135 — RPC / Endpoint Mapper
Service: Windows RPC/DCOM (epmap).
Top risks: service enumeration, info disclosure, exploitable RPC/DCOM RCEs.
Attacker use: fingerprint Windows services, chain to SMB/RDP exploits for lateral movement.
Priority mitigations: block on perimeter, patch Windows, restrict RPC to trusted subnets, require VPN/jump host for remote management.

139 — NetBIOS Session Service (SMB over NetBIOS)
Service: NetBIOS/legacy SMB transport.
Top risks: share enumeration, anonymous access, NTLM relay/credential harvesting, legacy protocol weaknesses.
Attacker use: list/mount shares, abuse writable shares, pivot laterally.
Priority mitigations: block from untrusted networks, disable NetBIOS over TCP/IP if unused, disable SMBv1, lock down share ACLs.

445 — SMB / Microsoft-DS
Service: SMB/CIFS (file sharing, domain services).
Top risks: wormable RCEs (e.g., EternalBlue class), data exfil, NTLM relay, lateral movement.
Attacker use: exploit SMB RCEs, capture/relay credentials, drop ransomware on writable shares.
Priority mitigations: do NOT expose to Internet, patch immediately, disable SMBv1, enforce SMB signing/NTLMv2, restrict access via firewall/VPN.

1521 — Oracle TNS Listener
Service: Oracle DB listener (TNS).
Top risks: service enumeration, default/weak creds, unpatched TNS/DB vulnerabilities → full DB compromise/data exfiltration.
Attacker use: enumerate SIDs/services, brute-force or exploit DB CVEs, access data.
Priority mitigations: block Internet access, bind listener to private IP, patch Oracle, enforce strong DB creds and least privilege, require VPN/bastion for DB access.
