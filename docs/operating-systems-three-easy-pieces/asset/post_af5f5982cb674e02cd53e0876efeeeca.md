
# Hard Disk Drives

The last chapter introduced the general concept of an I/O device and showed how the OS might interact with such a beast. In this chapter, we dive into more detail about one device in particular: the hard disk drive. These drives have been the main form of persistent data storage in computer systems for decades and much of the development of file system technology (coming soon) is predicated on their behavior. Thus, it is worth understanding the details of a disk's operation before building the file system software that manages it. Many of these details are available in excellent papers by Ruemmler and Wilkes [RW92] and Anderson, Dykes, and Riedel [ADR03].

> Crux: How to Store and Access Data On Disk
How do modern hard-disk drives store data? What is the interface? How is the data actually read or accessed? How does disk scheduling improve performance?

## 37.1 The Interface

Let's start by understanding the interface to a modern disk drive. The basic interface for all modern drives consists of a large number of sectors (512-byte blocks), each of which can be read or written. The sectors are numbered from 0 to $n-1$ on a disk with $n$ sectors. Thus, we can view the disk as an array of sectors; 0 to $n-1$ is the address space of the drive.

Multi-sector operations are possible; indeed, many file systems will read or write 4KB at a time (or more). However, when updating the disk, the only guarantee drive manufacturers make is that a single 512-byte write is atomic (i.e., either completes in its entirety or it won't complete at all); thus, if an untimely power loss occurs, only portion of a larger write may complete (sometimes called a torn write).

There are some assumptions most clients of disk drives make, but that are not specified in the interface; Schlosser and Ganger have

# HARD DISK DRIVES

![](img/133d518e3f69f4caaead32c569ae6c49_495_0.png)

Figure 37.1: A Disk With Just A Single Track

Let's start with the "unwritten" of disk drives [SG04]. Specifically, one can usually assume that accessing two blocks' near-another within the drive's address space will be faster than accessing two blocks that are far apart. One can also assume that accessing blocks in a contiguous chunk (i.e., a sequential read or write) is the fastest access mode, and usually much faster than any more random access pattern.

## 37.2 Basic Geometry

Let start to understand some of the components of a modern disk. We start with a platter, a circular hard surface on which data is stored by inducing magnetic changes to it. A disk may have one or more platters; each platter has 2 sides, each of which is a surface. These platters are usually made of some hard material (such as aluminum), and then coated with a thin magnetic layer that enables the drive to persistently store bits even when the drive is powered off.

The platters are all bonded together around the spindle, which is connected to a motor that spins the platters (while the drive is powered on) at a constant (fixed) rate. The rate of rotation is measured in rotations per minute (RPM), and typical modern values are in the 7,200 RPM to 15,000 RPM range. Note that we will often be interested in the time of a single rotation, e.g., a drive that rotates at 10,000 RPM means that a single rotation takes 6 milliseconds (ms).

Data is encoded on each surface in concentric circles of sectors; we have one concentric track per track. A single surface contains many thousands of thousands of tracks, tightly packed together, with hundreds of tracks fitting into the width of a human hand.

To read and write from the surface, we use a mechanism that allows us either sense (i.e., read) the magnetic patterns on the disk or to induce a change (i.e., write) them. This process of reading and writing is accomplished by the disk head; there is one head per surface of the drive. The disk head is attached to a single disk arm, which moves across the surface to position the head over the desired track.

> We, and others, use the terms block and sector interchangeably, assuming the reader will know exactly what is meant per context. Sorry about this!

458
OPERATING SYSTEMS[VERSION 1.01]
WWW.OSTEP.ORG

# HARD DISK DRIVES

# 459

Rotates this way

![](img/133d518e3f69f4caaead32c569ae6c49_496_0.png)

Figure 37.2: A Single Track Plus A Head

## 37.3 A Simple Disk Drive

Let's understand how disks work by building up a model track at a time. Assume we have a simple disk with a single track (Figure 37.1). This track has 12 sectors, each of which is 512 bytes in size (our typical sector size, recall) and addressed by the numbers 0 through 11. The single platter we have rotates over the spindle, to which a motor is attached.

Of course, the track itself isn't too interesting; we want to be able to read or write those sectors, and thus we need a disk head, attached to a disk arm as we now see (Figure 37.2). In the figure, the disk head, attached to the end of the arm, is positioned over sector 6, and the surface is rotating counterclockwise.

### Single-track Latency: The Rotational Delay

To understand how a request would be processed on our simple, one track disk, imagine we now receive a request to read block 0. How would the disk service service this request?

In our simple disk, the disk doesn't have to do much. In particular, it must wait for the desired sector to rotate under the disk head. This wait happens often enough in modern drives, and it is an important component of I/O service time, that it has a special name: rotational delay (sometimes rotation sounds weird). In the example of if the full rotational delay is R, the disk has to incur a rotational delay of about $R/2$ to wait for 0 under the read/write head (if we start at 6). A worst-case scenario on this single track would be to sector 5, causing nearly a full rotational delay in order to service such a request.

### Multiple Tracks: Seek Time

So far our disk has a single track, which is not too realistic; modern disks of course have many millions. Let's look at an ever-slightly more realistic disk surface, one with three tracks (Figure 37.3, left).

In the figure, the head is currently positioned over the innermost track (which contains sectors 24 through 35); the next track over contains next sectors of tracks (12, 23), and the outermost track contains the first sectors (0 through 11).

© 2008–19, APCACI-DUSSEAU
THREE EASY PIECES

# HARD DISK DRIVES

Rotates this way

![](img/133d518e3f69f4caaead32c569ae6c49_497_0.png)

Rotates this way

> Figure 37.3: Three Tracks Plus A Head (With: Seek)

To understand how the drive might access a given sector, we now trace what would happen on a request to a desired sector, or a reader to 11. To service this the drive has to move the disk to the correct track (in this case, the outermost), in a process known as a seek. Seeks, with rotations, are one of the most costly disk operations.
The seek, it should be noted, has many phases: first as the disk arm moves; then acceleration as the arm moves at full speed; then deceleration as the arm slows down; finally settling as the head is carefully positioned over the track. The settling time is often significant, e.g., 0.5 to 2 ms, as the drive must be certain to find the right track (imagine if it just could!).
After the seek, the disk arm has positioned head over the right track. A depiction of the seek is found in Figure 37.3 (right).
As we see, during the seek, the arm has moved to the desired track, and the platter of course has rotated, in this case about 3 sectors. Thus, sector 9 is just to pass under the disk head, and we must only endure a short rotational delay to complete the transfer.
When sector 11 passes under the disk head, the final phase of I/O takes place, known as the transfer, where data is either read from or written to the surface. And thus, we have a complete picture of I/O time: first a seek, waiting for rotational delay, and finally the transfer.

# Some Other Details

Though we won't spent too much time on it, there are some other details about how hard drives operate. Many drives employ some kind of track skew to make sure that sequential reads can be properly serviced even when crossing track boundaries. In our simple example disk, this may appear as in Figure 37.4 (page 461).
