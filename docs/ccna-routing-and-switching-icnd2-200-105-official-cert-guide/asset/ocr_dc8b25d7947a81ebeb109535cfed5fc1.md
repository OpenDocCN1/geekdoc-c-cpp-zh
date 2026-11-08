Next, consider how R1 thinks about the least-bandwidth part of the calculation. R1 discovers that its S0/1 interface bandwidth (1544 Kbps, or 1.544 Mbps) is less than the advertised minimum bandwidth of 100,000 Kbps, or 100 Mbps. R1 needs to use this new, slower bandwidth in the metric calculation. (If R1's S0/1 interface had a bandwidth of 100,000 Kbps or more in this case, R1 would instead use the minimum bandwidth listed in the EIGRP update from R2.)

As for interface delay, the router always adds its interface delay to the delay listed in the EIGRP update. However, the unit for delay can be a bit of a challenge. The units, and their use, are as follows:

+   - **Unit of microseconds:** Listed in the output of show commands such as **show interfaces** and **show ip eigrp topology**, and in the EIGRP update messages
+   - **Unit of tens of microseconds:** Used by the interface mode configuration command (`delay`), with which to set the delay, and in the EIGRP metric calculation

Because of this weird difference in units, when looking at the delay, make sure you keep the units straight. In this particular example:

+   - R1 received an update that lists delay of 100 (microseconds), which R1 converts to the equivalent 10 tens of microseconds before using it in the formula.
+   - R1 sees its S0/1 interface setting of 20,000 microseconds, which equals 2000 tens of microseconds
+   - For the purposes of the calculation, R1 adds 10 tens of microseconds from the update message to 2000 tens of microseconds for the interface for a total delay of 2010 tens of microseconds.

This example results in the following metric calculation:

$$Metric = \left( \left( \frac{10^7}{1544} \right) + (10 + 2000) \right) * 256 = 2,172,416$$

> > **NOTE** For those of you who repeat this math at home, IOS rounds down the division in this formula to the nearest integer before performing the rest of the formula. In this case, 10^7 / 1544 is rounded down to 6476, before adding the 2010 and then multiplying by 256.

If multiple possible routes to subnet 10.1.3.0/24 exist, Router R1 also calculates the metric for those routes and chooses the route with the best (lowest) metric to be added to the routing table.

> > **NOTE** The examples in this chapter show routers with Gigabit interfaces, which default their delay settings to 10 microseconds. However, IOS adjusts the delay based on the actual speed of a LAN interface. In the examples in this chapter and the next, all the LAN interfaces happen to be running at 100 Mbps, making the delay be 100 microseconds.

# ## Caveats with Bandwidth on Serial Links

EIGRP's robust metric gives it the ability to choose routes that include more router hops but with faster links. However, to ensure that the right routes are chosen, engineers must