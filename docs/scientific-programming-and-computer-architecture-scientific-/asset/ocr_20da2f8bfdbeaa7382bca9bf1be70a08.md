# Chapter 5. Threads and Shared Memory

```
work_count[i] += 1;
}
```

The manager does not join with any of the worker threads after it tells them to shut down. The worker threads were detached earlier. If the worker threads were not detached, the manager must join with the worker threads to prevent them from turning into zombies.

# Cache coherence and the cost of propagating writes

Table 5.6 shows that the plain C implementation we have described takes only 720 cycles per parallel region on an average when the number of threads is two. Why does each parallel region take 720 cycles? In answering that question, we run into a vital part of the hardware infrastructure for supporting threaded programming, namely, the cache coherence protocols.

The worker threads and the manager are exchanging information using the arrays work_count[], fnlist[], and arglist[]. The locations of these arrays are specified to be volatile. So we may think of the array entries as residing in DRAM memory, but that is not really correct. In a simple program such as this, the array entries are certain to be in L1 cache. That brings light a new issue. Suppose the manager increases the work_count() of a worker thread. The increment will take place in its own L1 cache. When the worker accesses the same entry, it will look up its own L1 cache. How do writes propagate from L1 to L1 cache?

The manner in which writes propagate from cache to cache is vital for the validity of threaded programs. Most of the time we must try to make each work on its portion of the memory and keep the threads as independent as possible. Threads cannot synchronize without shared memory. Because memory is mirrored in caches, any method of synchronization using shared memory is dependent on the manner in which writes propagate from cache to cache.

Many counters, such as those listed in table A.1 of the appendix, handle writes to cache as follows. Suppose a processor wants to write to a shared cache line. Before the write is complete, the hardware sends a signal to other caches to invalidate the copy of the same cache line. If the other caches do not hold a copy of the same cache line, nothing needs to be done. Indeed, the hardware stores sharing information for