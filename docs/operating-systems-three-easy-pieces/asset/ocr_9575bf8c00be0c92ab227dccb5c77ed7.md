# LOCKS

# 351

# # References

[D91] "Just Win, Al Davis and His Raiders" by Glenny Dixon. Harcourt, 1991. The book about Al Davis and his famous quote. Or suppose, the book is about Al Davis and the Raiders, and not so much about the quote. To be clear: we are not recommending this book, we just needed a citation.

[D13] "Everything You Wanted to Know about Synchronization but We Were Afraid to Ask" by Tudor David, Rachael Guerriao, Vileslavis Tritonikos. SOSP '13, Nemacoon-Leeds Pennsylvania, November 2013. An excellent paper comparing many different ways to build locks using primitives. To see how many ideas work on modern hardware.

[D68] "Sequential processes" by Eds Dijkstra. 1968. Available online: http://www.cs.utex.edu/dijkstra/sp.pdf. One of the early simple papers. Discusses how Dijkstra posted the originality problem, and Dekker's solution.

[M93] MIPS R4000 Microprocessor User's Manual by Joe Heinrich. Prentice-Hall, 1993. Available: http://cg.sail.net/docs/R4000_Manual.pdf. The old MIPS manual still exists

[H91] Free-choice Synchronization in ACM TOPLAS, Volume 13, Number 1, January 1991. A manual paper introducing a different approach to building concurrent data structures. Because of the complexity involved, some of these ideas have been slow to gain acceptance in deployment.

[O81] "Observations on the Development of an Operating System" by Hauger L. Pacific Grove, California, December 1981. A multi-user retrospective about the development of the MIPS OS, an early project. Full and many of highlights

[L92] "Linux includes threads" by Many authors.... Available: http://www.kernel.org/doc/linux/process.html, take a look at the npt subdirectory where you will find the first of thread support in Linux.

[M82] "The Architecture of Synchronization and the Burroughs B5000: 20 Years Later and Still Ahead of their Time" by A. Meyer. 1982. Available at: http://www.ajm.net/papers/B5000.html (RDK) is an unstable operation which reads and writes into a memory location. A Dekker-phase lock called Lamport then...

[O15] SpinLock is Unsafe by J. McCall. https://simaj.com/blog/2016/12/16/spinlock-unsafe. Calling SpinLock on a Mac is unsafe when threads of different priorities-which might spin forever! To be careful, make atomics fast, even your system can be less than...

[M91] "Algorithms for Synchronization in Shared-Memory Processors" by J. Miller-Crummy and M. L. Scott. ACM TOPLAS, Volume 9, Number 1, February 1991. An analysis of various locking algorithms. No operating systems use support, for just handles hardware.

[P81] "Methods about the Universal Expression" by G. L. Peterson. Information Processing 12, (3), pages 115–116, 1981. Peterson's algorithm introduced here.

[S05] "Guide to porting Solaris to Linux x86" by Ajay Sood, April 2005. Available: http://www.ibm.com/developers/linux/library/1/.

[S03] "OpenThreads Library Reference" by Sun. Code: src.solaris.org/src/sys/unix/xv3/. Pretty printing, on on/src/lib/pthread/threads_sync.h. Interesting, as who knew that threads were not for Oracle Solaris. Thanks to Mike Swift for the pointer.

[W00] "Link-Store-Condition" by E. Thomas. en.wikipedia.org/wiki/Link-Store-Condition. Can you reinforce Wikipedia? But, we found the information and it was not wrong. To further, if it was useful, listing the details for the different architectures: 1ldx/sti and ldq/stq (Alpha), 1/wap/stwcx (PowerPC), 1/sc (MIPS), and 1ldrex/strex (ARM). Actually Wikipedia is pretty amazing, so is it not sorry, or?

[W90] THE SPARC Architecture Manual: Version 9 by D. Weaver, T. German. SPARC International, 2000. http://www.sparc.org/standards/SPARC.pdf. For developers. sun.com/articles/atomic_sparc/ for more atom.

© 2008-19 ARC-PARDUSEE

THREE
EASY
PIECES