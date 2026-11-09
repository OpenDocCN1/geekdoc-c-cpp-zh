# Checking for Open Ports

Another basic tryout you should perform is to see what ports are open. Rkhunter does check for open ports such as 6666 and 6667, which, unless you are running your own IRC (chat) service, should be closed. However, you should look beyond what RKhunter checks and review all the open ports.

Type in the following at the command prompt:

```
netstat -az | more
```

This command instructs the server to show you all the open ports. The more command enables you to look at the long list of data more easily by providing a portion at a time, as shown in Figure 9-7.

![](bbox=[0.142, 0.33, 0.738, 0.393])

This is a basic connection to your machine. The *Local Address* that has been blurred out here is the server's IP address. The *Foreign Address* is the browsing IP address. This, of course, is simply a basic look. What you don't want to see is machines connecting to port 6667 or 6666, which would show up next to the IP address, such as `192.168.1.18:6667`. In that case, the action you would want to take is to close ports 6666 and 6667 (assuming they are open).

An easier method to discovering open ports is to use NMAP to scan your system (with permission from the host or owner of the machine only) and determine what ports are open. Figure 9-8 shows a view of a server's ports from NMAP. In this example, a variety of ports are open, but, in this case, all is well. If you were to see a system with hundreds of ports open, then you have a bigger problem.

![](bbox=[0.142, 0.662, 0.582, 0.954])