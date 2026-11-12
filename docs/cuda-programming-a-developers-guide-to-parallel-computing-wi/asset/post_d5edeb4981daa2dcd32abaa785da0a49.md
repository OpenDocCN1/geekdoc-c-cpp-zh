
With a liquid-cooled system, you have spare slots between the cards, as most liquid-cooled solutions are single slot. As soon as you add a RAID controller card, the associated slot drops to X8 or X4 for both the GPU and RAID card. This is unless you dedicate an X16 slot to the RAID controller, something we'd recommend.

There is a physical limit on the number of drive bays that can be included in a workstation format. Even a motherboard with seven PCI-E slots, often dubbed supercomputer motherboards, have only three slots left available once four liquid-cooled GPUs are present. This allows for two RAID controllers and a single high-speed network card to be squeezed into such systems.

RAID, however, is not simply about speed, although the RAID-0 mode is used for this. RAID-1 supports mirroring, where the data is completely duplicated onto another disk. Failure of one disk then means the system falls back to the remaining disk without significant impact on the operation of the system. Clearly, however, the faulty disk needs to be replaced as soon as possible. It saves you the case where several weeks of compute time could be lost due to a faulty hard drive.

With a small cluster, hard drives fail regularly enough that it's not that much of a problem. However, in a larger setup, with thousands of active drives, you will be changing drives regularly.

RAID-5 is a system that balances storage usage with redundancy, allowing data to be split over multiple drives in a safe manner. One of the drives in a set is a dedicated parity drive that, if one drive fails, can be used to recover the RAID array. RAID is something you definitely need to consider if restarting your job on another machine and losing the computations to date is not acceptable.

Check pointing is a system that is often used to avoid the effects of failure. After a certain period, the entire results to data are check-pointed or dumped to permanent storage. Thus, the job can be moved to another node by simply moving the check-pointed data and the associated program code. In designing applications that run for some period of time, you should always consider building a check pointing system into the application.

## HDSL

HDSL is a standard from a company called OCZ that has developed a number of innovative products in the SSD market. Most notable of these is the RevoDrive range, a product that is basically a number of SSD drives on a PCI-E card with a built-in hard disk controller. This original card achieved on the order of 500 MB/s, which is quite reasonable; the high-end cards (the R4 C series) claim 2800 MB/s. You would need a SATA-3 controller and at least five top-end SSDs to achieve the same sort of bandwidth.

The HDSL drive offered by OCZ is also an interesting product and an insight into where storage is likely to go. It embeds four older-style SSD drives into a standard 3.5 inch hard disk, with an embedded RAID-0 controller. A special controller card is used that basically extends four lanes of the PCI-E bus through a cable directly to the drive interface. Four PCI-E 2.0 lanes equates to around 1 GB/s in both directions, vastly superior to the unidirectional SATA-3 interface.

Being a new technology, it has some way to go before the drives themselves match this bandwidth. Currently, the drive peaks at around 750 MB/s, which is somewhat shy of the 1000 MB/s capacity of the link. The drive ships with a single-port X4 HDSL controller, but dual- and quad-port X8 and X16 controllers are planned. Assuming the drive picks up a little in speed to the full bandwidth of the interface, which is almost certain given the march of technology, this will be a very interesting technology to see evolve.

As the drives themselves are a 3.5 inch format, this means more drives can be put in the same physical space. Allocating two X8 slots would support four HDSL drives, giving a read/write capacity of around 3 GB/s.

## Mass storage requirements

As well as speed of input from the mass storage devices, we have the total storage capacity. Take one of the largest users of data in the world, Google. In 2008 they were processing 20 petabytes of data per day. A petabyte is 1000 terabytes, which is itself 1000 gigabytes. Given that the largest single mass storage drive available today is around 4 terabytes, just to store that amount of data would require (20 x 1000) ÷ 4 = 5000 hard disk drives!

So clearly one consideration in designing any node is mass storage needs. In practice, most large installations use dedicated storage nodes that do not have any compute functionality. Thus, the compute nodes need only the storage capacity necessary for a single compute run. They can download data over a high-speed interconnect from a central data cluster, meaning you can design them with high-speed, small-capacity SSD drives, which we've done with some of our test machines at CudaDeveloper.

