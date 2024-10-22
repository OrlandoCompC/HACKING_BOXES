# Footprinting Lab - Medium

---

This second server is a server that everyone on the internal network has access to. In our discussion with our client, we pointed out that these servers are often one of the main targets for attackers and that this server should be added to the scope.

Our customer agreed to this and added this server to our scope. Here, too, the goal remains the same. We need to find out as much information as possible about this server and find ways to use it against the server itself. For the proof and protection of customer data, a user named `HTB` has been created. Accordingly, we need to obtain the credentials of this user as proof.

![Screenshot 2024-10-22 at 1.48.26 PM.png](Footprinting%20Lab%20-%20Medium%2012724f42a85b80f392feff9f8a2e3f60/Screenshot_2024-10-22_at_1.48.26_PM.png)

ip=10.129.1.19

![Screenshot 2024-10-22 at 1.50.53 PM.png](Footprinting%20Lab%20-%20Medium%2012724f42a85b80f392feff9f8a2e3f60/Screenshot_2024-10-22_at_1.50.53_PM.png)

The first thing that comes to mind is to use nfs and smb to find creds and then access the server through  evil-winrm.

Now Ill run a deeper scan on nfs just to check it out 

```
┌─[us-academy-5]─[10.10.14.179]─[htb-ac-1456674@htb-0o7vf0cdpo]─[~]
└──╼ [★]$ sudo nmap --script nfs* 10.129.1.19 -Pn -sV -p111,2049
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-10-22 12:54 CDT
Nmap scan report for 10.129.1.19
Host is up (0.0083s latency).

PORT     STATE SERVICE  VERSION
111/tcp  open  rpcbind  2-4 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/tcp6  rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100000  2,3,4        111/udp6  rpcbind
|   100003  2,3         2049/udp   nfs
|   100003  2,3         2049/udp6  nfs
|   100003  2,3,4       2049/tcp   nfs
|   100003  2,3,4       2049/tcp6  nfs
|   100005  1,2,3       2049/tcp   mountd
|   100005  1,2,3       2049/tcp6  mountd
|   100005  1,2,3       2049/udp   mountd
|   100005  1,2,3       2049/udp6  mountd
|   100021  1,2,3,4     2049/tcp   nlockmgr
|   100021  1,2,3,4     2049/tcp6  nlockmgr
|   100021  1,2,3,4     2049/udp   nlockmgr
|   100021  1,2,3,4     2049/udp6  nlockmgr
|   100024  1           2049/tcp   status
|   100024  1           2049/tcp6  status
|   100024  1           2049/udp   status
|_  100024  1           2049/udp6  status
| nfs-ls: Volume /TechSupport
|   access: Read Lookup NoModify NoExtend NoDelete NoExecute
| PERMISSION  UID         GID         SIZE   TIME                 FILENAME
| rwx------   4294967294  4294967294  65536  2021-11-11T00:09:49  .
| ??????????  ?           ?           ?      ?                    ..
| rwx------   4294967294  4294967294  0      2021-11-10T15:19:28  ticket4238791283649.txt
| rwx------   4294967294  4294967294  0      2021-11-10T15:19:28  ticket4238791283650.txt
| rwx------   4294967294  4294967294  0      2021-11-10T15:19:28  ticket4238791283651.txt
| rwx------   4294967294  4294967294  0      2021-11-10T15:19:28  ticket4238791283652.txt
| rwx------   4294967294  4294967294  0      2021-11-10T15:19:28  ticket4238791283653.txt
| rwx------   4294967294  4294967294  0      2021-11-10T15:19:28  ticket4238791283654.txt
| rwx------   4294967294  4294967294  0      2021-11-10T15:19:29  ticket4238791283655.txt
| rwx------   4294967294  4294967294  0      2021-11-10T15:19:29  ticket4238791283656.txt
|_
| nfs-statfs: 
|   Filesystem    1K-blocks   Used        Available   Use%  Maxfilesize  Maxlink
|_  /TechSupport  25468924.0  15191288.0  10277636.0  60%   16.0T        1023
| nfs-showmount: 
|_  /TechSupport 
2049/tcp open  nlockmgr 1-4 (RPC #100021)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 53.52 seconds

```

![Screenshot 2024-10-22 at 1.59.00 PM.png](Footprinting%20Lab%20-%20Medium%2012724f42a85b80f392feff9f8a2e3f60/Screenshot_2024-10-22_at_1.59.00_PM.png)

When I tried to access the contents it specified that I did not have permission

![Screenshot 2024-10-22 at 2.12.49 PM.png](Footprinting%20Lab%20-%20Medium%2012724f42a85b80f392feff9f8a2e3f60/Screenshot_2024-10-22_at_2.12.49_PM.png)

```
1smtp {
 2    host=smtp.web.dev.inlanefreight.htb
 3    #port=25
 4    ssl=true
 5    user="alex"
 6    password="lol123!mD"
 7    from="alex.g@web.dev.inlanefreight.htb"
 8}

```

Next i see that smb is also available. Now i can enumerate the available shares.

![Screenshot 2024-10-22 at 2.27.03 PM.png](Footprinting%20Lab%20-%20Medium%2012724f42a85b80f392feff9f8a2e3f60/Screenshot_2024-10-22_at_2.27.03_PM.png)

![Screenshot 2024-10-22 at 2.28.28 PM.png](Footprinting%20Lab%20-%20Medium%2012724f42a85b80f392feff9f8a2e3f60/Screenshot_2024-10-22_at_2.28.28_PM.png)

Here I can see the Users share.

my current account doesn’t have access to winrm so I will now access that share and see if i can find another account.

![Screenshot 2024-10-22 at 2.31.06 PM.png](Footprinting%20Lab%20-%20Medium%2012724f42a85b80f392feff9f8a2e3f60/Screenshot_2024-10-22_at_2.31.06_PM.png)

After accessing alex’s desktop I found a mysql .lnk file

Using a get command I downloaded it .

I didn’t see any ports which indicated mssql but just in case i will try the following.

![Screenshot 2024-10-22 at 2.35.11 PM.png](Footprinting%20Lab%20-%20Medium%2012724f42a85b80f392feff9f8a2e3f60/Screenshot_2024-10-22_at_2.35.11_PM.png)

![Screenshot 2024-10-22 at 2.42.20 PM.png](Footprinting%20Lab%20-%20Medium%2012724f42a85b80f392feff9f8a2e3f60/Screenshot_2024-10-22_at_2.42.20_PM.png)

![Screenshot 2024-10-22 at 2.39.05 PM.png](Footprinting%20Lab%20-%20Medium%2012724f42a85b80f392feff9f8a2e3f60/Screenshot_2024-10-22_at_2.39.05_PM.png)

```
sa:87N1ns@slls83
```

the important file contained the following credentials

USER LIST in case of password reuse.

```
alex:lol123!mD
sa:87N1ns@slls83
alex:87N1ns@slls83
sa:lol123!mD
```

my next step is to use RDP to try and access the machine.

![Screenshot 2024-10-22 at 2.57.53 PM.png](Footprinting%20Lab%20-%20Medium%2012724f42a85b80f392feff9f8a2e3f60/Screenshot_2024-10-22_at_2.57.53_PM.png)

Now I see the SQL Server, I imagine the creds I previously got is for this.

![Screenshot 2024-10-22 at 2.58.44 PM.png](Footprinting%20Lab%20-%20Medium%2012724f42a85b80f392feff9f8a2e3f60/Screenshot_2024-10-22_at_2.58.44_PM.png)

This did not work.

![Screenshot 2024-10-22 at 3.01.25 PM.png](Footprinting%20Lab%20-%20Medium%2012724f42a85b80f392feff9f8a2e3f60/Screenshot_2024-10-22_at_3.01.25_PM.png)

After a few minutes of thinking I decided to run it as admin.

![Screenshot 2024-10-22 at 3.02.46 PM.png](Footprinting%20Lab%20-%20Medium%2012724f42a85b80f392feff9f8a2e3f60/Screenshot_2024-10-22_at_3.02.46_PM.png)

This worked. which Allowed me access to the server.

![Screenshot 2024-10-22 at 3.07.35 PM.png](Footprinting%20Lab%20-%20Medium%2012724f42a85b80f392feff9f8a2e3f60/Screenshot_2024-10-22_at_3.07.35_PM.png)

![Screenshot 2024-10-22 at 3.08.34 PM.png](Footprinting%20Lab%20-%20Medium%2012724f42a85b80f392feff9f8a2e3f60/Screenshot_2024-10-22_at_3.08.34_PM.png)

Here I managed to get the password.

This solved the lab.