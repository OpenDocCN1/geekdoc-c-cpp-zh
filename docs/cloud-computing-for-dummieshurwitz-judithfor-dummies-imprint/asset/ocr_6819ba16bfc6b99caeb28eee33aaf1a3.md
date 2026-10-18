With **Software as a Service (SaaS)**, the SaaS vendor provides a proprietary application as its value to customers. While the vendor invests in this software, it typically relies on partners to support many of the other functions. These vendors also take advantage of open-source components. See Chapter 12 for more about SaaS.

![](bbox=[0.11, 0.26, 0.19, 0.37])

# Open-source dynamic

The cloud is an economic and business model as much as a technology model.

It isn’t surprising, then, that open-source software is an important element for almost all cloud providers. Some of it is very high quality and nearly all of it can be used for no license fee, as long as you obey the restrictions of the associated license.

Open-source software has already become a business factor in the *Internet service provider (ISP)* business, with most ISPs providing an easily installed, highly functional software stack for building Web sites. Many cloud providers take open-source software as a foundation and customize it to optimize support for their workloads.

The other software area that impacts costs is the way operating systems are handled in the data center. Under traditional operation, an OS has many background processes running. All such processes have a function and quite a few of them run by default, whether you need them or not. Some of them are keeping logs, some are handling messages from the network, some fire off scheduled jobs, some handle printing, some provide directory services, and so on. They all sit there happily chewing up CPU cycles. None of them should be there unless they have a specific role to play.

![](bbox=[0.11, 0.68, 0.19, 0.78])

In a traditional environment, no one would think of deleting useful background processes, but nothing superfluous should run in an environment that prizes efficient resource usage. Not only that, but if you’re running a cloud data center, you may be interested in rewriting some of these tasks because you need them to run slightly differently. That’s why open source plays a large role in cloud operations.

# Economies of Scale

We spend a lot of time in this chapter saying why the economics of the cloud are so different than that of the traditional data center. Of course, not every workload is right for the cloud.