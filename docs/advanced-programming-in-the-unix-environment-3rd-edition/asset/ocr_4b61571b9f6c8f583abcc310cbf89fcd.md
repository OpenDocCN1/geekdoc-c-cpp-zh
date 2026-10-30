```
const char *inet_ntop(int domain, const void *restrict addr, char *restrict str, socklen_t size);
<arpa/inet.h>
Returns: pointer to address string on success, NULL on error
```

```
int inet_pton(int domain, const char *restrict str, void *restrict addr);
<arpa/inet.h>
Returns: 1 on success, 0 if the format is invalid, or -1 on error
```

```
int initgroups(const char *username, gid_t basegid);
<grp.h>    /* Linux & Solaris */
<unistd.h> /* FreeBSD & Mac OS X */
Returns: 0 if OK, -1 on error
```

```
int ioctl(int fd, int request, ...);
<unistd.h>    /* System V */
<sys/ioctl.h> /* BSD and Linux */
Returns: -1 on error, something else if OK
```

```
int isatty(int fd);
<unistd.h>
Returns: 1 (true) if terminal device, 0 (false) otherwise
```

```
int kill(pid_t pid, int signo);
<signal.h>
Returns: 0 if OK, -1 on error
```

```
int lchown(const char *path, uid_t owner, gid_t group);
<unistd.h>
Returns: 0 if OK, -1 on error
```