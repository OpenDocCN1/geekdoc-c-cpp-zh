# CHAPTER 30

# Task Parallelism and Data Parallelism

# IN THIS CHAPTER

+   - Pros and Cons of Threads 1502
+   - The Task Parallel Library 1503
+   - Task Parallelism 1508
+   - Data Parallelism 1529

In Chapter 29, "Threading and Synchronization," we looked at parallel programming from a rather low level, focusing on the concept of threads and a whole set of synchronization primitives. We also learned about the cost of various operating system facilities, giving rise to the creation of thread pools and lightweight synchronization tools for managed code.

Today's computing landscape has radically shifted toward a higher need for parallel programming to speed up programs. In the previous decades, a slow-running program or library wasn't too big of a deal. It was only a matter of time for processor clock speeds to increase enough to make the program run sufficiently faster. Things have changed, though. Although the density of transistors that fit on a chip is still growing at a rapid pace (conforming to Moore's law), we've hit a wall with regard to clock speeds. Instead of getting faster and faster processors, we get more such processor "cores" on a single chip.

Because of this change at the hardware level, we as software folks need to adapt to the standard being multicore machines. It should be clear that this kind of programming requires different tools and (more important) a different mindset to "reason concurrently."

This chapter presents some of the recent work done in the field of parallel programming, starting with the .NET 4 BCL. You learn how low-level concepts such as threads fall short in the changing landscape for a few reasons. During our discussion, we introduce two ways to think about parallel programming: task-oriented versus data-oriented.