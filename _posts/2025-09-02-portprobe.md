# Port Scanning & Packet Analysis using Nmap and Wireshark
This is the basic task of checking our local network for vulnerable ports. The ports are the most searched and most found vulnerabilities if they are not secured. 

There are 65535 ports. 

Well-Known Ports - 0 to 1023

Registered Ports - 1024 to 49151

Private Ports - 49152 to 65535

Tool Usage 
Nmap is a powerful tool used for network discovery and security auditing. It detects open ports, services, OS versions, IP addresses, and can perform vulnerability scans using NSE scripts.

Task 1:
Local network scan with NMAP
To check the ports available in our network, lets spin our kali linux in our VMware. Lets open terminal and run ip a.

ip a -> This command shows our ipaddress, where we now get the subnet and perform the nmap scan
lets say my ip is 192.168.45.1 and my subnet will be 192.168.45.0/24

<pre>
ip a

1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever

2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether XX:XX:XX:XX:XX:XX brd ff:ff:ff:ff:ff:ff
    inet 192.168.XXX.XXX/24 brd 192.168.XXX.255 scope global dynamic noprefixroute eth0
       valid_lft XXXXsec preferred_lft XXXXsec
    inet6 XXXX::XXXX:XXXX:XXXX:XXXX/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
</pre>

Now run the nmap, here i am using nmap in terminal we can also use zenmap for the scans.
nmap -sS 192.168.45.0/24 

<pre>
nmap -sS 192.168.178.0/24

