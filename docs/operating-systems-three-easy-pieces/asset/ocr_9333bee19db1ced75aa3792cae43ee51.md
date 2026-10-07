# FREE-SPACE MANAGEMENT

195

# References

[B+00] "Hoard: A Scalable Memory Allocator for Multithreaded Applications" by Emery D. Berger, Kathryn S. McKinley, Robert D. Blumofe, Paul R. Wilson. ASPLOS-IX, November 2000. Berger and company's excellent allocator for multiprocessor systems. Beyond just being a fun paper, also used in practice!

[U94] "The Slab Allocator: An Object-Caching Kernel Memory Allocator" by Jeff Bonwick. USENIX. 94. A free paper about how to build an allocator for an operating system kernel, and a great example of how to specialize for particular object sizes.

[E06] "A Concurrent Malloc: Implementation for FreeBSD" by Jason Evans, April, 2006. http://freebsd.org/jemalloc/jemalloc.pdf. A detailed look at how to build a modern allocator for multiprocessors. It is widespread today, with FreeBSD, NetBSD, Mozilla Firefox, and within Facebook.

[K65] \u201cA Fast Storage Allocator\u201d by Kenneth Knowton. Communications of the ACM, Volume 8:10, October 1965. The common reference for buddy allocation. Random strategy: Knuth gives credit for the idea not to keep statistics, a Nobel-prize winning economist. Another strategy: Knuth communicates all his emails via a secretary; he doesn't send email himself, rather he tells his secretary TeX, the tool he used to typeset this book. It is an amazing piece of software.". Last Knuth created TeX, the tool used to typeset this book.

[S15] \u201cUstanding glibc malloc\u201d by Sploftun. February, 2015. sploftun.wordpress.com/2015/understanding-glibc-malloc/. A deep dive into how glibc malloc works. Amazingly detailed and a very cool read

[W+95] \u201cDynamic Memory Allocation: A Survey and Critical Review\u201d by Paul R. Wilson, Mark S. Johnston, Michael Neely, David Boles. International Workshop on Memory Management, Scotland, UK, September 1995. An excellent and far-reaching survey of many facets of memory allocation. Far too much to detail in this tiny chapter!

> \u00b4 Actually we use LaTeX, which is based on Lamport's additions to TeX, but close enough.

\u00a9 2008\19, ARPAC-DUSSE

THREE
EASY
PIECES

* \u2013