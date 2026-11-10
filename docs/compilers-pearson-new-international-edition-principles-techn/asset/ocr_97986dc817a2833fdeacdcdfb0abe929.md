# # SONiC System Architecture

SONiC (Software for Open Networking in the Cloud) is an open-source network operating system based on Linux. It runs on commercial ASICs from multiple vendors and provides a full-suite of network functionality that has been production-hardened in the data centers of the world's largest cloud service providers. This page explains the SONiC architecture.

The figure below shows the high-level architecture of SONiC that offers flexibility to support multiple ASICs and multiple hardware platforms.

![](bbox=[0.112, 0.39, 0.888, 0.698])

# ## Containerized SONiC Components

SONiC is composed of multiple docker-based containers. The key components in the SONiC architecture include:

+   - **Teamd** containerizes the teamd protocol for link aggregation (LAG).
+   - **FPM (Forwarding Plane Manager)** containerizes the BGP and other routing protocol stacks.
+   - **SNMP** containerizes the SNMP server.
+   - **DHCP Relay** containerizes DHCP relay functionality.
+   - **LLDP** containerizes the Link Layer Discovery Protocol.
+   - **Pmon** containerizes platform monitoring services.
+   - **NAT** containerizes network address translation functionality.