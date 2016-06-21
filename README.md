# what is revssh?

revssh is a little bash script that wraps ssh and uses consistent hashing to identify all clients that are connected.

# Some examples of using revssh:

Add client ids to ~/.revssh so you can monitor there status
<pre>
jesse@server:~$ echo 'jesse-laptop' >> ~/.revssh
</pre>

get a list of clients and their status with

<pre>
jesse@server:~$ revssh -l
CLIENT_ID		PORT		STATUS

jesse-laptop			28207		disabled
</pre>

I also have the revssh client installed on my laptop. So now to connect my laptop to the server I run:

<pre>
jesse@laptop$ ./revssh -s jesse-laptop admin.buildpulse.com
</pre>

now back on the server

<pre>
jesse@server:~$ revssh -l
CLIENT_ID		PORT		STATUS

jesse-laptop			28207		active
</pre>

as you can see now we have a client connect and active.

revssh lets you run command remotely on the client or ssh directly in

<pre>
jesse@server:~$ revssh -h
usage: /home/curator/bin/revssh options

This script manages reverse ssh tunnels

OPTIONS:
   -h                   Show this message
   -l                   List all connected clients
   -c CLIENT_ID COMMAND Run command on client
   -o CLIENT_ID         Open terminal on client
   -s CLIENT_ID SERVER  Start reverse tunnel on server
</pre>

And this is how to run a remote command

<pre>
jesse@server:~$ revssh -c jesse-laptop google-chrome --version
The authenticity of host '[localhost]:28207 ([127.0.0.1]:28207)' can't be established.
ECDSA key fingerprint is ee:9e:74:b9:33:bc:f8:67:18:c7:a5:fe:be:23:4c:7a.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '[localhost]:28207' (ECDSA) to the list of known hosts.
jesse@localhost's password: 
Google Chrome 33.0.1750.117 
</pre>

Well thats basically it in a nut shell.
