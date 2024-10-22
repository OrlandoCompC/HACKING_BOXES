# Firewall and IDS/IPS Evasion - Medium Lab

---

After we conducted the first test and submitted our results to our client, the administrators made some changes and improvements to the `IDS/IPS` and firewall. We could hear that the administrators were not satisfied with their previous configurations during the meeting, and they could see that the network traffic could be filtered more strictly.

After the configurations are transferred to the system, our client wants to know if it is possible to find out our target's DNS server version. Submit the DNS server version of the target as the answer.

10.129.28.79

![Screenshot 2024-10-07 at 9.28.39 AM.png](Firewall%20and%20IDS%20IPS%20Evasion%20-%20Medium%20Lab%2011824f42a85b8085b2ffff2c09191a50/Screenshot_2024-10-07_at_9.28.39_AM.png)

TCP seems to be blocked so I now try to use UDP to see if maybe It is only blocking TCP 

So if it is being filtered then it is a good idea to try a UDP scan instead.