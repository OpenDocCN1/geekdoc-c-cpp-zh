reading, writing, or both; and whether its pre-existing contents should be deleted.

+   - **read(char +buf, int count):** Read count bytes from the current position in the file. The current file position moves forward as these are read. The bytes are read into array **buf**, which must be at least **count** bytes long.

+   - **write(char +buf, int count):** Write count bytes at the current position in the file (overwriting the bytes already at that position). The current file position moves forward as these are written. The bytes to be written from array **buf**.

+   - **seek(int pos):** Move the current position in the file to pos. This allows bytes at arbitrary places to be read or written. There are actually two “current” positions: one for reading and one for writing. Function **seek** changes the “get” or read position, while function **seek** changes the “put” or write position.

+   - **close():** Close a file at the end of processing.

Note that if this ADT is similar to the “message passing” version of the ADT for buffer pools described in Section 8.3.

# 8.5 External Sorting

We now consider the problem of sorting records too large to fit in main memory. The records must reside in peripheral or external memory, such sorting methods are called **external sorts**. In contrast to the internal sorts discussed in Chapter 7 which assume that the records to be sorted are stored in main memory. Sorting large collections of records is central to many applications, such as processing payroll and large database databases. Many external sorting algorithms have been devised. Years ago, sorting algorithm designers sought to optimize the use of specific hardware configurations, such as multiple tape or disk drives. Most computing today is done on personal computers and low-end workstations with relatively powerful CPUs, but only one or at two disk drives. The techniques presented here are geared towards optimizing on a single disk drive. This approach allows us to cover the most important issues in external sorting while skipping many important machine-dependent details. Readers who need to implement efficient external sorting algorithms that take advantage of more sophisticated hardware configurations should consult the references in Section 8.6.

When a collection of records is too large to fit in main memory, the only practical way to sort it is to read some records from disk, do some rearranging, then write them back to disk. This process is repeated until the file is sorted, with each record read happens many times. Given the high cost of disk I/O, it should come as