+   7. **C.** The requirements in the question ask that you gather all traffic sent between Host1 and Host2, to avoid gathering extra copies of the same frame. That requirement means you need to capture frames sent from Host1 to Host2, and frames sent from Host2 back to Host1. It also means that the solution should not capture the same frame multiple times. Each incorrect answer either gathers too little traffic, or gathers the required traffic but also more traffic than the correct answer would gather.
+   
+   First, the answer of collecting from F0/1 for a single (transmit) direction is incorrect because it gathers too little traffic. Frames sent by Host2 to Host1 would arrive in switch port F0/2 and then be sent out port F0/1 to Host1, and would be copied by the SPAN session. However, frames sent by Host1 would be received on switch port F0/1, and would not be copied by that SPAN session.
+   
+   The answer about using VLAN 5 as a source would work, but because all FastEthernet ports on the switch are in VLAN 5, this option gathers more traffic than is necessary.
+   
+   The answer about using F0/2 as the source, for both directions of traffic, is correct. It will copy all frames sent by Host1 to Host2 (frames that the switch transmits out port F0/2), as well as frames sent by Host2 to Host1 (which will be frames received on switch port F0/2). This option does gather frames sent between Host2 and other hosts as well.
+   
+   The final incorrect answer refers to collecting traffic from both F0/1 and F0/2, but in both directions. That option would gather all frames sent between Host1 and Host2 twice, which would work, but the question asked that you gather no more traffic than is required.

+   8. **A.** C. Local SPAN has a variety of configuration dependencies. Each Local SPAN session can have multiple sources, but they must be either interfaces or VLANs, and not a mix. Source ports can include both access and trunk ports as well as EtherChannel interfaces. Finally, each SPAN destination port can be used in only one SPAN session at the same time. To reuse that destination port, you must first unconfigure the destination port from the original SPAN session (no monitor session destination) and then configure it to be part of another SPAN session.

# Chapter 27

+   1. **B.** PaaS (Platform as a Service) supplies one or more virtual machines (VM) that have a working operating system (OS) as well as a predefined set of software development tools.
+   
+   As for the wrong answers, Software as a Service (SaaS) supplies a predefined software application, but typically with no ability to then later install your own applications. IaaS (Infrastructure as a Service) supplies one or more working VMs, optionally with an OS installed, so it could be used for software development, but the developer would have to install a variety of development tools, making IaaS less useful than a PaaS service. Finally, SLBaaS (Server Load Balancing as a Service) can be offered as a cloud service, but it is not a general service in which customers get access to VMs on which they can then install their own applications.