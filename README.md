# Network Troubleshooting Lab (WGU D412)

Hands on network troubleshooting completed for my B.S. in Cloud and Network Engineering (Microsoft Azure) at Western Governors University. I worked six help desk tickets in a simulated enterprise network and passed all six with a 100% score in November 2026.

![Lab result: Completed, 100% success score, 6 of 6 tickets passed](lab-result.png)

> This repo documents my methods and the tools I used. It intentionally leaves out the specific ticket answers, because the simulation is a graded assessment that other students still take.

## The environment

The lab ran in GNS3 and modeled a small company network:

* **Routers:** several VyOS routers connecting user, admin, server and DMZ subnets
* **Firewall:** OPNsense, separating the LAN, the DMZ and the internet
* **Servers:** Windows Server 2016 (DNS), Ubuntu Server, and Linux and Windows servers in a DMZ
* **Clients:** a Windows 10 laptop, a Linux desktop and a test PC
* **Tools:** Wireshark, PuTTY, TightVNC, the OPNsense web console, and the Linux and Windows command line

## The kinds of problems I solved

* Servers and clients that could not reach other networks or the internet
* Users sent to the wrong website by a bad name resolution answer
* A firewall change that cut off access to a server
* A device that dropped off its network after a configuration change
* Finding unauthorized services by scanning a server's open ports
* Identifying a suspicious server from a packet capture

## How I worked each ticket

1. **Ask the requester first.** What changed, when it started, what still works, and whether I may connect to their machine. Two requesters said no, so I proved where the fault lived from the network side before asking again.
2. **Test the path one hop at a time.** Local IP and gateway, then the gateway, then the next router, then DNS. I changed nothing until a test pointed at one device.
3. **Compare against a known good answer.** For DNS, I compared our internal server's reply with a public resolver. For routing, I compared each router's table with the network map.
4. **Make the smallest fix that solves it,** then save the change so it survives a reboot.
5. **Verify from the user's side,** then explain the cause and the fix to the requester in plain language and ask them to confirm.

## Lessons

* **The first guess is often wrong.** On one ticket I suspected the server, and the real cause was two routers away.
* **A loop looks different from a dead end.** "Time to live exceeded" replies pointed to a routing loop, while silence pointed to a host or service that was down.
* **Respecting a user's "no" made me a better troubleshooter.** It forced me to collect evidence on the network side first.
* **Document as you go.** Clear notes made the final write up fast and accurate.

See [commands.md](commands.md) for the commands I relied on.

## Links

* LinkedIn: [linkedin.com/in/jubriladams](https://www.linkedin.com/in/jubriladams)
* Portfolio: [jubriladams78.github.io](https://jubriladams78.github.io)
