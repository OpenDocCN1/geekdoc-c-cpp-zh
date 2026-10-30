

if ((name = malloc(sizeof(un.sun_path + 1))) == NULL)
    return(-1);
len = sizeof(un);
if ((clifd = accept(listenfd, (struct sockaddr *)&un, &len)) < 0) {
    free(name);
    return(-2);      /* often errno=EINTR, if signal caught */
}
/* obtain the client's uid from its calling address */
len -= offsetof(struct sockaddr_un, sun_path); /* len of pathname */
memcpy(name, un.sun_path, len);
name[len] = 0;      /* null terminate */
if (stat(name, &statbuf) < 0) {
    rval = -3;
    goto errout;
}
#ifdef S_ISSOCK  /* not defined for SVR4 */
if (S_ISSOCK(statbuf.st_mode) == 0) {
    rval = -4;      /* not a socket */
    goto errout;
}
#endif
if (((statbuf.st_mode & (S_IRWXG | S_IRWXO)) ||
    (statbuf.st_mode & S_IRWXU) != S_IRWXU) {
    rval = -5;      /* is not rwx------ */
    goto errout;
}

stale_time = time(NULL) - STALE;
if (statbuf.st_atime < stale_time ||
    statbuf.st_ctime < stale_time ||
    statbuf.st_mtime < stale_time) {
    rval = -6;      /* i-node is too old */
    goto errout;
}

if (uidptr != NULL)
    *uidptr = statbuf.st_uid;  /* return uid of caller */
unlink(name);      /* we're done with pathname now */
free(name);
return(clifd);

errout:
err = errno;
close(clifd);
free(name);
errno = err;
return(rval);
}

服务器在调用 `accept` 时阻塞，等待客户端调用 `cli_conn`。当 `accept` 返回时，其返回值是一个全新的描述符，已连接到客户端。此外，客户端为其套接字分配的路径名（包含客户端进程 ID 的名称）由 `accept` 通过第二个参数返回（指向 `sockaddr_un` 结构的指针）。我们复制此路径名并确保其以空字符结尾（如果路径名占用了 `sockaddr_un` 结构中 `sun_path` 成员的所有可用空间，则没有空间容纳终止的空字节）。然后我们调用 `stat` 来验证路径名确实是一个套接字，并且权限仅允许用户读、用户写和用户执行。我们还验证与套接字关联的三个时间是否不早于 30 秒。 （请回顾第 6.10 节，`time` 函数返回自纪元以来的当前时间和日期，以秒为单位。）

如果所有这些检查都通过，我们就假定客户端的身份（其有效用户 ID）是套接字的拥有者。虽然这种检查并不完美，但这是我们能用当前系统做到的最好方法。 （如果内核能通过 `accept` 的参数将有效用户 ID 返回给我们，那就更好了。）

客户端通过调用 `cli_conn` 函数（图 17.10）来发起与服务器的连接。

```
#include "apue.h"
#include <sys/socket.h>
#include <sys/un.h>
#include <errno.h>

#define CLI_PATH    "/var/tmp/"
#define CLI_PERM    S_IRWXU        /* rwx for user only */

/*
 * Create a client endpoint and connect to a server.
 * Returns fd if all OK, <0 on error.
 */
int
cli_conn(const char *name)
{
    int             fd, len, err, rval;
    struct sockaddr_un un, sun;
    int             do_unlink = 0;

    if (strlen(name) >= sizeof(un.sun_path)) {
        errno = ENAMETOOLONG;
        return(-1);
    }

    /* create a UNIX domain stream socket */
    if ((fd = socket(AF_UNIX, SOCK_STREAM, 0)) < 0)
        return(-1);

    /* fill socket address structure with our address */
    memset(&un, 0, sizeof(un));
    un.sun_family = AF_UNIX;
    sprintf(un.sun_path, "%s%05ld", CLI_PATH, (long)getpid());
```

```
len = offsetof(struct sockaddr_un, sun_path) + strlen(un.sun_path);
 unlink(un.sun_path);          /* in case it already exists */
 if (bind(fd, (struct sockaddr *)&un, len) < 0) {
    rval = -2;
    goto error;
 }
 if (chmod(un.sun_path, CLI_PERM) < 0) {
    rval = -3;
    do_unlink = 1;
    goto error;
 }

 /* fill socket address structure with server's address */
 memset(&sun, 0, sizeof(sun));
 sun.sun_family = AF_UNIX;
 strncpy(sun.sun_path, name);
 len = offsetof(struct sockaddr_un, sun_path) + strlen(name);
 if (connect(fd, (struct sockaddr *)&sun, len) < 0) {
    rval = -4;
    do_unlink = 1;
    goto error;
 }
 return(fd);

 error:
 err = errno;
 close(fd);
 if (do_unlink)
    unlink(un.sun_path);
 errno = err;
 return(rval);
 }
```

