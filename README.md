Basic Vulnerability Scanning Lab using OpenVAS
Overview
This repository documents a vulnerability assessment performed on a Windows PC using OpenVAS Community Edition. The goal was to identify and mitigate common security issues on the local machine.

Steps Performed
Installed OpenVAS Community Edition on the PC.

Configured OpenVAS to scan the machine with IP address 192.168.0.107.

Started a "Full and Fast" vulnerability scan using OpenVAS.

Waited for the scan to complete (about 15 minutes).

Reviewed the automatically generated PDF report for vulnerabilities.

Key Findings
SMB/NETBIOS NULL Session Authentication Bypass (High Severity, Port 445/tcp):

Issue: Possible to login to the share 'IPC$' with an empty username and password.

Impact: Attackers could use shares to cause the system to crash or access sensitive data.

Suggested Fix: Disable null session login, remove unnecessary shares, and require passwords for all shares.

DCE/RPC and MSRPC Services Enumeration Reporting (Medium Severity, Port 135/tcp):

Issue: DCE/RPC and MSRPC services on the host can be enumerated, revealing information.

Impact: Attackers may gain more knowledge about the remote system.

Suggested Fix: Filter or block incoming traffic to these ports using a firewall.

TCP Timestamps Information Disclosure (Low Severity, General TCP):

Issue: TCP timestamps allow the uptime of the host to be determined.

Impact: May provide minor information to attackers but is generally low risk.

Suggested Fix: Disable TCP timestamps where possible:

On Windows: Run netsh int tcp set global timestamps=disabled in Command Prompt as administrator.

On Linux: Add net.ipv4.tcp_timestamps = 0 to /etc/sysctl.conf and run sysctl -p.

Mitigation Steps Taken
Disabled guest/null session access and enforced password protection for network shares.

Restricted inbound access to sensitive ports with firewall rules.

Disabled TCP timestamps on the system as described above.
