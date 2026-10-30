
```
/*
 * "Timed" read - timout specifies the number of seconds to wait
 * per read call before giving up, but read exactly nbytes bytes.
 * Returns number of bytes read or -1 on error.
 *
 * LOCKING: none.
 */
ssize_t
treadn(int fd, void *buf, size_t nbytes, unsigned int timeout)
{
    size_t nleft;
    ssize_t nread;

    nleft = nbytes;
    while (nleft > 0) {
        if ((nread = tread(fd, buf, nleft, timeout)) < 0) {
            if (nleft == nbytes)
                return(-1); /* error, return -1 */
            else
                break; /* error, return amount read so far */
        } else if (nread == 0) {
            break; /* EOF */
        }
        nleft -= nread;
        buf += nread;
    }
    return(nbytes - nleft);    /* return >= 0 */
}

[120–146] We also provide a variation of tread, called treadn, that reads exactly the number of bytes requested. This is similar to the readn function described in Section 14.7, but with the addition of the timeout parameter.

To read exactly nbytes bytes, we have to be prepared to make multiple calls to read. The difficult part is trying to apply a single timeout value to multiple calls to read. We don't want to use an alarm, because signals can be messy to deal with in multithreaded applications. We can't rely on the system updating the timeval structure on return from select to indicate the amount of time left, because many platforms do not support this behavior (Section 14.4.1). Thus, we compromise and define the timeout value in this case to apply to an individual tread call. Instead of limiting the total amount of time we wait, it limits the amount of time we'll wait in every iteration of the loop. The maximum time we can wait is bounded by (nbytes × timeout) seconds (worst case, we'll receive only 1 byte at a time).

We use nleft to record the number of bytes remaining to be read. If tread fails and we have received data in a previous iteration, we break out of the while loop and return the number of bytes read; otherwise, we return −1.

The command used to submit a print job is shown next. The C source file is print.c.

```
/*
 * The client command for printing documents. Opens the file
 * and sends it to the printer spooling daemon. Usage:
 * print [-t] filename
 */
#include "apue.h"
#include "print.h"
#include <fcntl.h>
#include <pwd.h>
/*
 * Needed for logging funtions.
 */
int log_to_stderr = 1;

void submit_file(int, int, const char *, size_t, int);

int
main(int argc, char *argv[])
{
    int             fd, sfd, err, text, c;
    struct stat     sbuf;
    char            *host;
    struct addrinfo *ailist, *aip;

    err = 0;
    text = 0;
    while ((c = getopt(argc, argv, "t")) != -1) {
        switch (c) {
        case 't':
            text = 1;
            break;

        case '?':
            err = 1;
            break;
        }
    }
```

[1–14] We need to define an integer called log_to_stderr to be able to use the log functions in our library. If this integer is set to a nonzero value, error messages will be sent to the standard error stream instead of to a log file. Although we don't use any logging functions in print.c, we do link util.o with print.o to build the executable print command, and util.c contains functions for both user commands and daemons.

[15–33] We support one option, -t, to force the file to be printed as text (instead of as a PostScript program, for example). We use the getopt function (introduced in Section 17.6) to process the command options.

```
if (err || (optind != argc - 1))
    err_quit("usage: print [-t] filename");
if ((fd = open(argv[optind], O_RDONLY)) < 0)
    err_sys("print: can't open %s", argv[optind]);
if (fstat(fd, &sbuf) < 0)
    err_sys("print: can't stat %s", argv[optind]);
if (!S_ISREG(sbuf.st_mode))
    err_quit("print: %s must be a regular file", argv[optind]);
/*
 * Get the hostname of the host acting as the print server.
 */
if ((host = get_printserver()) == NULL)
    err_quit("print: no print server defined");
if ((err = getaddrlist(host, "print", &ailist)) != 0)
    err_quit("print: getaddrinfo error: %s", gai_strerror(err));
for (aip = ailist; aip != NULL; aip = aip->ai_next) {
    if ((sfd = connect_retry(AF_INET, SOCK_STREAM, 0,
        aip->ai_addr, aip->ai_addrlen)) < 0) {
        err = errno;
```

[34–41] When getopt completes processing the command options, it leaves the variable optind set to the index of the first nonoptional argument. If this is any value other than the index of the last argument, then the wrong number of arguments was specified (we support only one nonoptional argument). Our error processing includes checks to ensure that we can open the file to be printed and that it is a regular file (as opposed to a directory or other type of file).

[42–48] We get the name of the host where the printer spooling daemon is running by calling the get_printserver function from util.c. Then we translate the host name into a network address by calling getaddrlist (also from util.c).

Note that we specify the service as "print." As part of installing the printer spooling daemon on a system, we need to make sure that /etc/services (or the equivalent database) has an entry for the printer service. When we select a port number for the daemon, it would be a good idea to select one that is privileged, to prevent malicious users from writing applications that pretend to be a printer spooling daemon but instead steal copies of the files we try to print. This means that the port number should be less than 1,024 (recall Section 16.3.4) and that our daemon will have to run with superuser privileges to allow it to bind to a reserved port.

[49–52] We try to connect to the daemon using one address at a time from the list returned by getaddrinfo. We will try to send the file to the daemon using the first address to which we can connect.

```
```c
} else {
        submit_file(fd, sfd, argv[optind], sbuf.st_size, text);
        exit(0);
}
}
       err_exit(err, "print: can't contact %s", host);
}

 /*
  * Send a file to the printer daemon.
  */
void
submit_file(int fd, int sockfd, const char *fname, size_t nbytes,
            int text)
{
       int             nr, nw, len;
       struct passwd   *pwd;
       struct printreq  req;
       struct printresp res;
       char             buf[IOBUFSZ];

       /*
        * First build the header.
        */
       if ((pwd = getpwuid(geteuid())) == NULL) {
               strcpy(req.usernm, "unknown");
       } else {
               strncpy(req.usernm, pwd->pw_name, USERNM_MAX-1);
               req.usernm[USERNM_MAX-1] = '\0';
       }
```

**[53–59]** If we are able to connect to the printer spooling daemon, we call `submit_file` to transmit the file we want to print to the daemon. Then we exit with a value of 0 to indicate success. If we can't connect to any of the addresses, we call `err_exit` to print an error message and exit with a value of 1 to indicate failure. (Appendix B contains the source code for `err_exit` and the other error routines.)

**[60–80]** The `submit_file` function sends a print request to the daemon and reads the response. First, we build the `printreq` request header. We use `geteuid` to get the caller's effective user ID and pass this to `getpwuid` to look for the user in the system's password file. We copy the user's name to the request header or use the string unknown if we can't identify the user. We use `strncpy` when copying the name from the password file to avoid writing past the end of the user name buffer in the request header. If the name is longer than the size of the buffer, `strncpy` won't store a terminating null byte in the buffer, so we need to do it ourselves.
