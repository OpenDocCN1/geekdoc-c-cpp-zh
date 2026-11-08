# Key Topic

**Table 2-2 — Three Classes of Problems Caused by Not Using STP in Redundant LANs**

| Problem | Description |
|---|---|
| Broadcast storms | The forwarding of a frame repeatedly on the same links, consuming significant parts of the links’ capacity. |
| MAC table instability | The continual updating of a switch’s MAC address table with incorrect entries, in reaction to looping frames, resulting in frames being sent to the wrong locations |
| Multiple frame transmission | A side effect of looping frames in which multiple copies of one frame are delivered to the intended host, confusing the host |

# What IEEE 802.1D Spanning Tree Does

STP prevents loops by placing each switch port in either a forwarding state or a blocking state. Interfaces in the forwarding state act as normal, forwarding and receiving frames. However, interfaces in a blocking state do not process any frames except STP messages (and some other overhead messages). Interfaces that block do not forward user frames, do not learn MAC addresses of received frames, and do not process received user frames.

Figure 2-2 shows a simple STP tree that solves the problem shown in Figure 2-1 by placing one port on SW3 in the blocking state.

![](bbox=[0.174, 0.462, 0.781, 0.772])

**Figure 2-2**  *What STP Does: Blocks a Port to Break the Loop*

Now when Bob sends a broadcast frame, the frame does not loop. As shown in the steps in the figure:

+   1. **Step 1.** Bob sends the frame to SW3.
+   2. **Step 2.** SW3 forwards the frame only to SW1, but not out Gi0/2 to SW2, because SW3’s Gi0/2 interface is in a blocking state.
+   3. **Step 3.** SW1 floods the frame out both Fa0/11 and Gi0/1.
+   4. **Step 4.** SW2 floods the frame out Fa0/12 and Gi0/1.