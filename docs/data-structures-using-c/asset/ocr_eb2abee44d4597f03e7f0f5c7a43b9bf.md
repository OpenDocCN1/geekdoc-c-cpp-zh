```
PROGRAM CODE 6.30
void Llist :: ~Llist()
{
    Node *temp;
    while(Head != Null)
    {
        temp = Head;
        Head = Head->link;
        delete temp;
    }
}
```

# 6.15 APPLICATION OF LINKED LIST—GARBAGE COLLECTION

Memory is just an array of words. After a series of memory allocations and de-allocations, there are blocks of free memory scattered throughout the available heap space. To be able to reuse this memory, the memory allocator will usually link the freed blocks together in a free list by writing pointers to the next free block in the block itself. An external free list pointer points to the first block in the free list. When a new block of memory is requested, the allocator will generally scan the free list looking for a free block of suitable size and delete it from the free list (relinking the free list around the deleted block).

One of the components of an operating system is the memory management module. This module maintains a list, which consists of unused memory cells. This list very often requires the operations to be performed on the list, such as `insert`, `delete`, and `search` (traversal). Such a list implemented as a linked organization is called the *list of available space*, *free storage list*, or the *free pool*.

Suppose some memory block is freed by the program. The space available can be used for future use. One way to do so is to add the blocks in the free pool. For good memory utilization, the operating system periodically collects all the free blocks and inserts into the free pool. Any technique that does this collection is called *garbage collection*. Garbage collection usually takes place in two phases. First, the process runs through all the lists, tagging those cells, which are currently in use. In the second phase, the process runs through memory, collecting all untagged blocks and inserting the same in free pool. In general, garbage collection takes place when either overflow or underflow occurs. In addition, when the CPU is idle, the garbage collection starts. Note that the garbage collection is invisible to the programmer.

*Overflow* Sometimes, a new data node is to be inserted into data structure, but there is no available space, that is, free pool is empty. This situation is called *overflow*.