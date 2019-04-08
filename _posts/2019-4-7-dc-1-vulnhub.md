---
layout: post
title: Quick trip to root! DC-1 (Vulnhub)
---
<img src="https://www.hackthebox.eu/badge/image/45668" alt="Hack The Box"><br>

[@Kr0ff](https://twitter.com/CptXrat)

# ~$Ov3rv1ew

This is a writeup of the [DC-1 VulnHub](https://www.vulnhub.com/series/dc-1,199/) box. The vulnerability was that there was installed an outdated version of [Drupal CMS](https://unit42.paloaltonetworks.com/unit42-exploit-wild-drupalgeddon2-analysis-cve-2018-7600/) which lead to the exploitation of the webserver and getting a shell as 'www-data'. After that, a short digging in the system has showed that "find" program in Linux has a SUID which allowed the attacker to privilige escalate to root user.

Although this is an easy box, there was a rabbit hole that some people might have felt in. This rabbit hole was the kernel version of the system (3.2.0-6-428). Some people may have thought that [DirtyCow](https://github.com/dirtycow/dirtycow.github.io/wiki/VulnerabilityDetails) exploit would work, but DirtyCow is not always a good idea to run, due to possible crashes of the system that it can cause. Even if DirtyCow would've worked, it should be the last option for privilige escalation.

Official CVE page of the Drupal exploit can be found [here](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-7600)

## ~$St4rt_J0urn3y

Our journey will start with a Nmap scan on the target to determine what services are open on the target. Maybe there could be something that is outdated or possibly something is misconfigured and Nmap's scripts could identify that.

```bash
$ nmap -sC -sV -v -oN <PATH_TO_OUTPUT> <IP>
```

![nmap]({{ site.baseurl }}/images/dc-1-vulnhub/nmap.png)

We can see that Nmap has found 3 ports open:

- 80 / HTTP
- 111 / RPC
- 22 / SSH

We can also see that Nmap has found some default folders and files that can be found with an installation of Drupal CMS. We can check for 'robots.txt'. We find the file "CHANGELOG.txt" which is placed in the root directory of the webserver, however, we get that the file was not found.

![robots.txt]({{ site.baseurl }}/images/dc-1-vulnhub/robots-txt.png)

![changelog]({{ site.baseurl }}/images/dc-1-vulnhub/changelog-nonexisting.png)

Luckily, there is a tool called 'droopescan', it will enumerate the webserver and the installation of the Drupal CMS and it will find any misconfigurations and possible vulnerabilities that we can exploit.

Quick clone of the repository of Droopscan and running the commands:

```bash
1. git clone https://github.com/droope/droopescan
2. cd droopescan
3. pip install -r requirements.txt
4. ./droopescan scan --help

If you would like to install the tool on the system run:
1. cd droopescan
2. python setup.py install
```

That will install the tool and we are ready to use it. Now let's enumerate the machine with the tool.

```droopescan scan drupal -u <IP_OF_TARGET> -t 10```

![droopescan]({{ site.baseurl }}/images/dc-1-vulnhub/droopescan.png)

By the output of droopescan, we can determine that the version of the installed Drupal CMS is one between 7.22 - 7.26. If we search for vulnerabilities that were found in any version between these that the tool found, we can test that against the target. Although, this is not a good practice to test random exploits on a system that we don't know the exact version of, it is our only option.

A simple google search would show that there is a vulnerability that is known in versions before 7.58, 8.x before 8.3.9, 8.4.x before 8.4.6, and 8.5.x before 8.5.1. This vulnerability is known as 'Drupalgeddon'. We will use it to try and get a reverse shell on the target system.

I try to stay away from metasploit because of the OSCP requirement and as so, we will use a python exploit that will give us a netcat reverse shell.

Exploit link -> [Drupalgeddon2](https://github.com/lorddemon/drupalgeddon2)

## ~#Pr1vil3ge 3scal4tion

![drupalgeddon]({{ site.baseurl }}/images/dc-1-vulnhub/drupalgeddon.png)

![revshell]({{ site.baseurl }}/images/dc-1-vulnhub/revshell.png)

After getting the reverse shell, we want to get a python tty shell and make the arrow keys and tab completion work.
For this to work we background the netcat reverse shell and type:

```bash
ctrl + z
$ stty raw -echo
$ fg
```

When you type the stty command you will not see input but press enter and you will access the reverse shell again. Lastly, we want to be able to clear the screen if we need it, so this can be done by setting a global environment variable to 'xterm'.

```bash
$ export TERM=xterm
```

As we now have a shell in the system, it is time to enumerate it. Checking the usual locations where something could be found misconfigured, such as /usr/bin, /bin/, /etc/ssh/ and others, we can find that in /usr/bin/, the program 'find' has a SUID set.

![find-suid]({{ site.baseurl }}/images/dc-1-vulnhub/find-proof.png)

We can use this to exploit the system and get root! Going to [GTFObins](https://gtfobins.github.io/gtfobins/find/#shell), we search for "find" tool and use the command shown to execute a system shell and get root.

```bash
$ find . -exec /bin/sh \; -quit
```

For a detailed explanation of the command you can go to [explainshell.com](https://explainshell.com/explain?cmd=find+.+-exec+%2Fbin%2Fsh+%5C%3B+-quit)

![root]({{ site.baseurl }}/images/dc-1-vulnhub/root-taken.png)

We now have an effective user ID of root and got the flag! The box is completed!
