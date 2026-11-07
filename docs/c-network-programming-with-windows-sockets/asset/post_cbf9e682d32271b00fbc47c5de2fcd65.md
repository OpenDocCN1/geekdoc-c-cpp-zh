
```c
#define PF_PUP        AF_PUP
#define PF_CHAOS      AF_CHAOS
#define PF_NS         AF_NS
#define PF_IPX        AF_IPX
#define PF_ISO        AF_ISO
#define PF_OSI        AF_OSI
#define PF_ECMA       AF_ECMA
#define PF_DATAKIT    AF_DATAKIT
#define PF_CCITT      AF_CCITT
#define PF_SNA        AF_SNA
#define PF_DECnet     AF_DECnet
#define PF_DLI        AF_DLI
#define PF_LAT        AF_LAT
#define PF_HYLINK     AF_HYLINK
#define PF_APPLETALK  AF_APPLETALK

#define PF_MAX        AF_MAX

/*
 * Structure used for manipulating linger option.
 */
struct linger {
    u_short l_onoff;                 /* option on/off */
    u_short l_linger;                /* linger time */
};

/*
 * Level number for (get/set)sockopt() to apply to socket itself.
 */
#define SOL_SOCKET    0xffff         /* options for socket level */

/*
 * Maximum queue length specifiable by listen.
 */
#define SOMAXCONN     5

#define MSG_OOB       0x1            /* process out-of-band data */
#define MSG_PEEK      0x2            /* peek at incoming message */
#define MSG_DONTROUTE 0x4            /* send without using routing tables */

#define MSG_MAXIOVLEN 16

#define MSG_PARTIAL   0x8000         /* partial send or recv for message xport */

/*
 * Define constant based on rfc883, used by gethostbyxxx() calls.
 */
#define MAXGETHOSTSTRUCT         1024

/*
 * Define flags to be used with the WSAAsyncSelect() call.
 */
#define FD_READ       0x01
#define FD_WRITE      0x02
#define FD_OOB        0x04
#define FD_ACCEPT     0x08
#define FD_CONNECT    0x10
#define FD_CLOSE          0x20

/*
 * All Windows Sockets error constants are biased by WSABASEERR from
 * the "normal"
 */
#define WSABASEERR        10000
/*
 * Windows Sockets definitions of regular Microsoft C error constants
 */
#define WSAEINTR          (WSABASEERR+4)
#define WSAEBADF          (WSABASEERR+9)
#define WSAEACCES         (WSABASEERR+13)
#define WSAEFAULT         (WSABASEERR+14)
#define WSAEINVAL         (WSABASEERR+22)
#define WSAEMFILE         (WSABASEERR+24)

/*
 * Windows Sockets definitions of regular Berkeley error constants
 */
#define WSAEWOULDBLOCK    (WSABASEERR+35)
#define WSAEINPROGRESS    (WSABASEERR+36)
#define WSAEALREADY       (WSABASEERR+37)
#define WSAENOTSOCK       (WSABASEERR+38)
#define WSAEDESTADDRREQ   (WSABASEERR+39)
#define WSAEMSGSIZE       (WSABASEERR+40)
#define WSAEPROTOTYPE     (WSABASEERR+41)
#define WSAENOPROTOOPT    (WSABASEERR+42)
#define WSAEPROTONOSUPPORT (WSABASEERR+43)
#define WSAESOCKTNOSUPPORT (WSABASEERR+44)
#define WSAEOPNOTSUPP     (WSABASEERR+45)
#define WSAEPFNOSUPPORT   (WSABASEERR+46)
#define WSAEAFNOSUPPORT   (WSABASEERR+47)
#define WSAEADDRINUSE     (WSABASEERR+48)
#define WSAEADDRNOTAVAIL  (WSABASEERR+49)
#define WSAENETDOWN       (WSABASEERR+50)
#define WSAENETUNREACH    (WSABASEERR+51)
#define WSAENETRESET      (WSABASEERR+52)
#define WSAECONNABORTED   (WSABASEERR+53)
#define WSAECONNRESET     (WSABASEERR+54)
#define WSAENOBUFS        (WSABASEERR+55)
#define WSAEISCONN        (WSABASEERR+56)
#define WSAENOTCONN       (WSABASEERR+57)
#define WSAESHUTDOWN      (WSABASEERR+58)
#define WSAETOOMANYREFS   (WSABASEERR+59)
#define WSAETIMEDOUT      (WSABASEERR+60)
#define WSAECONNREFUSED   (WSABASEERR+61)
#define WSAELOOP          (WSABASEERR+62)
#define WSAENAMETOOLONG   (WSABASEERR+63)
#define WSAEHOSTDOWN      (WSABASEERR+64)
#define WSAEHOSTUNREACH   (WSABASEERR+65)
#define WSAENOTEMPTY      (WSABASEERR+66)
#define WSAEPROCLIM       (WSABASEERR+67)
#define WSAEUSERS         (WSABASEERR+68)
#define WSAEDQUOT         (WSABASEERR+69)
#define WSAESTALE         (WSABASEERR+70)
#define WSAEREMOTE        (WSABASEERR+71)
#define WSAEDISCON                  (WSABASEERR+101)

/*
 * Extended Windows Sockets error constant definitions
 */
#define WSASYSNOTREADY              (WSABASEERR+91)
#define WSAVERNOTSUPPORTED           (WSABASEERR+92)
#define WSANOTINITIALISED            (WSABASEERR+93)

/*
 * Error return codes from gethostbyname() and gethostbyaddr()
 * (when using the resolver). Note that these errors are
 * retrieved via WSAGetLastError() and must therefore follow
 * the rules for avoiding clashes with error numbers from
 * specific implementations or language run-time systems.
 * For this reason the codes are based at WSABASEERR+100.
 * Note also that [WSA]NO_ADDRESS is defined only for
 * compatibility purposes.
 */
#define h_errno                     WSAGetLastError()

/* Authoritative Answer: Host not found */
#define WSAHOST_NOT_FOUND           (WSABASEERR+1001)
#define HOST_NOT_FOUND              WSAHOST_NOT_FOUND

/* Non-Authoritative: Host not found, or SERVERFAIL */
#define WSATRY_AGAIN                (WSABASEERR+1002)
#define TRY_AGAIN                   WSATRY_AGAIN

/* Non recoverable errors, FORMERR, REFUSED, NOTIMP */
#define WSANO_RECOVERY              (WSABASEERR+1003)
#define NO_RECOVERY                 WSANO_RECOVERY

/* Valid name, no data record of requested type */
#define WSANO_DATA                  (WSABASEERR+1004)
#define NO_DATA                     WSANO_DATA

/* no address, look for MX record */
#define WSANO_ADDRESS               WSANO_DATA
#define NO_ADDRESS                  WSANO_ADDRESS

/*
 * Windows Sockets errors redefined as regular Berkeley error constants.
 * These are commented out in Windows NT to avoid conflicts with errno.h.
 * Use the WSA constants instead.
 */
#if 0
#define EWOULDBLOCK                 WSAEWOULDBLOCK
#define EINPROGRESS                 WSAEINPROGRESS
#define EALREADY                    WSAEALREADY
#define ENOTSOCK                    WSAENOTSOCK
#define EDESTADDRREQ                WSAEDESTADDRREQ
#define EMSGSIZE                    WSAEMSGSIZE
#define EPROTOTYPE                  WSAEPROTOTYPE
#define ENOPROTOOPT                 WSAENOPROTOOPT
#define EPROTONOSUPPORT             WSAEPROTONOSUPPORT
#define ESOCKTNOSUPPORT             WSAESOCKTNOSUPPORT
#define EOPNOTSUPP          WSAEOPNOTSUPP
#define EPFNOSUPPORT        WSAEPFNOSUPPORT
#define EAFNOSUPPORT        WSAEAFNOSUPPORT
#define EADDRINUSE          WSAEADDRINUSE
#define EADDRNOTAVAIL       WSAEADDRNOTAVAIL
#define ENETDOWN            WSAENETDOWN
#define ENETUNREACH         WSAENETUNREACH
#define ENETRESET           WSAENETRESET
#define ECONNABORTED        WSAECONNABORTED
#define ECONNRESET          WSAECONNRESET
#define ENOBUFS             WSAENOBUFS
#define EISCONN             WSAEISCONN
#define ENOTCONN            WSAENOTCONN
#define ESHUTDOWN           WSAESHUTDOWN
#define ETOOMANYREFS        WSAETOOMANYREFS
#define ETIMEDOUT           WSAETIMEDOUT
#define ECONNREFUSED        WSAECONNREFUSED
#define ELOOP               WSAELOOP
#define ENAMETOOLONG        WSAENAMETOOLONG
#define EHOSTDOWN           WSAEHOSTDOWN
#define EHOSTUNREACH        WSAEHOSTUNREACH
#define ENOTEMPTY           WSAENOTEMPTY
#define EPROCLIM            WSAEPROCLIM
#define EUSERS              WSAEUSERS
#define EDQUOT              WSAEDQUOT
#define ESTALE              WSAESTALE
#define EREMOTE             WSAEREMOTE
#endif

/* Socket function prototypes */

#ifdef __cplusplus
extern "C" {
#endif

SOCKET PASCAL FAR accept (SOCKET s, struct sockaddr FAR *addr,
                          int FAR *addrlen);

int PASCAL FAR bind (SOCKET s, const struct sockaddr FAR *addr, int namelen);

int PASCAL FAR closesocket (SOCKET s);

int PASCAL FAR connect (SOCKET s, const struct sockaddr FAR *name, int namelen);

int PASCAL FAR ioctlsocket (SOCKET s, long cmd, u_long FAR *argp);

int PASCAL FAR getpeername (SOCKET s, struct sockaddr FAR *name,
                            int FAR * namelen);

int PASCAL FAR getsockname (SOCKET s, struct sockaddr FAR *name,
                            int FAR * namelen);

int PASCAL FAR getsockopt (SOCKET s, int level, int optname,
                           char FAR * optval, int FAR *optlen);

u_long PASCAL FAR htonl (u_long hostlong);

u_short PASCAL FAR htons (u_short hostshort);
```
