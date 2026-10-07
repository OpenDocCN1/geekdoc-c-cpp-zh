# LOCK-BASED CURRENT DATA STRUCTURES

# References

[B+10] "Analysis of Linux Scalability to Many Cores" by Silas Boyd-Wickizer, Austin T. Devoshi, Yangdong Mao, Alexey Peseter, M. Franks Kaashok, Robert Morris, Nikolai Zedovich. OSI '10, Vancouver, Canada, October 2010. A great study of how Linux performs on multicore machines, as well as some simple solutions. It needs a *sloppy* counter to solve one of the scaling problem contention.

[BH73] "Operating Systems Principles" by Peter Hahn. Prentice-Hall, 1973. Available: http://portal.acm.org/citation.cfm=540365. One of the first books on operating systems simply ahead of its time. Introduced as a concurrency primitive.

[BC05] "The Linux Kernel (Third Edition)" by Daniel P. Bovet and Marco Cesati. O'Reilly Media, 2005. The classic on the Linux kernel. You should read it.

[C06] "The Search for Fast Cycles" by Jonathan Bonter. February 1, 2006. Available: http://lwn.net/Articles/170003. LWN has many wonderful articles about the latest in Linux This article is a short description of approximate counting; read it, and others, to learn about the latest in Linux.

[L13] "An Analysis of Linux File System Evolution" by Lanye Lu, Andrea C. Arpaci-Dusseau, Remi H. Arpaci-Dusseau, Shan Lu. San Jose, CA, February 2013. Our study traces patches to Linux file systems over nearly a decade. Lots of finds there; read it to see! The work was painful to do; the poor graduate student, Lanye Lu, to look through every detail by hand in order.

[M98] "Nonblocking Algorithms and Preemption-Safe Locking on Multiprocessed Shared-Memory Processors." M. Michael. Scott. Journal of Parallel and Distributed Computing, Vol. 51, No. 1, 1998 Professor Scott and his students have been at the forefront of concurrency algorithms and data structures for many years; check out his web page, numerous papers, or to find out.

[MS04] "Concurrent Data Structures" by Mok Nair and S Sahni. Chapman and Hall/CRC Press, 2004. Available: www.cs.tsau.edu.cn/shani/concurrent-data-structures.pdf. A short but comprehensive reference on concurrent data structures. Though it is missing some of the latest works in the field, it is an incredibly useful reference.

[MM00] "Internals: Kernel Architecture" by Jim Mauro and Richard McDougall. Prentice Hall, October 2000. The Solaris book. But If you want to learn about something other than Linux.

[S+11] "Making the Common Case the Only Case with Anticipatory Memory Allocation" by Sundarasan, Sundarasan, Jupu Zhang, Seiram Subramanianian, Andrea C. Arpaci-Dusseau, Remzi H. Arpaci-Dusseau . FAST '11, San Jose, CA, February 2011. Our work on removing possibly-failing allocation calls from kernel nodes. By allocating all potentially needed memory before doing any work, we avoid failure depth in the storage stack.