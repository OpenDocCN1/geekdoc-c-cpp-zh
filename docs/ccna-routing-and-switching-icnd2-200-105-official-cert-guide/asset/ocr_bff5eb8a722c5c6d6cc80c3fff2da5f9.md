![](bbox=[0.143, 0.09, 0.714, 0.373])

# ## Finding Area Mismatches

Earlier in this chapter, the “OSPF Interface Troubleshooting” section showed how to use the `show ip ospf interface` command to list the area numbers and find OSPF area mismatches. This next topic shows how to see that same issue using the `debug ip ospf adj` command, as shown in Example 11-11. This command lists messages related to OSPF neighbor adjacency events, and shows messages that identify the area mismatch (with R2).

# ### Example 11-11 *Finding Mismatched Area Problem with R1 debug*

```
~~~
R1# debug ip ospf adj
OSPF adjacency events debugging is on
R1#
*Nov 15 13:42:02.298: OSPF-1 ADJ   Gi0/0: Rcv pkt from 10.1.1.2, area 0.0.0.0,
  mismatched area 0.0.0.1 in the header
R1#
R1# undebug all
All possible debugging has been turned off
~~~
```

As noted in Table 11-4, the `debug ip ospf adj` command helps troubleshoot mismatched OSPF area problems. The first part of the highlighted message in the example lists short-hand about a received packet (“Rcv pkt”) from 10.1.1.2, which is R2’s IP address. The rest of the message mentions R1’s area (0.0.0.0), and the area claimed by the other router (0.0.0.1). (Note that the message lists the 32-bit area number as a dotted-decimal number.)

This particular example focuses on the symptom (that a neighbor relationship does not start), and the debug messages that identify the problem (mismatched areas). However, finding the configuration error may take some work, because the problem could be more complex than just having the wrong area number configured on a command.

One harder-to-notice configuration error happens when the configuration has multiple `network` commands, with different area numbers, that all happen to match one interface’s IP address. IOS stores the OSPF `network` commands to the configuration in the same order they are configured (which is the same order listed in the output of `show running-config`). IOS processes the commands in sequence, so that the first `network` command that matches a particular interface is used to set the OSPF area number.