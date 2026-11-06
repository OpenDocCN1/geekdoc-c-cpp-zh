size:

```
```cpp
class FdUnget: public std::streambuf
{
    int       d_fd;
    size_t    d_bufsize;
    size_t    d_reserved;
    char      *d_buffer;
    char      *d_base;
public:
    FdUnget(int fd, size_t bufsz, size_t unget);
    virtual ~FdUnget();
private:
    int underflow();
};
```
```

+   - The class’s constructor expects a file descriptor, a buffer size and the number of characters that can be ungot or pushed back as its arguments. This number determines the size of a reserved area, defined as the first d_reserved bytes of the class’s input buffer.

+   - The input buffer will always be at least one byte larger than d_reserved. So, a certain number of bytes may be read. Once d_reserved bytes have been read at most d_reserved bytes can be ungot.
+   - Next, the starting point for reading operations is configured. It is called d_base, pointing to a location d_reserved bytes beyond the location represented by d_buffer. This is always the location where buffer refills start.
+   - Now that the buffer has been constructed, we’re ready to define streambuf’s buffer pointers using setg. As no characters have been read yet, all pointers are set to point to d_base. If unget is called at this point, no characters are available, and unget (correctly) fails.
+   - Eventually, the refill buffer’s size is determined as the number of allocated bytes minus the size of the reserved area.

Here is the class’s constructor:

```
```cpp
FdUnget::FdUnget(int fd, size_t bufsz, size_t unget)
:
    d_fd(fd),
    d_reserved(unget)
{
    size_t allocate =
            bufsz > d_reserved ?
                    bufsz
                    :
                    d_reserved + 1;

    d_buffer = new char[allocate];

    d_base = d_buffer + d_reserved;
    setg(d_base, d_base, d_base);

    d_bufsize = allocate - d_reserved;
}
```
```

+   - The class’s destructor simply returns the memory allocated for the buffer to the common pool:

```
```cpp
inline FdUnget::~FdUnget()
{
    delete[] d_buffer;
}
```
```