+   - **Regular Scan** — This conducts a default Nmap scan
+   - **Slow comprehensive scan** — This produces the following command:

```
nmap -sS -sU -T4 -A -v -PE -PP -p PS21,22,23,25,80,113,31339
-PA80,113,143,10042 -PO --script all
```

> **NOTE** For more information on these options, see http://nmap.org/book/
> docs/nmap-usage.txt.

# Telnet

Although Telnet should be removed from your server, it’s great as a testing tool and still the norm for connecting to specific types of network gear. Telnet is a very old protocol that allows you to connect to a machine and issue commands. By default, Telnet runs on port 23.

To start using Telnet on a Windows machine, click Start » Accessories » Command Prompt. At the command prompt, type telnet. The TELNET> prompt appears.

To Telnet to another machine, enter the following:

```
machine name port
```

Replace the machine name with the IP or hostname and the port number. Telnet can be used to connect and send e-mail on misconfigured servers. For example, the following command will attempt to connect you to the Mail Services:

```
telnet machine name 25
```

If you are successful in connecting, you can often send unauthorized e-mail through the server. This is also a means to check for open relays in your mail system.

Following is a list of common parameters used with the Windows version of Telnet:

+   - `c` — Close the connection.
+   - `d` — Display operating parameters.
+   - `o` — Connect to hostname (defaults to port 23).
+   - `q` — Exit (quit) Telnet.
+   - `set` — Set options (see `set ?` for more information).
+   - `sen` — Send strings (commands) to server.
+   - `st` — Print status information.