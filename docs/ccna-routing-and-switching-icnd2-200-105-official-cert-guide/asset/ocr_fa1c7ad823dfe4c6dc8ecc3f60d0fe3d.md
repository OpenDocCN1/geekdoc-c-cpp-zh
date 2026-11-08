the configuration uses two different hostnames with the following tunnel destination commands:

+   - **tunnel destination test 1:** Resolves to 10.1.6.1, which also has a matching route
+   - **tunnel destination test 2:** Name does not resolve

# **Example 15-7**  *Examples of Using Hostnames with Tunnels*

```
R1# configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
R1(config)# interface tunnel 11
R1(config-if)# tunnel source G0/1
R1(config-if)# tunnel destination test1

R1(config)# interface tunnel 12
R1(config-if)# tunnel source G0/1
R1(config-if)# tunnel destination test2
Translating "test2"

% Invalid input detected at '^' marker.
R1(config-if)# ^Z
! Below, note that hostname test1 resolved to IP address 10.1.6.1 as stored in
the tunnel destination command
R1# show running-config interface tunnel 11
interface Tunnel11
 no ip address
 tunnel source GigabitEthernet0/1
 tunnel destination 10.1.6.1
end
! Below, note the absence of the tunnel destination command because it was rejected
R1# show running-config interface tunnel 12
interface Tunnel12
 no ip address
 tunnel source GigabitEthernet0/1
end

R1# show ip interface brief | include Tunnel
Tunnel11                         unassigned      YES unset  up                    up
Tunnel12                         unassigned      YES unset  up                  down
```

Working through the example, first look at the portions related to tunnel 11. The configuration on interface tunnel 11 uses a hostname (test1). The show running-config interface tunnel11 command reveals that the router resolved that name to address 10.1.6.1. Finally, the show ip interface brief command at the bottom of the example reveals that interface tunnel 11 reaches an up/up state. (Not shown: there is a route that matches 10.1.6.1.)

Now focus on interface tunnel 12. In the configuration section, note that the tunnel destination test2 command was rejected by IOS. The message stating “Translating test2”