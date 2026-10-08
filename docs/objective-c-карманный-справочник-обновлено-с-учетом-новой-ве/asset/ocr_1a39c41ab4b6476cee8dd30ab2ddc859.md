# CHAPTER 17: Network Access

# Finding Network Peers

From: netservice.m

Over the years, lots of protocols have been used for finding services on the local network. Both NetBIOS and AppleTalk were common on local networks until the mid '90s, until they started to be phased out in favor of TCP/IP.

The TCP/IP protocol stack didn’t include anything for doing this. The closest it came was the broadcast address. If you send a packet to the broadcast address then it will be sent to everyone on the local segment. This has a lot of problems; it only works on the local physical segment, it’s inefficient on modern switched networks, and it’s a very low-level approach.