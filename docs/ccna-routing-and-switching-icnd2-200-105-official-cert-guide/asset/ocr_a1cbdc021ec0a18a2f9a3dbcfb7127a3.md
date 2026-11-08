5. Host A and Host B sit in two different subnets. The path between the subnets of these two hosts runs through three different Layer 3 forwarding devices (routers and Layer 3 switches). A network engineer uses the APIC-EM Path Trace ACL Analysis tool to analyze the path used for Host A to send packets to Host B. Which part of the function does the engineer use specifically by the ACL Analysis or ACL Trace part of the tool?

+   a. Discovery of the topology that exists between the two hosts
+   b. Analysis of the Layer 3 forwarding decisions in the path from Host A to B
+   c. Analysis of the Layer 2 forwarding decisions in the path from Host A to B
+   d. Analysis of the impact of ACLs on the packets that would flow from Host A to B

# Foundation Topics

# SDN and Network Programmability Basics

Networking devices forward data in the form of messages, typically data link frames like Ethernet frames. You have learned about how switches and routers do that forwarding for the entire length of preparing for the CCNA R&S exam.

Network programmability and SDN takes those ideas, analyzes the pieces, finds ways to improve them for today’s needs, and reassembles those ideas into a new way of making networks work. At the end of that rearrangement, the devices in the network still forward messages, but the how and why has changed.

This first major section explains the most central concepts of SDN and network programmability. It starts by breaking down some of the components of what exists in traditional networking devices. Then this section explains how some centralized controller software, called a controller, creates an architecture for easier programmatic control of a network.

# The Data, Control, and Management Planes

Stop and think about what networking devices do. What does a router do? What does a switch do?

Many ideas should come to mind. For instance, they physically connect to each other with cables, and with wireless, to create networks. They forward messages: switches forward Ethernet frames, and routers forward packets. They use many different protocols to learn useful information, like routing protocols for learning network layer routes.

Everything that networking devices do can be categorized as being in a particular plane. This section takes those familiar facts about how networking devices work, and describes the three planes most often used to describe how network programmability works: the data plane, the control plane, and the management plane.

# The Data Plane

The term *data plane* refers to the tasks that a networking device does to forward a message. In other words, anything to do with receiving data, processing it, and forwarding that same data—whether you call the data a frame, packet, or, more generically, a message—is part of the data plane.