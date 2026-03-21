1.) Reconnaissance
  ssh open, http, rpc on 111 and 48869
  nothing of interest from enum4linux
  check website, nothing too interesting
  ran nikto, saw a wordpress folder
  ran dirb, don't think I saw anything interesting
  Used wpscan to look for vulnerabilities
  found xmlrpc and wpcron
  saw michael and steven as users
  since michael had more info, I tried sshing into his user
2.) Remote Access
  not sure what the password is, but I tried it blank, and I tried 'michael' and michael took
    I think when I looked at the link I was given, michael appeared twice so maybe that's the bit
  checking /var/www gives you flag2(fc3fd58dcdad9ab23faca6e9a36e581c}
  raven.local/service.html has flag1{b9bbcb33e11b80be759c4e844862482d}
  looking for a way to escalate now
3.) Privilege Escalation
  catting the wp-config file at /var/www/html/wordpress/wp-config.php gets you the root name and pw
    Name: root, PW: R@v3nSecurity
  type mysql -u root -p, and type the password to log into the mysql as root
  find the wp_users table to find flags 3 and 4
    flag3{afc01ab56b50591e7dccf93122770cd2}
    flag4{715dea6c055b9fe3337544932f2941ce}
  Think I have to get root now
  steven's pw: pink84
  can ssh in on another terminal, or use su steven on the michael session to log in as steven
  use sudo -l to see commands you can run as steven
  use sudo python -c 'import pty;pty.spawn("/bin/bash");' to get root access
  flag4 was in the root directory, but also in the sql table, strange
