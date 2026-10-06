name, the ID, and even the path to the binary. This is useful both when we're looking at system information on a target host, as well as when we're troubleshooting malware.

# Linux Network Information Gathering

Many of the commands we used when gathering Windows information are going to be similar on Linux. We want to gather the IP addresses on the system, the route, the DNS information, and the network connections along with the processes that own them. In order to gather the information about what process owns each connection, we will need to be root on the system. Let's build our script.

```
ip addr >> /tmp/net
echo "----------------" >> /tmp/net
cat /etc/resolv.conf >> /tmp/net
echo "----------------" >> /tmp/net
netstat -rn >> /tmp/net
echo "----------------" >> /tmp/net
netstat -anlp >> /tmp/net
```

For each command we run we may not have distinct headers to indicate that it's a new command, so we add a line separator between each command so that we can easily find the output from each command. We begin with the ip command, which shows information about the IP stack. the addr option tells the command to list each IP address on the system. To determine DNS information, there isn't an easy command that we can run, like there is in Windows. The easiest way to gather DNS information is by looking in the /etc/resolv.conf file. This file is the configuration file for the system's DNS information, and if all the system tools consult this, it should be good enough for us.

To gather routing information and other connection information, we can use the netstat command, just like Windows. To gather the routing information, we can use the -r option. By specifying the -n option to any command, we instruct netstat not to use DNS resolution, which would slow down our execution. Once the routing information is printed to our file, we use netstat again to print all the connections along with the process that owns each connection. The -a