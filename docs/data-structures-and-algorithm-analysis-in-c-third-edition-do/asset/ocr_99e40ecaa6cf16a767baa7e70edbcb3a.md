# Sec. 8.2 Disk Drives

![](bbox=[0.291, 0.185, 0.708, 0.353])

**Figure 8.2** (a) A disk drive arranged as a stack of platters. (b) One track on a disk platter.

to head. The data on a single platter that are accessible to any position of the head for platter are collectively called a *track*, that is, all data on a platter that are a fixed distance from the spindle, as shown in Figure 8.2(b). The collection of all tracks that are a fixed distance from the spindle is called a *cylinder*. Thus, a cylinder is all of the data that can be read in a particular position.

Each track is subdivided into *sectors*. Between each sector there are *inter gaps* in which no data is stored. These gaps allow the read head to recognize the size of each sector. Note that each sector contains the same amount of data. Because the outer tracks have greater length, they contain fewer bits per inch than the inner tracks. Thus, about half of the potential storage space is wasted, because only the innermost tracks are read at the highest possible data density. This arrangement is illustrated by Figure 8.3. Disk drives today actually group tracks into “zones” such that the tracks in the innermost adjust their data density going out to maintain the radial data density, the tracks of the next zone read the data density to make better use of their storage ability, and so on. This arrangement is shown in Figure 8.3.

In contrast to the physical layout of a hard disk, a CD-ROM consists of a single spiral track. Bits of information along the track are equally spaced, so the information density is the same at both the outer and inner portions of the track. To keep the information flow at a constant rate along the spiral, the drive must speed up the rate of spin as the I/O head moves toward the center of the disk. This makes for a more complicated and slower mechanism.

Three separate steps take place when reading a particular byte or series of bytes from a hard disk. First, the I/O head moves so that it is positioned over the track containing the data. This movement is called a *seek*. Second, the sector containing the data rotates to under the head. When in the disk is always

compromises over time. In addition, most of the description given here for disk drives is a simplified version of the reality. But this is a useful working model to understand what is going on.