

## 17.2.1 命名UNIX域套接字

尽管`socketpair`函数创建的套接字彼此连接，但各个套接字并没有名字。这意味着它们无法被无关进程寻址。

在16.3.4节中，我们学习了如何将地址绑定到Internet域套接字。与Internet域套接字一样，UNIX域套接字也可以被命名并用于通告服务。然而，UNIX域套接字使用的地址格式与Internet域套接字使用的地址格式不同。

回忆一下16.3节，套接字地址格式因实现而异。UNIX域套接字的地址由`sockaddr_un`结构表示。在Linux 3.2.0和Solaris 10上，`sockaddr_un`结构在头文件`<sys/un.h>`中定义如下：

```
struct sockaddr_un {
    sa_family_t sun_family;    /* AF_UNIX */
    char        sun_path[108]; /* pathname */
};
```

然而，在FreeBSD 8.0和Mac OS X 10.6.8上，`sockaddr_un`结构定义为：

```
struct sockaddr_un {
    unsigned char sun_len;     /* sockaddr length */
    sa_family_t   sun_family;  /* AF_UNIX */
    char          sun_path[104]; /* pathname */
};
```

`sockaddr_un`结构的`sun_path`成员包含一个路径名。当我们将地址绑定到UNIX域套接字时，系统会创建一个同名的`S_IFSOCK`类型文件。

该文件仅用作向客户端通告套接字名称的手段。应用程序不能打开该文件，也不能用它进行通信。

如果我们尝试绑定同一地址时，该文件已经存在，则绑定请求将失败。当我们关闭套接字时，该文件不会自动删除，因此我们需要确保在应用程序退出前将其unlink。

### 示例

图17.5中的程序展示了将地址绑定到UNIX域套接字的示例。

```
#include "apue.h"
#include <sys/socket.h>
#include <sys/un.h>

int
main(void)
{
    int fd, size;
    struct sockaddr_un un;
    un.sun_family = AF_UNIX;
    strncpy(un.sun_path, "foo.socket");
    if ((fd = socket(AF_UNIX, SOCK_STREAM, 0)) < 0)
      err_sys("socket failed");
    size = offsetof(struct sockaddr_un, sun_path) + strlen(un.sun_path);
    if (bind(fd, (struct sockaddr *)&un, size) < 0)
      err_sys("bind failed");
    printf("UNIX domain socket bound\n");
    exit(0);
}
```

### 图17.5 将地址绑定到UNIX域套接字

当我们运行这个程序时，绑定请求成功。然而，如果我们第二次运行程序，会得到一个错误，因为该文件已存在。只有删除该文件后，程序才能再次成功运行。

```
$ ./a.out                          run the program
UNIX domain socket bound
$ ls -l foo.socket                  look at the socket file
srwxr-xr-x 1 sar        0 May 18 00:44 foo.socket
$ ./a.out                           try to run the program again
bind failed: Address already in use
$ rm foo.socket                     remove the socket file
$ ./a.out                           run the program a third time
UNIX domain socket bound            now it succeeds
```

我们确定要绑定的地址大小的方法是：计算`sockaddr_un`结构中`sun_path`成员的偏移量，再加上路径名的长度（不包括结尾的空字节）。由于不同实现中，`sockaddr_un`结构中位于`sun_path`之前的成员各不相同，我们使用`<stddef.h>`（由`apue.h`包含）中的`offsetof`宏来计算`sun_path`成员相对于结构体起始位置的偏移量。如果你查看`<stddef.h>`，会看到类似下面的定义：

```
#define offsetof(TYPE, MEMBER)  ((int)&((TYPE *)0)->MEMBER)
```

该表达式计算得到一个整数，即该成员的起始地址，其中假设结构体从地址0开始。

## 17.3 唯一连接

服务器可以使用标准的`bind`、`listen`和`accept`函数为客户端安排唯一的UNIX域连接。客户端使用`connect`联系服务器；在服务器接受连接请求后，客户端与服务器之间就存在一条唯一连接。这种操作方式与我们在图16.16和图16.17中展示的Internet域套接字的方式相同。

![](img/244bf0c3b6d0288ae397336907e37851_669_0.png)

### 图17.6 连接前的客户端和服务器套接字

