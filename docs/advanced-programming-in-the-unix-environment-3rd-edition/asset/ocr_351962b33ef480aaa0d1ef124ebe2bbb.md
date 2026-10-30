```
struct sockaddr_in6 {
    sa_family_t    sin6_family;    /* address family */
    in_port_t      sin6_port;      /* port number */
    uint32_t       sin6_flowinfo;  /* traffic class and flow info */
    struct in6_addr sin6_addr;     /* IPv6 address */
    uint32_t       sin6_scope_id;  /* set of interfaces for scope */
};
```

These are the definitions required by the Single UNIX Specification. Individual implementations are free to add more fields. For example, on Linux, the sockaddr_in structure is defined as

```
struct sockaddr_in {
    sa_family_t    sin_family;  /* address family */
    in_port_t      sin_port;    /* port number */
    struct in_addr sin_addr;    /* IPv4 address */
    unsigned char  sin_zero[8]; /* filler */
};
```

where the sin_zero member is a filler field that should be set to all-zero values.

Note that although the sockaddr_in and sockaddr_in6 structures are quite different, they are both passed to the socket routines cast to a sockaddr structure. In Section 17.2, we will see that the structure of a UNIX domain socket address is different from both of the Internet domain socket address formats.

It is sometimes necessary to print an address in a format that is understandable by a person instead of a computer. The BSD networking software included the inet_addr and inet_ntoa functions to convert between the binary address format and a string in dotted-decimal notation (a.b.c.d). These functions, however, work only with IPv4 addresses. Two new functions—inet_ntop and inet_pton—support similar functionality and work with both IPv4 and IPv6 addresses.

```
#include <arpa/inet.h>

const char *inet_ntop(int domain, const void *restrict addr,
                      char *restrict str, socklen_t size);
    Returns: pointer to address string on success, NULL on error

int inet_pton(int domain, const char *restrict str,
              void *restrict addr);
    Returns: 1 on success, 0 if the format is invalid, or -1 on error
```

The inet_ntop function converts a binary address in network byte order into a text string; inet_pton converts a text string into a binary address in network byte order. Only two domain values are supported: AF_INET and AF_INET6.

For inet_ntop, the size parameter specifies the size of the buffer (str) to hold the text string. Two constants are defined to make our job easier: INET_ADDRSTRLEN is large enough to hold a text string representing an IPv4 address, and INET6_ADDRSTRLEN is large enough to hold a text string representing an IPv6 address. For inet_pton, the addr buffer needs to be large enough to hold a 32-bit address if domain is AF_INET or large enough to hold a 128-bit address if domain is AF_INET6.