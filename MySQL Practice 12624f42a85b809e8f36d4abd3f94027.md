# MySQL Practice

---

![Screenshot 2024-10-21 at 9.03.46 AM.png](MySQL%20Practice%2012624f42a85b809e8f36d4abd3f94027/Screenshot_2024-10-21_at_9.03.46_AM.png)

Ip =10.129.12.121

I will first start by scanning the MySQL server to determine the version.

```
sudo nmap -sS -sV --script mysql* -p3306 10.129.12.121
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-10-21 08:05 CDT
Nmap scan report for 10.129.12.121
Host is up (0.0087s latency).

PORT     STATE SERVICE VERSION
3306/tcp open  mysql   MySQL 8.0.27-0ubuntu0.20.04.1
| mysql-enum: 
|   Accounts: No valid accounts found
|_  Statistics: Performed 9 guesses in 5 seconds, average tps: 1.8
| mysql-info: 
|   Protocol: 10
|   Version: 8.0.27-0ubuntu0.20.04.1
|   Thread ID: 11
|   Capabilities flags: 65535
|   Some Capabilities: InteractiveClient, IgnoreSpaceBeforeParenthesis, SupportsTransactions, SupportsCompression, DontAllowDatabaseTableColumn, Speaks41ProtocolOld, ODBCClient, LongColumnFlag, FoundRows, IgnoreSigpipes, SwitchToSSLAfterHandshake, Speaks41ProtocolNew, SupportsLoadDataLocal, Support41Auth, LongPassword, ConnectWithDatabase, SupportsMultipleStatments, SupportsMultipleResults, SupportsAuthPlugins
|   Status: Autocommit
|   Salt: g%"(<+*	}\x18Z)}hM\x01~J\x1A(
|_  Auth Plugin Name: caching_sha2_password
| mysql-brute: 
|   Accounts: No valid accounts found
|   Statistics: Performed 39136 guesses in 420 seconds, average tps: 98.6
|_  ERROR: The service seems to have failed or is heavily firewalled...

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 427.62 seconds

```

I previously had the creds, robin:robin so I will now try these creds on this server.

![Screenshot 2024-10-21 at 9.16.56 AM.png](MySQL%20Practice%2012624f42a85b809e8f36d4abd3f94027/Screenshot_2024-10-21_at_9.16.56_AM.png)

![Screenshot 2024-10-21 at 9.18.16 AM.png](MySQL%20Practice%2012624f42a85b809e8f36d4abd3f94027/Screenshot_2024-10-21_at_9.18.16_AM.png)

I am now supposed to find the email address of the customer Otto Lang.

![Screenshot 2024-10-21 at 9.20.01 AM.png](MySQL%20Practice%2012624f42a85b809e8f36d4abd3f94027/Screenshot_2024-10-21_at_9.20.01_AM.png)

![Screenshot 2024-10-21 at 9.21.24 AM.png](MySQL%20Practice%2012624f42a85b809e8f36d4abd3f94027/Screenshot_2024-10-21_at_9.21.24_AM.png)

Here we can see the email.

This completed the lab.