Box was completed a long time ago on a different machines, but steps were about as follows:
Run nmap on IP
Check https:// \[TargetIP] on a specific port to get a flag
Check http:// \[TargetIP], check page element
Run dirb on the site
There's a URL you can put in to bring you to a site meant to ping devices
type "; whoami" to figure out the box connects to a terminal
type nc -nvlp 444 to listen, and use the ping box to get a reverse shell
once you get it, look at the different users and use hydra to break into summer's ssh
I think there's a file in Morty's home directory that you use strings on to find a password
"cat" doesn't work so for any files you have to use head or tail
That's about all I can remember, but the box was pretty simple and was doable with little to no pentesting knowledge if I remember correctly