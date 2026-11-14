This function performs

+   - 2n additions
+   - n assignments
+   - 3n reads
+   - n writes

The call of this function:
add3(x, y, z, w);

is of course less elegant than the operator notation. It is also a little bit more prone to errors: we need to look at the documentation to see whether the first or the last argument contains the result. With operators, the semantics are evident.

In high-performance software, programmers tend to implement a hard-coded version of every important operation instead of freely composing them from smaller expressions. The reason is obvious; our operator implementation performed additionally

+   - 2n assignments
+   - 2n reads
+   - 2n writes
+   - 2 memory allocations
+   - 2 memory deallocations

The good news is we have not performed additional arithmetic. The bad news is that the operations above are more expensive. On modern computers, it takes much more time to read large amounts of data from or to write to the memory than executing fixed or floating-point operations.

Unfortunately, vectors in scientific applications tend to be rather long, often larger than the caches of the platform, and the vectors must really be transferred to and from main memory. In Figure 5-1, we depict the memory hierarchy symbolically. The chip on top represents the processor, the blue chips beneath it the L1 cache, the disks L2, the floppies the main memory, and the cassettes the virtual memory. The hierarchy consists of small fast memory close to the processor and large slow memory. When a data item from small memory is read (marked in the second (blue) cassette), a copy is held in every faster memory (second floppy, first disk, first blue L1 cache chip).

In case of shorter vectors, the data might reside in L1 or L2 cache and the data transfer is less critical. But in this case, the allocation and deallocation become serious slow-down factors.

# 5.3.2 An Expression Template Class

The purpose of Expression Templates (ET) is to keep the original operator notation without introducing the overhead induced by temporaries. The technique was independently discovered by Todd Veldhuizen and Daveed Vandevoorde.