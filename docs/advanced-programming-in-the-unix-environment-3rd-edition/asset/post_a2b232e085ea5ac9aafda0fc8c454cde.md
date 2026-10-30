
```c
typedef u_short comp_t; /* 3-bit base 8 exponent; 13-bit fraction */
struct acct
{
    char ac_flag;      /* flag (see Figure 8.26) */
    char ac_stat;      /* termination status (signal & core flag only) */
                     /* (Solaris only) */
    uid_t ac_uid;      /* real user ID */
    gid_t ac_gid;      /* real group ID */
    dev_t ac_tty;      /* controlling terminal */
    time_t ac_btime;   /* starting calendar time */
    comp_t ac_utime;   /* user CPU time */
    comp_t ac_stime;   /* system CPU time */
    comp_t ac_etime;   /* elapsed time */
    comp_t ac_mem;     /* average memory usage */
    comp_t ac_io;      /* bytes transferred (by read and write) */
                     /* "blocks" on BSD systems */
    comp_t ac_rw;      /* blocks read or written */
                     /* (not present on BSD systems) */
    char ac_comm[8];   /* command name: [8] for Solaris, */
                     /* [10] for Mac OS X, [16] for FreeBSD, and */
                     /* [17] for Linux */
};
```

Times are recorded in units of clock ticks on most platforms, but FreeBSD stores microseconds instead. The `ac_flag` member records certain events during the execution of the process. These events are described in Figure 8.26.

The data required for the accounting record, such as CPU times and number of characters transferred, is kept by the kernel in the process table and initialized whenever a new process is created, as in the child after a `fork`. Each accounting record is written when the process terminates. This has two consequences.

First, we don’t get accounting records for processes that never terminate. Processes like `init` that run for the lifetime of the system don’t generate accounting records. This also applies to kernel daemons, which normally don’t exit.

Second, the order of the records in the accounting file corresponds to the termination order of the processes, not the order in which they were started. To know the starting order, we would have to go through the accounting file and sort by the starting calendar time. But this isn’t perfect, since calendar times are in units of seconds (Section 1.10), and it’s possible for many processes to be started in any given second. Alternatively, the elapsed time is given in clock ticks, which are usually between 60 and 128 ticks per second. But we don’t know the ending time of a process; all we know is its starting time and ending order. Thus, even though the elapsed time is more accurate than the starting time, we still can’t reconstruct the exact starting order of various processes, given the data in the accounting file.

The accounting records correspond to processes, not programs. A new record is initialized by the kernel for the child after a `fork`, not when a new program is executed. Although `exec` doesn’t create a new accounting record, the command name changes, and the `AFORK` flag is cleared. This means that if we have a chain of three programs—A execs B, then B execs C, and C exits—only a single accounting record is written. The command name in the record corresponds to program C, but the CPU times, for example, are the sum for programs A, B, and C.

## Figure 8.26 Values for ac_flag from accounting record

| ac_flag | Description | FreeBSD 8.0 | Linux 3.2.0 | Mac OS X 10.6.8 | Solaris 10 |
|---|---|---|---|---|---|
| AFORK | process is the result of fork, but never called exec | • | • | • |  |
| ASU | process used superuser privileges | • | • | • | • |
| ACORE | process dumped core | • | • | • |  |
| AXSIG | process was killed by a signal | • | • | • |  |
| AEXPND | expanded accounting entry |  |  |  | • |
| ANVER | new record format | • |  |  |  |

## Example

To have some accounting data to examine, we’ll create a test program to implement the diagram shown in Figure 8.27.

![](img/244bf0c3b6d0288ae397336907e37851_304_0.png)

## Figure 8.27 Process structure for accounting example

The source for the test program is shown in Figure 8.28. It calls `fork` four times. Each child does something different and then terminates.

```c
#include "apue.h"
int
main(void)
{
    pid_t  pid;
    if ((pid = fork()) < 0)
        err_sys("fork error");
    else if (pid != 0) {      /* parent */
        sleep(2);
        exit(2);               /* terminate with exit status 2 */
    }
    if ((pid = fork()) < 0)
        err_sys("fork error");
    else if (pid != 0) {      /* first child */
        sleep(4);
        abort();               /* terminate with core dump */
    }
    if ((pid = fork()) < 0)
        err_sys("fork error");
    else if (pid != 0) {      /* second child */
        exec1("/bin/dd", "dd", "if=/etc/passwd", "of=/dev/null", NULL);
        exit(7);               /* shouldn't get here */
    }
    if ((pid = fork()) < 0)
        err_sys("fork error");
    else if (pid != 0) {      /* third child */
        sleep(8);
        exit(0);               /* normal exit */
    }
    sleep(6);                  /* fourth child */
    kill(getpid(), SIGKILL);   /* terminate w/signal, no core dump */
    exit(6);                   /* shouldn't get here */
}
```

## Figure 8.28 Program to generate accounting data

