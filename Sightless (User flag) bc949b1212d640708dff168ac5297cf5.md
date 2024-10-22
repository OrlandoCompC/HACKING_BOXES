# Sightless (User flag)

---

```
                                                                                                                                            
┌──(kali㉿kali)-[~]
└─$ sudo nmap -Pn -sV sightless.htb
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-10-12 21:18 EDT
Nmap scan report for sightless.htb (10.10.11.32)
Host is up (0.042s latency).
Not shown: 997 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
21/tcp open  ftp
22/tcp open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.10 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    nginx 1.18.0 (Ubuntu)
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port21-TCP:V=7.94SVN%I=7%D=10/12%Time=670B1FFB%P=x86_64-pc-linux-gnu%r(
SF:GenericLines,A0,"220\x20ProFTPD\x20Server\x20\(sightless\.htb\x20FTP\x2
SF:0Server\)\x20\[::ffff:10\.10\.11\.32\]\r\n500\x20Invalid\x20command:\x2
SF:0try\x20being\x20more\x20creative\r\n500\x20Invalid\x20command:\x20try\
SF:x20being\x20more\x20creative\r\n");
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

```
──(kali㉿kali)-[~]
└─$ sudo nmap -Pn -A -sC -p21,22,80  sightless.htb
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-10-12 21:20 EDT
Nmap scan report for sightless.htb (10.10.11.32)
Host is up (0.040s latency).

PORT   STATE SERVICE VERSION
21/tcp open  ftp
| fingerprint-strings: 
|   GenericLines: 
|     220 ProFTPD Server (sightless.htb FTP Server) [::ffff:10.10.11.32]
|     Invalid command: try being more creative
|_    Invalid command: try being more creative
22/tcp open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.10 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 c9:6e:3b:8f:c6:03:29:05:e5:a0:ca:00:90:c9:5c:52 (ECDSA)
|_  256 9b:de:3a:27:77:3b:1b:e1:19:5f:16:11:be:70:e0:56 (ED25519)
80/tcp open  http    nginx 1.18.0 (Ubuntu)
|_http-server-header: nginx/1.18.0 (Ubuntu)
|_http-title: Sightless.htb

```

![image.png](Sightless%20(User%20flag)%20bc949b1212d640708dff168ac5297cf5/image.png)

I  couldn’t connect to the FTP server.

The next step is to look at the website.

```
┌──(kali㉿kali)-[~]
└─$ gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u http://sightless.htb/    
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://sightless.htb/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/images               (Status: 301) [Size: 178] [--> http://sightless.htb/images/]
/icones               (Status: 301) [Size: 178] [--> http://sightless.htb/icones/]
```

![image.png](Sightless%20(User%20flag)%20bc949b1212d640708dff168ac5297cf5/image%201.png)

![image.png](Sightless%20(User%20flag)%20bc949b1212d640708dff168ac5297cf5/image%202.png)

![image.png](Sightless%20(User%20flag)%20bc949b1212d640708dff168ac5297cf5/image%203.png)

![image.png](Sightless%20(User%20flag)%20bc949b1212d640708dff168ac5297cf5/image%204.png)

![image.png](Sightless%20(User%20flag)%20bc949b1212d640708dff168ac5297cf5/image%205.png)

```
{"currentUser":{"id":"noauth","email":"noauth@example.com","role":"admin","name":"noauth"},
```

![image.png](Sightless%20(User%20flag)%20bc949b1212d640708dff168ac5297cf5/image%206.png)

I don’t know if its an error but im root.

![image.png](Sightless%20(User%20flag)%20bc949b1212d640708dff168ac5297cf5/image%207.png)

![image.png](Sightless%20(User%20flag)%20bc949b1212d640708dff168ac5297cf5/image%208.png)

```
michael:$6$mG3Cp2VPGY.FDE8u$KVWVIHzqTzhOSYkzJIpFc2EsgmqvPa.q2Z9bLUU6tlBWaEwuxCDEP9UFHIXNUcF2rBnsaFYuJa6DUh/pL2IJD/
```

![image.png](Sightless%20(User%20flag)%20bc949b1212d640708dff168ac5297cf5/image%209.png)

![image.png](Sightless%20(User%20flag)%20bc949b1212d640708dff168ac5297cf5/image%2010.png)

![image.png](Sightless%20(User%20flag)%20bc949b1212d640708dff168ac5297cf5/image%2011.png)

```
$6$mG3Cp2VPGY.FDE8u$KVWVIHzqTzhOSYkzJIpFc2EsgmqvPa.q2Z9bLUU6tlBWaEwuxCDEP9UFHIXNUcF2rBnsaFYuJa6DUh/pL2IJD/:insaneclownposse
```

```
insaneclownposse
```

![image.png](Sightless%20(User%20flag)%20bc949b1212d640708dff168ac5297cf5/image%2012.png)

![image.png](Sightless%20(User%20flag)%20bc949b1212d640708dff168ac5297cf5/image%2013.png)

![image.png](Sightless%20(User%20flag)%20bc949b1212d640708dff168ac5297cf5/image%2014.png)

There is a new user now.

![image.png](Sightless%20(User%20flag)%20bc949b1212d640708dff168ac5297cf5/image%2015.png)

I then went into chrome developer tools

![image.png](Sightless%20(User%20flag)%20bc949b1212d640708dff168ac5297cf5/image%2016.png)