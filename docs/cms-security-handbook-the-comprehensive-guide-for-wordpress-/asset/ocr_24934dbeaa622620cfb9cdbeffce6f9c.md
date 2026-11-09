Securing the WAP is simple and easy. Following are a few things you want to consider:

+   - *Stop telling everyone you have a wireless network* — Even though you probably aren’t verbally telling people this fact, the device still broadcasts itself to intended devices. In essence, changing your setting for `SSID BROADCAST` to no prevents the device from letting people know it’s there. With that said, a very experienced attacker will still be able to find it. However, this countermeasure stops most of the slackers who want to slurp up free Internet.

+   - *Purchase a modern WAP* — If you’ve had your WAP for a few years, buy a new one that supports the backward-compatible standards. Look for WAPs that use the 802.11g or 802.11n protocols. These offer the latest (depending on the manufacturer) security tools. Older systems use security protocols that are now broken.

+   - *Use a high level of encryption (WPA2/802.11i strongly preferred)* — As described earlier in this chapter, use strong password keys, and change them every 30 days or so. If you connect to the network server over a wireless connection, use the Secure Shell (SSH) and Transported Layer Security/Hypertext Protocol Secure (TLS/HTTPS) protocols. In other words, put SSL on your site, as described earlier in this chapter. Using an encrypted virtual private network (VPN) will likely mitigate the effects of tools such as Firesheep.

+   - *Use MAC filtering* — Every machine that has a network connection has a unique address in it called a Media Access Control (MAC) address. Although faking this address (a process known as *spoofing*) is possible, for the most part, it’s a sure thing. If you have a limited number of machines, set `MAC Filtering` to allow your machines in and everyone else out.

+   - *Activate any firewall in your wireless router* — The term “firewall” is often confused with Network Address Translation (NAT). The firewall is there to keep out bad things. The NAT separates your internal IP addresses from the Internet IP address you have been assigned. If a firewall in your router is available, use it.

+   - *Create a dedicated segment for your wireless network, and take additional steps to restrict access to this segment* — In other words, make sure this particular network segment is firewalled off from the rest of your network.

+   - *Check whether the firmware for your WAP and drivers for your wireless adapter(s) are up to date* — Update the drivers if necessary.

+   - *Test your wireless network for holes on a regular basis* — Learn to use the tools that hackers use. Be sure you stay in compliance with your local laws.