# Footprinting Lab - Easy

---

We were commissioned by the company `Inlanefreight Ltd` to test three different servers in their internal network. The company uses many different services, and the IT security department felt that a penetration test was necessary to gain insight into their overall security posture.

The first server is an internal DNS server that needs to be investigated. In particular, our client wants to know what information we can get out of these services and how this information could be used against its infrastructure. Our goal is to gather as much information as possible about the server and find ways to use that information against the company. However, our client has made it clear that it is forbidden to attack the services aggressively using exploits, as these services are in production.

Additionally, our teammates have found the following credentials "ceil:qwer1234", and they pointed out that some of the company's employees were talking about SSH keys on a forum.

The administrators have stored a `flag.txt` file on this server to track our progress and measure success. Fully enumerate the target and submit the contents of this file as proof.

creds=ceil:qwer1234

![Screenshot 2024-10-22 at 1.19.26 PM.png](Footprinting%20Lab%20-%20Easy%2012724f42a85b80ebabd8e05c5855b30c/Screenshot_2024-10-22_at_1.19.26_PM.png)

I start by scanning all the ports and then I will do a deeper scan on these services.

![Screenshot 2024-10-22 at 1.20.55 PM.png](Footprinting%20Lab%20-%20Easy%2012724f42a85b80ebabd8e05c5855b30c/Screenshot_2024-10-22_at_1.20.55_PM.png)

![Screenshot 2024-10-22 at 1.23.40 PM.png](Footprinting%20Lab%20-%20Easy%2012724f42a85b80ebabd8e05c5855b30c/Screenshot_2024-10-22_at_1.23.40_PM.png)

I tried to use anonymous login just in case. Now I will use the creds.

![Screenshot 2024-10-22 at 1.25.34 PM.png](Footprinting%20Lab%20-%20Easy%2012724f42a85b80ebabd8e05c5855b30c/Screenshot_2024-10-22_at_1.25.34_PM.png)

![Screenshot 2024-10-22 at 1.26.49 PM.png](Footprinting%20Lab%20-%20Easy%2012724f42a85b80ebabd8e05c5855b30c/Screenshot_2024-10-22_at_1.26.49_PM.png)

The creds seem to work now I will try to download the contents of the ftp server.

FTP server was empty

![Screenshot 2024-10-22 at 1.29.18 PM.png](Footprinting%20Lab%20-%20Easy%2012724f42a85b80ebabd8e05c5855b30c/Screenshot_2024-10-22_at_1.29.18_PM.png)

![Screenshot 2024-10-22 at 1.37.07 PM.png](Footprinting%20Lab%20-%20Easy%2012724f42a85b80ebabd8e05c5855b30c/Screenshot_2024-10-22_at_1.37.07_PM.png)

After I entered the .ssh directory I found

```
-rw-rw-r--   1 ceil     ceil          738 Nov 10  2021 authorized_keys
-rw-------   1 ceil     ceil         3381 Nov 10  2021 id_rsa
-rw-r--r--   1 ceil     ceil          738 Nov 10  2021 id_rsa.pub

```

now I got the private key through which I can use to ssh into the machine.

![Screenshot 2024-10-22 at 1.40.47 PM.png](Footprinting%20Lab%20-%20Easy%2012724f42a85b80ebabd8e05c5855b30c/Screenshot_2024-10-22_at_1.40.47_PM.png)

![Screenshot 2024-10-22 at 1.42.19 PM.png](Footprinting%20Lab%20-%20Easy%2012724f42a85b80ebabd8e05c5855b30c/Screenshot_2024-10-22_at_1.42.19_PM.png)

Here I got the flag and solved the mini lab.