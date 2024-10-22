# Simple FTP Practice

---

I am given an Ip of 10.129.208.13 and I have to find the banner of the ftp server as well as look for the flag.

This is a very simple lab

```
┌──(kali㉿kali)-[~/Desktop/academy]
└─$ sudo nmap -Pn -p21 -sV -sC 10.129.208.13 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-10-07 22:42 EDT
Nmap scan report for 10.129.208.13
Host is up (0.039s latency).

PORT   STATE SERVICE VERSION
21/tcp open  ftp
| fingerprint-strings: 
|   GenericLines: 
|     220 InFreight FTP v1.1
|     Invalid command: try being more creative
|_    Invalid command: try being more creative
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port21-TCP:V=7.94SVN%I=7%D=10/7%Time=67049C1B%P=x86_64-pc-linux-gnu%r(G
SF:enericLines,74,"220\x20InFreight\x20FTP\x20v1\.1\r\n500\x20Invalid\x20c
SF:ommand:\x20try\x20being\x20more\x20creative\r\n500\x20Invalid\x20comman
SF:d:\x20try\x20being\x20more\x20creative\r\n");

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 63.77 seconds
```

![image.png](Simple%20FTP%20Practice%2011924f42a85b809786b0e4717459e8ae/image.png)

This is the banner.

Now I will try to login into the FTP server. My first try is using anonymous login.

![image.png](Simple%20FTP%20Practice%2011924f42a85b809786b0e4717459e8ae/image%201.png)

Now I am able to find the flag.txt and download it using the get command.

```
ftp> get flag.txt
local: flag.txt remote: flag.txt
200 EPRT command successful
150 Opening BINARY mode data connection for flag.txt (39 bytes)
    39        0.97 MiB/s 
226 Transfer complete
39 bytes received in 00:00 (0.84 KiB/s)
ftp> exit
221 Goodbye.
                                                                                                                                              
┌──(kali㉿kali)-[~/Desktop/academy]
└─$ ls
academy-regular.ovpn  flag.txt  nmap.txt
                                                                                                                                              
┌──(kali㉿kali)-[~/Desktop/academy]
└─$ cat flag.txt                                   
HTB{b7skjr4c76zhsds7fzhd4k3ujg7nhdjre}

```