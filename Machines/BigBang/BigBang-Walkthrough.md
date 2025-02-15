![Nmap Scan Results](https://raw.githubusercontent.com/Shaks-k/HacktheBox-Walkthrough/main/Machines/BigBang/Images/nmap_scan.png)

Scan Results
The Nmap scan revealed two open ports:

22/tcp (SSH) running OpenSSH 8.9p1 on Ubuntu 3ubuntu0.10
80/tcp (HTTP) running Apache 2.4.62 (Debian)
Additionally, the HTTP service indicates a redirect to http://blog.bigbang.htb/, which suggests that a virtual host is in use. This means we might need to add blog.bigbang.htb to our /etc/hosts file for proper enumeration.



The WPScan results indicate several important security weaknesses:

Server Information:

Apache/2.4.62 (Debian)
PHP 8.3.2
The website is running WordPress 6.5.4, which is outdated (latest version is newer).
Potential Attack Vectors Identified:

XML-RPC enabled: http://blog.bigbang.htb/xmlrpc.php
This can be exploited for brute force attacks and pingback DoS attacks.
Directory listing enabled: http://blog.bigbang.htb/wp-content/uploads/
Possible information disclosure or file upload vulnerability.
External WP-Cron enabled: http://blog.bigbang.htb/wp-cron.php
Could be abused to execute unauthorized scheduled tasks.
Outdated WordPress Theme:

twentytwentyfour (Version 1.1)
Latest version available: 1.3
Directory listing enabled under the theme directory, possibly leaking sensitive files.
Outdated WordPress Plugin - BuddyForms

***Installed Version: 2.7.7
Latest Version: 2.8.15
This might contain security vulnerabilities that could be exploited.***
