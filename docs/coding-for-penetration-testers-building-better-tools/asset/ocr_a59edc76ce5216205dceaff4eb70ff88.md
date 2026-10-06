by altering the port specified in the first line. Our target device has a Telnet port open also, so let's see where we get by simply changing the port to 23 (Telnet) and running it again.

Uh-oh, no output. We can use Netcat again here to go talk to the Telnet port on the device and see if we can figure out what happened, running it as netcat 10.0.0.50 23. Hmm, now we get back something along the lines of:

```
yüöýHP JetDirect
Password is not set
Please type "menu" for the MENU system,
or or "/" for help, or "/" for current settings.
```

So, we might need to try sending a character at it from our Nash script in order to get the output. We can modify the script like this:

```
socket = open_sock_tcp(23);
if (! socket) exit(0);
mesg = raw_string(0xd);
send(socket:socket,data:mesg);
banner = recv_line(socket:socket, length:4096);
display(banner);
```

Here we have an extra couple of lines. The first new line, starting with mesg, will take a raw ASCII string, in this case 0x0d (a carriage return), and place it in the mesg variable. Directly below that, we use our socket to send the contents of mesg to the target on the other end of the socket, and then we carry on with the script. Let's run the script again and see where this gets us using openvas-nasl -t 10.0.0.50 telnet.nasl. The results here should look something like Fig. 7.5. Much better.