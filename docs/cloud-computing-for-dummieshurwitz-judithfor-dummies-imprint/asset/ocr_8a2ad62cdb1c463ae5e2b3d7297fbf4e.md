Managing data center resources is hard under any circumstance — and even harder when those resources are running in virtual partitions. These managed resources need to provide the right level of performance, accountability, and predictability to users, suppliers, and customers. Virtualization must be managed carefully.

# Virtualizing storage

Increasingly, organizations also need to virtualize storage. This trend currently works in favor of NASes rather than SANs, because a NAS is less expensive and more flexible than a SAN.

Because the virtualized environment has at least the same requirements as the traditional data center in terms of the actual amount of data stored, managing virtualized storage becomes very important.

In addition to application data, virtual machine images need to be stored. When virtual machines aren’t in use, they’re stored as disk files that can be instantiated at a moment’s notice. Consequently, you need a way to centrally store virtual machine images.

# Hardware provisioning

Before virtualization, hardware provisioning was simply a matter of commissioning new hardware and configuring it to run new applications (or possibly repurposing hardware to run some new application).

Virtualization makes this process a little simpler in one way: You don’t have to link the setup of new hardware to the instantiation of a new application. Now you can add a server to the pool and enable it to run virtual machines. Thereafter, those virtual machines are ready when they’re needed. When you add a new application, your cloud data center administrator or your service provider (via a self-service interface) will enable you to configure it to run on a virtual machine.

One of the key benefits that companies have found with cloud computing is the ability to quickly and effectively provision additional hardware resources from Infrastructure as a Service providers.

Provisioning is now the act of allocating a virtual machine to a specific server from a central console. Be aware of a catch, however: You can run into trouble if you go too far. You may decide to virtualize entire sets of applications and virtualize the servers that those applications are running on, for example.