Starting Nmap 7.95 ( https://nmap.org ) at 2025-08-04 08:24 EDT

Nmap scan report for 192.168.178.xxx
Host is up (0.021s latency).
All 1000 scanned ports on 192.168.178.xxx are in ignored states.
Not shown: 1000 filtered tcp ports (no-response)
MAC Address: [REDACTED_VMWARE_MAC]

Nmap scan report for 192.168.xxx.xxx
Host is up (0.00014s latency).
Not shown: 999 closed tcp ports (reset)
PORT   STATE SERVICE
53/tcp open  domain
MAC Address: [REDACTED_VMWARE_MAC]

Nmap scan report for 192.168.xxx.xxx
Host is up (0.0016s latency).
Not shown: 977 closed tcp ports (reset)
PORT     STATE SERVICE
21/tcp   open  ftp  
22/tcp   open  ssh  
23/tcp   open  telnet  
25/tcp   open  smtp  
53/tcp   open  domain  
80/tcp   open  http  
111/tcp  open  rpcbind  
139/tcp  open  netbios-ssn  
445/tcp  open  microsoft-ds  
512/tcp  open  exec  
513/tcp  open  login  
514/tcp  open  shell  
1099/tcp open  rmiregistry  
1524/tcp open  ingreslock  
2049/tcp open  nfs  
2121/tcp open  ccproxy-ftp  
3306/tcp open  mysql  
5432/tcp open  postgresql  
5900/tcp open  vnc  
6000/tcp open  X11  
6667/tcp open  irc  
8009/tcp open  ajp13  
8180/tcp open  unknown  
MAC Address: [REDACTED_VMWARE_MAC]

Nmap scan report for 192.168.xxx.xxx
Host is up (0.00048s latency).
All 1000 scanned ports on 192.168.xxx.xxx are in ignored states.
Not shown: 1000 filtered tcp ports (no-response)
MAC Address: [REDACTED_VMWARE_MAC]

Nmap scan report for 192.168.xxx.xxx
Host is up (0.0000040s latency).
All 1000 scanned ports on 192.168.xxx.xxx are in ignored states.
Not shown: 1000 closed tcp ports (reset)

Nmap done: 256 IP addresses (5 hosts up) scanned in 8.11 seconds
</pre>

** I have used Metasploitable tool here for further understanding and exploitation **

Note -  Metasploitable is a vulnerable virtual machine designed for better understanding

Here my seaarch result showed all vulnerable ports in my network, but I know the ports, but what versions the ports using/following, is the vulnerability already known, or is the vulnerability already patched. ushhh so many questions lets get answers to these with further scanning 
Now let's get versions now,

<pre>
nmap -sS -sV 192.168.xxx.xxx
Starting Nmap 7.95 ( https://nmap.org ) at 2025-08-04 08:25 EDT
Nmap scan report for 192.168.XXX.XXX
Host is up (0.0016s latency).
Not shown: 977 closed tcp ports (reset)
PORT     STATE SERVICE     VERSION
21/tcp   open  ftp         vsftpd 2.3.4
22/tcp   open  ssh         OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)
23/tcp   open  telnet      Linux telnetd
25/tcp   open  smtp        Postfix smtpd
53/tcp   open  domain      ISC BIND 9.4.2
80/tcp   open  http        Apache httpd 2.2.8 ((Ubuntu) DAV/2)
111/tcp  open  rpcbind     2 (RPC #100000)
139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
512/tcp  open  exec        netkit-rsh rexecd
513/tcp  open  login       OpenBSD or Solaris rlogind
514/tcp  open  tcpwrapped
1099/tcp open  java-rmi    GNU Classpath grmiregistry
1524/tcp open  bindshell   Metasploitable root shell
2049/tcp open  nfs         2-4 (RPC #100003)
2121/tcp open  ftp         ProFTPD 1.3.1
3306/tcp open  mysql       MySQL 5.0.51a-3ubuntu5
5432/tcp open  postgresql  PostgreSQL DB 8.3.0 - 8.3.7
5900/tcp open  vnc         VNC (protocol 3.3)
6000/tcp open  X11         (access denied)
6667/tcp open  irc         UnrealIRCd
8009/tcp open  ajp13       Apache Jserv (Protocol v1.3)
8180/tcp open  http        Apache Tomcat/Coyote JSP engine 1.1
MAC Address: 00:0C:29:XX:XX:XX (VMware)
Service Info: Hosts:  *.localdomain, irc.*.LAN; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 11.82 seconds
</pre>

Now as the nmap scan is done, we can check and get the information through wireshark too. Lets start the Wireshark scan and see how the network flows //Before getting into the Wireshark, the basic to know is OSI and TCP models, to get clear clarity on OSI model, [Visit my Cybersecurity Blog](https://wearejam.github.io/cyberjournallogs/)

With the above scan we can see much data but the required ports can be filtered and highlighted according to our findings, Here i have filtered TCP packets
As we performed syn scan, we are performing only half handshake mean while tcp scan -sT does full handshake and burdens the server.
In this sync scan host sends SYN flag, if the port open the server sends SYN/ACK and later the host closes with RST flag which drops the handshake. LESS NOISE

![Port Probe Result](https://github.com/WEAREJAM/Kickstart_at_ElevateLabs-PortProbe/blob/main/asserts/sample2.png?raw=true)

![Port Probe Result](https://github.com/WEAREJAM/Kickstart_at_ElevateLabs-PortProbe/blob/main/asserts/sample3.png?raw=true)

The above Wireshark result shows how the flags are communicating - the best way to escape a noisy TCP 3-way handshake. May ways to bypass just KNOW THE USAGE

Now we know the vulnerable ports and protocols. Do you know the nmap also scans for vulnerabilities (Aggressive scan), as for the basic and all lets see with simple scan rather than NSE scripts for further deep analysis we can proceed with script scans 
Drawback - DETECTABLE 

<pre>
nmap -A -T4 192.168.xxx.xxx
Starting Nmap 7.95 ( https://nmap.org ) at 2025-08-04 08:28 EDT
Nmap scan report for 192.168.XXX.XXX
Host is up (0.0051s latency).
Not shown: 977 closed tcp ports (reset)
PORT     STATE SERVICE     VERSION
21/tcp   open  ftp         vsftpd 2.3.4
|_ftp-anon: Anonymous FTP login allowed (FTP code 230)
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to 192.168.XXX.XXX
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      vsFTPd 2.3.4 - secure, fast, stable
|_End of status
22/tcp   open  ssh         OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)
| ssh-hostkey: 
|   1024 XX:XX:XX:XX:XX:XX:XX:XX:XX:XX:XX:XX:XX:XX:XX:XX (DSA)
|_  2048 XX:XX:XX:XX:XX:XX:XX:XX:XX:XX:XX:XX:XX:XX:XX:XX (RSA)
23/tcp   open  telnet      Linux telnetd
25/tcp   open  smtp        Postfix smtpd
|_smtp-commands: *.localdomain, PIPELINING, SIZE 10240000, VRFY, ETRN, STARTTLS, ENHANCEDSTATUSCODES, 8BITMIME, DSN
|_ssl-date: 2025-08-04T12:28:35+00:00; 0s from scanner time.
| sslv2: 
|   SSLv2 supported
|   ciphers: 
|     SSL2_DES_64_CBC_WITH_MD5
|     SSL2_RC4_128_WITH_MD5
|     SSL2_RC2_128_CBC_EXPORT40_WITH_MD5
|     SSL2_RC4_128_EXPORT40_WITH_MD5
|     SSL2_RC2_128_CBC_WITH_MD5
|_    SSL2_DES_192_EDE3_CBC_WITH_MD5
| ssl-cert: Subject: commonName=*.localdomain/organizationName=OCOSA/stateOrProvinceName=Hidden/countryName=XX
| Not valid before: 2010-03-17T14:07:45
|_Not valid after:  2010-04-16T14:07:45
53/tcp   open  domain      ISC BIND 9.4.2
| dns-nsid: 
|_  bind.version: 9.4.2
80/tcp   open  http        Apache httpd 2.2.8 ((Ubuntu) DAV/2)
|_http-server-header: Apache/2.2.8 (Ubuntu) DAV/2
|_http-title: Metasploitable2 - Linux
111/tcp  open  rpcbind     2 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100003  2,3,4       2049/tcp   nfs
|   100003  2,3,4       2049/udp   nfs
|   100005  1,2,3      XXXXX/tcp   mountd
|   100005  1,2,3      XXXXX/udp   mountd
|_  100021  1,3,4      XXXXX/tcp   nlockmgr
139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn Samba smbd 3.0.20-Debian (workgroup: WORKGROUP)
512/tcp  open  exec        netkit-rsh rexecd
513/tcp  open  login       OpenBSD or Solaris rlogind
514/tcp  open  tcpwrapped
1099/tcp open  java-rmi    GNU Classpath grmiregistry
1524/tcp open  bindshell   Metasploitable root shell
2049/tcp open  nfs         2-4 (RPC #100003)
2121/tcp open  ftp         ProFTPD 1.3.1
3306/tcp open  mysql       MySQL 5.0.51a-3ubuntu5
| mysql-info: 
|   Protocol: 10
|   Version: 5.0.51a-3ubuntu5
|   Thread ID: 10
|   Capabilities flags: 43564
|   Some Capabilities: Support41Auth, LongColumnFlag, SupportsTransactions, SwitchToSSLAfterHandshake, ConnectWithDatabase, SupportsCompression, Speaks41ProtocolNew
|   Status: Autocommit
|_  Salt: [REDACTED]
5432/tcp open  postgresql  PostgreSQL DB 8.3.0 - 8.3.7
| ssl-cert: Subject: commonName=*.localdomain/organizationName=OCOSA/stateOrProvinceName=Hidden/countryName=XX
| Not valid before: 2010-03-17T14:07:45
|_Not valid after:  2010-04-16T14:07:45
|_ssl-date: 2025-08-04T12:28:35+00:00; 0s from scanner time.
5900/tcp open  vnc         VNC (protocol 3.3)
| vnc-info: 
|   Protocol version: 3.3
|   Security types: 
|_    VNC Authentication (2)
6000/tcp open  X11         (access denied)
6667/tcp open  irc         UnrealIRCd
| irc-info: 
|   users: 1
|   servers: 1
|   lusers: 1
|   lservers: 0
|   server: irc.*.LAN
|   version: Unreal3.2.8.1. irc.*.LAN 
|   uptime: 0 days, 0:19:59
|   source ident: nmap
|   source host: [REDACTED]
|_  error: Closing Link: [REDACTED] (Quit: [REDACTED])
8009/tcp open  ajp13       Apache Jserv (Protocol v1.3)
|_ajp-methods: Failed to get a valid response for the OPTION request
8180/tcp open  http        Apache Tomcat/Coyote JSP engine 1.1
|_http-favicon: Apache Tomcat
|_http-title: Apache Tomcat/5.5
|_http-server-header: Apache-Coyote/1.1
MAC Address: 00:0C:29:XX:XX:XX (VMware)
Device type: general purpose
Running: Linux 2.6.X
OS CPE: cpe:/o:linux:linux_kernel:2.6
OS details: Linux 2.6.9 - 2.6.33
Network Distance: 1 hop
Service Info: Hosts:  *.localdomain, irc.*.LAN; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_clock-skew: mean: 1h00m00s, deviation: 2h00m01s, median: 0s
| smb-os-discovery: 
|   OS: Unix (Samba 3.0.20-Debian)
|   Computer name: metasploitable
|   NetBIOS computer name: 
|   Domain name: localdomain
|   FQDN: *.localdomain
|_  System time: 2025-08-04T08:28:27-04:00
|_nbstat: NetBIOS name: METASPLOITABLE, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
|_smb2-time: Protocol negotiation failed (SMB2)
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)

TRACEROUTE
HOP RTT     ADDRESS
1   5.09 ms 192.168.XXX.XXX

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 22.70 seconds
</pre>

I you observe i have done full vunerability scan with -A adn gave it a time gap with T4 which reduces vm burdening the server with force scanning
Do all domains respond YES 
Do all domains expose vulnerabilities? NO -> For every scan, we are burdening the server with N number of requests. The server might not respond quickly, and some of these requests may also be blocked by the firewall.
Once the vulnerabilites are to be noted and saved as we dont know the firewall may block us for the next aggressive scan. // Yah happened to me // 

WE HAVE THE TARGET NOW, WITH PORTS AND VULNERABLE SERVICES AND WITH THE AGGRESSIVE SCAN WE ALSO HAVE THE PATH TO ATTACK 

LET'S PROCEED FURTHER ON HOW TO EXPLOIT THE PORTS ........ >< ........ 

____Jamming With Jam____
