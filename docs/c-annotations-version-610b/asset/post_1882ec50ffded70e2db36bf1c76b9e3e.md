
## Chapter 23: Concrete Examples

In this chapter concrete examples of C++ programs, classes and templates are presented. Topics covered by the C++ Annotations such as virtual functions, static members, etc. are illustrated in this chapter. The examples roughly follow the organization of earlier chapters.

As an additional topic, not just providing examples of C++ the subjects of scanner and parser generators are covered. We show how these tools may be used in C++ programs. These additional examples assume a certain familiarity with the concepts underlying these tools, like grammars, parse-trees and parse-tree decoration. Once the input for a program exceeds a certain level of complexity, it's attractive to use scanner- and parser-generators to create the code doing the actual input processing. One of the examples in this chapter describes the usage of these tools in a C++ environment.

### 23.1 Using file descriptors with `streambuf` classes

#### 23.1.1 Classes for output operations

Reading and writing from and to *file descriptors* are not part of the C++ standard. But on most operating systems *file descriptors* are available and can be considered a device. It seems natural to use the class `std::streambuf` as the starting point for constructing classes interfacing such file descriptor devices.

Below we’ll construct classes that can be used to write to a device given its file descriptor. The devices may be files, but they could also be pipes or sockets. Section 23.1.2 covers reading from such devices; section 23.2.3 reconsiders redirection, discussed earlier in section 6.6.1.

Using the streambuf class as a base class it is relatively easy to design classes for output operations. The only member function that must be overridden is the (virtual) member `int streambuf::overflow(int c)`. This member’s responsibility is to write characters to the device. If fd is an output file descriptor and if output should not be buffered then the member `overflow()` can simply be implemented as:

```cpp
class UnbufferedFD: public std::streambuf
{
    public:
        virtual int overflow(int c);
        ...
};

int UnbufferedFD::overflow(int c)
{
    if (c != EOF)
    {
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

- First, we should allow the user of the class to specify the size of the output buffer.
- Second, it should be possible to construct an object of our class before the file descriptor is actually known. Later, in section 23.2 we'll encounter a situation where this feature is actually used.

To save some space in the C++ Annotations, the successful completion of the functions designed here is not checked in the example code. In 'real life' implementations these checks should of course not be omitted. Our class `OFdStreambuf` has the following characteristics:

- Its member functions use low-level functions operating on file descriptors. So apart from `streambuf` the `<unistd.h>` header file must have been read by the compiler before its member functions can be compiled.
- The class is derived from `std::streambuf`.
- It defines three data members. These data members keep track of, respectively, the size of the buffer, the file descriptor, and the buffer itself. Here is the full class interface

```cpp
class OFdStreambuf: public std::streambuf
{
    size_t d_bufsize;
    int    d_fd;
    char  *d_buffer;

  public:
    OFdStreambuf();
    OFdStreambuf(int fd, size_t bufsize = 1);
    virtual ~OFdStreambuf();
    void open(int fd, size_t bufsize = 1);
  private:
    virtual int sync();
    virtual int overflow(int c);
};
```

- Its default constructor merely initializes the buffer to 0. Slightly more interesting is its constructor expecting a file descriptor and a buffer size. This constructor passes its arguments on to the class's `open` member (see below). Here are the constructors:

```cpp
inline OFdStreambuf::OFdStreambuf()
:
    d_bufsize(0),
    d_buffer(0)
{}
inline OFdStreambuf::OFdStreambuf(int fd, size_t bufsize)
{
    open(fd, bufsize);
}
```

- The destructor calls `sync`, flushing any characters stored in the output buffer to the device. In implementations not using a buffer the destructor can be given a default implementation:

```cpp
inline OFdStreambuf::~OFdStreambuf()
{
    if (d_buffer)
    {
        sync();
        delete[] d_buffer;
    }
}
```

This implementation does not close the device. It is left as an exercise to the reader to change this class in such a way that the device is optionally closed (or optionally remains open). This approach was adopted by, e.g. the Bobcat library⁴. See also section 23.1.2.

- The `open` member initializes the buffer. Using `streambuf::setp`, the begin and end points of the buffer are defined. This is used by the `streambuf` base class to initialize `streambuf::pbase`, `streambuf::pptr`, and `streambuf::epptr`:

```cpp
inline void OFdStreambuf::open(int fd, size_t bufsize)
{
    d_fd = fd;
    d_bufsize = bufsize == 0 ? 1 : bufsize;

    d_buffer = new char[d_bufsize];
    setp(d_buffer, d_buffer + d_bufsize);
}
```

- The member `sync` flushes the as yet unflushed contents of the buffer to the device. After the flush the buffer is reinitialized using `setp`. After successfully flushing the buffer `sync` returns 0:

```cpp
inline int OFdStreambuf::sync()
{
    if (pptr() > pbase())
    {
        write(d_fd, d_buffer, pptr() - pbase());
        setp(d_buffer, d_buffer + d_bufsize);
    }
    return 0;
}
```

- The member `streambuf::overflow` is also overridden. Since this member is called from the `streambuf` base class when the buffer is full it should first call `sync` to flush the buffer to the device. Next it should write the character `c` to the (now empty) buffer. The character `c` should be written using `pptr` and `streambuf::pbump`. Entering a character into the buffer should be implemented using available `streambuf` member functions, rather than 'by hand' as doing so might invalidate `streambuf`'s internal bookkeeping. Here is `overflow`'s implementation:

```cpp
inline int OFdStreambuf::overflow(int c)
{
        sync();
        if (c != EOF)
        {
                *pptr() = c;
                pbump(1);
        }
        return c;
}
```

The next program uses the OFdStreambuf class to copy its standard input to file descriptor STDOUT_FILENO, which is the symbolic name of the file descriptor used for the standard output:

```cpp
#include <string>
#include <iostream>
#include <istream>
#include "fdout.h"
using namespace std;

int main(int argc, char **argv)
{
        OFdStreambuf   fds(STDOUT_FILENO, 500);
        ostream        os(&fds);

        switch (argc)
        {
                case 1:
                        for (string s; getline(cin, s); )
                                os << s << '\n';
                        os << "COPIED cin LINE BY LINE\n";
                        break;

                case 2:
                        cin >> os.rdbuf();          // Alternatively, use: cin >> &fds;
                        os << "COPIED cin BY EXTRACTING TO os.rdbuf()\n";
                        break;

                case 3:
                        os << cin.rdbuf();
                        os << "COPIED cin BY INSERTING cin.rdbuf() into os\n";
                        break;
        }
}
```

#### 23.1.2 Classes for input operations

When classes for input operation are derived from std::streambuf, they should be provided with an input buffer of at least one character. The one-character input buffer allows for the use of the member functions istream::putback or istream::ungetc. Strictly speaking it is not necessary to implement a buffer in classes derived from streambuf. But using buffers in these classes is strongly advised. Their implementation is very simple and straightforward and the applicability of such classes is greatly improved. Therefore, all our classes derived from the class streambuf define a buffer of at least one character.

⁴http://bobcat.sourceforge.net
