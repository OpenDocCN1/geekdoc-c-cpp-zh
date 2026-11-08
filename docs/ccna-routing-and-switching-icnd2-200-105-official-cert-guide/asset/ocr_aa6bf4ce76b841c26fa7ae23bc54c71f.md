# # “Do I Know This Already?” Quiz

The troubleshooting chapters of this book pull in concepts from many other chapters. In fact, troubleshooting IPv4 may be one of the most important topics to learn for both the CCENT and CCNA R&S certifications. So, it is useful to read this chapter (and the next chapter, also about troubleshooting IPv4 networks) regardless of your current knowledge level. For these reasons, some troubleshooting chapters do not include a “Do I Know This Already?” quiz.

# ## Foundation Topics

# ### Problem Isolation Using the ping Command

Someone sends you an email or text, or a phone message, asking you to look into a user's network problem. You Secure Shell (SSH) to a router and issue a `ping` command that works. What does that result rule out as a possible reason for the problem? What does it rule in as still being a possible root cause?

Then you issue another ping to another address, and this time the ping fails. Again, what does the failure of that ping command tell you? What parts of IPv4 routing may still be a problem, and what parts do you now know are not a problem?

The `ping` command gives us one of the most common network troubleshooting tools. When the `ping` command succeeds, it confirms many individual parts of how IP routing works, ruling out some possible causes of the current problem. When a ping command fails, it often helps narrow down where in the internetwork the root cause of the problem may be happening, further isolating the problem.

This section begins with a brief explanation of how ping works. It then moves on to some suggestions and analysis of how to use the `ping` command to isolate problems by removing some items from consideration.

# ### Ping Command Basics

The `ping` command tests connectivity by sending packets to an IP address, expecting the device at that address to send packets back. The command sends packets that mean “if you receive this packet, and it is addressed to you, send a reply back.” Each time the ping command sends one of these packets and receives back the message sent back by the other host, the `ping` command knows a packet made it from the source host to the destination and back.

More formally, the ping command uses the Internet Control Message Protocol (ICMP), specifically the ICMP echo request and ICMP echo reply messages. ICMP defines many other messages as well, but these two messages were made specifically for connectivity testing by commands like ping. As a protocol, ICMP does not rely on TCP or UDP, and it does not use any application layer protocol. It exists as a protocol used to assist IP by helping manage the IP network functions.