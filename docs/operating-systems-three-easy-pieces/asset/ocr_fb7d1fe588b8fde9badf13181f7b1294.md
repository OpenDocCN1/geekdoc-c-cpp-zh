# The 80-20 Workload

![](bbox=[0.268, 0.159, 0.755, 0.452])

Figure 22.7: The 80-20 Workload

You might be noting: is LRU's improvement over Random and FIFO really that big of a deal? The answer, as usual, is, "it depends." If each miss is very costly (not uncommon), then even a small increase in hit rate (reduction in miss rate) can make a huge difference in performance. If misses are not so costly, then of course the benefits possible with LRU are not nearly as important.

Let's look at one final workload. We call this the "looping-sequential workload," as it, we refer to 50 pages in sequence, starting at 0, then 1 ... up to page 49, and then loop, repeating those accesses, for a total of 10,000 accesses to 50 unique pages. The last graph in Figure 22.8 shows the behavior of the policies under this workload.

This common, in many applications (including important commercial applications such as databases [CD85]), represents a worst case for both LRU and FIFO. These algorithms, under a looping-sequential workload, kick out old pages; unfortunately, due to the looping of the workload, these older pages are going to be accessed sooner than the pages that they prefer to keep in cache. Indeed, even with a cache of 49, a looping-sequential workload of 50 pages results in a 0% hit rate. Interestingly, Random fares notably better, not quite approaching optimal, but at least achieving a non-zero hit rate. Turns out that random has some nice properties; one property is not having weird corner-case behaviors.