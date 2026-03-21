Kioptrix 4 notes, thought process/notes
1.) Reconnaissance
  Run the regulars, arp-scan and fully loaded nmap
  Initial viewing of the website shows a login page, that supposedly can't be SQLi'd
  ```
  Samba 3.X on 139, Samba 3.0.28a on 445
  Running linux kernel 2.6.X 
  ```
  There's php, but it has suhosin-patch, so eh
  enum4linux worked here, but I'm not sure why it didn't earlier
  ```
  Users
    nobody
    robert : ADGAdsafdfwt4gadfga==   
    root
    john : MyNameIsJohn
    loneferret
  ```
  although it looks like the actual users are john robert and loneferret
  You use sqli, but you enter the usernames, and sqli the password with root'OR'1=1
  john gets a password, but nothing else does
2.) Remote Access
  With username and password, checking ssh
  Credentials work, but both ssh users have limited access
  echo os.system("/bin/bash") puts you into a normal bash shell
  looking at the checklogin.php file, in /var/www, it looks like the input is supposed to be sanitized, but the password is left unscrubbed
  additionally, the file accesses mysql as root without a password
  use SELECT * FROM mysql.func; to find the User defined functions
  use SELECT sys_exec('usermod -a -G admin john'); to add john as a root user
  Close the ssh session and reconnect to john and use sudo su to escalate to root
