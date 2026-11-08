This next section takes a short look at IP SLA, but from a little different perspective than many other topics in this book. While this section does show some IP SLA configuration, the goal here is to show how to use IP SLA for troubleshooting, rather than to work through all the details of configuration. Think of it as if you need to operate the network, and another more experienced engineer may have set up some IP SLA configurations in different places in the network. Your job: use the information available from IP SLA to troubleshoot a network.

# ## An Overview of IP SLA

Network engineers could measure network performance and availability for SLAs by measuring actual end-user traffic. However, measuring end-user traffic could require placing some kind of software on the user devices themselves, with those hidden applications then measuring key facts such as application response time, QoS metrics like jitter and loss, or simple availability information, like whether the host can ping a particular other host.

IP SLA gives network engineers a much different option that does not bother end-user devices. IP SLA runs on a router and generates traffic that mimics user traffic, but without placing any software on the end-user devices. IP SLA—a router-specific feature not found on Cisco switches—can be configured to perform over a dozen different types of IP SLA operations. These operations can be as simple as the equivalent of issuing a ping command (to send an ICMP Echo message), to sending messages whose headers mimic voice traffic so that VoIP delay, jitter, and loss can be measured with packets that receive the same QoS treatment as end-user voice traffic.

IP SLA *operations* generate this traffic, receive responses, measure the results, and then make that information available.

To see how IP SLA works in at least some cases, Figure 26-11 shows a simple design with a couple of routers. The two routers sit at different sites. The senior network engineer wants to track voice delay and jitter over the WAN in preparation for an upcoming revision to an end-user SLA. The engineer could use one of several IP SLA operations—for instance, the RTP-based VoIP operation, called a UDP Jitter probe, which generates IP packets that include a UDP and RTP header like normal VoIP traffic.

![](bbox=[0.149, 0.615, 0.851, 0.743])

**Figure 26-11** *Using ICMP UDP Jitter Probes*

Many of the IP SLA probes rely on one router to generate the packets (the *IP SLA source*), with another router replying back (the *IP SLA responder*), as shown in Figure 26-11. However, some IP SLA operations do not require an IP SLA responder, like the ICMP Echo probe. This operation generates an ICMP Echo Request message, so any host that will respond to a normal ICMP Echo Request (as a normal ping) will reply back with an ICMP Echo Reply. Using the IP SLA ICMP Echo probe means that you can monitor the state of and performance sending packets to any IP address in the network, including servers and user hosts, as shown in Figure 26-12. Steps 1 and 2 show Router R1 as an IP SLA source,