图17.6展示了在两者之间存在连接之前的客户端进程和服务器进程。服务器已将其套接字绑定到一个`sockaddr_un`地址，并且正在监听连接请求。图17.7展示了在服务器接受客户端的连接请求后，客户端与服务器之间的唯一连接。

![](img/244bf0c3b6d0288ae397336907e37851_669_1.png)

### 图17.7 连接后的客户端和服务器套接字

现在我们将开发三个函数，用于在同一台机器上运行的无关进程之间创建唯一连接。这些函数模仿了16.4节中讨论的面向连接的套接字函数。这里我们使用UNIX域套接字作为底层通信机制。

```
#include "apue.h"

int serv_listen(const char *name);

Returns: file descriptor to listen on if OK, negative value on error

int serv_accept(int listenfd, uid_t *uidptr);

Returns: new file descriptor if OK, negative value on error

int cli_conn(const char *name);

Returns: file descriptor if OK, negative value on error
```

`serv_listen`函数（图17.8）可供服务器使用，以通告其愿意在一个众所周知的名字（文件系统中的某个路径名）上监听客户端的连接请求。当客户端想要连接到服务器时，将使用这个名字。返回值是服务器用于接收客户端连接请求的UNIX域套接字。

`serv_accept`函数（图17.9）供服务器使用，用于等待客户端的连接请求到达。当请求到达时，系统会自动创建一个新的UNIX域套接字，将其连接到客户端的套接字，并将新套接字返回给服务器。此外，客户端的有效用户ID会存储到`uidptr`指向的内存中。

客户端调用`cli_conn`（图17.10）来连接到服务器。客户端指定的`name`参数必须与服务器调用`serv_listen`通告的名字相同。返回时，客户端获得一个连接到服务器的文件描述符。

### 图17.8 serv_listen函数

```
#include "apue.h"
#include <sys/socket.h>
#include <sys/un.h>
#include <errno.h>

#define QLEN 10

/*
 * Create a server endpoint of a connection.
 * Returns fd if all OK, <0 on error.
 */
int
serv_listen(const char *name)
{
    int                 fd, len, err, rval;
    struct sockaddr_un  un;

    if (strlen(name) >= sizeof(un.sun_path)) {
        errno = ENAMETOOLONG;
        return(-1);
    }

    /* create a UNIX domain stream socket */
    if ((fd = socket(AF_UNIX, SOCK_STREAM, 0)) < 0)
        return(-2);

    unlink(name);  /* in case it already exists */

    /* fill in socket address structure */
    memset(&un, 0, sizeof(un));
    un.sun_family = AF_UNIX;
    strcpy(un.sun_path, name);
    len = offsetof(struct sockaddr_un, sun_path) + strlen(name);

    /* bind the name to the descriptor */
    if (bind(fd, (struct sockaddr *)&un, len) < 0) {
        rval = -3;
        goto err out;
    }
    if (listen(fd, QLEN) < 0) { /* tell kernel we're a server */
        rval = -4;
        goto err out;
    }
    return(fd);
err out:
    err = errno;
    close(fd);
    errno = err;
    return(rval);
}
```

首先，我们通过调用`socket`创建一个UNIX域套接字。然后，我们用要赋给该套接字的众所周知路径名填充`sockaddr_un`结构。该结构是`bind`的参数。注意，我们不需要设置某些平台上存在的`sun_len`字段，因为操作系统会根据我们传递给`bind`函数的地址长度为我们设置该字段。

最后，我们调用`listen`（16.4节）告诉内核，该进程将充当服务器，等待来自客户端的连接。当客户端的连接请求到达时，服务器会调用`serv_accept`函数（图17.9）。

```
#include "apue.h"
#include <sys/socket.h>
#include <sys/un.h>
#include <time.h>
#include <errno.h>

#define STALE 30 /* client's name can't be older than this (sec) */
/*
 * Wait for a client connection to arrive, and accept it.
 * We also obtain the client's user ID from the pathname
 * that it must bind before calling us.
 * Returns new fd if all OK, <0 on error
 */
int
serv_accept(int listenfd, uid_t *uidptr)
{
    int clifd, err, rval;
    socklen_t len;
    time_t statetime;
    struct sockaddr_un un;
    struct stat statbuf;
    char *name;

    /* allocate enough space for longest name plus terminating null */
```

