The external Mergesort algorithm just described requires that log n passes be made to sort a file of n records. Thus, each record must be read from disk and written log n times. The number of passes can be significantly reduced by observing that it is not necessary to use Mergesort on small runs. A simple modification is to read in a block of data, sort it in memory (perhaps using Quicksort), and then output it as a single sorted run.

Example 8.7 Assume that we have blocks of size 4KB, and records are eight bytes with four bytes of data and a 4-byte key. Thus, each block contains 512 records. Standard Mergesort would require nine passes to generate runs of 512, processing each block as a unit can be done in one pass with an internal sort. These runs can be merged by Mergesort. Standard Mergesort requires eighteen passes to create 256k records. Using an internal sort reduces runs of 512 records to one initial pass to create the runs and nine merges to put them all together, approximately half as many passes.

We can extend this concept to improve performance even further. Available main memory is much more than one block in size. If we process large initial runs, the number of passes required by Mergesort is further reduced. For example, most modern computers provide tens or even hundreds of megabytes of RAM to sort. If all of memory (excepting a small amount for buffers and local variables) is devoted to building initial runs as large as possible, then large files can be processed in few passes. The next section presents a technique for producing large runs, typically twice as large as could fit directly into main memory.

Another way to reduce the number of passes required is to increase the number of runs that are merged together during each pass. While the standard Mergesort algorithm merges two runs at a time, there is no reason why merging cannot be limited in this way. Section 8.5.3 discusses the technique of multiway merging.

Over the years, many variants on external sorting have been presented, but all are based on the following two steps:

+   1. Break the file into initial runs.

+   2. Merge the runs together to form a single sorted file.

# 8.5.2 Replacement Selection

This section treats the problem of creating initial runs as large as possible from a disk file, assuming a fixed amount of RAM is available for processing. As mentioned previously, a simple approach is to allocate as much RAM as possible to a large array, fill this array from disk, and sort the array using Quicksort. Thus, if