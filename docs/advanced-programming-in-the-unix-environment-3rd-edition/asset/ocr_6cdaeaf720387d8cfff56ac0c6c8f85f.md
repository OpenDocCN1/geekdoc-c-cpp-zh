```
int getrlimit(int resource, struct rlimit *rlptr);
<sys/resource.h>
resource: RLIMIT_CORE, RLIMIT_CPU, RLIMIT_DATA, RLIMIT_FSIZE, RLIMIT_NOFILE, RLIMIT_STACK, RLIMIT_AS (FreeBSD 8.0, Linux 3.2.0, Solaris 10), RLIMIT_MEMLOCK (FreeBSD 8.0, Linux 3.2.0, Mac OS X 10.6.8), RLIMIT_MSGQUEUE (Linux 3.2.0), RLIMIT_NICE (Linux 3.2.0), RLIMIT_NPROC (FreeBSD 8.0, Linux 3.2.0, Mac OS X 10.6.8), RLIMIT_NPTS (FreeBSD 8.0), RLIMIT_RSS (FreeBSD 8.0, Linux 3.2.0, Mac OS X 10.6.8), RLIMIT_SBSIZE (FreeBSD 8.0), RLIMIT_SIGPENDING (Linux 3.2.0), RLIMIT_SWAP (FreeBSD 8.0), RLIMIT_VMEM (Solaris 10)
Returns: 0 if OK, -1 on error
p. 220
```

```
char *gets(char *buf);
<stdio.h>
Returns: buf if OK, NULL on end of file or error
p. 152
```

```
struct servent *getservbyname(const char *name, const char *proto);
<netdb.h>
Returns: pointer if OK, NULL on error
p. 599
```

```
struct servent *getservbyport(int port, const char *proto);
<netdb.h>
Returns: pointer if OK, NULL on error
p. 599
```

```
struct servent *getservent(void);
<netdb.h>
Returns: pointer if OK, NULL on error
p. 599
```

```
pid_t getsid(pid_t pid);
<unistd.h>
Returns: session leader's process group ID if OK, -1 on error
p. 296
```

```
int getsockname(int sockfd, struct sockaddr *restrict addr, socklen_t *restrict alenp);
<sys/socket.h>
Returns: 0 if OK, -1 on error
p. 605
```