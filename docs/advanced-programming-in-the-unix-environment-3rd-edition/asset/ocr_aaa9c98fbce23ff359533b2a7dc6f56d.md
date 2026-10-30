# 16.3.3 Address Lookup

Ideally, an application won’t have to be aware of the internal structure of a socket address. If an application simply passes socket addresses around as sockaddr structures and doesn’t rely on any protocol-specific features, then the application will work with many different protocols that provide the same type of service.

Historically, the BSD networking software has provided interfaces to access the various network configuration information. In Section 6.7, we briefly discussed the networking data files and the functions used to access them. In this section, we discuss them in a little more detail and introduce the newer functions used to look up addressing information.

The network configuration information returned by these functions can be kept in a number of places. This information can be kept in static files (e.g., /etc/hosts, /etc/services), or it can be managed by a name service, such as DNS (Domain Name System) or NIS (Network Information Service). Regardless of where the information is kept, the same functions can be used to access it.

The hosts known by a given computer system are found by calling gethostent.

```
#include <netdb.h>

struct hostent *gethostent(void);

Returns: pointer if OK, NULL on error

void sethostent(int stayopen);
void endhostent(void);
```

If the host database file isn’t already open, gethostent will open it. The gethostent function returns the next entry in the file. The sethostent function will open the file or rewind it if it is already open. When the stayopen argument is set to a nonzero value, the file remains open after calling gethostent. The endhostent function can be used to close the file.

When gethostent returns, we get a pointer to a hostent structure, which might point to a static data buffer that is overwritten each time we call gethostent. The hostent structure is defined to have at least the following members:

```
struct hostent {
    char *h_name;          /* name of host */
    char **h_aliases;      /* pointer to alternate host name array */
    int   h_addrtype;      /* address type */
    int   h_length;        /* length in bytes of address */
    char **h_addr_list;    /* pointer to array of network addresses */
    :
};
```

The addresses returned are in network byte order.

Two additional functions—gethostname and gethostbyaddr—originally were included with the hostent functions, but are now considered to be obsolete. They were removed from Version 4 of the Single UNIX Specification. We’ll see replacements for them shortly.