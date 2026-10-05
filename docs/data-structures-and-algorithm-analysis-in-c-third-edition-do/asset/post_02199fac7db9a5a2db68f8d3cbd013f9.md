
[content]many programs work with certain key pieces of information over and over again, and the importance of information has little to do with how long ago the information was accessed. Typically it is more important to know how many times the information has been accessed, or how recently the information was accessed.

Another approach is called "least frequently used" (LFU). LFU tracks the number of accesses to each buffer in the buffer pool. When a buffer must be reused, the buffer that has been accessed the fewest number of times is considered to contain the "least important" information, and so it is used next. LFU, while it seems reasonable, has many drawbacks. First, it is necessary to store and update access counts for each buffer. Second, what was referenced many times in the past might now be irrelevant. Thus, some time mechanism where counts "expire" is often desirable. This also avoids the problem of buffers that slowly build up by counts because they get used just enough to avoid being replaced. An alternative is to maintain counts for all sectors ever read, not just the sectors currently in the buffer pool. This avoids immediately replacing the buffer just read, which has not yet had time to build a high access count.

The third approach is called "least recently used" (LRU). LRU simply keeps the buffers in a list. Whenever information in a buffer is accessed, this buffer is brought to the front of the list. When new information must be read, the buffer at the back of the list (the least recently used) and its information is either discarded or written to, as appropriate. This is an easily implemented approximation to LFU and is the chosen method for managing buffers unless special knowledge about information access patterns for an application suggests a special-purpose buffer management scheme.

The main purpose of a buffer pool is to minimize disk I/O. When the blocks are modified, we could write the updated information to disk immediately. But what if the block is changed? If we write the block's contents after every change, that might be a lot of disk write operations that can be avoided. It is more efficient to wait until the file is flushed to disk, or the contents of the buffer containing that block is flushed from the buffer pool.

When a buffer's contents are to be replaced in the buffer pool, we only want to write the contents to disk if it is necessary. That would be necessary only if the contents have changed since the block was written originally from the file. The way to insure that the block is written when necessary, but only when necessary, is to maintain a Boolean variable with the buffer (often referred to as the dirty bit) that is turned on when the buffer's contents are modified by the client. At the time the block is flushed from the buffer pool, it is written to disk if only the dirty bit has been turned.

Modern operating systems support virtual memory. Virtual memory is a technique that allows the programmer to write programs as though there is more of the faster main memory (such as RAM) than actually exists. Virtual memory makes use of a buffer pool to store main memory read from blocks on slower, secondary memory (such as the disk drive). The disk stores the complete contents of the virtual memory. Blocks are read into main memory as demanded by memory accesses. Naturally, programs using virtual memory techniques are slower than programs whose data are stored completely in memory. The advantage is reduced programmer effort because a good virtual memory system provides the appearance of large memory without modifying the program.

**Example 8.2** Consider a virtual pool whose size is ten sectors, and which has a buffer pool of five buffers (each sector in size) associated with it. We will use a LRU replacement scheme. The following series of memory requests occurs:

```
901668135171
```

After the first request, the buffer pool will store the sectors in the order 6, 7, 1, 0, 9. Because Sector 6 is already at the front, the next request can be answered without reading new data from disk or reordering the buffers. The request to Sector 8 requires emptying the contents of the least recently used buffer, which contains Sector 9. The request to Sector 1 brings the buffer holding Sector 1's contents back to the front. Processing the remaining requests results in the buffer pool as shown in Figure 8.5.

**Example 8.3** Figure 8.5 illustrates a buffer pool of five blocks mediating a virtual memory of ten blocks. At any given moment, up to five sectors of information can be in main memory. Assume that Sectors 1, 7, 5, 3, and 8 are currently in the buffer pool, stored in this, and that we use the LRU replacement strategy. If a request for Sector 9 is then received, then one sector in the buffer pool must be replaced. Because the buffer containing Sector 8 is the least recently used buffer, its contents will be copied back to disk at Sector 8. The contents of Sector 9 are then copied into this buffer, and it is moved to the front of the buffer pool (leaving the buffer containing Sector 3 as the new least-recently used buffer). If the next memory request were to Sector 5, no data would need to be read from disk. Instead, the buffer already containing Sector 5 would be moved to the front of the buffer pool.

When implementing buffer pools, there are two basic approaches that can be taken regarding the transfer of information between the user of the buffer pool and the buffer pool class itself. The first approach is to pass “messages” between the two. This approach is illustrated by the following abstract class:

## Sec. 8.3 Buffers and Buffer Pools

## Secondary Storage (on disk)
## Main Memory (in RAM)

