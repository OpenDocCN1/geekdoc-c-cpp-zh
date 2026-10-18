
![](img/2d28ab1e4ea39ed71271c8bf426f216b_223_0.png)

## A short history of virtualization

IBM introduced virtualization in the early 1960s to enable users to run more than one operating system on a mainframe. Mainframe virtualization became less relevant in the 1980s and 1990s. Indeed, in the 1990s, companies stopped worrying about the efficiency of the computer platform because computers were getting so powerful.

For more than a decade, IT organizations expanded the capabilities of their data centers by adding servers. Servers had become so cheap that each time a new application was added, it was easier to buy a new server than to share resources with other applications. Eventually, organizations realized that maintaining, upgrading, and managing a large and growing number of servers was getting out of hand. The number of support-staff employees required to operate the data center was climbing swiftly, so the manpower cost of maintaining the data center as a percentage of the total cost was rising. At the same time, other costs were growing in an unpredicted manner, particularly the costs of electricity to power the computers, air conditioning to cool them, and floor space to house them.

One of the main problems was that the servers were horribly inefficient. In the days of the mainframe, great efforts were made to use 100 percent of the computer’s CPU and memory resources. Even under normal circumstances, it was possible to achieve better than 95 percent utilization. On the cheap servers that IT departments had been deploying, however, CPU efficiency was often 6 percent or less — sometimes as low as 2 percent. Memory and disk input/output I/O usage were similarly low.

This situation seems almost insane until you realize that applications simply don’t require a great deal of resources, and with the servers that were being delivered by the year 2000, you didn’t put more than one application on a server. Why? Because the operating systems that almost everyone had — Windows and Linux, typically — can’t effectively schedule resource use between competing applications. In a competitive hardware market, vendors began increasing the power of servers at an affordable price. Most of these servers had more power than typical applications needed. The same inefficiencies of Windows and Linux didn’t address the efficiency problem, however. If an organization decided to stay with older but lower-powered hardware, it couldn’t find people to maintain those aging platforms.

If you had an application that only ever needed 5 percent of a current CPU, what were you going to do other than provide it with its own server? Some companies actually used old PCs for some applications of this kind, maintaining the PCs themselves; but there’s a limit to the amount of old equipment that you can reuse.

The solution to this squandering of resources was to add scheduling capability to computers, which is precisely what one IT vendor, VMware, introduced. Adding scheduling changed the dynamics of computer optimization and set the stage for the modern virtualization revolution. The mainframe is dead; long live the mainframe!

![](img/2d28ab1e4ea39ed71271c8bf426f216b_224_0.png)

## Defining types

Different hypervisors support different aspects of the cloud. Hypervisors come in several types:

- **Native hypervisors,** which sit directly on the hardware platform are most likely used to gain better performance for individual users.
- **Embedded hypervisors** are integrated into a processor on a separate chip. Using this type of hypervisor is how a service provider gains performance improvements.
- **Hosted hypervisors** run as a distinct software layer above both the hardware and the OS. This type of hypervisor is useful both in private and public clouds to gain performance improvements.

## Abstracting hardware assets

One of the benefits of virtualization is the way that it *abstracts* hardware assets, in essence allowing a single piece of hardware to be used for multiple tasks.

The following list summarizes hardware abstraction and its management:

- **File system virtualization:** Virtual machines can access different file systems and storage resources via a common interface.
- **Virtual symmetric multiprocessing:** A single virtual machine can use multiple physical processors simultaneously and thus pretend to be a server cluster. It also can emulate a fairly large grid of physical servers.
- **Virtual high-availability support:** If a virtual machine fails, that virtual machine needs to automatically restart on another server.
- **Distributed resource scheduler:** You could think of the scheduler as being the super-hypervisor that manages all the other hypervisors. This mechanism assigns and balances computing capability dynamically across a collection of hardware resources that support the virtual machines. Therefore, a process can be moved to a different resource when it becomes available.
- **Virtual infrastructure client console:** This console provides an interface that allows administrators to connect remotely to virtual center management servers or to an individual hypervisor so that the server and the hypervisor can be managed manually.

![](img/2d28ab1e4ea39ed71271c8bf426f216b_225_0.png)

## Managing Virtualization

For cloud computing to operate consistently, the service provider has to track all the virtualized resources.

You must keep track of

- Where everything is
- What everything has to accomplish
- For what purpose

When managing virtualization, the service provider whether in your own organization or in a private cloud must be able to do the following:

- Know and understand the relationships among all elements of the network.
- Be able to change things dynamically when elements within this universe change.
- Keep the placement of virtual resources in step with all the other information held in the configuration management database CMDB. Given that few organizations have anything approaching a comprehensive CMDB, that's asking for a lot. In fact, the CMDB needs to know how all service management capabilities are integrated.

## Foundational issues

Managing a virtual environment involves some foundational issues that determine how well the components function as a system. These issues include

- How licenses are managed
- How workloads are controlled
- How the network itself is managed

In cloud environments, customers request additional add CPU cycles or storage as their needs grow. They're protected from the details, but this protection doesn't happen by magic. The provider has to do a lot of work behind the scenes to manage this highly dynamic environment.

![](img/2d28ab1e4ea39ed71271c8bf426f216b_225_1.png)

The foundations have to be in synch between the two worlds. And when your company reviews different cloud options, management must understand how the cloud provider deals with foundational issues:

![](img/2d28ab1e4ea39ed71271c8bf426f216b_226_0.png)

- **License management:** Many license agreements tie license fees to physical servers rather than to virtual servers. Resolve these licenses before using the associated software in a virtual environment. The constraints of such licenses may become an obstacle to efficiency.
- **Service levels:** Measuring, managing, and maintaining service levels can become more complicated simply because the environment itself is more complex. When cloud computing is added in to the mix, the cloud consumer is responsible for establishing service levels for both internally virtualized environments as well as those living in the cloud.
- **Network management:** The real target of network management becomes the virtual network, which may be harder to manage than the physical network.
- **Workload administration:** Set policies to determine how new resources can be provisioned, and under what circumstances. Before a new resource can be introduced, it needs to be approved by management. Also, the administrator has to be sure that the right security policies are included.
- **Capacity planning:** Although it’s convenient to think that all servers deliver roughly the same capacity, they don’t. With virtualization, you have more control of hardware purchases and can plan network resources accordingly.

## Abstraction layer

Managing virtualization requires an *abstraction layer* that hides and manages things between the physical storage subsystems. The virtualization software needs to present the whole storage resource to the virtualized environment as a unified, sharable resource. That process can be more difficult than it sounds.

All the administrative functions that you’d need in a physical data center have to be deployed in a virtualized environment, for example. Following are some of the most important considerations:

**A business can use virtualized storage for backup, recovery, and disaster recovery.** Virtualized storage can reinforce or replacing existing backup and recovery capabilities. It can also create *mirrored systems* duplicates of all system components and, thus, might participate in disaster-recovery plans. This issue must be resolved both for internally virtualized environments as well as those leveraging external clouds.
