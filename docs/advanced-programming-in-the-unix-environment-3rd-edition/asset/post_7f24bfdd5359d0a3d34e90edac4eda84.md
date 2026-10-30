
```
struct utmp {
    char ut_line[8]; /* tty line: "ttyh0", "ttyd0", "ttyp0", ... */
    char ut_name[8]; /* login name */
    long ut_time;    /* seconds since Epoch */
};
```

On login, one of these structures was filled in and written to the utmp file by the login program, and the same structure was appended to the wtmp file. On logout, the entry in the utmp file was erased—filled with null bytes—by the init process, and a new entry was appended to the wtmp file. This logout entry in the wtmp file had the ut_name field zeroed out. Special entries were appended to the wtmp file to indicate when the system was rebooted and right before and after the system's time and date was changed. The who(1) program read the utmp file and printed its contents in a readable form. Later versions of the UNIX System provided the last(1) command, which read through the wtmp file and printed selected entries.

Most versions of the UNIX System still provide the utmp and wtmp files, but as expected, the amount of information in these files has grown. The 20-byte structure that was written by Version 7 grew to 36 bytes with SVR2, and the extended utmp structure with SVR4 takes more than 350 bytes!

> The detailed format of these records in Solaris is given in the utmpx(4) manual page. With Solaris 10, both files are in the /var/adm directory. Solaris provides numerous functions described in getutxent(3) to read and write these two files.

> On FreeBSD 8.0 and Linux 3.2.0, the utmp(5) manual page gives the format of their versions of these login records. The pathnames of these two files are /var/run/utmp and /var/log/wtmp. On Mac OS X 10.6.8, the utmp and wtmp files do not exist. As of Mac OS X 10.5, the information found in the wtmp file can be obtained from the system logging facility, and the utmpx file contains information about the active login sessions.

## 6.9 System Identification

POSIX.1 defines the uname function to return information on the current host and operating system.

```
#include <sys/utsname.h>

int uname(struct utsname *name);

Returns: non-negative value if OK, -1 on error
```

We pass the address of a utsname structure to this function, and the function then fills it in. POSIX.1 defines only the minimum fields in the structure, which are all character arrays, and it's up to each implementation to set the size of each array. Some implementations provide additional fields in the structure.

```
struct utsname {
    char sysname[];    /* name of the operating system */
    char nodename[];   /* name of this node */
    char release[];    /* current release of operating system */
    char version[];    /* current version of this release */
    char machine[];    /* name of hardware type */
};
```

Each string is null terminated. The maximum name lengths, including the terminating null byte, supported by the four platforms discussed in this book are listed in Figure 6.7. The information in the utsname structure can usually be printed with the uname(1) command.

> POSIX.1 warns that the nodename element may not be adequate to reference the host on a communications network. This function is from System V, and in older days, the nodename element was adequate for referencing the host on a UUCP network.
> 
> Realize also that the information in this structure does not give any information on the POSIX.1 level. This should be obtained using _POSIX_VERSION, as described in Section 2.6.
> 
> Finally, this function gives us a way only to fetch the information in the structure; there is nothing specified by POSIX.1 about initializing this information.

Historically, BSD-derived systems provided the gethostname function to return only the name of the host. This name is usually the name of the host on a TCP/IP network.

```
#include <unistd.h>

int gethostname(char *name, int namelen);

Returns: 0 if OK, -1 on error
```

The namelen argument specifies the size of the name buffer. If enough space is provided, the string returned through name is null terminated. If insufficient room is provided, however, it is unspecified whether the string is null terminated.

The gethostname function, which is now defined as part of POSIX.1, specifies that the maximum host name length is HOST_NAME_MAX. Figure 6.7 summarizes the maximum name lengths supported by the four implementations covered in this book.

| Interface | Maximum name length |  |  |  |
|---|---|---|---|---|
|  | FreeBSD 8.0 | Linux 3.2.0 | Mac OS X 10.6.8 | Solaris 10 |
| uname | 256 | 65 | 256 | 257 |
| gethostname | 256 | 64 | 256 | 256 |

Figure 6.7 System identification name limits

If the host is connected to a TCP/IP network, the host name is normally the fully qualified domain name of the host.

