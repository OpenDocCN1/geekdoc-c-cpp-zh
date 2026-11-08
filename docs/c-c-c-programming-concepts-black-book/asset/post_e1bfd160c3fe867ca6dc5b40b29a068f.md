
**Q4.** Directory.GetAccessControl(dr) returns an object of ------------.
- i. The Security class
- ii. The AccessControl class
- iii. The Directory class
- iv. The DirectorySecurity class

**Q5.** Which of the following is not the namespace used for compression/decompression operation?
- i. ICSharpCode.SharpZipLib.Zip
- ii. ICSharpCode.SharpZipLib.Core
- iii. ICSharpCode.SharpZipLib.Unzip
- iv. ICSharpCode.SharpZipLib.Crc32

**Q6.** StreamUtils is the class that comes under
- i. ICSharpCode.SharpZipLib.Zip
- ii. ICSharpCode.SharpZipLib.Core
- iii. ICSharpCode.SharpZipLib.Unzip
- iv. ICSharpCode.SharpZipLib.Crc32

**Q7.** Isolated storage has
- i. Application and user-specific scope
- ii. Application and machine-specific scope
- iii. Machine and domain-specific scope
- iv. User and assembly-specific scope
- v. User and machine-specific scope

**Q8.** Isolated storage can be used as an alternative of
- i. Text files
- ii. Assembly files
- iii. INI files
- iv. INI, registry, and config files

**Q9.** The IIS embedded server used mostly to transfer an email is
- i. The POP server
- ii. The MIME server
- iii. The SMTP server
- iv. The HTTP server

**Q10.** Namespace used for sending an email is
- i. System.Mail.Net
- ii. System.IO.Net
- iii. System.Net.Mail
- iv. System.Net.Email

![](img/43c5f409f9b17790a628c4b4df854b61_764_0.png)

## 22 An Introduction to Network and Socket Programming

| If you need information on: | See page: |
| --- | --- |
| Socket Address Structure | 724 |
| Generic Socket Address Structures | 725 |
| IPv6 Socket Address Structure | 726 |
| Byte Ordering Functions | 726 |
| Byte Manipulation Functions | 727 |
| Address Conversion Functions | 728 |
| Elementary Socket Functions | 728 |
| Client-Server Implementation in C | 734 |
| I/O Multiplexing | 738 |
| I/O Multiplexing Model | 740 |
| Advanced I/O Handling | 743 |

This chapter mainly focuses on network sockets. A network socket is described as an endpoint of an inter-process communication taking place over a network. A socket is identified with the help of a socket address. A socket address for a Transmission Control Protocol (TCP) connection is defined as the grouping of an Internet Protocol (IP) address and a port. It uniquely identifies every TCP connection on the Internet. This chapter mainly provides the description of different socket Application Programming Interface (API) that uses network sockets. Before describing the socket APIs, let us take a look at the socket structures that are passed to each and every socket API.

### Socket Address Structure

As an argument, a pointer to a socket address structure is required by most socket functions. The socket address structures of the different protocol suites are defined by themselves. The naming convention of these structures starts with sockaddr_ and concludes with a distinct suffix for every protocol suite.

IPv4 socket address structures are identified by the naming convention sockaddr_in, where in stands for Internet socket address. The structure is defined inside the header file `<netinet/in.h>`. Listing 22.1 shows a detailed description of the structure:

**Listing 22.1:** Describing the sockaddr_in structure

```c
struct in_addr {
    in_addr_t   s_addr;                 /* 32-bit IPv4 address network byte ordered */
};

struct sockaddr_in {
    uint8_t     sin_len;                /* length of the structure */
    sa_family_t sin_family;             /* AF_INET */
    in_port_t   sin_port;               /* 16-bit UDP or TCP port number */
    struct in_addr sin_addr;            /* 32-bit IPv4 address network byte ordered */
    char        sin_zero[8];            /* unused */
};
```

With the help of the preceding listing, some important points that are worth mentioning about socket address structures are as follows:

- The socket address structure mentioned in Listing 22.1 conforms to the POSIX.1g standards. The first member of this structure, that is, sin_len, was introduced during the release of 4.3BSD-Reno with the support for Open Systems Interconnection (OSI) protocols. Prior to the release of 4.3BSD-Reno, sin_family was the first member of this structure. The length field is not widely supported across all vendors for socket address structures, although the inclusion of the sin_len field helps in handling variable-length socket address structures.
- Although the sin_len field is present in the structure, it is never set or examined. The field is used within the kernel when routing sockets are used.
- Only the three members, that is, sin_family, sin_addr, and sin_port, of the sockaddr_in structure are required by the POSIX.1g standards. Any POSIX-compliant implementation is free to add its own structure members. For example, most of the implementations add the sin_zero field to their sockaddr_in address structure.
- In Listing 22.1, we have seen the POSIX.1g data types used for the sockaddr_in structure. Table 22.1 provides a description of the data types for the sockaddr_in structure:

Table 22.1: Describing the data types for the sockaddr_in structure

| Datatype | Description | Header |
| --- | --- | --- |
| int8_t | signed 8-bit integer | `<sys/types.h>` |
| uint8_t | unsigned 8-bit integer | `<sys/types.h>` |
| int16_t | signed 16-bit integer | `<sys/types.h>` |
| int32_t | signed 32-bit integer | `<sys/types.h>` |
| uint32_t | unsigned 32-bit integer | `<sys/types.h>` |
| sa_family_t | address family of socket address structure | `<sys/socket.h>` |
| socklen_t | length of socket address structure normally uint32_t | `<sys/socket.h>` |
| in_addr_t | IPv4 address, normally uint32_t | `<netinet/in.h>` |
| in_port_t | TCP or UDP port, normally uint16_t | `<netinet/in.h>` |

- The storing of the IPv4 addresses and the TCP or UDP ports is always in network byte order.
- The IPv4 address stored inside the sockaddr_in structure can be used in two different ways. Let us assume that the server is a variable of Internet socket address structure type. Then we can refer to the IPv4 address of the socket address structure as server.sin_addr. The syntax server.sin_addr refers to the 32-bit IPv4 address as the in_addr structure, whereas the same IPv4 address can be referenced as server.sin_addr.s_addr. In the second scenario, we refer to a 32-bit unsigned integer. We should be referencing the IPv4 address correctly while passing the sockaddr_in structure to functions.
- The sin_zero field of the structure remains unused. By convention, the field is always set to zero.
- The socket address structures are only used on a single host.

### Generic Socket Address Structures

Socket address structures are always passed as a reference to socket functions. The socket functions take pointers to one of the socket structures passed to them as an argument. They must be compatible with socket address structures belonging to any protocol family, which means that we would require a generic address structure which can be used across all protocol families. The generic socket address structure is defined inside the `<sys/socket.h>` header. Listing 22.2 defines a generic socket address structure:

**Listing 22.2:** Describing a generic socket address structure

```c
struct sockaddr {
    uint8_t        sa_len;
    sa_family_t    sa_family;    /* Address family */
    char           sa_data[14];  /* Protocol specific address */
};
```

The socket functions that we would be discussing in this chapter take a pointer to the generic socket address structure. Before passing the argument, explicit type casting is required. Let us take an example of a function called bind whose signature is:

```c
int bind(int, struct sockaddr *, socklen_t);
```

Any call made to the function requires the socket address structures to be cast from a protocol specific to a generic one. For instance:

```c
struct sockaddr_in serverAddress;

bind(sockfd, (struct sockaddr*)&serverAddress, sizeof(serverAddress));
```
