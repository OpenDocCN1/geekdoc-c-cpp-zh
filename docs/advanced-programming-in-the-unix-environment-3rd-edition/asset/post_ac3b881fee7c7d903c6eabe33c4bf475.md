
```
{ int i; if (client == NULL) client = malloc(NALLOC * sizeof(Client)); else client = realloc(client, (client_size+NALLOC)*sizeof(Client)); if (client == NULL) err_sys("can't alloc for client array"); /* initialize the new entries */ for (i = client_size; i < client_size + NALLOC; i++) client[i].fd = -1; /* fd of -1 means entry available */ client_size += NALLOC; } /* * Called by loop() when connection request from a new client arrives. */ int client_add(int fd, uid_t uid) { int i; if (client == NULL) /* first time we're called */ client_alloc(); again: for (i = 0; i < client_size; i++) { if (client[i].fd == -1) { /* find an available entry */ client[i].fd = fd; client[i].uid = uid; return(i); /* return index in client[] array */ } } /* client array full, time to realloc for more */ client_alloc(); goto again; /* and search again (will work this time) */ } /* * Called by loop() when we're done with a client. */ void client_del(int fd) { int i; for (i = 0; i < client_size; i++) { if (client[i].fd == fd) { client[i].fd = -1;
return;
}
log_quit("can't find client entry for fd %d", fd);
}
```

## Figure 17.27 Functions to manipulate client array

The first time client_add is called, it calls client_alloc, which in turn calls malloc to allocate space for ten entries in the array. After these ten entries are all in use, a later call to client_add causes realloc to allocate additional space. By dynamically allocating space this way, we have not limited the size of the client array at compile time to some value that we guessed and put into a header. These functions call the log_ functions (Appendix B) if an error occurs, since we assume that the server is a daemon.

Normally the server will run as a daemon, but we want to provide an option that allows it to be run in the foreground, with diagnostic messages sent to the standard error. This should make the server easier to test and debug, especially if we don't have permission to read the log file where the diagnostic messages are normally written. We'll use a command-line option to control whether the server runs in the foreground or as a daemon in the background.

It is important that all commands on a system follow the same conventions, because this makes them easier to use. If someone is familiar with the way command-line options are formed with one command, it would create more chances for mistakes if another command followed different conventions.

This problem is sometimes visible when dealing with white space on the command line. Some commands require that an option be separated from its argument by white space, but other commands require the argument to follow immediately after its option, without any intervening spaces. Without a consistent set of rules to follow, users either have to memorize the syntax of all commands or resort to a trial-and-error process when invoking them.

The Single UNIX Specification includes a set of conventions and guidelines that promote consistent command-line syntax. They include such suggestions as “Restrict each command-line option to a single alphanumeric character” and “All options should be preceded by a – character.”

Luckily, the getopt function exists to help command developers process command-line options in a consistent manner.

```
#include <unistd.h>

int getopt(int argc, char * const argv[], const char *options);

extern int optind, opterr, optopt;
extern char *optarg;

Returns: the next option character, or
-1 when all options have been processed
```

The argc and argv arguments are the same ones passed to the main function of the program. The options argument is a string containing the option characters supported by the command. If an option character is followed by a colon, then the option takes an argument. Otherwise, the option exists by itself. For example, if the usage statement for a command was

```
command [-i] [-u username] [-z] filename
```

we would pass "iuz:" as the options string to getopt.

The getopt function is normally used in a loop that terminates when getopt returns -1. During each iteration of the loop, getopt will return the next option processed. It is up to the application to sort out any conflict in options, however; getopt simply parses the options and enforces a standard format.

When it encounters an invalid option, getopt returns a question mark instead of the character. If an option's argument is missing, getopt will also return a question mark, but if the first character in the options string is a colon, getopt returns a colon instead. The special pattern -- will cause getopt to stop processing options and return -1. This allows users to provide command arguments that start with a minus sign but aren't options. For example, if you have a file named -bar, you can't remove it by typing

```
rm -bar
```

because rm will try to interpret -bar as options. The way to remove the file is to type

