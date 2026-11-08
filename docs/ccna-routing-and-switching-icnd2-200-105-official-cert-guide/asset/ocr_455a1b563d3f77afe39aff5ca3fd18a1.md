![](bbox=[0.134, 0.091, 0.813, 0.187])

The Telnet connections shown in Figure J-18 work because each Telnet in this case uses source and destination addresses in the same subnet. For example, R1’s telnet 10.1.2.2 command uses 10.1.2.2 as the destination of course. R1 uses the outgoing interface IP address used to send packets to 10.1.2.2, 10.1.2.1 in this case. Because each of these telnet commands connects to an IP address in a connected subnet, the routing protocol could be completely misconfigured, and you could still Telnet/SSH to each successive device to troubleshoot and fix the problem.

Network engineers also use the IOS Telnet and SSH client just for preference. For instance, if you need to log in to several Cisco devices, you could open several windows and tabs on your PC, and log in from your PC (assuming the network was not having problems). Or, you could log in from your PC to some nearby Cisco router or switch, and from there Telnet or SSH to other Cisco devices.

# IOS Telnet and SSH Examples

Using the IOS Telnet client via the telnet host command is pretty simple. Just use the IP address or hostname to identify the host to which you want to connect, and press Enter. Example J-7 shows an example based on Figure J-18, with R1 using Telnet to connect to 10.1.2.2 (R2).

# Example J-7  *Telnet from R1 to R2 to View Interface Status on R2*

```
R1# telnet 10.1.2.2
Trying 10.1.2.2 ... Open

User Access Verification

Username: wendell
Password:
R2>
R2> show ip interface brief
Interface                  IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0         unassigned      YES unset  administratively down down
GigabitEthernet0/1         10.1.3.2        YES manual up                    up
GigabitEthernet0/2         10.1.2.2        YES manual up                    up
GigabitEthernet0/3         unassigned      YES unset  administratively down down
```

Take the time to pay close attention to the command prompts. The example begins with the user logged in to Router R1, with the R1# command prompt. The first command confirms the IP addresses and interfaces shown for Router R1 in Figure J-17 and Figure J-18. After