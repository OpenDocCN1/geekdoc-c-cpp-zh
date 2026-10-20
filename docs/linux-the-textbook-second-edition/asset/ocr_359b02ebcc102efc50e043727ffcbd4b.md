```
Device    Start       End     Sectors  Size Type
/dev/sdb1  2048 15240542 15238495  7.3G Linux
```

```
Command (m for help): w
The partition table has been altered.
Calling ioctl() to reread partition table.
Syncing disks.
$
```

3. In order for this partition to be usable, you must add a file system to it. We would like to add an ext4 file system to the partition. To do this, use the mkfs command as follows:

```
$ sudo mkfs -t ext4 /dev/sdb1
[sudo] password for bob:
mke2fs 1.42.13 (17-May-2015)
Creating file system with 1893320 4k blocks and 474208 inodes
file system UUID: b89135c2-c38e-45a3-85ff-375781777546
Superblock backups stored on blocks:
    32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632

Allocating group tables: done
Writing inode tables: done
Creating journal (32768 blocks): done
Writing superblocks and file system accounting information:
done

$
```

To use this partition for data, you can create directories and files in those directories.

Conclusion: Using the fdisk utility, and the mkfs command, we deleted any existing partitions on a USB thumb drive, and created a Linux partition on it with an ext4 file system.

# Exercise 17.11

Do the steps of Example 17.6 to partition a USB thumb drive with a single primary partition, and then add an ext4 file system to it. Create directories on the thumb drive.

# Exercise 17.12

Do the steps of Example 17.6 to partition an externally mounted hard drive in a USB enclosure, placing a single primary partition on it, and then add an ext4 file system. Create directories on the hard drive.

# 17.5 Configuring a Printer

We briefly discussed the Linux commands for printing files in Chapter 2, and in more detail in Chapter 6, Section 6.8. There are additional basic methods for adding and configuring a local printer, and printing documents on it, using the CUPS. We detail these methods extensively in Section W26.5 titled “What the Common Unix Printing System Accomplishes,” at the book website. There, we also give some additional details of print commands such as lpadmin, lpc, lpinfo, lpmove, lpoptions, lpq, lp, lpr, lprm, and lpstat.

# 17.6 File System Backup Strategies and Techniques

The general necessity of backing up user and system files on a single-user Linux system, as a part of an ordinary user's routine operations, should be quite obvious. Also, for complex multiuser systems, it is a necessary procedure for anyone responsible for the administration of the system.