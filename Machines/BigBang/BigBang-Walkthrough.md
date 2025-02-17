![Nmap Scan Results](https://raw.githubusercontent.com/Shaks-k/HacktheBox-Walkthrough/main/Machines/BigBang/Images/nmap_scan.png)

Scan Results
The Nmap scan revealed two open ports:

22/tcp (SSH) running OpenSSH 8.9p1 on Ubuntu 3ubuntu0.10
80/tcp (HTTP) running Apache 2.4.62 (Debian)
Additionally, the HTTP service indicates a redirect to http://blog.bigbang.htb/, which suggests that a virtual host is in use. This means we might need to add blog.bigbang.htb to our /etc/hosts file for proper enumeration.

![WPScan Results](https://raw.githubusercontent.com/Shaks-k/HacktheBox-Walkthrough/main/Machines/BigBang/Images/wpscan.png)

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

**Outdated WordPress Plugin - BuddyForms**

***Installed Version: 2.7.7
Latest Version: 2.8.15
This might contain security vulnerabilities that could be exploited.***

Upon searching for known vulnerabilitis for BuddyForms 2.7.7 one can find an unauthenticated insecure deserialization vulnerability found in the in the BuddyForm plugin.

In the vulnerable versions, the problem lies in the ‘buddyforms_upload_image_from_url()’ function of the ‘./includes/functions.php’ file

The exploitation of this vulnerability is based on 3 steps

Create a malicious phar file by making it look like an image.
Send the malicious phar file on the server
Call the file with the ‘phar://’ wrapper.

https://medium.com/tenable-techblog/wordpress-buddyforms-plugin-unauthenticated-insecure-deserialization-cve-2023-26326-3becb5575ed8

Go through this blog by Joshua Martinelle

Joshua Martinelle
Follow
Joshua Martinelle
34 Followers
Security Researcher, working at Tenable

and find a way to manage to trigger an arbitrary deserialization
So create the phar file, host it from your system and upload it to the server

![Http_Host]https://raw.githubusercontent.com/Shaks-k/HacktheBox-Walkthrough/main/Machines/BigBang/Images/http_host.png

Upload the file

![File_Upload]https://raw.githubusercontent.com/Shaks-k/HacktheBox-Walkthrough/main/Machines/BigBang/Images/evil_phar_upload.png

Now you can see this file 

![File_Upload]https://raw.githubusercontent.com/Shaks-k/HacktheBox-Walkthrough/main/Machines/BigBang/Images/wp-content_uploads.png

Now the file stored on server, you try to execute it with phar:// ../ filter to read the file but deserialization fails, as we dont have valid plugin (Dummy Plugin) as mentioned in the above blog by Joshua Martinelle

![File_Read]https://raw.githubusercontent.com/Shaks-k/HacktheBox-Walkthrough/main/Machines/BigBang/Images/phar_read.png










