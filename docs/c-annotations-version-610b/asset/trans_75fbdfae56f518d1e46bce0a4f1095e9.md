

### 23.1.2.1 使用单字符缓冲区

当使用一个单字符缓冲区从 streambuf 派生类（例如 IFdStreambuf）时，至少应覆盖其成员 streambuf::underflow，因为该成员最终会接收所有输入请求。成员 streambuf::setg 用于告知 streambuf 基类输入缓冲区的大小和位置，以便它能够相应地设置其输入缓冲区指针。这确保 streambuf::eback、streambuf::gptr 和 streambuf::egptr 返回正确的值。

IFdStreambuf 类的设计如下：

- 其成员函数使用操作文件描述符的低层函数。因此，除了 streambuf，编译器在编译其成员函数之前必须先读取 `<unistd.h>` 头文件。

- 与大多数为输入操作设计的类一样，该类也派生自 std::streambuf。

- 该类定义了两个数据成员，其中一个是固定大小的单字符缓冲区。数据成员被定义为保护数据成员，以便派生类（例如，参见 23.1.2.3 节）可以访问它们。以下是完整的类接口：

    ```cpp
    class IFdStreambuf: public std::streambuf
    {
        protected:
            int     d_fd;
            char    d_buffer[1];
        public:
            IFdStreambuf(int fd);
        private:
            int underflow();
    };
    ```

- 构造函数初始化缓冲区。但是，该初始化将 gptr 的返回值设置为等于 egptr 的返回值。这意味着缓冲区是空的，因此会立即调用 *underflow* 来填充缓冲区：

    ```cpp
    inline IFdStreambuf::IFdStreambuf(int fd)
    :
        d_fd(fd)
    {
        setg(d_buffer, d_buffer + 1, d_buffer + 1);
    }
    ```

- 最后覆盖了 *underflow*。通过从文件描述符读取来重新填充缓冲区。如果失败（无论出于什么原因），则返回 EOF。当然，更复杂的实现可以在此处采取更智能的操作。如果缓冲区能够重新填充，则调用 setg 来正确设置 streambuf 的缓冲区指针：

    ```cpp
    inline int IFdStreambuf::underflow()
    {
        if (read(d_fd, d_buffer, 1) <= 0)
            return EOF;

        setg(d_buffer, d_buffer, d_buffer + 1);
        return *gptr();
    }
    ```

下面的 main 函数演示了如何使用 IFdStreambuf：

```cpp
int main()
{
    IFdStreambuf fds(STDIN_FILENO);
    istream       is(&fds);

    cout << is.rdbuf();
}
```

### 23.1.2.2 使用 n 字符缓冲区

如果我们决定使用一个大小可观的缓冲区，事情会变得多复杂？并不那么复杂。下面的类允许我们指定缓冲区的大小，但除此之外，它与上一节中开发的 `IFdStreambuf` 类基本相同。为了让事情变得更有趣一些，这里开发的 `IFdNStreambuf` 类也覆盖了成员 `streambuf::xsgetn`，以优化读取一系列字符。此外，还提供了一个默认构造函数，可以与 open 成员结合使用，在文件描述符可用之前构造一个 `istream` 对象。在这种情况下，一旦描述符变得可用，就可以使用 open 成员来初始化对象的缓冲区。稍后，在 23.2 节中，我们会遇到这种情况。

为了节省篇幅，没有检查各种调用的成功情况。在‘现实生活’的实现中，这些检查当然不应省略。类 `IFdNStreambuf` 具有以下特点：

- 其成员函数使用操作文件描述符的低层函数。因此，除了 `streambuf`，编译器在编译其成员函数之前必须先读取 `<unistd.h>` 头文件。

- 像往常一样，它派生自 `std::streambuf`。

- 与类 `IFdStreambuf`（23.1.2.1 节）一样，其数据成员是保护的。由于缓冲区的大小是可配置的，该大小保存在一个专门的数据成员 `d_bufsize` 中：

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

- 默认构造函数不分配缓冲区。它可以在文件描述符变为已知之前用来构造对象。第二个构造函数只是将其参数传递给 `open`。然后 `open` 将初始化对象，使其能够真正被使用：

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

- 一旦对象通过 open 初始化，其析构函数将删除对象的缓冲区，并使用文件描述符关闭设备：

    ```cpp
    IFdNStreambuf::~IFdNStreambuf()
    {
        if (d_bufsize)
        {
            close(d_fd);
            delete[] d_buffer;
        }
    }
    ```

