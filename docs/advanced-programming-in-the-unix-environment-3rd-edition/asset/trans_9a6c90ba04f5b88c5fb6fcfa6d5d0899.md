
oflag参数是一个位掩码，指定主设备的打开方式，类似于`open(2)`中使用的同名参数。然而，并非所有打开标志都受支持。通过`posix_openpt`，我们可以指定`O_RDWR`以读写方式打开主设备，也可以指定`O_NOCTTY`以防止主设备成为调用者的控制终端。所有其他打开标志将导致未定义行为。

在使用从伪终端设备之前，需要设置其权限，使其可被应用程序访问。`grantpt`函数正是完成此事。它将从设备节点的用户ID设置为调用者的真实用户ID，并将节点的组ID设置为未指定的值，通常是对终端设备有访问权限的某个组。权限被设置为允许属主读写，并允许属组写（0620）。

实现通常将从PTY设备的属组设置为`tty`组。需要向系统上所有活动终端写入权限的程序会将组ID（set-group-ID）设置为`tty`组。这类程序的例子有`wall(1)`和`write(1)`。由于从PTY设备启用了组写权限，这些程序可以向其写入。

```
#include <stdlib.h>
int grantpt(int fd);
int unlockpt(int fd);

Both return: 0 on success, -1 on error
```

为了修改从设备节点的权限，`grantpt`可能需要`fork`并`exec`一个set-user-ID程序（例如Solaris上的`/usr/lib/pt_chmod`）。因此，如果调用者正在捕获`SIGCHLD`，其行为是未指定的。

`unlockpt`函数用于授予对从伪终端设备的访问权限，从而允许应用程序打开该设备。通过阻止其他程序打开从设备，设置设备的应用程序有机会在设备可供使用之前正确初始化从设备和主设备。

请注意，在`grantpt`和`unlockpt`中，文件描述符参数都是与主伪终端设备关联的文件描述符。

`ptsname`函数用于在给定主设备文件描述符的情况下，查找从伪终端设备的路径名。这使应用程序能够标识从设备，而不依赖特定平台可能遵循的任何约定。注意，返回的名称可能存储在静态内存中，因此在连续调用时可能会被覆盖。

```
#include <stdlib.h>
char *ptsname(int fd);

Returns: pointer to name of PTY slave if OK, NULL on error
```

图19.8总结了单一UNIX规范中的伪终端函数，并指出本文讨论的平台支持哪些函数。

```
int
pty m_open(char *pts_name, int pts_namesz)
{
    char    *ptr;
    int     fdm, err;

    if ((fdm = posix_openpt(O_RDWR)) < 0)
        return(-1);
    if (grantpt(fdm) < 0)          /* grant access to slave */
        goto errout;
    if (unlockpt(fdm) < 0)         /* clear slave's lock flag */
        goto errout;
    if ((ptr = ptsname(fdm)) == NULL)  /* get slave's name */
        goto errout;

    /*
     * Return name of slave. Null terminate to handle
     * case where strlen(ptr) > pts_namesz.
     */
    strncpy(pts_name, ptr, pts_namesz);
    pts_name[pts_namesz - 1] = '\0';
    return(fdm);                   /* return fd of master */
errout:
    err = errno;
    close(fdm);
    errno = err;
    return(-1);
}

int
ptys_open(char *pts_name)
{
    int fds;
#ifdef SOLARIS
    int err, setup;
#endif

    if ((fds = open(pts_name, O_RDWR)) < 0)
        return(-1);

#ifdef SOLARIS
    /*
     * Check if stream is already set up by autopush facility.
     */
    if ((setup = ioctl(fds, I_FIND, "ldterm")) < 0)
        goto errout;

    if (setup == 0) {
        if (ioctl(fds, I_PUSH, "ptem") < 0)
            goto errout;
        if (ioctl(fds, I_PUSH, "ldterm") < 0)
            goto errout;

```

```
if (ioctl(fds, I_PUSH, "ttcompat") < 0) {
    errout:
        err = errno;
        close(fds);
        errno = err;
        return(-1);
    }
#endif
    return(fds);
}
```

图19.9 伪终端打开函数

