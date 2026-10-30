We can get network names and numbers with a similar set of interfaces.

```
#include <netdb.h>

struct netent *getnetbyaddr(uint32_t net, int type);
struct netent *getnetbyname(const char *name);
struct netent *getnetent(void);

All return: pointer if OK, NULL on error

void setnetent(int stayopen);
void endnetent(void);
```

The netent structure contains at least the following fields:

```
struct netent {
    char      *n_name;      /* network name */
    char      **n_aliases;  /* alternate network name array pointer */
    int        n_addrtype;  /* address type */
    uint32_t   n_net;       /* network number */
    :
};
```

The network number is returned in network byte order. The address type is one of the address family constants (AF_INET, for example).

We can map between protocol names and numbers with the following functions.

```
#include <netdb.h>

struct protoent *getprotobyname(const char *name);
struct protoent *getprotobynumber(int proto);
struct protoent *getprotoent(void);

All return: pointer if OK, NULL on error

void setprotoent(int stayopen);
void endprotoent(void);
```

The protoent structure as defined by POSIX.1 has at least the following members:

```
struct protoent {
    char    *p_name;    /* protocol name */
    char    **p_aliases; /* pointer to alternate protocol name array */
    int      p_proto;   /* protocol number */
    :
};
```

Services are represented by the port number portion of the address. Each service is offered on a unique, well-known port number. We can map a service name to a port