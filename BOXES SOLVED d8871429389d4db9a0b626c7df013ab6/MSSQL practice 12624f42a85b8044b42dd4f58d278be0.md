# MSSQL practice

---

This is some simple practice with mssql to learn how to work with it.

![Screenshot 2024-10-21 at 10.11.19 AM.png](MSSQL%20practice%2012624f42a85b8044b42dd4f58d278be0/Screenshot_2024-10-21_at_10.11.19_AM.png)

Ip = 10.129.230.249

I will start by trying to get information on the MSSQL server but instead of nmap I will be using metasploit because it is very useful when dealing with MSSQL 

![Screenshot 2024-10-21 at 10.13.51 AM.png](MSSQL%20practice%2012624f42a85b8044b42dd4f58d278be0/Screenshot_2024-10-21_at_10.13.51_AM.png)

I will be using this  module.

![Screenshot 2024-10-21 at 10.15.17 AM.png](MSSQL%20practice%2012624f42a85b8044b42dd4f58d278be0/Screenshot_2024-10-21_at_10.15.17_AM.png)

Here we can see the host name of the server which is ILF-SQL-01

In this case I have access to an account with the creds backdoor:Password1

so I will use this to connect to it .

![Screenshot 2024-10-21 at 10.17.49 AM.png](MSSQL%20practice%2012624f42a85b8044b42dd4f58d278be0/Screenshot_2024-10-21_at_10.17.49_AM.png)

I will be using the following format to connect. I always try to use impacket when I can because its something I trust and know that works.

When I orignally ran the command it did not work because these are windows creds so I have to use the -windows-auth to get authenticated.

![Screenshot 2024-10-21 at 10.20.56 AM.png](MSSQL%20practice%2012624f42a85b8044b42dd4f58d278be0/Screenshot_2024-10-21_at_10.20.56_AM.png)

![Screenshot 2024-10-21 at 10.24.35 AM.png](MSSQL%20practice%2012624f42a85b8044b42dd4f58d278be0/Screenshot_2024-10-21_at_10.24.35_AM.png)

This completed the lab.