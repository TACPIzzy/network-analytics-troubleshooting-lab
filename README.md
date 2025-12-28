# Network Analytics and Troubleshooting Lab

This project documents a hands-on troubleshooting lab where I resolved six network issues in a simulated enterprise
environment using GNS3, Wireshark, Linux/VyOS CLI, and firewall analysis tools.

The lab scenarios cover DNS misconfiguration, illegal FTP hosting, routing failures, endpoint IP misconfigurations,
firewall rule errors, and unauthorized open ports on a DMZ server.

## Lab environment

- GNS3-based virtual network
- VyOS routers (routing and OSPF)
- OPNsense firewall
- Windows Server and Windows client machines
- Ubuntu servers
- DMZ and internal subnets

## Helpdesk tickets covered

### Ticket 1 – DNS redirection and suspicious site

- **Issue:** Users on `USER_Net` could not reach `www.wgu.edu` and were redirected to a suspicious site.
- **Tools:** `ping`, `ipconfig /flushdns`, `ipconfig /all`, Windows Update, Windows Defender, Windows Server Manager.
- **Root cause:** Misconfigured DNS server and incorrect preferred DNS settings on `DMZ_Server_3`.
- **Resolution:** Corrected DNS configuration and preferred DNS server, verified resolution from both server and client.

### Ticket 2 – Illegal FTP hosting

- **Issue:** Security team suspected an illegal FTP site distributing copyrighted software.
- **Tools:** Wireshark (`ftp` filter), Linux CLI (`ls`, `find`, `cd`).
- **Root cause:** Unauthorized `photoshop.zip` file hosted on `DMZ_Server_2` at `/srv/ftp/pub/warez/`.
- **Resolution:** Identified server IP `10.10.20.2`, confirmed location of the file, and recommended quarantining the server and hardening FTP configuration.

### Ticket 3 – Ubuntu server cannot reach networks or internet

- **Issue:** `Ubuntu_Server` could not reach assigned networks or the internet, blocking security patch updates.
- **Tools:** Linux CLI (`ping`, `traceroute`, `nslookup`, `ifconfig` after installing `net-tools`), VyOS CLI (`show ip route`, `show interfaces`, `show protocols`, static routes, OSPF configuration).
- **Root cause:** Incorrect static routing and OSPF configuration between Router4 and Router5.
- **Resolution:** Corrected next-hop routes and OSPF settings, then verified connectivity to the firewall, `8.8.8.8`, and DNS resolution for `wgu.edu`.

### Ticket 4 – Laptop unable to access network via Ethernet

- **Issue:** `Windows_Laptop_1` could not access internet or network resources over Ethernet.
- **Tools:** VyOS CLI (`show interface`), Windows `ipconfig /all`, `ping`, `nslookup`, Ethernet adapter IPv4 settings.
- **Root cause:** Self-assigned IP (`169.254.0.1`) and missing default gateway due to invalid IP configuration.
- **Resolution:** Manually assigned static IP, subnet mask, default gateway, and DNS servers, then verified connectivity and name resolution.

### Ticket 5 – No access to DMZ server after firewall change

- **Issue:** Devices outside the DMZ could no longer access `DMZ_Server_1`.
- **Tools:** OPNsense firewall GUI, Linux CLI (`ping`, `ifconfig`, `tcpdump`), Windows `ping`.
- **Root cause:** Firewall rule misconfigured with `reject` action instead of `pass` for DMZ traffic.
- **Resolution:** Corrected firewall rule, validated connectivity using `ping` from multiple subnets, and confirmed traffic using `tcpdump` on `DMZ_Server_1`.

### Ticket 6 – Unauthorized open ports on DMZ server

- **Issue:** Security team requested an assessment of open ports on `DMZ_Server_2`.
- **Tools:** Linux CLI (`ss -tuln`, `lsof -I -P | grep LISTEN`).
- **Root cause:** Multiple unauthorized services running on non-approved ports (e.g., Telnet, HTTP, HTTPS, Docker, potential backdoor ports).
- **Resolution:** Identified all non-approved ports and recommended reporting to security, shutting down unauthorized services, and aligning with approved service/port policy.

## Skills demonstrated

- Network troubleshooting and root cause analysis
- Packet capture and analysis (Wireshark)
- Linux and VyOS CLI for routing and diagnostics
- Firewall rule analysis and correction (OPNsense)
- DNS, FTP, and TCP/IP fundamentals
- Documentation of incident handling and recommendations

## Files

- `network-analytics-and-troubleshooting-lab.pdf` — Full lab report and screenshots

## Author

**Ismael “Izzy” Ibarra**  
Systems engineer focused on network troubleshooting, secure architectures, and cloud/network automation.

