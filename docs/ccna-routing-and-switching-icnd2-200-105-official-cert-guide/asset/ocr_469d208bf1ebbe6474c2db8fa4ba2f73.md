# Chapter 27

A VM—that is, an OS instance that is decoupled from the server hardware—still must execute on hardware. Each VM has configuration as the minimum number of vCPUs it needs, minimum RAM, and so on. The virtualization system then starts each VM on some physical server so that enough physical server hardware capacity exists to support all the VMs running on that host. So, at any one point in time, each VM is running on a physical server, using a subset of the CPU, RAM, storage, and NICs on that server. Figure 27-3 shows a graphic of that concept, with four separate VMs running on one physical server.

![](bbox=[0.143, 0.263, 0.746, 0.438])