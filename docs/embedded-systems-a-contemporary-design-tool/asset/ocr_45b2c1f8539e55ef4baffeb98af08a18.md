with an external supply as we see in the upper diagram in Figure 14.33. Looking inside the black box, as illustrated in the lower diagram, we see the state diagram reflecting the behavior of the system when power is first applied to the system. We move from Power OFF to Static then to Dynamic power consumption. With the voltage applied, current flows into the box from the power source. Following Power ON, the typical system will enter a boot up or initialization state and has initiated minimal activity.

![](bbox=[0.28, 0.2, 0.82, 0.55])

Figure 14.33 States of Power Consumption.

+   **Idle State**
+   As the system, or a portion thereof, transitions from a passive state to a dynamic state, a significant current surge can occur as the current that the active elements are requiring increases. Following the initial activity, the system may enter an Idle State or any of the states in which it is now running both the hardware and software as it is performing its intended tasks.

+   **Maximum dynamic**
+   **Normal dynamic**
+   The dynamic state can be characterized as being comprised of varying groups of parts with differing levels of activity ranging from OFF, to sleep, to idle, to low power, or to fully active. When the system is engaged in performing its worst case operating activity, as noted earlier, the state is identified as the level of maximum dynamic power consumption. Power consumption levels between these two extremes typify normal dynamic activity and evolve to and from differing levels, corresponding to the level of activity.

# 14.21.3.1 Sources of Dynamic Power Consumption – Hardware

Sources of the hardware contribution to dynamic power consumption can classified into two major groups:

+   **Pure hardware**
+   * Pure hardware comprises those components that are essential to the core operation of the system in its active state and, therefore, must be operational full-time.