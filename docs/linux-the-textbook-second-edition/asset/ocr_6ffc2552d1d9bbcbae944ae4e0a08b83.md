menu choice Edit>Apply All Operations. In the warning window, click Apply. Click the Close button when the Applying pending operations appears.

13. You now have a created a partition table on, partitioned and formatted a usable disk on our system, shown in Figure 17.6.

14. Quit GParted by making the pull-down menu choice GParted>Quit.

> Conclusion: We have added a new hard disk to our Linux system, and partitioned it with GParted.

# 17.4.4 Adding Disks Using fdisk

A more traditional approach to adding a disk to the system a significant time after installation is covered in this section. We conform to our recommended storage model, as in the previous section where we implemented it for an additional hard disk added using ZFS. In this section, we use the fdisk command to partition additional disks. The example in this section uses an externally mounted USB thumb drive, which is more easily added, and is much easier available to the ordinary user. This example can be easily extended to internally mounted SATA bus drives or other bus architectures. In Chapter W22, titled “ZFS Administration and Use” at the book website, we give more examples of ZFS-based redundancy, to illustrate a similar level of this redundancy within ZFS.

# 17.4.4.1 Partitioning a Disk Using fdisk

fdisk is a command line, interactive, dialog-driven program used to create and manage partition tables on Linux. The following is a brief description of fdisk syntax and use:

```
fdisk [options] device
fdisk -1 [device...]
```

Output: New or manipulated partitions on disk device

+   - N Create a new partition. You enter a partition number, starting sector, and an ending sector. Both start and end sectors can be specified in absolute terms as sector numbers. Pressing the Enter key with no input specifies the default value, which is the start of the largest available block for the start sector and the end of the same block for the end sector
+   
+   - p Display basic partition summary data. This includes partition numbers, starting and ending sector numbers, partition sizes, fdisk's partition types codes, and partition names
+   
+   - t Change a single partition's type code. You enter the type code using a two-byte hexadecimal number
+   
+   - w Write data. Use this command to save your changes

sudo fdisk /dev/sdb
As superuser, run fdisk on the disk /dev/sdb

# Example 17.6 Placing a Single Partition on a USB Thumbdrive Using fdisk

+   - Objectives: To practice placing a Linux partition, with an ext4 filesysem on that partition, on a USB thumb drive.

+   - Prerequisites: Having a usable USB thumb drive for your system.