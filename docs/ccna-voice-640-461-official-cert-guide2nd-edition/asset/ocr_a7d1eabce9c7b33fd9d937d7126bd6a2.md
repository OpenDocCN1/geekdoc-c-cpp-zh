![](bbox=[0.145, 0.055, 0.855, 0.305])

Figure 11-19 Intercom Button Configuration

Figure 11-20 illustrates the configuration of a BLF Speed Dial.

# Configuring Presence-Enabled Call Lists

As described earlier, the CUCM system can track the on-hook status of phones both through BLF Speed Dials and Presence-Enabled Call Lists. Presence-Enabled Call Lists use the device's configured Subscribe CSS and/or Presence Group subscription policies to determine whether a device can watch a DN's Presence status:

+   - If the Subscribe applied does not include the Partition of the DN being watched, Presence status is unavailable.

+   - If the Inter-Presence Group subscription is denied between the two groups, Presence status information is unavailable.

+   - If both the Subscribe CSS and Presence Groups are used together, both must allow the subscription in order for Presence status to be watched.

Configuring Presence-Enabled Call Lists is somewhat more complex than BLF Speed Dials, but it allows greater flexibility, precision, and scalability when large numbers of devices need to watch large numbers of DNs. To configure Presence-Enabled Call Lists, follow these steps:

+   1. Navigate to System > Enterprise Parameters. Scroll down to Enterprise Parameters Configuration.

+   2. Set Enable BLF for Call Lists to Enabled.