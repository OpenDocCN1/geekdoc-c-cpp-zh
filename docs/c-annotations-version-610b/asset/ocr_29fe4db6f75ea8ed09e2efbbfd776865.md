```
inline OFdnStreambuf::OFdnStreambuf()
:
    d_bufsize(0),
    d_buffer(0)
{}
inline OFdnStreambuf::OFdnStreambuf(int fd, size_t bufsize)
{
    open(fd, bufsize);
}
```

+   - The destructor calls `sync`, flushing any characters stored in the output buffer to the device. In implementations not using a buffer the destructor can be given a default implementation:

```
inline OFdnStreambuf::~OFdnStreambuf()
{
    if (d_buffer)
    {
        sync();
        delete[] d_buffer;
    }
}
```

This implementation does not close the device. It is left as an exercise to the reader to change this class in such a way that the device is optionally closed (or optionally remains open). This approach was adopted by, e.g. the Bobcat library⁴. See also section 23.1.2.

+   - The `open` member initializes the buffer. Using `streambuf::setp`, the begin and end points of the buffer are defined. This is used by the `streambuf` base class to initialize `streambuf::pbase`, `streambuf::pptr`, and `streambuf::epptr`:

```
inline void OFdnStreambuf::open(int fd, size_t bufsize)
{
    d_fd = fd;
    d_bufsize = bufsize == 0 ? 1 : bufsize;

    d_buffer = new char[d_bufsize];
    setp(d_buffer, d_buffer + d_bufsize);
}
```

+   - The member `sync` flushes the as yet unflushed contents of the buffer to the device. After the flush the buffer is reinitialized using `setp`. After successfully flushing the buffer `sync` returns 0:

```
inline int OFdnStreambuf::sync()
{
    if (pptr() > pbase())
    {
        write(d_fd, d_buffer, pptr() - pbase());
        setp(d_buffer, d_buffer + d_bufsize);
    }
    return 0;
}
```

+   - The member `streambuf::overflow` is also overridden. Since this member is called from the `streambuf` base class when the buffer is full it should first call `sync` to flush the buffer to the device. Next it should write the character `c` to the (now empty) buffer. The character `c` should be written using `pptr` and `streambuf::pbump`. Entering a character into the buffer should be implemented using available `streambuf` member functions, rather than 'by hand' as doing so might invalidate `streambuf`'s internal bookkeeping. Here is `overflow`'s implementation:

```
inline int OFdnStreambuf::overflow(int c)
```

⁴http://bobcat.sourceforge.net