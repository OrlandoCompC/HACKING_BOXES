# Firewall and IDS/IPS Evasion - Hard Lab

---

With our second test's help, our client was able to gain new insights and sent one of its administrators to a `training course` for `IDS/IPS` systems. As our client told us, the training would last `one week`. Now the administrator has taken all the necessary precautions and wants us to test this again because specific services must be changed, and the communication for the provided software had to be modified.

Now our client wants to know if it is possible to find out the version of the running services. Identify the version of service our client was talking about and submit the flag as the answer.

Ip=10.129.17.115

I start by attempting to identify all the ports open on the system.

![Screenshot 2024-10-07 at 10.04.26 AM.png](Firewall%20and%20IDS%20IPS%20Evasion%20-%20Hard%20Lab%2011824f42a85b8028a578e2d53437998c/Screenshot_2024-10-07_at_10.04.26_AM.png)

Here I decided to run another with -p- in case I had missed anything else and indeed I had.

![Screenshot 2024-10-07 at 10.16.04 AM.png](Firewall%20and%20IDS%20IPS%20Evasion%20-%20Hard%20Lab%2011824f42a85b8028a578e2d53437998c/Screenshot_2024-10-07_at_10.16.04_AM.png)

```
┌─[us-academy-5]─[10.10.15.36]─[htb-ac-1456674@htb-9az7vd5c3v]─[~]
└──╼ [★]$ sudo ncat -nv --source-port 53 10.129.17.115 50000
Ncat: Version 7.94SVN ( https://nmap.org/ncat )
Ncat: Connected to 10.129.17.115:50000.
220 HTB{kjnsdf2n982n1827eh76238s98di1w6}

```