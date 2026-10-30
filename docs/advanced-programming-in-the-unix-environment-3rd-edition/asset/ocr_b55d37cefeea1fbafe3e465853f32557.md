```
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

# Figure 17.8 The serv_listen function

First, we create a single UNIX domain socket by calling socket. We then fill in a sockaddr_un structure with the well-known pathname to be assigned to the socket. This structure is the argument to bind. Note that we don't need to set the sun_len field present on some platforms, because the operating system sets this for us, deriving it from the address length we pass to the bind function.

Finally, we call listen (Section 16.4) to tell the kernel that the process will be acting as a server awaiting connections from clients. When a connect request from a client arrives, the server calls the serv_accept function (Figure 17.9).

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