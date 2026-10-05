block. In particular, the formerly revised buffer-passing ADT does not actually read data in the acquireBuffer readBuffer method. Users who wish to see the old contents must issue a readBlock request to read the data from disk into the buffer, and then a getDataPointer request to gain direct access to the buffer's data contents.

// A single buffer in the buffer pool

```
class Buffer {
public:
    // Read the associated block from disk (if necessary) and
    // return a pointer to the data
    void readBlock() = 0;

    // Return a pointer to the buffer's data array
    // (without reading from disk)
    void +getDataPointer() = 0;

    // Flag the buffer's contents as having changed, so that
    // flushing the buffer will write it back to disk
    void markDirty() = 0;

    // Release the block's access to this buffer. Further
    // accesses to this buffer are illegal.
    void releaseBuffer() = 0;
}
```

// The bufferpool

```
class BufferPool {
public:
    // Constructor: The bufferpool has "numbuff" buffers that
    // each "nuffsize" bytes of data.
    BufferPool(int numbuff, int buffsize) = 0;

    // Relate a block to a buffer, returning a pointer to a
    // buffer object
    Buffer +acquireBuffer(int block) = 0;
}
```

Again, a mode parameter could be added to the acquireBuffer method, eliminating the need for readBlock and markDirty methods.

Clearly, the buffer-passing approach places more obligations on the user of the buffer pool. These obligations include knowing the size of a block, not corrupting the buffer pool's space, and forming the buffer pool when a block has been modified and it is no longer needed. So many obligations make this approach prone to error. An advantage is that there is no need to do an extra step when getting information from the user to the buffer. If the size of the records is large (especially if the record size and buffer size are the same, as is typically the case when implementing B-trees, see Section 10.5), then this efficiency issue might