`ptym_open`函数使用XSI PTY函数来查找并打开一个未使用的PTY主设备，并初始化相应的PTY从设备。`ptys_open`函数打开从PTY设备。然而，在Solaris系统上，我们可能需要在从PTY设备表现得像终端之前采取额外的步骤。

在Solaris上，打开从设备之后，我们可能需要将从设备的流上推入三个STREAMS模块。伪终端仿真模块（`ptem`）和终端行规程模块（`ldterm`）合在一起表现得像一个真正的终端。`ttcompat`模块为较旧的V7、4BSD和Xenix的`ioctl`调用提供兼容性。它是一个可选模块，但由于网络登录时会自动推入，我们也将其推入从设备的流。

我们可能不需要推入这三个模块的原因在于它们可能已经存在。STREAMS系统支持一种称为autopush的机制，它允许管理员配置一个模块列表，每当打开特定设备时就将这些模块推入流中（更多细节参见Rago [1993]）。我们使用`I_FIND`的`ioctl`命令来查看流上是否已经存在`ldterm`。如果已经存在，我们就假定该流已经由autopush机制配置好，从而避免再次推入这些模块。

Linux、Mac OS X和Solaris遵循历史上的System V行为：如果调用者是一个尚未拥有控制终端的会话首进程，那么`open`调用会把PTY从设备分配为控制终端。如果我们不希望发生这种情况，可以为`open`指定`O_NOCTTY`标志。然而，在FreeBSD上，打开从PTY设备并没有分配设备作为控制终端的副作用。在下一节中，我们将看到在FreeBSD上运行时如何分配控制终端。

## 19.4 pty_fork 函数

现在，我们使用上一节中的两个函数`ptym_open`和`ptys_open`来编写一个新函数，称为`pty_fork`。这个新函数将打开主设备和从设备与`fork`调用结合起来，使子进程成为一个拥有控制终端的会话首进程。

```
#include "apue.h"
#include <termios.h>

pid_t pty_fork(int *ptrfdm, char *slave_name, int slave_namesz,
               const struct termios *slave_termios,
               const struct winsize *slave_winsize);
    Returns: 0 in child, process ID of child in parent, -1 on error
```

PTY主设备的文件描述符通过*ptrfdm*指针返回。

如果*slave_name*非空，从设备的名称将存储在该位置。调用者负责分配该参数所指向的存储空间。

如果指针*slave_termios*非空，系统将使用所引用的结构来初始化从设备的终端行规程。如果该指针为空，系统将从设备的*termios*结构设置为实现定义的初始状态。类似地，如果*slave_winsize*指针非空，所引用的结构将初始化从设备的窗口大小。如果该指针为空，*winsize*结构通常初始化为0。

图19.10显示了该函数的代码。它调用*pty_open*和*ptys_open*函数，能在本文描述的所有四个平台上工作。

打开PTY主设备后，调用*fork*。如前所述，我们希望等到进入子进程并调用*setsid*建立新会话之后再调用*ptys_open*。当子进程调用*setsid*时，它不是进程组组长，因此会发生第9.5节列出的三个步骤：(a) 创建一个新会话，子进程作为会话首进程；(b) 为子进程创建一个新进程组；(c) 子进程失去它可能与先前控制终端存在的任何关联。在Linux、Mac OS X和Solaris下，当调用*ptys_open*时，从设备会成为这个新会话的控制终端。在FreeBSD下，我们必须使用*TIOCSCTTY*的*ioctl*命令来分配控制终端。（回顾图9.8——其他三个平台也支持*TIOCSCTTY*，但我们只在FreeBSD上才需要调用它。）

然后在子进程中初始化*termios*和*winsize*两个结构。最后，从设备文件描述符在子进程中被复制到标准输入、标准输出和标准错误。这意味着调用者从子进程*exec*出的任何进程，其这三个描述符都将连接到从PTY（即其控制终端）。

调用*fork*之后，父进程仅返回PTY主设备描述符和子进程的进程ID。在下一节中，我们将在*pty*程序中使用*pty_fork*函数。

```
#include "apue.h"
#include <termios.h>

pid_t
pty_fork(int *ptrfdm, char *slave_name, int slave_namesz,
         const struct termios *slave_termios,
         const struct winsize *slave_winsize)
{
    int     fdm, fds;
```

