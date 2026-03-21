1.) Initial server
  First things first, download the network config file for openvpn
  Check tryhackme.com/access or the like to confirm connection
  Run nmap -p-15000 -sV to answer questions 1&2(4, and centos)
  Ports 22,80,443,10000 are open, and 9090 is closed
  Attempting to connect to the webserver will return an error so configure the dns at /etc/hosts
  connect to https://thomaswreath.thm and click advanced -> accept risk anyways
    The error comes from self signed certificate, but its a lab so eh
  Look at the services and find that the web service(miniserv 1.890) is vulnerable to CVE-2019-15107
  Another quick google search will show a exploit for the service:
    github.com/MuirlandOracle/CVE-2019-15107
      although there's also a metasploit exploit for it so you don't have to clone it
  pip3 -r requirements.txt to download the dependencies, and then run it.
  type shell to begin getting a reverse shell and follow the instructions
  python3 -c 'import pty;pty.spawn("/bin/bash")' to spawn a bash shell,
  export TERM=xterm, then ctrl+z to background the shell
  enter stty raw -echo; fg, and the shell should be stabilized
  whoami should return root, so we have access to the server
2.) Pivoting
  For pivoting methods, check obsidian, otherwise, I'm using sshuttle
  chisel takes a little more work and isn't working
  connecting web browser to foxyproxy and navigating to the ip gives us the website
  the service running the website is gitstack(as can be seen on just the ip)
  opened port 15678 on the firewall

*I ran into technical difficulties and had to do some troubleshooting.  Notes are incomplete, but they will be completed*