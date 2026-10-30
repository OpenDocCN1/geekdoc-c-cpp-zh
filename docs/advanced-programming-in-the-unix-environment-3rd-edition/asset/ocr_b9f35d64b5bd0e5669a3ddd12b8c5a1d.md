number with getservbyname, map a port number to a service name with getservbyport, or scan the services database sequentially with getservent.

```
#include <netdb.h>

struct servent *getservbyname(const char *name, const char *proto);

struct servent *getservbyport(int port, const char *proto);

struct servent *getservent(void);

All return: pointer if OK, NULL on error

void setservent(int stayopen);

void endservent(void);
```

The servent structure is defined to have at least the following members:

```
struct servent {
    char *s_name;      /* service name */
    char **s_aliases;  /* pointer to alternate service name array */
    int s_port;        /* port number */
    char *s_proto;     /* name of protocol */
    ;
};
```

POSIX.1 defines several new functions to allow an application to map from a host name and a service name to an address, and vice versa. These functions replace the older gethostbyname and gethostbyaddr functions.

The getaddrinfo function allows us to map a host name and a service name to an address.

```
#include <sys/socket.h>
#include <netdb.h>

int getaddrinfo(const char *restrict host,
                const char *restrict service,
                const struct addrinfo *restrict hint,
                struct addrinfo **restrict res);

Returns: 0 if OK, nonzero error code on error

void freeaddrinfo(struct addrinfo *ai);
```

We need to provide the host name, the service name, or both. If we provide only one name, the other should be a null pointer. The host name can be either a node name or the host address in dotted-decimal notation.

The getaddrinfo function returns a linked list of addrinfo structures. We can use freeaddrinfo to free one or more of these structures, depending on how many structures are linked together using the ai_next field in the structures.