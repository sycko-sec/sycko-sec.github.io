---
layout: post
category: writeups
title: THM Owasp Top 10 Machine
---


As I start the module, a prompt alerts me to the machine’s vulnerability and points out that all the information I need for exploitation is available online. Having just covered the OWASP Top 10 vulnerabilities, like Cross-Site Scripting, SQL Injection, and Remote Code Execution, I have a solid foundation for the task. I begin by running an Nmap scan to identify the machine's active services.

![Untitled](assets/images/owasp2.png)

The scan reveals nothing unusual—just SSH and an Apache-hosted website. I visit the website to explore further and notice it’s built with PHP and MySQL. Recalling from earlier in the module that many known exploits are listed on [Exploit-DB](https://www.exploit-db.com/), I search for "bookstore exploit-db" in Firefox, which brings up several relevant Exploit-DB links.

![Untitled](assets/images/owasp3.png)

![Untitled](assets/images/owasp4.png)

Clicking on the first result, I find several links and a lot of code. Looking at the first URL, it's clear that this exploit targets the website I explored earlier—this must be the exploit I need!

Reviewing the code, I see it’s a Python script that embeds a payload into a fake image, which can be uploaded to the site to establish a web shell. To run the script, I download it and execute it in my terminal using the command `python3 <name of file> <URL>`.

![Untitled](assets/images/owasp5.png)

![Untitled](assets/images/owasp6.png)

Success! The web shell is up and running, letting me execute commands on the web server. I begin by checking my current location and access permissions. Next, I test if I can read `/etc/passwd`—and I can. The module asks for the number of characters in the `/etc/passwd` file, which I can quickly count using the command `wc -c /etc/passwd`.

![Untitled](assets/images/owasp7.png)

![Untitled](assets/images/owasp8.png)

![Untitled](assets/images/owasp1.png)

This hands-on experience has been a valuable step in strengthening my web exploitation skills!