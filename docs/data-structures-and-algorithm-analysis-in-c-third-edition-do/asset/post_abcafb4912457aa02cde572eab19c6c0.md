
A variation on this approach is to have the getblock function take another parameter to indicate the "mode" of use for the information. If the mode is READ then the pool assumes that no changes will be made to the buffer’s contents (and no write operation be done when the buffer is reused to store another block). If the mode is WRITE then the buffer pool assumes the client will not look at the contents of the buffer and no read from the file is necessary. If the mode is AND WRITE then the buffer pool will read the existing contents of the block in disk, and write the contents of the buffer to disk when the buffer is to be reused. Using the "mode" approach, the dirtyblock method is avoided.

One problem with the buffer-passing ADT is the risk of stale pointers. When the buffer pool user is given a pointer to some buffer space at time TI, that pointer does refer to the desired data at that time. As further requests are made to the buffer pool, it is possible that the data in any given buffer will be removed and replaced with new data. If the buffer pool user refers to later time T2 then the data are no longer valid because the buffer contents have been replaced in the meantime. Then the pointer into the buffer pool’s memory becomes “stale.” To guarantee that a pointer is not stale, it should not be used if intervening requests to the buffer pool have taken place.

We can solve this problem by introducing the concept of a user (or possibly multiple users) gaining access to a buffer, and only releasing the buffer when done. We will add method acquireBuffer and releaseBuffer for this purpose. Method acquireBuffer takes a block ID as input and returns a pointer to the buffer that will be used to store it. The buffer pool will keep a count of the number of requests currently active for this block. Method releaseBuffer will reduce the count of active users for the active block. Buffers with active blocks will not be eligible for flushing from the buffer pool. This will lead to a problem if the client neglects to release active blocks when they are no longer needed. There would be a problem if there were more total active blocks than buffers in the buffer pool; however, the buffer pool should be initialized to include more buffers than ever at one time.

An additional problem with both ADTs presents so far comes when the user intends to completely overwrite the contents of a block, and does not need to read the old contents on disk. however the buffer pool cannot generalize whether the user wishes to use the old contents or not. This is especially true with the message-passing approach where a given message might only overwrite part of the block. In this case, the block will be read into memory even when not needed, and then its contents will be overwritten.

This inefficiency can be avoided (at least in the buffer-passing version) by separating the assignment of blocks to buffers from actually reading in data for the block. In particular, the formerly revised buffer-passing ADT does not actually read data in the acquireBuffer readBuffer method. Users who wish to see the old contents must issue a readBlock request to read the data from disk into the buffer, and then a getDataPointer request to gain direct access to the buffer's data contents.

// A single buffer in the buffer pool

```cpp
class Buffer {
public:
    // Read the associated block from disk (if necessary) and
    // return a pointer to the data
    void readBlock() = 0;

    // Return a pointer to the buffer's data array
    // (without reading from disk)
    void* getDataPointer() = 0;

    // Flag the buffer's contents as having changed, so that
    // flushing the buffer will write it back to disk
    void markDirty() = 0;

    // Release the block's access to this buffer. Further
    // accesses to this buffer are illegal.
    void releaseBuffer() = 0;
}
```

// The bufferpool

```cpp
class BufferPool {
public:
    // Constructor: the bufferpool has "numbuff" buffers that
    // each "nuffsize" bytes of data.
    BufferPool(int numbuff, int buffsize) = 0;

    // Relate a block to a buffer, returning a pointer to a
    // buffer object
    Buffer* acquireBuffer(int block) = 0;
}
```

Again, a mode parameter could be added to the acquireBuffer method, eliminating the need for readBlock and markDirty methods.

Clearly, the buffer-passing approach places more obligations on the user of the buffer pool. These obligations include knowing the size of a block, not corrupting the buffer pool's space, and forming the buffer pool when a block has been modified and it is no longer needed. So many obligations make this approach prone to error. An advantage is that there is no need to do an extra step when getting information from the user to the buffer. If the size of the records is large (especially if the record size and buffer size are the same, as is typically the case when implementing B-trees, see Section 10.5), then this efficiency issue might become important. Note however that the in-memory copy time will always be far less than the time required to write the contents of a buffer to disk. For applications where disk I/O is the bottleneck for the program, even the time to copy lots of information between the buffer pool user and the buffer might be inconsequential. Another advantage of buffer passing is the reduction in unnecessary read operations for data that will be overwritten anyway.

You should note that these implementations for the buffer pool ADT do not use templates. Instead, the space parameter and the buffer pointer are declared to be void*. When a class uses a template, that the record type is arbitrary, but using a void* for the space means that not only is the record type arbitrary, but also the buffer pool does not know what the user's record type is. In fact, a buffer pool might have many users who store many types of records.

In a buffer pool, the user decides whether a record will be stored but has no control over the precise mechanism by which data are transferred to the backing storage. This is in contrast to the memory manager described in Section 12.3 in which the user passes a record to the manager and has no control at all over where the record is stored.

# 8.4 The Programmer's View of Files

The C++ programmer's logical view of a random access file is a single stream of bytes. Interaction with a file can be viewed as a communications channel for issuing one of three instructions: read bytes from the current position in the file, write bytes to the current position in the file, and move the current position within the file. You do not normally see how the bytes are stored in sectors, clusters, and so forth. The mapping from logical to physical addresses is done by the file system, and sector-level buffering is done automatically by the disk controller.

When processing records in a disk, the order of access can have a great effect on I/O. Random access processes records in order independent of their logical layout. Sequential access processes records in logical order. C++ provides several mechanisms for manipulating disk files. One of the most commonly is fstream class. The following methods can be used to manipulate file:

- open(char *name, openmode flags): Open file name for processing. Flags control various details such as reading, writing, or both; and whether pre-existing contents should be deleted.
- read(char *buf, int count): Read count bytes from the current position in the file. The current file position moves forward as these are read. The bytes are read into array **buf**, which must be at least **count** bytes long.
- write(char *buf, int count): Write count bytes at the current position in the file (overwriting bytes already at that position). The current file position moves forward as these are written. The bytes to be written from array **buf**.
- seek(int pos): Move the current position in the file to pos. This allows bytes at arbitrary places to be read or. There are actually two “current” positions: one for reading and one for writing. Function **seek** changes the "get" or read position, while function **seek** changes the "put" or write position.
- close(): Close the file at the end of processing.

Note that if this ADT is similar to the “message passing” version of buffer pools described in Section 8.3.

# 8.5 External Sorting

We now consider the problem of sorting records too large to fit in main memory. The records must reside in peripheral or external memory, such sorting methods are called external sorts. In contrast to the internal sorts discussed in Chapter 7 which assume that the records to be sorted are stored in main memory. Sorting large collections of records is central to many applications, such as processing payroll and large databases. When a collection of records is too large to fit in main memory, the only practical way to sort it is to read some records from disk, do some rearranging, then write them back to disk. This process is repeated until the file is sorted, with each record read happens many times. Given the high cost of disk I/O, it should come as