There is also a hostname(1) command that can fetch or set the host name. (The host name is set by the superuser using a similar function, sethostname.) The host name is normally set at bootstrap time from one of the start-up files invoked by /etc/rc or init.

## 6.10 Time and Date Routines

The basic time service provided by the UNIX kernel counts the number of seconds that have passed since the Epoch: 00:00:00 January 1, 1970, Coordinated Universal Time (UTC). In Section 1.10, we said that these seconds are represented in a time_t data type, and we call them calendar times. These calendar times represent both the time and the date. The UNIX System has always differed from other operating systems in (a) keeping time in UTC instead of the local time, (b) automatically handling conversions, such as daylight saving time, and (c) keeping the time and date as a single quantity.

The time function returns the current time and date.

```
#include <time.h>

time_t time(time_t *calptr);

Returns: value of time if OK, -1 on error
```

The time value is always returned as the value of the function. If the argument is non-null, the time value is also stored at the location pointed to by calptr.

The real-time extensions to POSIX.1 added support for multiple system clocks. In Version 4 of the Single UNIX Specification, the interfaces used to control these clocks were moved from an option group to the base. A clock is identified by the clockid_t type. Standard values are summarized in Figure 6.8.

| Identifier | Option | Description |
|---|---|---|
| CLOCK_REALTIME |  | real system time |
| CLOCK_MONOTONIC | _POSIX_MONOTONIC_CLOCK | real system time with no negative jumps |
| CLOCK_PROCESS_CPUTIME_ID | _POSIX_CPUTIME | CPU time for calling process |
| CLOCK_THREAD_CPUTIME_ID | _POSIX_THREAD_CPUTIME | CPU time for calling thread |

Figure 6.8 Clock type identifiers

The clock_gettime function can be used to get the time of the specified clock. The time is returned in a timespec structure, introduced in Section 4.2, which expresses time values in terms of seconds and nanoseconds.

```
#include <sys/time.h>

int clock_gettime(clockid_t clock_id, struct timespec *tsp);

Returns: 0 if OK, -1 on error
```

When the clock ID is set to CLOCK_REALTIME, the clock_gettime function provides similar functionality to the time function, except with clock_gettime, we might be able to get a higher-resolution time value if the system supports it.

We can use the clock_getres function to determine the resolution of a given system clock.

```
#include <sys/time.h>
int clock_getres(clockid_t clock_id, struct timespec *tsp);
Returns: 0 if OK, -1 on error
```

The clock_getres function initializes the timespec structure pointed to by the tsp argument to the resolution of the clock corresponding to the clock_id argument. For example, if the resolution is 1 millisecond, then the tv_sec field will contain 0 and the tv_nsec field will contain the value 1000000.

To set the time for a particular clock, we can call the clock_settime function.

```
#include <sys/time.h>
int clock_settime(clockid_t clock_id, const struct timespec *tsp);
Returns: 0 if OK, -1 on error
```

We need the appropriate privileges to change a clock's time. Some clocks, however, can't be modified.

Historically, on implementations derived from System V, the stime(2) function was called to set the system time, whereas BSD-derived systems used settimeofday(2).

Version 4 of the Single UNIX Specification specifies that the gettimeofday function is now obsolescent. However, a lot of programs still use it, because it provides greater resolution (up to a microsecond) than the time function.

```
#include <sys/time.h>
int gettimeofday(struct timeval *restrict tp, void *restrict tzp);
Returns: 0 always
```

The only legal value for tzp is NULL; other values result in unspecified behavior. Some platforms support the specification of a time zone through the use of tzp, but this is implementation specific and not defined by the Single UNIX Specification.

The gettimeofday function stores the current time as measured from the Epoch in the memory pointed to by tp. This time is represented as a timeval structure, which stores seconds and microseconds.

Once we have the integer value that counts the number of seconds since the Epoch, we normally call a function to convert it to a broken-down time structure, and then call another function to generate a human-readable time and date. Figure 6.9 shows the relationships between the various time functions. (The three functions in this figure that are shown with dashed lines—localtime, mktime, and strftime—are all affected by the TZ environment variable, which we describe later in this section. The dotted lines show how the calendar time is obtained from time-related structures.)
