# Knowledge Check HTB academy

---

Ip 10.129.42.249

## Enumeration

```
                                                                                 
┌──(kali㉿kali)-[~/Desktop/academy]
└─$ sudo nmap -sS -Pn 10.129.42.249           
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-10-03 12:05 EDT
Nmap scan report for 10.129.42.249
Host is up (0.042s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 0.79 seconds
```

I ran an -p- but only these ports were open

```
──(kali㉿kali)-[~/Desktop/academy]
└─$ whatweb 10.129.42.249                         
http://10.129.42.249 [200 OK] AddThis, Apache[2.4.41], Country[RESERVED][ZZ], HTML5, HTTPServer[Ubuntu Linux][Apache/2.4.41 (Ubuntu)], IP[10.129.42.249], Script[text/javascript], Title[Welcome to GetSimple! - gettingstarted]

```

I then ran gobusters and started looking at the site.

I started looking around the site with burp to get an idea of the site.

![image.png](Knowledge%20Check%20HTB%20academy%2011424f42a85b8048bd2ef4266cddedce/image.png)

```
┌──(kali㉿kali)-[~/Desktop/academy]
└─$ gobuster dir -u http://10.129.42.249 -t 4 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt 
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.129.42.249
[+] Method:                  GET
[+] Threads:                 4
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/data                 (Status: 301) [Size: 313] [--> http://10.129.42.249/data/]
/admin                (Status: 301) [Size: 314] [--> http://10.129.42.249/admin/]
/plugins              (Status: 301) [Size: 316] [--> http://10.129.42.249/plugins/]                                                                                 
/theme                (Status: 301) [Size: 314] [--> http://10.129.42.249/theme/]
/backups              (Status: 301) [Size: 316] [--> http://10.129.42.249/backups/
```

I then visit all of them one by one

![image.png](Knowledge%20Check%20HTB%20academy%2011424f42a85b8048bd2ef4266cddedce/image%201.png)

![image.png](Knowledge%20Check%20HTB%20academy%2011424f42a85b8048bd2ef4266cddedce/image%202.png)

In the /data found some admin credentials.

```
<USR>admin</USR>
<NAME/>
<PWD>d033e22ae348aeb5660fc2140aec35850c4da997</PWD>
<EMAIL>admin@gettingstarted.com</EMAIL>
```

![image.png](Knowledge%20Check%20HTB%20academy%2011424f42a85b8048bd2ef4266cddedce/image%203.png)

I attempted to use the creds but they did not work. I also attempted to SSH but this also failed.

![image.png](Knowledge%20Check%20HTB%20academy%2011424f42a85b8048bd2ef4266cddedce/image%204.png)

![image.png](Knowledge%20Check%20HTB%20academy%2011424f42a85b8048bd2ef4266cddedce/image%205.png)

I then tried default creds such as admin:admin and this worked.

![image.png](Knowledge%20Check%20HTB%20academy%2011424f42a85b8048bd2ef4266cddedce/image%206.png)

There was an exploit. Ill now check metasploit to see if I can use it to exploit this site and get RCE

![image.png](Knowledge%20Check%20HTB%20academy%2011424f42a85b8048bd2ef4266cddedce/image%207.png)

![image.png](Knowledge%20Check%20HTB%20academy%2011424f42a85b8048bd2ef4266cddedce/image%208.png)

![image.png](Knowledge%20Check%20HTB%20academy%2011424f42a85b8048bd2ef4266cddedce/image%209.png)

![image.png](Knowledge%20Check%20HTB%20academy%2011424f42a85b8048bd2ef4266cddedce/image%2010.png)

![image.png](Knowledge%20Check%20HTB%20academy%2011424f42a85b8048bd2ef4266cddedce/image%2011.png)

![image.png](Knowledge%20Check%20HTB%20academy%2011424f42a85b8048bd2ef4266cddedce/image%2012.png)

Now I got root so now I can read the root.txt