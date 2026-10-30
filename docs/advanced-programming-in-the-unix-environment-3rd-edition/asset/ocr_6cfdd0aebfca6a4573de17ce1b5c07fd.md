```
void *realloc(void *ptr, size_t newsize);
<stdlib.h>
Returns: non-null pointer if OK, NULL on error
```

```
ssize_t recv(int sockfd, void *buf, size_t nbytes, int flags);
<sys/socket.h>
flags: MSG_PEEK, MSG_OOB, MSG_WAITALL
MSG_CMSG_CLOEXEC (Linux 3.2.0),
MSG_DONTWAIT (FreeBSD 8.0, Linux 3.2.0,
Solaris 10),
MSG_ERRQUEUE (Linux 3.2.0),
MSG_TRUNC (Linux 3.2.0)
Returns: length of message in bytes, 0 if no messages are available and peer has done an orderly shutdown, or -1 on error
```

```
ssize_t recvfrom(int sockfd, void *restrict buf, size_t len, int flags, struct sockaddr *restrict addr, socklen_t *restrict addrlen);
<sys/socket.h>
flags: MSG_PEEK, MSG_OOB, MSG_WAITALL
MSG_CMSG_CLOEXEC (Linux 3.2.0),
MSG_DONTWAIT (FreeBSD 8.0, Linux 3.2.0,
Solaris 10),
MSG_ERRQUEUE (Linux 3.2.0),
MSG_TRUNC (Linux 3.2.0)
Returns: length of message in bytes, 0 if no messages are available and peer has done an orderly shutdown, or -1 on error
```

```
ssize_t recvmsg(int sockfd, struct msghdr *msg, int flags);
<sys/socket.h>
flags: MSG_PEEK, MSG_OOB, MSG_WAITALL
MSG_CMSG_CLOEXEC (Linux 3.2.0),
MSG_DONTWAIT (FreeBSD 8.0, Linux 3.2.0,
Solaris 10),
MSG_ERRQUEUE (Linux 3.2.0),
MSG_TRUNC (Linux 3.2.0)
Returns: length of message in bytes, 0 if no messages are available and peer has done an orderly shutdown, or -1 on error
```

```
int remove(const char *path);
<stdio.h>
Returns: 0 if OK, -1 on error
```

```
int rename(const char *oldname, const char *newname);
<stddio.h>
Returns: 0 if OK, -1 on error
```