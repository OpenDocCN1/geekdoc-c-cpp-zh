```
```c
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
```
```