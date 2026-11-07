```
```c
#define timerclear(typ)        (typ)->tv_sec = (typ)->tv_usec = 0

/*
 * Commands for ioctl(socket), taken from the BSD file fcntl.h.
 *
 * Ioctl's have the command encoded in the lower word,
 * and the size of any in or out parameters in the upper
 * word.  The high 2 bits of the upper word are used
 * to encode the in/out status of the parameter; for now
 * we restrict parameters to at most 128 bytes.
 */
#define IOC_PARAM_MASK   0x7f          /* parameters must be < 128 bytes */
#define IOC_VOID         0x20000000    /* no parameters */
#define IOC_OUT          0x40000000    /* copy out parameters */
#define IOC_IN           0x80000000    /* copy in parameters */
#define IOC_INOUT        (IOC_IN|IOC_OUT)
                                      /* 0x20000000 distinguishes new &
                                         old ioctl's */
#define _IO(x,y)         (IOC_VOID|((x)<<8)|y)

#define _IOR(x,y,t)      (IOC_OUT|(((long)sizeof(t)&IOCPARM_MASK)<<16)|(x<<8)|y)

#define _IOW(x,y,t)      (IOC_IN|(((long)sizeof(t)&IOCPARM_MASK)<<16)|(x<<8)|y)

#define FIONREAD         _IOR('f', 127, u_long) /* get # bytes to read */
#define FIONBIO          _IOW('f', 126, u_long) /* set/clear non-blocking i/o */
#define FIOASYNC         _IOW('f', 125, u_long) /* set/clear async i/o */

/* Socket I/O Controls */
#define SIOCSHIWAT   _IOW('s',  0, u_long)  /* set high watermark */
#define SIOCGHIWAT   _IOR('s',  1, u_long)  /* get high watermark */
#define SIOCSLOWAT   _IOW('s',  2, u_long)  /* set low watermark */
#define SIOCGLOWAT   _IOR('s',  3, u_long)  /* get low watermark */
#define SIOCATMARK   _IOR('s',  7, u_long)  /* at oob mark? */

/*
 * Structures returned by network data base library, taken from the
 * BSD file netdb.h.  All addresses are supplied in host order, and
 * returned in network order (suitable for use in system calls).
 */
struct  hostent {
        char    FAR * h_name;          /* official name of host */
        char    FAR * FAR * h_aliases; /* alias list */
        short   h_addrtype;            /* host address type */
        short   h_length;              /* length of address */
        char    FAR * FAR * h_addr_list; /* list of addresses */
#define h_addr  h_addr_list[0]         /* address, for backward compat */
};

/*
 * It is assumed here that a network number
 * fits in 32 bits.
 */
struct  netent {
        char    FAR * n_name;          /* official name of net */
        char    FAR * FAR * n_aliases; /* alias list */
```
```