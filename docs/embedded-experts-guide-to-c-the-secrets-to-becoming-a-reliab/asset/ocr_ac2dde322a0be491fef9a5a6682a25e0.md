```
/* Check the queue is not empty and then read
 * the the next data element. */
if(queue_read_index != queue_write_index)
{
    *p_data = queue_data[queue_read_index];
    queue_read_index =
    (queue_read_index + 1) % QUEUE_SIZE;
    success = true;
}
return success;
}
```

Fig 3.4 - Queues, or FIFOs, are used when data needs to be read in the same order as which it was written (the opposite of a stack).

# Pools

A pool is a memory block of fixed size which may be allocated and freed as required. While this may, at first, appear no different to allocating memory using a call to malloc or a careful implementation can avoid the issues associated with more general methods of allocating memory. Firstly, it is important to note the pools are of a fixed size – therefore, either a pool is available for allocation or it is not; memory fragmentation, although not eliminated, is no longer a problem. The space required for the pools themselves can be statically allocated. Secondly, the overhead of tracking the amount of allocated and free space is significantly reduced, since it is only necessary to know whether a given pool is free, rather than maintaining a complete map of free memory blocks and their size. The problem of dangling pointers, however, remains and is difficult to completely resolve.