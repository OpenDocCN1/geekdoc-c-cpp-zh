| Header | FreeBSD 8.0 | Linux 3.2.0 | Mac OS X 10.6.8 | Solaris 10 | Description |
|---|---|---|---|---|---|
| <fmtmsg.h> | • | • | • | • | message display structures |
| <ftw.h> | • | • | • | • | file tree walking (Section 4.22) |
| <libgen.h> | • | • | • | • | pathname management functions |
| <ndbm.h> | • | • | • | • | database operations |
| <search.h> | • | • | • | • | search tables |
| <syslog.h> | • | • | • | • | system error logging (Section 13.4) |
| <utmpx.h> | • | • | • | • | user accounting database |
| <sys/ipc.h> | • | • | • | • | IPC (Section 15.6) |
| <sys/msg.h> | • | • | • | • | XSI message queues (Section 15.7) |
| <sys/resource.h> | • | • | • | • | resource operations (Section 7.11) |
| <sys/sem.h> | • | • | • | • | XSI semaphores (Section 15.8) |
| <sys/shm.h> | • | • | • | • | XSI shared memory (Section 15.9) |
| <sys/time.h> | • | • | • | • | time types |
| <sys/uio.h> | • | • | • | • | vector I/O operations (Section 14.6) |

Figure 2.3 XSI option headers defined by the POSIX standard

After more than twenty years of work, the standards are mature and stable. The POSIX.1 standard is maintained by an open working group known as the Austin Group (.../.../.../.../www.opengroup.org/austin). That they are still relevant, the standards need to be either updated or reaffirmed every so often.

# 2.2.3 The Single UNIX Specification

The Single UNIX Specification, a superset of the POSIX.1 standard, specifies additional interfaces that extend the functionality provided by the POSIX.1 specification. POSIX.1 is equivalent to the Base Specifications portion of the Single UNIX Specification.

The X/Open System Interfaces (XSI) option in POSIX.1 describes optional interfaces and defines which optional portions of POSIX.1 must be supported for an implementation to be deemed XSI conforming. These include file synchronization, thread stack address and size attributes, thread process-shared synchronization, and the _XOPEN_UNIX symbolic constant (marked "SUS mandatory" in Figure 2.5). Only XSI-conforming implementations can be called UNIX systems.

> The Open Group owns the UNIX trademark and uses the Single UNIX Specification to define the interfaces an implementation must support to call itself a UNIX system. Vendors must file conformance statements, pass test suites to verify conformance, and license the right to use the UNIX trademark.

| Header | FreeBSD 8.0 | Linux 3.2.0 | Mac OS X 10.6.8 | Solaris 10 | Description |
|---|---|---|---|---|---|
| <mqueue.h> | • | • |  | • | message queues |
| <spawn.h> | • | • | • | • | real-time spawn interface |

Figure 2.4 Optional headers defined by the POSIX standard