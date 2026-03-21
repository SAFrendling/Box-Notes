1.) Reconnaissance
  nmap shows only one port open
  Its Microsoft IIS 6.0 which is vulnerable
  searching on msfconsole will show a couple exploits, and the one you want is:
  iis_webdav_upload_asp, which will open a shell
  background and use the local exploit suggester
  trial and error will show ms15_051_client_copy_image is the exploit you want.
  the process the shell is running on is very limited, so you want to find a different process
  In this case, davcdata.exe is the one we want, migrate with migrate [processid]
    use ps to see running processes
  run the exploit and your shell will become a root shell
  cd into the administrator and lakis desktop to cat the flags