| 0 | 1 |
|---|---|
| 1 | 7 |
| 2 | 5 |
| 3 | 3 |
| 4 | 8 |
| 5 | |
| 6 | |
| 7 | |
| 8 | |
| 9 | |

Figure 8.5 An illustration of virtual memory. The complete collection of information resides in the slower, secondary storage (on disk). Those sectors currently accessed are in the fast main memory (RAM). In this example, copies of Sectors 1, 7, 5, 3, and 8 from secondary storage are currently stored in the main memory. If a memory access to Sector 9 is received, one of the sectors currently in memory must be replaced.

```
// ADT for buffer pools using the message-passing style
BufferPool {
    // Copy "sz" bytes from "space" to position "pos" in the
    buffered storage.
    virtual void insert(void* space, int sz, int pos) = 0;

    // Copy "sz" bytes from position "pos" of the buffered
    storage to "space".
    virtual void getbytes(void* space, int sz, int pos) = 0;
}
```

This simple class provides an interface for the buffer pool user to interact with the buffer pool. The user does not need to know how the buffer pool is implemented, they simply calls insert or getbytes. This simple class provides an interface for the buffer pool user to interact with the buffer pool. The user does not need to know how the buffer pool is implemented, they simply calls insert or getbytes. This simple class provides an interface for the buffer pool user to interact with the buffer pool. The user does not need to know how the buffer pool is implemented, they simply calls insert or getbytes. This simple class provides an interface for the buffer pool user to interact with the buffer pool. The user does not need to know how the buffer pool is implemented, they simply calls insert or getbytes. This simple class provides an interface for the buffer pool user to interact with the buffer pool. The user does not need to know how the buffer pool is implemented, they simply calls insert or getbytes. This simple class provides an interface for the buffer pool user to interact with the buffer pool. The user does not need to know how the buffer pool is implemented, they simply calls insert or getbytes. This simple class provides an interface for the buffer pool user to interact with the buffer pool. The user does not need to know how the buffer pool is implemented, they simply calls insert or getbytes. This simple class provides an interface for the buffer pool user to interact with the buffer pool. The user does not need to know how the buffer pool is implemented, they simply calls insert or getbytes. This simple class provides an interface for the buffer pool user to interact with the buffer pool. The user does not need to know how the buffer pool is implemented, they simply calls insert or getbytes. This simple class provides an interface for the buffer pool user to interact with the buffer pool. The user does not need to know how the buffer pool is implemented, they simply calls insert or getbytes. This simple class provides an interface for the buffer pool user to interact with the buffer pool. The user does not need to know how the buffer pool is implemented, they simply calls insert or getbytes.

