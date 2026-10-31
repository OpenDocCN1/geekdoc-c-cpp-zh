cation and reflects the time it takes for the disk head to move to the proper track.

avgAccessRate_accesses/sec = 1 / (avgSeekTime_sec + avgRotationalLatency_sec + dataTransferTime_sec)

The seek time for the disk being used as an example is 2 milliseconds. The sum of the seek time and average rotational latency is 5 milliseconds. The data transfer time is so small in relation to this value that it can be ignored. This yields an average access rate of 200 accesses per second (IOPS) for this single disk.

The specifications for solid-state drives generally give the access time or rate and the read and write rates. Typical numbers at the time of this writing are random reads at 40,000 IOPS, random writes at 50,000 IOPS, sequential read data rates at 415 MB/second and write data rates at 260 MB/second.

Calculating access rates for RAID arrays is significantly complicated, as it depends upon the type of disk, the number of spindles in the array, the RAID configuration, the mixture of read and write operations, and the size of the dataset being transferred. There are a number of online calculators that you can use to determine the actual rates, such as Marek Wolynko's IOPS calculator at http://www.wmarow.com/. For a comprehensive discussion of RAID array performance, see Chapter 3 of Somasundaram and Shrivastava's Information Storage and Management: Storing, Managing, and Protecting Digital Information.¹

Calculations for storage subsystems, particularly those with battery-backed memory, are so dependent upon the design of the storage subsystem and the mechanisms used to access them that you will have to search online or consult the vendor to determine the characteristics of the system you are using.

Contention for the disk is another issue you need to take into consideration. Disks tend to be shared resources, and it is often difficult to determine the actual level of disk utilization. For this reason, your computations regarding disk performance should be taken as upper

1. G. Somasundaram and Alok Shrivastava, Information Storage and Management: Storing, Managing, and Protecting Digital Information, Indianapolis: John Wiley & Sons (2009).