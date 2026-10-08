Here's the process you should use for troubleshooting network-related issues:

# Issue 1: Verifying PoE

Obviously, if the IP phone does not receive power, nothing is going to work correctly. You can quickly diagnose this issue by asking the user if her phone is displaying anything on the screen. If not, here are your areas of focus:

+   - Check the physical connections: Verify that the IP phone is securely plugged in, verify all patch panel connections, and verify the Ethernet cable used has all eight pins functioning properly (because PoE uses the four pins not used by data).

+   - Check the PoE switch: Ensure that the switch is online and operational, verify that the PoE clients have not exhausted the switch power supply using the show power inline command, and use a show run command to verify that the port does not have the command power inline never (which disables PoE).

+   - Check the IP phone: Verify that the IP phone does not have expansion modules causing it to exceed PoE capabilities, move the IP phone to a different port to see if it receives power, try a different IP phone on the same port to see if it receives power, and be sure that the IP phone and PoE switch support a compatible PoE standard (Cisco inline, 802.2af, and 802.3at).

> Tip: Before you move too far into the troubleshooting process, it's always best to reset the phone's configuration settings to default factory. Although the various IP phones have different locations to reset the configuration, all of them will have the option. Often, a bogus configuration item will end up in one of the key fields that you may not initially see. Resetting the phone configuration gives you a clean starting ground to work.

# Issue 2: Voice VLAN Assignment

If an IP phone is assigned to the wrong VLAN, it may not be able to contact the supporting servers (DHCP, TFTP, CME, and so on). You can diagnose this and the following issues when you receive a report that the IP phone is continuously rebooting:

+   - Check the switch configuration: Ensure that you correctly configured the voice VLAN by viewing the running-configuration (show run), verifying the interface operating mode by entering a show interface <interface name>switchport command, verifying that you created the voice VLAN on the switch (show VLAN), verifying that the voice VLAN is added to all applicable trunk connections (show interface trunk), and verifying CDP is enabled on the port connected to the IP phone (because the voice VLAN is sent to the IP phone using CDP).

+   - Check the IP phone: If you have physical access to the IP phone, navigate to the network settings page (using the Settings button on the phone). Verify that the IP phone has received the VLAN configuration, verify the IP phone has an IP address, and access the IP address in a web browser and view the log files for more clues.