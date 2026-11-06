```
    if (write(d_fd, &c, 1) != 1)
        return EOF;
    }
  return c;
}
```

The argument received by `overflow` is either written to the file descriptor (and returned from `overflow`), or `EOF` is returned.

This simple function does not use output buffering. For various reasons, using a buffer is usually a good idea (see also the next section).

When output buffering is used, the `overflow` member is a bit more complex as it is only called when the buffer is full. Once the buffer is full, we *first* have to flush the buffer. Flushing the buffer is the responsibility of the (virtual) function `streambuf::sync`. Since `sync` is a virtual function, classes derived from `streambuf` may redefine `sync` to flush a buffer `streambuf` itself doesn't know about.

Overriding `sync` and using it in `overflow` is not all that has to be done. When the object of the class defining the buffer reaches the end of its lifetime the buffer may be only partially full. In that situation the buffer must also be flushed. This is easily done by simply calling `sync` from the class's destructor.

Now that we've considered the consequences of using an output buffer, we're almost ready to design our derived class. Several more features are added as well, though:

+   - First, we should allow the user of the class to specify the size of the output buffer.
+   - Second, it should be possible to construct an object of our class before the file descriptor is actually known. Later, in section 23.2 we'll encounter a situation where this feature is actually used.

To save some space in the C++ Annotations, the successful completion of the functions designed here is not checked in the example code. In 'real life' implementations these checks should of course not be omitted. Our class `OFdnStreambuf` has the following characteristics:

+   - Its member functions use low-level functions operating on file descriptors. So apart from `streambuf` the `<unistd.h>` header file must have been read by the compiler before its member functions can be compiled.
+   - The class is derived from `std::streambuf`.
+   - It defines three data members. These data members keep track of, respectively, the size of the buffer, the file descriptor, and the buffer itself. Here is the full class interface

```
    class OFdnStreambuf: public std::streambuf
    {
        size_t d_bufsize;
        int    d_fd;
        char  *d_buffer;

      public:
        OFdnStreambuf();
        OFdnStreambuf(int fd, size_t bufsize = 1);
        virtual ~OFdnStreambuf();
        void open(int fd, size_t bufsize = 1);
      private:
        virtual int sync();
        virtual int overflow(int c);
    };
```

+   - Its default constructor merely initializes the buffer to 0. Slightly more interesting is its constructor expecting a file descriptor and a buffer size. This constructor passes its arguments on to the class's `open` member (see below). Here are the constructors: