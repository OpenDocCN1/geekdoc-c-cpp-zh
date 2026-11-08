# **Example I-9**  *Charlotte Configuration*

```
```
interface serial0/1/1
 encapsulation frame-relay
!
interface serial 0/1/1.1 point-to-point
 ip address 140.1.1.2 255.255.255.0
 frame-relay interface-dlci 51
!
interface gigabitethernet 0/0
 ip address 140.1.12.2 255.255.255.0
```
```

# **Example I-10**  *Nashville Configuration*

```
```
interface serial0/1/1
 encapsulation frame-relay
!
interface serial 0/1/1.2 point-to-point
 ip address 140.1.2.3 255.255.255.0
 frame-relay interface-dlci 51
!
interface gigabitethernet 0/0
 ip address 140.1.13.3 255.255.255.0
```
```

# **Example I-11**  *Boston Configuration*

```
```
interface serial0/1/1
 encapsulation frame-relay
!
interface serial 0/1/1.3 point-to-point
 ip address 140.1.3.4 255.255.255.0
 frame-relay interface-dlci 51
!
interface gigabitethernet 0/0
 ip address 140.1.14.4 255.255.255.0
```
```

Again, defaults abound in this configuration, but some defaults are different than when you’re configuring on the physical interface. The LMI type is autosensed, and Cisco encapsulation is used, which is just like the fully meshed examples. Inverse ARP is not really needed on point-to-point subinterfaces, but it is enabled by default in case the router on the other end of the VC needs to use Inverse ARP, as explained later in this section.

Two new commands create the configuration required with point-to-point subinterfaces. First, the interface serial 0/1/1.1 point-to-point command creates logical subinterface number 1 under physical interface serial 0/1/1. This command also defines the subinterface as a point-to-point subinterface instead of point-to-multipoint. Then, the configuration must associate one PVC with the subinterface; the frame-relay interface-dlci subinterface subcommand tells the router which single local DLCI is associated with that subinterface.