尽管在上述实现中设备被关闭，但这并不总是可取的。在打开的文件描述符已经可用的情况下，意图可能是重复使用该描述符，每次都使用一个新构造的 IFdNStreambuf 对象。如何修改这个类，使设备可以选择性地被关闭，这留给读者作为练习。例如，在 Bobcat 库² 中采用了这种方法。

- open 成员只是分配对象的缓冲区。它假定调用程序已经打开了设备。一旦缓冲区被分配，就会使用基类成员 setg 来确保 streambuf::eback、streambuf::gptr 和 streambuf::egptr 返回正确的值：

    ```cpp
    void IFdNStreambuf::open(int fd, size_t bufsize)
    {
        d_fd = fd;
        d_bufsize = bufsize;
        d_buffer = new char[d_bufsize];
        setg(d_buffer, d_buffer + d_bufsize, d_buffer + d_bufsize);
    }
    ```

- 被覆盖的成员 underflow 的实现与 IFdStreambuf（23.1.2.1 节）的成员几乎相同。唯一的区别是当前类支持更大尺寸的缓冲区。因此，可以一次从设备读取更多字符（最多 d_bufsize）：

    ```cpp
    int IFdNStreambuf::underflow()
    {
        if (gptr() < egptr())
            return *gptr();

        int nread = read(d_fd, d_buffer, d_bufsize);

        if (nread <= 0)
            return EOF;

        setg(d_buffer, d_buffer, d_buffer + nread);
        return *gptr();
    }
    ```

- 最后，xsgetn 被覆盖。在一个循环中，n 不断减小直到 0，此时函数终止。或者，如果 underflow 无法获得更多字符，该成员也会返回。该成员优化了字符序列的读取。它不是调用 streambuf::sbumpc n 次，而是将一块可用字符复制到目标位置，并通过一次函数调用使用 streambuf::gbump 消耗缓冲区中的可用字符。

```cpp
std::streamsize IFdNStreambuf::xsgetn(char *dest, std::streamsize n)
{
    int nread = 0;
```

在这种情况下，重置输入缓冲区的参数必须进行调整，使其第二个和第三个参数指向可用输入缓冲区之外。让我们看看 IFdSeek 的特点：

- 如前所述，IFdSeek 派生自 IFdStreambuf。与后一类一样，IFdSeek 的成员函数使用 unistd.h 中声明的设施。因此，在编译器能够编译类的成员函数之前，必须先读取头文件 <unistd.h>。为了减少指定来自 streambuf 和 std::ios 的类型和常量时的输入量，该类定义了几个 typedef。这些 typedef 引用了头文件 <ios> 中定义的类型，因此编译器在编译 IFdSeek 的类接口之前也必须包含该头文件：

    ```cpp
    class IFdSeek: public IFdStreambuf
    {
        typedef std::streambuf::pos_type       pos_type;
        typedef std::streambuf::off_type       off_type;
        typedef std::ios::seekdir              seekdir;
        typedef std::ios::openmode             openmode;

        public:
            IFdSeek(int fd);
        private:
            pos_type seekoff(off_type offset, seekdir dir, openmode);
            pos_type seekpos(pos_type offset, openmode mode);
    };
    ```

- 该类的接口非常简单。它的（唯一）构造函数期望设备的文件描述符。它没有需要执行的特殊任务，只是调用其基类构造函数：

    ```cpp
    inline IFdSeek::IFdSeek(int fd)
    :
        IFdStreambuf(fd)
    {}
    ```

- 成员 seekoff 负责执行实际的 seek 操作。它调用 lseek 在文件描述符已知的设备中寻找新位置。如果 seek 成功，则调用 setg 来定义一个已经为空的缓冲区，以便基类的 underflow 成员在下一个输入请求时重新填充缓冲区。

    ```cpp
    IFdSeek::pos_type IFdSeek::seekoff(off_type off, seekdir dir, openmode)
    {
        pos_type pos =
            lseek
            (
                d_fd, off,
                (dir == std::ios::beg) ? SEEK_SET :
                (dir == std::ios::cur) ? SEEK_CUR :
                                          SEEK_END
            );

        if (pos < 0)
            return -1;

        setg(d_buffer, d_buffer + 1, d_buffer + 1);
        return pos;
    }
    ```

- 最后，伴随函数 seekpos 也被覆盖：它实际上被定义为对 seekoff 的调用：

```cpp
inline IFdSeek::pos_type IFdSeek::seekpos(pos_type off, openmode mode)
```