```
rm -- -bar
```

The getopt function supports four external variables.

+   optarg If an option takes an argument, getopt sets optarg to point to the option's argument string when an option is processed.
+   opterr If an option error is encountered, getopt will print an error message by default. To disable this behavior, applications can set opterr to 0.
+   optind The index in the argv array of the next string to be processed. It starts at 1 and is incremented for each argument processed by getopt.
+   optopt If an error is encountered during options processing, getopt will set optopt to point to the option string that caused the error.

The open server's main function (Figure 17.28) defines the global variables, processes the command-line options, and calls the function loop. If we invoke the server with the -d option, the server runs interactively instead of as a daemon. This option is used when testing the server.

```
#include "opend.h"
#include <syslog.h>

int debug, oflag, client_size, log_to_stderr;
char errmsg[MAXLINE];
char *pathname;

Client *client = NULL;
int
main(int argc, char *argv[])
{
    int c;

    log_open("open.serv", LOG_PID, LOG_USER);
   opterr = 0;  /* don't want getopt() writing to stderr */
    while ((c = getopt(argc, argv, "d")) != EOF) {
        switch (c) {
        case 'd':   /* debug */
            debug = log_to_stderr = 1;
            break;

        case '?':
            err_quit("unrecognized option: -%c", optopt);
        }
    }

    if (debug == 0)
        daemonize("opend");
    loop();      /* never returns */
}
```

## Figure 17.28 The server main function, version 2

The function loop is the server's infinite loop. We'll show two versions of this function. Figure 17.29 shows one version that uses select; Figure 17.30 shows another version that uses poll.

```
#include "opend.h"
#include <sys/select.h>

void
loop(void)
{
    int i, n, maxfd, maxi, listenfd, clifd, nread;
    char buf[MAXLINE];
    uid_t uid;
    fd_set rset, allset;

    FD_ZERO(&allset);

    /* obtain fd to listen for client requests on */
    if ((listenfd = serv_listen(CS_OPEN)) < 0)
        log_sys("serv_listen error");
    FD_SET(listenfd, &allset);
    maxfd = listenfd;
    maxi = -1;

for ( ; ; ) {
    rset = allset; /* rset gets modified each time around */
    if ((n = select(maxfd + 1, &rset, NULL, NULL, NULL)) < 0)
        log_sys("select error");

    if (FD_ISSET(listenfd, &rset)) {
        /* accept new client request */
        if ((clifd = serv_accept(listenfd, &uid)) < 0)
            log_sys("serv_accept error: %d", clifd);
        i = client_add(clifd, uid);
        FD_SET(clifd, &allset);
        if (clifd > maxfd)
            maxfd = clifd;  /* max fd for select() */
        if (i > maxi)
            maxi = i;   /* max index in client[] array */
        log_msg("new connection: uid %d, fd %d", uid, clifd);
        continue;
    }

    for (i = 0; i <= maxi; i++) {  /* go through client[] array */
        if ((clifd = client[i].fd) < 0)
            continue;
        if (FD_ISSET(clifd, &rset)) {
            /* read argument buffer from client */
            if ((nread = read(clifd, buf, MAXLINE)) < 0) {
                log_sys("read error on fd %d", clifd);
            } else if (nread == 0) {
                log_msg("closed: uid %d, fd %d",
                    client[i].uid, clifd);
                client_del(clifd);  /* client has closed cxn */
                FD_CLR(clifd, &allset);
                close(clifd);
            } else {
                /* process client's request */
                handle_request(buf, nread, clifd, client[i].uid);
            }
        }
    }
}
```

## Figure 17.29 The loop function using select

This function calls serv_listen (Figure 17.8) to create the server’s endpoint for the client connections. The remainder of the function is a loop that starts with a call to select. Two conditions can be true after select returns.

+   1. The descriptor listenfd can be ready for reading, which means that a new client has called cli_conn. To handle this, we call serv_accept (Figure 17.9) and then update the client array and associated bookkeeping information for the new client. (We keep track of the highest descriptor number for the first
