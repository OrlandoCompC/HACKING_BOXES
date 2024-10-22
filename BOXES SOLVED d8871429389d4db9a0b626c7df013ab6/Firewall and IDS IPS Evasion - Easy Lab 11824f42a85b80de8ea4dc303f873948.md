# Firewall and IDS/IPS Evasion - Easy Lab

---

A company hired us to test their IT security defenses, including their `IDS` and `IPS` systems. Our client wants to increase their IT security and will, therefore, make specific improvements to their `IDS/IPS` systems after each successful test. We do not know, however, according to which guidelines these changes will be made. Our goal is to find out specific information from the given situations.

Our client wants to know if we can identify which operating system their provided machine is running on. Submit the OS name as the answer.

IP = 10.129.14.87

```
└──╼ [★]$ sudo nmap -sS -Pn 10.129.14.87
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-10-07 08:11 CDT
Nmap scan report for 10.129.14.87
Host is up (0.0081s latency).
Not shown: 869 closed tcp ports (reset), 128 filtered tcp ports (no-response)
PORT      STATE SERVICE
22/tcp    open  ssh
80/tcp    open  http
10001/tcp open  scp-config

Nmap done: 1 IP address (1 host up) scanned in 1.66 seconds

```

```
sudo nmap -sS -Pn -A -sV -p22,80,10001 10.129.14.87
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-10-07 08:13 CDT
Nmap scan report for 10.129.14.87
Host is up (0.016s latency).

PORT      STATE SERVICE     VERSION
22/tcp    open  ssh         OpenSSH 7.6p1 Ubuntu 4ubuntu0.7 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 71:c1:89:90:7f:fd:4f:60:e0:54:f3:85:e6:35:6c:2b (RSA)
|   256 e1:8e:53:18:42:af:2a:de:c0:12:1e:2e:54:06:4f:70 (ECDSA)
|_  256 1a:cc:ac:d4:94:5c:d6:1d:71:e7:39:de:14:27:3c:3c (ED25519)
80/tcp    open  http        Apache httpd 2.4.29 ((Ubuntu))
|_http-title: Apache2 Ubuntu Default Page: It works
|_http-server-header: Apache/2.4.29 (Ubuntu)
10001/tcp open  scp-config?
| fingerprint-strings: 
|   GetRequest: 
|_    220 HTB{pr0F7pDv3r510nb4nn3r}
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port10001-TCP:V=7.94SVN%I=7%D=10/7%Time=6703DE99%P=x86_64-pc-linux-gnu%
SF:r(GetRequest,1F,"220\x20HTB{pr0F7pDv3r510nb4nn3r}\r\n");
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Aggressive OS guesses: Linux 5.0 (96%), Linux 4.15 - 5.8 (96%), Linux 5.0 - 5.5 (95%), Linux 3.1 (95%), Linux 3.2 (95%), AXIS 210A or 211 Network Camera (Linux 2.6.17) (95%), Linux 2.6.32 (94%), Linux 5.3 - 5.4 (94%), ASUS RT-N56U WAP (Linux 3.4) (93%), Linux 3.16 (93%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 10001/tcp)
HOP RTT     ADDRESS
1   7.74 ms 10.10.14.1
2   8.27 ms 10.129.14.87

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 178.39 seconds

```

From this scan I can see it is running Ubuntu Linux.