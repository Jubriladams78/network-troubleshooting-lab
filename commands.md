# Troubleshooting Command Reference

General commands I used in the lab, grouped by where they run. Addresses below are examples.

## Linux (Ubuntu)

| Goal | Command |
| --- | --- |
| Show interfaces and IP addresses | `ip a` |
| Show the routing table and default gateway | `ip route` |
| See the saved network config | `sudo cat /etc/netplan/*.yaml` |
| Apply netplan changes with automatic rollback | `sudo netplan try` |
| Check IP forwarding | `sysctl net.ipv4.ip_forward` |
| Trace the path to a host | `tracepath -n 10.0.0.1` |
| See neighbors found by ARP | `ip neigh` |
| Check which DNS server is in use | `resolvectl status` |
| Ask a specific DNS server | `nslookup example.com 8.8.8.8` |
| Scan every TCP port without nmap | `nc -znv -w1 10.0.0.20 1-65535 2>&1 \| grep succeeded` |

## VyOS routers

| Goal | Command |
| --- | --- |
| Show interfaces and addresses | `show interfaces` |
| Show the routing table | `show ip route` |
| List configured static routes | `show configuration commands \| match static` |
| See devices on attached networks | `show arp` |
| Ping from the router | `ping 10.0.0.4 count 3` |
| Run a show command in config mode | `run show ip route` |
| Replace a default route | `configure`, then `delete protocols static route 0.0.0.0/0 next-hop <old>`, `set protocols static route 0.0.0.0/0 next-hop <new>`, `commit`, `save`, `exit` |

## Windows

| Goal | Command or tool |
| --- | --- |
| Full adapter details | `ipconfig /all` |
| Open adapter settings | `ncpa.cpl` |
| Open DNS Manager on a DNS server | `dnsmgmt.msc` |
| Test a path | `tracert example.com` |

## Wireshark

| Goal | Display filter |
| --- | --- |
| FTP control traffic | `ftp \|\| tcp.port == 21` |
| DNS queries and answers | `dns` |
| Traffic to or from one host | `ip.addr == 10.0.0.2` |

## OPNsense firewall

* **Firewall > Rules** lists rules per interface (LAN, DMZ, WAN, Floating). Rules are read top down and the first match wins.
* Check each rule's **action** (Pass, Block, Reject), **direction**, **destination** and whether it is **disabled**.
* After editing, click **Apply changes**, or the old rules stay active.
