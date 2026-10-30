We can set a socket option with the setsockopt function.

```
#include <sys/socket.h>
int setsockopt(int sockfd, int level, int option, const void *val,
    socklen_t len);
Returns: 0 if OK, -1 on error
```

The level argument identifies the protocol to which the option applies. If the option is a generic socket-level option, then level is set to SOL_SOCKET. Otherwise, level is set to the number of the protocol that controls the option. Examples are IPPROTO_TCP for TCP options and IPPROTO_IP for IP options. Figure 16.21 summarizes the generic socket-level options defined by the Single UNIX Specification.

| Option | Type of val argument | Description |
|---|---|---|
| SO_ACCEPTCONN | int | Return whether a socket is enabled for listening (getsockopt only). |
| SO_BROADCAST | int | Broadcast datagrams if *val is nonzero. |
| SO_DEBUG | int | Debugging in network drivers enabled if *val is nonzero. |
| SO_DONTROUTE | int | Bypass normal routing if *val is nonzero. |
| SO_ERROR | int | Return and clear pending socket error (getsockopt only). |
| SO_KEEPALIVE | int | Periodic keep-alive messages enabled if *val is nonzero. |
| SO_LINGER | struct linger | Delay time when unsent messages exist and socket is closed. |
| SO_OOBINLINE | int | Out-of-band data placed inline with normal data if *val is nonzero. |
| SO_RCVBUF | int | The size in bytes of the receive buffer. |
| SO_RCVLOWAT | int | The minimum amount of data in bytes to return on a receive call. |
| SO_RCVTIMEO | struct timeval | The timeout value for a socket receive call. |
| SO_REUSEADDR | int | Reuse addresses in bind if *val is nonzero. |
| SO_SNDBUF | int | The size in bytes of the send buffer. |
| SO_SNDLOWAT | int | The minimum amount of data in bytes to transmit in a send call. |
| SO_SNDTIMEO | struct timeval | The timeout value for a socket send call. |
| SO_TYPE | int | Identify the socket type (getsockopt only). |

Figure 16.21 Socket options

The val argument points to a data structure or an integer, depending on the option. Some options are on/off switches. If the integer is nonzero, then the option is enabled. If the integer is zero, then the option is disabled. The len argument specifies the size of the object to which val points.
We can find out the current value of an option with the getsockopt function.

```
#include <sys/socket.h>
int getsockopt(int sockfd, int level, int option, void *restrict val,
    socklen_t *restrict lenp);
Returns: 0 if OK, -1 on error
```