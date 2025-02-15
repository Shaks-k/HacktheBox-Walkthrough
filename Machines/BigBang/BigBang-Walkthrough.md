![Nmap Scan Results](https://raw.githubusercontent.com/Shaks-k/HacktheBox-Walkthrough/main/Machines/BigBang/Images/nmap_scan.png)

Scan Results
The Nmap scan revealed two open ports:

22/tcp (SSH) running OpenSSH 8.9p1 on Ubuntu 3ubuntu0.10
80/tcp (HTTP) running Apache 2.4.62 (Debian)
Additionally, the HTTP service indicates a redirect to http://blog.bigbang.htb/, which suggests that a virtual host is in use. This means we might need to add blog.bigbang.htb to our /etc/hosts file for proper enumeration.
