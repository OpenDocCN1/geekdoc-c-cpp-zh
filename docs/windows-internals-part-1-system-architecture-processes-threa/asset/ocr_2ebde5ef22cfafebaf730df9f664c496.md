The main point to remember when thinking about robustness—and SuperFetch optimizations in general—is that SuperFetch constantly monitors patterns and updates its understanding of the system to avoid fetching useless data. Although changes in a user's daily activities or application startup might cause SuperFetch to pollute the cache with irrelevant data or throw out that it might think is useless, it quickly adapt to any pattern changes. If the user's actions are erratic and random, the worst that can happen is that the system will behave in a similar state as SuperFetch were not present at all. If SuperFetch is ever in doubt or cannot track reliably, it quiets itself and doesn't makes to a given process or page.

# # ReadyBoost

These days, RAM is easily available and relatively cheap compared to a decade ago. Still, it doesn't beat the cost of secondary storage such as hard drives. Unfortunately, mechanical hard disks contain many moving parts, they are fragile, and more importantly, are relatively slow compared to RAM, especially during seeking. As a result, storing active SuperFetch data on the drive would be as bad as paging out a page and hard-fault inside memory.

Solid state and hybrid drives offset some of these disadvantages but they are pricier and slower than RAM. Portable solid media such as USB flash disk (UFD), CompactFlash, and Secure Digital cards, however, provide a useful compromise. They are cheaper than RAM and available in larger sizes, but also have shorter times than mechanical hard drives because of the lack of moving parts.

> Note In practice, CompactFlash and Secure Digital cards are almost always faced through a USB adapter, so they all appear to the system as USB flash disks.

Random disk I/O is especially expensive because disk seek time puts rotational latency typical desktop hard drives total about 10 milliseconds—an eternity for today's 3 or 4 GHz processors. Flash memory, however, can service read up to 10 times faster than a typical hard drive. Windows includes a feature ReadyBoost to take advantage of flash storage devices by creating an intermediate caching layer on them that logically sits between memory and disks.

ReadyBoost (not to be confused with ReadyBoost) is implemented with a driver of (%System-Root%\System32\Drivers\Readyboost.sys) that is responsible for writing the cached data to the non-volatile RAM (NVRAM). When you insert a USB flash disk into a system, ReadyBoost looks at the device to determine its performance characteristics and the results of its insert in HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Endmgmt (End is for external memory, the working name for ReadyBoost during its development).

If the new device is between 256 MB and 32 GB in size, it has a transfer rate of 2.5 MB per second or higher for random 4 KB reads, and has a transfer rate of 1.75 MB per second or higher for random 512 KB writes, ReadyBoost will ask you if you'd like to dedicate some of the space for caching. If you agree, ReadyBoost creates a file named ReadyBoost.scache in the root of the device, which it uses to store cached pages.

CHAPTER 5 Memory management 479