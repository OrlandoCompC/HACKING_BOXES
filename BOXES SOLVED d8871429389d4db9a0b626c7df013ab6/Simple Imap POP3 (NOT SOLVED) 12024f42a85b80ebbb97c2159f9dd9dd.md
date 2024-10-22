# Simple Imap/POP3 (NOT SOLVED)

---

I get this Ip and now i got to find information about the organization

10.129.88.216

```
┌─[us-academy-5]─[10.10.14.189]─[htb-ac-1456674@htb-al4tbdpkje]─[~]
└──╼ [★]$  sudo nmap 10.129.88.216 -sV -p110,143,993,995 -sC
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-10-15 10:47 CDT
Nmap scan report for 10.129.88.216
Host is up (0.62s latency).

PORT    STATE SERVICE  VERSION
110/tcp open  pop3     Dovecot pop3d
|_pop3-capabilities: PIPELINING TOP RESP-CODES SASL AUTH-RESP-CODE STLS UIDL CAPA
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=dev.inlanefreight.htb/organizationName=InlaneFreight Ltd/stateOrProvinceName=London/countryName=UK
| Not valid before: 2021-11-08T23:10:05
|_Not valid after:  2295-08-23T23:10:05
143/tcp open  imap     Dovecot imapd
| ssl-cert: Subject: commonName=dev.inlanefreight.htb/organizationName=InlaneFreight Ltd/stateOrProvinceName=London/countryName=UK
| Not valid before: 2021-11-08T23:10:05
|_Not valid after:  2295-08-23T23:10:05
|_ssl-date: TLS randomness does not represent time
|_imap-capabilities: LOGIN-REFERRALS post-login have listed IMAP4rev1 ENABLE capabilities Pre-login OK LOGINDISABLEDA0001 ID LITERAL+ IDLE STARTTLS more SASL-IR
993/tcp open  ssl/imap Dovecot imapd
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=dev.inlanefreight.htb/organizationName=InlaneFreight Ltd/stateOrProvinceName=London/countryName=UK
| Not valid before: 2021-11-08T23:10:05
|_Not valid after:  2295-08-23T23:10:05
|_imap-capabilities: AUTH=PLAINA0001 post-login LOGIN-REFERRALS IMAP4rev1 ENABLE have ID OK capabilities Pre-login LITERAL+ IDLE listed more SASL-IR
995/tcp open  ssl/pop3 Dovecot pop3d
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=dev.inlanefreight.htb/organizationName=InlaneFreight Ltd/stateOrProvinceName=London/countryName=UK
| Not valid before: 2021-11-08T23:10:05
|_Not valid after:  2295-08-23T23:10:05
|_pop3-capabilities: PIPELINING TOP RESP-CODES SASL(PLAIN) AUTH-RESP-CODE USER UIDL CAPA

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 16.06 seconds
```

```
─[us-academy-5]─[10.10.14.189]─[htb-ac-1456674@htb-al4tbdpkje]─[~]
└──╼ [★]$ curl -k 'imaps://10.129.88.216' --user robin:robin -v
*   Trying 10.129.88.216:993...
* Connected to 10.129.88.216 (10.129.88.216) port 993 (#0)
* TLSv1.3 (OUT), TLS handshake, Client hello (1):
* TLSv1.3 (IN), TLS handshake, Server hello (2):
* TLSv1.3 (IN), TLS handshake, Encrypted Extensions (8):
* TLSv1.3 (IN), TLS handshake, Certificate (11):
* TLSv1.3 (IN), TLS handshake, CERT verify (15):
* TLSv1.3 (IN), TLS handshake, Finished (20):
* TLSv1.3 (OUT), TLS change cipher, Change cipher spec (1):
* TLSv1.3 (OUT), TLS handshake, Finished (20):
* SSL connection using TLSv1.3 / TLS_AES_256_GCM_SHA384
* Server certificate:
*  subject: C=UK; ST=London; L=London; O=InlaneFreight Ltd; OU=DevOps Dep�artment; CN=dev.inlanefreight.htb; emailAddress=cto.dev@dev.inlanefreight.htb
*  start date: Nov  8 23:10:05 2021 GMT
*  expire date: Aug 23 23:10:05 2295 GMT
*  issuer: C=UK; ST=London; L=London; O=InlaneFreight Ltd; OU=DevOps Dep�artment; CN=dev.inlanefreight.htb; emailAddress=cto.dev@dev.inlanefreight.htb
*  SSL certificate verify result: self-signed certificate (18), continuing anyway.
* TLSv1.3 (IN), TLS handshake, Newsession Ticket (4):
* TLSv1.3 (IN), TLS handshake, Newsession Ticket (4):
* old SSL session ID is stale, removing
< * OK [CAPABILITY IMAP4rev1 SASL-IR LOGIN-REFERRALS ID ENABLE IDLE LITERAL+ AUTH=PLAIN] HTB{roncfbw7iszerd7shni7jr2343zhrj}
> A001 CAPABILITY
< * CAPABILITY IMAP4rev1 SASL-IR LOGIN-REFERRALS ID ENABLE IDLE LITERAL+ AUTH=PLAIN
< A001 OK Pre-login capabilities listed, post-login capabilities have more.
> A002 AUTHENTICATE PLAIN AHJvYmluAHJvYmlu
< * CAPABILITY IMAP4rev1 SASL-IR LOGIN-REFERRALS ID ENABLE IDLE SORT SORT=DISPLAY THREAD=REFERENCES THREAD=REFS THREAD=ORDEREDSUBJECT MULTIAPPEND URL-PARTIAL CATENATE UNSELECT CHILDREN NAMESPACE UIDPLUS LIST-EXTENDED I18NLEVEL=1 CONDSTORE QRESYNC ESEARCH ESORT SEARCHRES WITHIN CONTEXT=SEARCH LIST-STATUS BINARY MOVE SNIPPET=FUZZY PREVIEW=FUZZY LITERAL+ NOTIFY SPECIAL-USE
< A002 OK Logged in
> A003 LIST "" *
< * LIST (\Noselect \HasChildren) "." DEV
* LIST (\Noselect \HasChildren) "." DEV
< * LIST (\Noselect \HasChildren) "." DEV.DEPARTMENT
* LIST (\Noselect \HasChildren) "." DEV.DEPARTMENT
< * LIST (\HasNoChildren) "." DEV.DEPARTMENT.INT
* LIST (\HasNoChildren) "." DEV.DEPARTMENT.INT
< * LIST (\HasNoChildren) "." INBOX
* LIST (\HasNoChildren) "." INBOX
< A003 OK List completed (0.006 + 0.000 + 0.005 secs).
* Connection #0 to host 10.129.88.216 left intact

```