## Networking

Networking is one of the key issues when you consider a system that contains more than a single node. Clusters of nodes have become very common in universities and commercial organizations as the availability of cheap commodity hardware has become commonplace. It is relatively straightforward to configure a small network of machines and have them work together on a problem.

You typically see two types of networks: those based on gigabit Ethernet and those using somewhat faster, but considerably more expensive, InfiniBand networks. Gigabit Ethernet is cheap, usually comes as free on the motherboard, and can be connected to a 16-, 24-, or 32-port switch with relative ease. Some motherboards offer dual-gigabit Ethernet connections, which often include a feature called Link Aggregation. This, when supported by the switch, allows for the two physical links to be used as one, doubling the amount of bandwidth available to and from that node.

How critical networking is to your problem depends greatly on the amount of data that needs to be shared. If you can stay within a single node and go the multiple-GPU route, this will be far, far more effective than going down the multiple-node route in most cases.

Systems like Google's MapReduce is one example where, due to the huge amount of data being used, you are forced to split the data between multiple nodes. MapReduce works on the principle of a shared and distributed file system, making the file system appear as one very large disk. The data itself is located in chunks on the local storage of each node. Instead of bringing the data to the program, MapReduce sends the program to where the data is physically located. Hadoop is an open-source implementation of MapReduce, allowing you to set up a very similar framework for distributing and scheduling such jobs. Typically the dataset is very large and the program very small, so this type of approach works really well in greatly reducing network traffic.

Dedicated communication with something like MPI is also typically how such a system is set up. However, as soon as network communication becomes the dominant feature of the program, in terms of time, you need to move to a faster network architecture such as InfiniBand. This obviously incurs cost, which you may be able to avoid through clever programming, such as asynchronous communication, compressing data packets, etc.

Peer-to-peer communication within a node between the GPUs is now supported with the CUDA 4.0 SDK. In addition, the GPUs can talk directly to certain InfiniBand cards in the same way, without the interaction of the host CPU. Thus, for larger-scale GPU installations, InfiniBand and other higher-speed interconnects can become a necessity if network traffic plays a significant role.

## POWER CONSIDERATIONS

Power usage is a big consideration when designing machines that constantly run. Often the operating costs of running a supercomputer over just a few years can equate to the cost of installing it in the first place. Certainly, the cost of running such a machine over its lifetime will easily exceed the original installation costs.

Power usage comes from the components themselves, but also from the cooling necessary to allow such computers to operate. Even one high-end workstation with four GPUs requires some planning on how to keep it cool. Unless you live in a cold climate and can banish the computer to somewhere cold, it will do a nice job of heating up the office for you. Put a number of such machines into one room, and very rapidly the air temperature in that room will start to rise to quite unacceptable levels.

A significant amount of power is therefore expended on installing air conditioning systems to ensure computers remain cool and can operate without producing errors. This is especially so where summer temperatures can reach 85°F/30°C or higher. Air conditioning is expensive to run. Significant thought should be given to how best to cool such a system and if the heat energy can in some way be reused. Liquid-cooled systems are very efficient in this way in that the liquid can be circulated through a heat exchanger and into a conventional heating system without any chance of the two liquids ever mixing. I’m always amazed by the lack of thought that goes into how to reuse waste heat in computer installations. With the ever-increasing costs of natural resources, and the increasing pressures on companies to be seen as green, simply pumping the heat out the window is no longer economically or socially acceptable.

If you look at the top-end GPU cards, they typically come in around the 250 W mark in terms of power consumption. A typical GPU card is around 125 W by comparison. A typical power budget for a four-GPU system might therefore be as shown in Table 11.1.

| Component | Number | Power per Unit | Total Power |
| :--- | :--- | :--- | :--- |
| GPU | 4 | 250 | 1000 |
| CPU | 1 | 125 | 125 |
| Memory | 16 | 1 | 16 |
| Motherboard | 1 | 50 | 50 |
| Boot drive | 2 | 5 | 10 |
| Data drive | 8 | 5 | 40 |
| Peripherals | 1 | 10 | 10 |
| Total | | | 1251 |