## 图 17.10 `cli_conn` 函数

我们调用 `socket` 来创建客户端的 UNIX 域套接字的一端。然后我们用一个客户端特定的名称填充 `sockaddr_un` 结构。

我们不让系统为我们选择默认地址，因为服务器将无法区分一个客户端和另一个客户端（如果我们不显式地将名称绑定到 UNIX 域套接字，内核会代表我们隐式地将其绑定到一个地址，并且不会在文件系统中创建表示该套接字的<|message|>）。相反，我们绑定自己的地址——这是在开发使用套接字的客户端程序时我们通常不会采取的步骤。

我们绑定的路径名的最后五个字符由客户端的进程 ID 组成。我们调用 `unlink`，以防路径名已存在。然后我们调用 `bind` 为客户端的套接字分配一个名称。这会在文件系统中创建一个套接字文件，其名称与绑定的路径名相同。我们调用 `chmod` 关闭除用户读、用户写和用户执行之外的所有权限。在 `serv_accept` 中，服务器检查这些权限和套接字的用户 ID 以验证客户端的身份。

然后我们必须填充另一个 `sockaddr_un` 结构，这次使用服务器的众所周知的路径名。最后，我们调用 `connect` 函数来启动与服务器的连接。

## 17.4 传递文件描述符

在进程之间传递打开的文件描述符是一种强大的技术。它可以带来设计客户端-服务器应用程序的不同方式。它允许一个进程（通常是服务器）完成打开文件所需的一切（涉及将网络名称翻译为网络地址、拨号调制解调器以及为文件协商锁等细节），然后简单地将可用于所有 I/O 函数的描述符返回给调用进程。打开文件或设备所涉及的所有细节都对客户端隐藏。

我们必须更具体地说明我们所说的“从一个进程向另一个进程传递打开的文件描述符”的含义。请回顾图 3.8，其中显示了打开了同一文件的两个进程。虽然它们共享同一个 v-node，但每个进程都有自己的文件表项。

当我们从一个进程向另一个进程传递打开的文件描述符时，我们希望传递进程和接收进程共享同一个文件表项。图 17.11 显示了期望的安排。

从技术上讲，我们是将指向打开文件表项的指针从一个进程传递到另一个进程。此指针被分配给接收进程中的第一个可用描述符。 （说我们传递的是打开的描述符会让人误以为接收进程中的描述符号与发送进程中的相同，而这通常不是真的。）两个进程共享一个打开的文件表，这正是 `fork` 之后发生的情况（请回顾图 8.2）。

通常，当描述符从一个进程传递到另一个进程时，发送进程在传递描述符后会关闭该描述符。发送方关闭描述符实际上并不会关闭文件或设备，因为接收方仍认为该描述符是打开的（即使接收方尚未具体接收该描述符）。

我们定义了本章中使用的以下三个函数来发送和接收文件描述符。稍后在本节中，我们将展示这三个函数的代码。

```
#include "apue.h"

int send_fd(int fd, int fd_to_send);

int send_err(int fd, int status, const char *errmsg);

    Both return: 0 if OK, -1 on error

int recv_fd(int fd, ssize_t (*userfunc)(int, const void *, size_t));

    Returns: file descriptor if OK, negative value on error
```

## 图 17.11 将打开的文件从上层进程传递到底层进程

一个想要向另一个进程传递描述符的进程（通常是服务器）调用 `send_fd` 或 `send_err`。等待接收描述符的进程（客户端）调用 `recv_fd`。

`send_fd` 函数通过 `fd` 表示的 UNIX 域套接字发送描述符 `fd_to_send`。`send_err` 函数通过 `fd` 发送 `errmsg`，随后发送状态字节。`status` 的值必须在 -1 到 -255 范围内。

客户端调用 `recv_fd` 来接收描述符。如果一切正常（发送方调用了 `send_fd`），则非负描述符作为函数的值返回。否则，返回的值是 `send_err` 发送的状态（-1 到 -255 范围内的负值）。此外，如果服务器发送了错误消息，则客户端的 `userfunc` 会被调用来处理该消息。`userfunc` 的第一个参数是常量 `STDFR_FILENO`，随后是指向错误消息的指针及其长度。`userfunc` 的返回值是写入的字节数或出错时的负数。通常，客户端指定普通的 `write` 函数作为 `userfunc`。

我们实现了这些三个函数使用的自己的协议。要发送描述符，`send_fd` 发送两个 0 字节，然后是实际的描述符。要发送错误，`send_err` 发送 `errmsg`，然后是一个 0 字节，然后是状态字节的绝对值（1 到 255）。`recv_fd` 函数读取套接字上的所有内容

![](img/244bf0c3b6d0288ae397336907e37851_676_0.png)