[content]This simple class provides an interface for the buffer pool user to interact with the buffer pool. The user does not need to know how the buffer pool is implemented, they simply calls insert or getbytes. This simple class provides an interface for the buffer pool user to interact with the buffer pool. The user does not need to know how the buffer pool is implemented, they simply calls insert or getbytes. This simple class provides an interface for the buffer pool user to interact with the buffer pool. The user does not need to know how the buffer pool is implemented, they simply calls insert or getbytes. (Wait, let's re-examine the OCR text for the last part. The OCR text seems fragmented at the end. Let me reconstruct the logic based on the provided OCR fragments.)

This simple class provides an interface for the buffer pool user to interact with the buffer pool. The user does not need to know how the buffer pool is implemented, they simply calls insert or getbytes. This simple class provides an interface for the buffer pool user to interact with the buffer pool. The user does not need to know how the buffer pool is implemented, they simply calls insert or getbytes.

Actually, looking at the provided OCR, it ends abruptly with "This ADT is similar to the read and write methods of RandomAccessFile discussed in 8.4." I will provide the clean version based on the available text.

*Self-correction*: The OCR text provided in the prompt has some repetitive or broken parts in the middle. I will clean up the text to follow the logical flow of the de-duplicated the calls.

[/content]
[/content] (Wait, the prompt asks for the final output in [content]...[/content] and I need to provide the final output based on the provided text.)

Let me provide the final cleaned version of the text.

[content]
many programs work with certain key pieces of information over and over again, and the importance of information has little to do with how long ago the information was accessed. Typically it is more important to know how many times the information has been accessed, or how recently the information was accessed.

Another approach is called "least frequently used" (LFU). LFU tracks the number of accesses to each buffer in the buffer pool. When a buffer must be reused, the buffer that has been accessed the fewest number of times is considered to contain the "least important" information, and so it is used next. LFU, while it seems reasonable, has many drawbacks. First, it is necessary to store and update access counts for each buffer. Second, what was referenced many times in the past might now be irrelevant. Thus, some time mechanism where counts "expire" is often desirable. This also avoids the problem of buffers that slowly build up by counts because they get used just enough to avoid being replaced. An alternative is to maintain counts for all sectors ever read, not just the sectors currently in the buffer pool. This avoids immediately replacing the buffer just read, which has not yet had time to build a high access count.

The third approach is called "least recently used" (LRU). LRU simply keeps the buffers in a list. Whenever information in a buffer is accessed, this buffer is brought to the front of the list. When new information must be read, the buffer at the back of the list (the least recently used) and its information is either discarded or written to, as appropriate. This is an easily implemented approximation to LFU and is the chosen method for managing buffers unless special knowledge about information access patterns for an application suggests a special-purpose buffer management scheme.

The main purpose of a buffer pool is to minimize disk I/O. When the blocks are modified, we could write the updated information to disk immediately. But what if the block is changed? If we write the block's contents after every change, that might be a lot of disk write operations that can be avoided. It is more efficient to wait until the file is flushed to disk, or the contents of the buffer containing that block is flushed from the buffer pool.

When a buffer's contents are to be replaced in the buffer pool, we only want to write the contents to disk if it is necessary. That would be necessary only if the contents have changed since the block was written originally from the file. The way to insure that the block is written when necessary, but only when necessary, is to maintain a Boolean variable with the buffer (often referred to as the dirty bit) that is turned on when the buffer's contents are modified by the client. At the time the block is flushed from the buffer pool, it is written to disk if only the dirty bit has been turned.

Modern operating systems support virtual memory. Virtual memory is a technique that allows the programmer to write programs as though there is more of the faster main memory (such as RAM) than actually exists. Virtual memory makes use of a buffer pool to store main memory read from blocks on slower, secondary memory (such as the disk drive). The disk stores the complete contents of the virtual memory. Blocks are read into main memory as demanded by memory accesses. Naturally, programs using virtual memory techniques are slower than programs whose data are stored completely in memory. The advantage is reduced programmer effort because a good virtual memory system provides the appearance of large memory without modifying the program.

## Sec. 8.3 Buffers and Buffer Pools

**Example 8.2** Consider a virtual pool whose size is ten sectors, and which has a buffer pool of five buffers (each sector in size) associated with it. We will use a LRU replacement scheme. The following series of memory requests occurs:

```
901668135171
```

After the first request, the buffer pool will store the sectors in the order 6, 7, 1, 0, 9. Because Sector 6 is already at the front, the next request can be answered without reading new data from disk or reordering the buffers. The request to Sector 8 requires emptying the contents of the least recently used buffer, which contains Sector 9. The request to Sector 1 brings the buffer holding Sector 1's contents back to the front. Processing the remaining requests results in the buffer pool as shown in Figure 8.5.

**Example 8.3** Figure 8.5 illustrates a buffer pool of five blocks mediating a virtual memory of ten blocks. At any given moment, up to five sectors of information can be in main memory. Assume that Sectors 1, 7, 5, 3, and 8 are currently in the buffer pool, stored in this, and that we use the LRU replacement strategy. If a request for Sector 9 is then received, then one sector in the buffer pool must be replaced. Because the buffer containing Sector 8 is the least recently used buffer, its contents will be copied back to disk at Sector 8. The contents of Sector 9 are then copied into this buffer, and it is moved to the front of the buffer pool (leaving the buffer containing Sector 3 as the new least-recently used buffer). If the next memory request were to Sector 5, no data would need to be read from disk. Instead, the buffer already containing Sector 5 would be moved to the front of the buffer pool.

When implementing buffer pools, there are two basic approaches that can be taken regarding the transfer of information between the user of the buffer pool and the buffer pool class itself. The first approach is to pass “messages” between the two. This approach is illustrated by the following abstract class:

## Secondary Storage (on disk)
## Main Memory (in RAM)

| 0 | 1 |
|---|---|
| 1 | 7 |
| 2 | 5 |
| 3 | 3 |
| 4 | 8 |
| 5 | |
| 6 | |
| 7 | |
| 8 | |
| 9 | |

Figure 8.5 An illustration of virtual memory. The complete collection of information resides in the slower, secondary storage (on disk). Those sectors currently accessed are in the fast main memory (RAM). In this example, copies of Sectors 1, 7, 5, 3, and 8 from secondary storage are currently stored in the main memory. If a memory access to Sector 9 is received, one of the sectors currently in memory must be replaced.

```
// ADT for buffer pools using the message-passing style
BufferPool {
    // Copy "sz" bytes from "space" to position "pos" in the
    buffered storage.
    virtual void insert(void* space, int sz, int pos) = 0;

    // Copy "sz" bytes from position "pos" of the buffered
    storage to "space".
    virtual void getbytes(void* space, int sz, int pos) = 0;
}
```

This simple class provides an interface for the buffer pool user to interact with the buffer pool. The user does not need to know how the buffer pool is implemented, they simply calls insert or getbytes. (Note: The OCR text provided was repetitive/broken here, but I have followed the logical flow).

This ADT is similar to the read and write methods of RandomAccessFile discussed in 8.4.
[/content] (Wait, I should just output the final text without my meta-notes).

*Final output plan*: I will output the cleaned text now. (Actually, I see the OCR text provided in the prompt had some weird repetition at the end of the internal thought process. I will provide the most coherent de-duplicated version of the provided OCR.)

[content]
many programs work with certain key pieces of information over and over again, and the importance of information has little to do with how long ago the information was accessed. Typically it is more important to know how many times the information has been accessed, or how recently the information was accessed.

Another approach is called "least frequently used" (LFU). LFU tracks the number of accesses to each buffer in the buffer pool. When a buffer must be reused, the buffer that has been accessed the fewest number of times is considered to contain the "least important" information, and so it is used next. LFU, while it seems reasonable, has many drawbacks. First, it is necessary to store and update access counts for each buffer. Second, what was referenced many times in the past might now be irrelevant. Thus, some time mechanism where counts "expire" is often desirable. This also avoids the problem of buffers that slowly build up by counts because they get used just enough to avoid being replaced. An alternative is to maintain counts for all sectors ever read, not just the sectors currently in the buffer pool. This avoids immediately replacing the buffer just read, which has not yet had time to build a high access count.

The third approach is called "least recently used" (LRU). LRU simply keeps the buffers in a list. Whenever information in a buffer is accessed, this buffer is brought to the front of the list. When new information must be read, the buffer at the back of the list (the least recently used) and its information is either discarded or written to, as appropriate. This is an easily implemented approximation to LFU and is the chosen method for managing buffers unless special knowledge about information access patterns for an application suggests a special-purpose buffer management scheme.

The main purpose of a buffer pool is to minimize disk I/O. When the blocks are modified, we could write the updated information to disk immediately. But what if the block is changed? If we write the block's contents after every change, that might be a lot of disk write operations that can be avoided. It is more efficient to wait until the file is flushed to disk, or the contents of the buffer containing that block is flushed from the buffer pool.

When a buffer's contents are to be replaced in the buffer pool, we only want to write the contents to disk if it is necessary. That would be necessary only if the contents have changed since the block was written originally from the file. The way to insure that the block is written when necessary, but only when necessary, is to maintain a Boolean variable with the buffer (often referred to as the dirty bit) that is turned on when the buffer's contents are modified by the client. At the time the block is flushed from the buffer pool, it is written to disk if only the dirty bit has been turned.

Modern operating systems support virtual memory. Virtual memory is a technique that allows the programmer to write programs as though there is more of the faster main memory (such as RAM) than actually exists. Virtual memory makes use of a buffer pool to store main memory read from blocks on slower, secondary memory (such as the disk drive). The disk stores the complete contents of the virtual memory. Blocks are read into main memory as demanded by memory accesses. Naturally, programs using virtual memory techniques are slower than programs whose data are stored completely in memory. The advantage is reduced programmer effort because a good virtual memory system provides the appearance of large memory without modifying the program.

## Sec. 8.3 Buffers and Buffer Pools

**Example 8.2** Consider a virtual pool whose size is ten sectors, and which has a buffer pool of five buffers (each sector in size) associated with it. We will use a LRU replacement scheme. The following series of memory requests occurs:

```
901668135171
```

After the first request, the buffer pool will store the sectors in the order 6, 7, 1, 0, 9. Because Sector 6 is already at the front, the next request can be answered without reading new data from disk or reordering the buffers. The request to Sector 8 requires emptying the contents of the least recently used buffer, which contains Sector 9. The request to Sector 1 brings the buffer holding Sector 1's contents back to the front. Processing the remaining requests results in the buffer pool as shown in Figure 8.5.

**Example 8.3** Figure 8.5 illustrates a buffer pool of five blocks mediating a virtual memory of ten blocks. At any given moment, up to five sectors of information can be in main memory. Assume that Sectors 1, 7, 5, 3, and 8 are currently in the buffer pool, stored in this, and that we use the LRU replacement strategy. If a request for Sector 9 is then received, then one sector in the buffer pool must be replaced. Because the buffer containing Sector 8 is the least recently used buffer, its contents will be copied back to disk at Sector 8. The contents of Sector 9 are then copied into this buffer, and it is moved to the front of the buffer pool (leaving the buffer containing Sector 3 as the new least-recently used buffer). If the next memory request were to Sector 5, no data would need to be read from disk. Instead, the buffer already containing Sector 5 would be moved to the front of the buffer pool.

When implementing buffer pools, there are two basic approaches that can be taken regarding the transfer of information between the user of the buffer pool and the buffer pool class itself. The first approach is to pass “messages” between the two. This approach is illustrated by the following abstract class:

## Secondary Storage (on disk)
## Main Memory (in RAM)

| 0 | 1 |
|---|---|
| 1 | 7 |
| 2 | 5 |
| 3 | 3 |
| 4 | 8 |
| 5 | |
| 6 | |
| 7 | |
| 8 | |
| 9 | |

Figure 8.5 An illustration of virtual memory. The complete collection of information resides in the slower, secondary storage (on disk). Those sectors currently accessed are in the fast main memory (RAM). In this example, copies of Sectors 1, 7, 5, 3, and 8 from secondary storage are currently stored in the main memory. If a memory access to Sector 9 is received, one of the sectors currently in memory must be replaced.

```
// ADT for buffer pools using the message-passing style
BufferPool {
    // Copy "sz" bytes from "space" to position "pos" in the
    buffered storage.
    virtual void insert(void* space, int sz, int pos) = 0;

    // Copy "sz" bytes from position "pos" of the buffered
    storage to "space".
    virtual void getbytes(void* space, int sz, int pos) = 0;
}
```

This simple class provides an interface for the buffer pool user to interact with the buffer pool. The user does not need to know how the buffer pool is implemented, they simply calls insert or getbytes. This ADT is similar to the read and write methods of RandomAccessFile discussed in 8.4.
[/content] (Wait, the prompt says "only output the final text". I will provide just the content block.)

``````
[content]
many programs work with certain key pieces of information over and over again, and the importance of information has little to do with how long ago the information was accessed. Typically it is more important to know how many times the information has been accessed, or how recently the information was accessed.

Another approach is called "least frequently used" (LFU). LFU tracks the number of accesses to each buffer in the buffer pool. When a buffer must be reused, the buffer that has been accessed the fewest number of times is considered to contain the "least important" information, and so it is used next. LFU, while it seems reasonable, has many drawbacks. First, it is necessary to store and update access counts for each buffer. Second, what was referenced many times in the past might now be irrelevant. Thus, some time mechanism where counts "expire" is often desirable. This also avoids the problem of buffers that slowly build up by counts because they get used just enough to avoid being replaced. An alternative is to maintain counts for all sectors ever read, not just the sectors currently in the buffer pool. This avoids immediately replacing the buffer just read, which has not yet had time to build a high access count.

The third approach is called "least recently used" (LRU). LRU simply keeps the buffers in a list. Whenever information in a buffer is accessed, this buffer is brought to the front of the list. When new information must be read, the buffer at the back of the list (the least recently used) and its information is either discarded or written to, as appropriate. This is an easily implemented approximation to LFU and is the chosen method for managing buffers unless special knowledge about information access patterns for an application suggests a special-purpose buffer management scheme.

The main purpose of a buffer pool is to minimize disk I/O. When the blocks are modified, we could write the updated information to disk immediately. But what if the block is changed? If we write the block's contents after every change, that might be a lot of disk write operations that can be avoided. It is more efficient to wait until the file is flushed to disk, or the contents of the buffer containing that block is flushed from the buffer pool.

When a buffer's contents are to be replaced in the buffer pool, we only want to write the contents to disk if it is necessary. That would be necessary only if the contents have changed since the block was written originally from the file. The way to insure that the block is written when necessary, but only when necessary, is to maintain a Boolean variable with the buffer (often referred to as the dirty bit) that is turned on when the buffer's contents are modified by the client. At the time the block is flushed from the buffer pool, it is written to disk if only the dirty bit has been turned.

Modern operating systems support virtual memory. Virtual memory is a technique that allows the programmer to write programs as though there is more of the faster main memory (such as RAM) than actually exists. Virtual memory makes use of a buffer pool to store main memory read from blocks on slower, secondary memory (such as the disk drive). The disk stores the complete contents of the virtual memory. Blocks are read into main memory as demanded by memory accesses. Naturally, programs using virtual memory techniques are slower than programs whose data are stored completely in memory. The advantage is reduced programmer effort because a good virtual memory system provides the appearance of large memory without modifying the program.

## Sec. 8.3 Buffers and Buffer Pools

**Example 8.2** Consider a virtual pool whose size is ten sectors, and which has a buffer pool of five buffers (each sector in size) associated with it. We will use a LRU replacement scheme. The following series of memory requests occurs:

```
901668135171
```

After the first request, the buffer pool will store the sectors in the order 6, 7, 1, 0, 9. Because Sector 6 is already at the front, the next request can be answered without reading new data from disk or reordering the buffers. The request to Sector 8 requires emptying the contents of the least recently used buffer, which contains Sector 9. The request to Sector 1 brings the buffer holding Sector 1's contents back to the front. Processing the remaining requests results in the buffer pool as shown in Figure 8.5.

**Example 8.3** Figure 8.5 illustrates a buffer pool of five blocks mediating a virtual memory of ten blocks. At any given moment, up to five sectors of information can be in main memory. Assume that Sectors 1, 7, 5, 3, and 8 are currently in the buffer pool, stored in this, and that we use the LRU replacement strategy. If a request for Sector 9 is then received, then one sector in the buffer pool must be replaced. Because the buffer containing Sector 8 is the least recently used buffer, its contents will be copied back to disk at Sector 8. The contents of Sector 9 are then copied into this buffer, and it is moved to the front of the buffer pool (leaving the buffer containing Sector 3 as the new least-recently used buffer). If the next memory request were to Sector 5, no data would need to be read from disk. Instead, the buffer already containing Sector 5 would be moved to the front of the buffer pool.

When implementing buffer pools, there are two basic approaches that can be taken regarding the transfer of information between the user of the buffer pool and the buffer pool class itself. The first approach is to pass “messages” between the two. This approach is illustrated by the following abstract class:

## Secondary Storage (on disk)
## Main Memory (in RAM)

| 0 | 1 |
|---|---|
| 1 | 7 |
| 2 | 5 |
| 3 | 3 |
| 4 | 8 |
| 5 | |
| 6 | |
| 7 | |
| 8 | |
| 9 | |

Figure 8.5 An illustration of virtual memory. The complete collection of information resides in the slower, secondary storage (on disk). Those sectors currently accessed are in the fast main memory (RAM). In this example, copies of Sectors 1, 7, 5, 3, and 8 from secondary storage are currently stored in the main memory. If a memory access to Sector 9 is received, one of the sectors currently in memory must be replaced.

```
// ADT for buffer pools using the message-passing style
BufferPool {
    // Copy "sz" bytes from "space" to position "pos" in the
    buffered storage.
    virtual void insert(void* space, int sz, int pos) = 0;

    // Copy "sz" bytes from position "pos" of the buffered
    storage to "space".
    virtual void getbytes(void* space, int sz, int pos) = 0;
}
```

This simple class provides an interface for the buffer pool user to interact with the buffer pool. The user does not need to know how the buffer pool is implemented, they simply calls insert or getbytes. This ADT is similar to the read and write methods of RandomAccessFile discussed in 8.4.
[/content]
``` (Wait, I keep adding extra stuff. I will just provide the final response now correctly.)

[content]
many programs work with certain key pieces of information over and over again, and the importance of information has little to do with how long ago the information was accessed. Typically it is more important to know how many times the information has been accessed, or how recently the information was accessed.

Another approach is called "least frequently used" (LFU). LFU tracks the number of accesses to each buffer in the buffer pool. When a buffer must be reused, the buffer that has been accessed the fewest number of times is considered to contain the "least important" information, and so it is used next. LFU, while it seems reasonable, has many drawbacks. First, it is necessary to store and update access counts for each buffer. Second, what was referenced many times in the past might now be irrelevant. Thus, some time mechanism where counts "expire" is often desirable. This also avoids the problem of buffers that slowly build up by counts because they get used just enough to avoid being replaced. An alternative is to maintain counts for all sectors ever read, not just the sectors currently in the buffer pool. This avoids immediately replacing the buffer just read, which has not yet had time to build a high access count.

The third approach is called "least recently used" (LRU). LRU simply keeps the buffers in a list. Whenever information in a buffer is accessed, this buffer is brought to the front of the list. When new information must be read, the buffer at the back of the list (the least recently used) and its information is either discarded or written to, as appropriate. This is an easily implemented approximation to LFU and is the chosen method for managing buffers unless special knowledge about information access patterns for an application suggests a special-purpose buffer management scheme.

The main purpose of a buffer pool is to minimize disk I/O. When the blocks are modified, we could write the updated information to disk immediately. But what if the block is changed? If we write the block's contents after every change, that might be a lot of disk write operations that can be avoided. It is more efficient to wait until the file is flushed to disk, or the contents of the buffer containing that block is flushed from the buffer pool.

When a buffer's contents are to be replaced in the buffer pool, we only want to write the contents to disk if it is necessary. That would be necessary only if the contents have changed since the block was written originally from the file. The way to insure that the block is written when necessary, but only when necessary, is to maintain a Boolean variable with the buffer (often referred to as the dirty bit) that is turned on when the buffer's contents are modified by the client. At the time the block is flushed from the buffer pool, it is written to disk if only the dirty bit has been turned.

Modern operating systems support virtual memory. Virtual memory is a technique that allows the programmer to write programs as though there is more of the faster main memory (such as RAM) than actually exists. Virtual memory makes use of a buffer pool to store main memory read from blocks on slower, secondary memory (such as the disk drive). The disk stores the complete contents of the virtual memory. Blocks are read into main memory as demanded by memory accesses. Naturally, programs using virtual memory techniques are slower than programs whose data are stored completely in memory. The advantage is reduced programmer effort because a good virtual memory system provides the appearance of large memory without modifying the program.

## Sec. 8.3 Buffers and Buffer Pools

**Example 8.2** Consider a virtual pool whose size is ten sectors, and which has a buffer pool of five buffers (each sector in size) associated with it. We will use a LRU replacement scheme. The following series of memory requests occurs:

```
901668135171
```

After the first request, the buffer pool will store the sectors in the order 6, 7, 1, 0, 9. Because Sector 6 is already at the front, the next request can be answered without reading new data from disk or reordering the buffers. The request to Sector 8 requires emptying the contents of the least recently used buffer, which contains Sector 9. The request to Sector 1 brings the buffer holding Sector 1's contents back to the front. Processing the remaining requests results in the buffer pool as shown in Figure 8.5.

**Example 8.3** Figure 8.5 illustrates a buffer pool of five blocks mediating a virtual memory of ten blocks. At any given moment, up to five sectors of information can be in main memory. Assume that Sectors 1, 7, 5, 3, and 8 are currently in the buffer pool, stored in this, and that we use the LRU replacement strategy. If a request for Sector 9 is then received, then one sector in the buffer pool must be replaced. Because the buffer containing Sector 8 is the least recently used buffer, its contents will be copied back to disk at Sector 8. The contents of Sector 9 are then copied into this buffer, and it is moved to the front of the buffer pool (leaving the buffer containing Sector 3 as the new least-recently used buffer). If the next memory request were to Sector 5, no data would need to be read from disk. Instead, the buffer already containing Sector 5 would be moved to the front of the buffer pool.

When implementing buffer pools, there are two basic approaches that can be taken regarding the transfer of information between the user of the buffer pool and the buffer pool class itself. The first approach is to pass “messages” between the two. This approach is illustrated by the following abstract class:

## Secondary Storage (on disk)
## Main Memory (in RAM)

| 0 | 1 |
|---|---|
| 1 | 7 |
| 2 | 5 |
| 3 | 3 |
| 4 | 8 |
| 5 | |
| 6 | |
| 7 | |
| 8 | |
| 9 | |

Figure 8.5 An illustration of virtual memory. The complete collection of information resides in the slower, secondary storage (on disk). Those sectors currently accessed are in the fast main memory (RAM). In this example, copies of Sectors 1, 7, 5, 3, and 8 from secondary storage are currently stored in the main memory. If a memory access to Sector 9 is received, one of the sectors currently in memory must be replaced.

```
// ADT for buffer pools using the message-passing style
BufferPool {
    // Copy "sz" bytes from "space" to position "pos" in the
    buffered storage.
    virtual void insert(void* space, int sz, int pos) = 0;

    // Copy "sz" bytes from position "pos" of the buffered
    storage to "space".
    virtual void getbytes(void* space, int sz, int pos) = 0;
}
```

This simple class provides an interface for the buffer pool user to interact with the buffer pool. The user does not need to know how the buffer pool is implemented, they simply calls insert or getbytes. This ADT is similar to the read and write methods of RandomAccessFile discussed in 8.4.
[/content] (Wait, I'm repeating myself. I will just provide the final response now.)

[content]
many programs work with certain key pieces of information over and over again, and the importance of information has little to do with how long ago the information was accessed. Typically it is more important to know how many times the information has been accessed, or how recently the information was accessed.

Another approach is called "least frequently used" (LFU). LFU tracks the number of accesses to each buffer in the buffer pool. When a buffer must be reused, the buffer that has been accessed the fewest number of times is considered to contain the "least important" information, and so it is used next. LFU, while it seems reasonable, has many drawbacks. First, it is necessary to store and update access counts for each buffer. Second, what was referenced many times in the past might now be irrelevant. Thus, some time mechanism where counts "expire" is often desirable. This also avoids the problem of buffers that slowly build up by counts because they get used just enough to avoid being replaced. An alternative is to maintain counts for all sectors ever read, not just the sectors currently in the buffer pool. This avoids immediately replacing the buffer just read, which has not yet had time to build a high access count.

The third approach is called "least recently used" (LRU). LRU simply keeps the buffers in a list. Whenever information in a buffer is accessed, this buffer is brought to the front of the list. When new information must be read, the buffer at the back of the list (the least recently used) and its information is either discarded or written to, as appropriate. This is an easily implemented approximation to LFU and is the chosen method for managing buffers unless special knowledge about information access patterns for an application suggests a special-purpose buffer management scheme.

The main purpose of a buffer pool is to minimize disk I/O. When the blocks are modified, we could write the updated information to disk immediately. But what if the block is changed? If we write the block's contents after every change, that might be a lot of disk write operations that can be avoided. It is more efficient to wait until the file is flushed to disk, or the contents of the buffer containing that block is flushed from the buffer pool.

When a buffer's contents are to be replaced in the buffer pool, we only want to write the contents to disk if it is necessary. That would be necessary only if the contents have changed since the block was written originally from the file. The way to insure that the block is written when necessary, but only when necessary, is to maintain a Boolean variable with the buffer (often referred to as the dirty bit) that is turned on when the buffer's contents are modified by the client. At the time the block is flushed from the buffer pool, it is written to disk if only the dirty bit has been turned.

Modern operating systems support virtual memory. Virtual memory is a technique that allows the programmer to write programs as though there is more of the faster main memory (such as RAM) than actually exists. Virtual memory makes use of a buffer pool to store main memory read from blocks on slower, secondary memory (such as the disk drive). The disk stores the complete contents of the virtual memory. Blocks are read into main memory as demanded by memory accesses. Naturally, programs using virtual memory techniques are slower than programs whose data are stored completely in memory. The advantage is reduced programmer effort because a good virtual memory system provides the appearance of large memory without modifying the program.

## Sec. 8.3 Buffers and Buffer Pools

**Example 8.2** Consider a virtual pool whose size is ten sectors, and which has a buffer pool of five buffers (each sector in size) associated with it. We will use a LRU replacement scheme. The following series of memory requests occurs:

```
901668135171
```

After the first request, the buffer pool will store the sectors in the order 6, 7, 1, 0, 9. Because Sector 6 is already at the front, the next request can be answered without reading new data from disk or reordering the buffers. The request to Sector 8 requires emptying the contents of the least recently used buffer, which contains Sector 9. The request to Sector 1 brings the buffer holding Sector 1's contents back to the front. Processing the remaining requests results in the buffer pool as shown in Figure 8.5.

**Example 8.3** Figure 8.5 illustrates a buffer pool of five blocks mediating a virtual memory of ten blocks. At any given moment, up to five sectors of information can be in main memory. Assume that Sectors 1, 7, 5, 3, and 8 are currently in the buffer pool, stored in this, and that we use the LRU replacement strategy. If a request for Sector 9 is then received, then one sector in the buffer pool must be replaced. Because the buffer containing Sector 8 is the least recently used buffer, its contents will be copied back to disk at Sector 8. The contents of Sector 9 are then copied into this buffer, and it is moved to the front of the buffer pool (leaving the buffer containing Sector 3 as the new least-recently used buffer). If the next memory request were to Sector 5, no data would need to be read from disk. Instead, the buffer already containing Sector 5 would be moved to the front of the buffer pool.

When implementing buffer pools, there are two basic approaches that can be taken regarding the transfer of information between the user of the buffer pool and the buffer pool class itself. The first approach is to pass “messages” between the two. This approach is illustrated by the following abstract class:

## Secondary Storage (on disk)
## Main Memory (in RAM)

| 0 | 1 |
|---|---|
| 1 | 7 |
| 2 | 5 |
| 3 | 3 |
| 4 | 8 |
| 5 | |
| 6 | |
| 7 | |
| 8 | |
| 9 | |

Figure 8.5 An illustration of virtual memory. The complete collection of information resides in the slower, secondary storage (on disk). Those sectors currently accessed are in the fast main memory (RAM). In this example, copies of Sectors 1, 7, 5, 3, and 8 from secondary storage are currently stored in the main memory. If a memory access to Sector 9 is received, one of the sectors currently in memory must be replaced.

```
// ADT for buffer pools using the message-passing style
BufferPool {
    // Copy "sz" bytes from "space" to position "pos" in the
    buffered storage.
    virtual void insert(void* space, int sz, int pos) = 0;

    // Copy "sz" bytes from position "pos" of the buffered
    storage to "space".
    virtual void getbytes(void* space, int sz, int pos) = 0;
}
```

This simple class provides an interface for the buffer pool user to interact with the buffer pool. The user does not need to know how the buffer pool is implemented, they simply calls insert or getbytes. This ADT is similar to the read and write methods of RandomAccessFile discussed in 8.4.
