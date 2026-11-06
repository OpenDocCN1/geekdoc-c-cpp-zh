```
```cpp
{
    IFdStreambuf fds(STDIN_FILENO);
    istream       is(&fds);

    cout << is.rdbuf();
}
```
```

# 23.1.2.2  Using an n-character buffer

How complex would things get if we decided to use a buffer of substantial size? Not that complex. The following class allows us to specify the size of a buffer, but apart from that it is basically the same class as `IFdStreambuf` developed in the previous section. To make things a bit more interesting, in the class `IFdNStreambuf` developed here, the member `streambuf::xsgetn` is also overridden, to optimize reading a series of characters. Also a default constructor is provided that can be used in combination with the open member to construct an `istream` object before the file descriptor becomes available. In that case, once the descriptor becomes available, the open member can be used to initiate the object’s buffer. Later, in section 23.2, we’ll encounter such a situation.

To save some space, the success of various calls was not checked. In ‘real life’ implementations, these checks should of course not be omitted. The class `IFdNStreambuf` has the following characteristics:

+   - Its member functions use low-level functions operating on file descriptors. So apart from `streambuf` the `<unistd.h>` header file must have been read by the compiler before its member functions can be compiled.

+   - As usual, it is derived from `std::streambuf`.

+   - Like the class `IFdStreambuf` (section 23.1.2.1), its data members are protected. Since the buffer’s size is configurable, this size is kept in a dedicated data member, `d_bufsize`:

```
```cpp
class IFdNStreambuf: public std::streambuf
{
  protected:
    int         d_fd;
    size_t      d_bufsize;
    char*       d_buffer;
  public:
    IFdNStreambuf();
    IFdNStreambuf(int fd, size_t bufsize = 1);
    virtual ~IFdNStreambuf();
    void open(int fd, size_t bufsize = 1);
  private:
    virtual int underflow();
    virtual std::streamsize xsgetn(char *dest, std::streamsize n);
};
```
```

+   - The default constructor does not allocate a buffer. It can be used to construct an object before the file descriptor becomes known. A second constructor simply passes its arguments to `open`. `open` will then initialize the object so that it can actually be used:

```
```cpp
inline IFdNStreambuf::IFdNStreambuf()
:
    d_bufsize(0),
    d_buffer(0)
{}
inline IFdNStreambuf::IFdNStreambuf(int fd, size_t bufsize)
{
    open(fd, bufsize);
}
```
```