We’ll run the test program on Solaris and then use the program in Figure 8.29 to print out selected fields from the accounting records.

```c
#include "apue.h"
#include <sys/acct.h>

#if defined(BSD)  /* different structure in FreeBSD */
#define acct acctv2
#define ac_flag ac_trailer.ac_flag
#define FMT "%8s e = %6.0f, chars = %6.0f, %c %c %c %c\n"
#elif defined(HAS_AC_STAT)
#define FMT "%8s e = %6ld, chars = %7ld, stat = %3u: %c %c %c %c\n"
#else
#define FMT "%8s e = %6ld, chars = %7ld, %c %c %c %c\n"
#endif
#if defined(LINUX)
#define acct acct_v3  /* different structure in Linux */
#endif

#if !defined(HAS_ACORE)
#define ACORE 0
#endif
#if !defined(HAS_AXSIG)
#define AXSIG 0
#endif

#if !defined(BSD)
static unsigned long
compt2ulong(comp_t comptime)    /* convert comp_t to unsigned long */
{
        unsigned long   val;
        int             exp;

        val = comptime & 0x1fff;    /* 13-bit fraction */
        exp = (comptime >> 13) & 7; /* 3-bit exponent (0-7) */
        while (exp-- > 0)
                val <<= 3;
        return(val);
}
#endif

int
main(int argc, char *argv[])
{
        struct acct   acdata;
        FILE           *fp;

        if (argc != 2)
                err_quit("usage: pract filename");
        if ((fp = fopen(argv[1], "r")) == NULL)
                err_sys("can't open %s", argv[1]);
        while (fread(&acdata, sizeof(acdata), 1, fp) == 1) {
                printf("%*.s,", sizeof(acdata.ac_comm),
#if defined(BSD)
                        sizeof(acdata.ac_comm), acdata.ac_comm,
#else
                        acdata.ac_etime, acdata.ac_io,
#endif
                        compt2ulong(acdata.ac_etime), compt2ulong(acdata.ac_io),
#if defined(HAS_AC_STAT)
                        (unsigned char) acdata.ac_stat,
#endif
                        acdata.ac_flag & ACORE ? 'D' : ' ',
                        acdata.ac_flag & AXSIG ? 'K' : ' ',
                        acdata.ac_flag & AFORK ? 'F' : ' ',
                        acdata.ac_flag & ASU ? 'S' : ' ');
        }
        if (ferror(fp))
                err_sys("read error");
        exit(0);
}
```

## Figure 8.29 Print selected fields from system’s accounting file

BSD-derived platforms don’t support the `ac_stat` member, so we define the `HAS_AC_STAT` constant on the platforms that do support this member. Basing the defined symbol on the feature instead of on the platform makes the code read better and allows us to modify the program simply by adding the new definition to our compilation command. The alternative would be to use

```c
#if !defined(BSD) && !defined(MACOS)
```

which becomes unwieldy as we port our application to additional platforms.

We define similar constants to determine whether the platform supports the `ACORE` and `AXSIG` accounting flags. We can’t use the flag symbols themselves, because on Linux, they are defined as enum values, which we can’t use in a `#ifdef` expression.

To perform our test, we do the following:

- 1. Become superuser and enable accounting, with the `acct on` command. Note that when this command terminates, accounting should be on; therefore, the first record in the accounting file should be from this command.
- 2. Exit the superuser shell and run the program in Figure 8.28. This should append six records to the accounting file: one for the superuser shell, one for the test parent, and one for each of the four test children.
- A new process is not created by the `exec` in the second child. There is only a single accounting record for the second child.
- 3. Become superuser and turn accounting off. Since accounting is off when this `acct on` command terminates, it should not appear in the accounting file.
- 4. Run the program in Figure 8.29 to print the selected fields from the accounting file.

The output from step 4 follows. We have appended the description of the process in italics to selected lines, for the discussion later.

```text
acct on    e = 1, chars = 336, stat = 0:      S
sh         e = 1550, chars = 20168, stat = 0:   S
dd         e = 2, chars = 1585, stat = 0:      second child
a.out      e = 202, chars = 0, stat = 0:      parent
a.out      e = 420, chars = 0, stat = 134:  F   first child
a.out      e = 600, chars = 0, stat = 9:   F   fourth child
a.out      e = 801, chars = 0, stat = 0:  F   third child
```

For this system, the elapsed time values are measured in units of clock ticks. Figure 2.15 shows that this system generates 100 clock ticks per second. For example, the `sleep(2)` in the parent corresponds to the elapsed time of 202 clock ticks. For the first child, the `sleep(4)` becomes 420 clock ticks. Note that the amount of time a process sleeps is not exact. (We’ll return to the `sleep` function in Chapter 10.) Also, the calls to `fork` and `exit` take some amount of time.

Note that the `ac_stat` member is not the true termination status of the process, but rather corresponds to a portion of the termination status we have discussed in
