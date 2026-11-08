```
```text
interface gigabitethernet 0/0
 ip address 199.1.10.1 255.255.255.0
!
router eigrp 1
 network 199.1.1.0
 network 199.1.10.0
```
```

# **Example I-2**  *Mount Pilot Configuration*

```
```text
interface serial0/1/1
 encapsulation frame-relay
 ip address 199.1.1.2 255.255.255.0
!
interface gigabitethernet 0/0
 ip address 199.1.1.2 255.255.255.0
!
router eigrp 1
 network 199.1.1.0
 network 199.1.11.0
```
```

# **Example I-3**  *Raleigh Configuration*

```
```text
interface serial0/1/1
 encapsulation frame-relay
 ip address 199.1.1.3 255.255.255.0
!
interface gigabitethernet 0/0
 ip address 199.1.12.3 255.255.255.0
!
router eigrp 1
 network 199.1.1.0
 network 199.1.12.0
```
```

The configuration is simple in comparison with the protocol concepts. The **encapsulation frame-relay** command tells the routers to use Frame Relay data link protocols instead of the default, which is High-Level Data Link Control (HDLC). Note that the IP addresses on the three routers' serial interfaces are all in the same Class C network. Also, this simple configuration takes advantage of the following IOS default settings.

+   - The LMI type is automatically sensed.
+   - The (default) encapsulation is Cisco.
+   - PVC DLCIs are learned via LMI status messages.
+   - Inverse ARP is enabled (by default) and is triggered when a router receives an LMI status message declaring that the VCs are up.