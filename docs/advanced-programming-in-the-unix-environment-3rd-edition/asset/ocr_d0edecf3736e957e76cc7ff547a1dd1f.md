```
}

switch (signo) {
case SIGHUP:
    syslog(LOG_INFO, "Re-reading configuration file");
    reread();
    break;

case SIGTERM:
    syslog(LOG_INFO, "got SIGTERM; exiting");
    exit(0);

default:
    syslog(LOG_INFO, "unexpected signal %d\n", signo);
}
    return(0);
}

int
main(int argc, char *argv[])
{
    int             err;
    pthread_t       tid;
    char            *cmd;
    struct sigaction sa;

    if ((cmd = strchr(argv[0], '/')) == NULL)
        cmd = argv[0];
    else
        cmd++;

    /*
     * Become a daemon.
     */
    daemonize(cmd);

    /*
     * Make sure only one copy of the daemon is running.
     */
    if (already_running()) {
        syslog(LOG_ERR, "daemon already running");
        exit(1);
    }

    /*
     * Restore SIGHUP default and block all signals.
     */
    sa.sa_handler = SIG_DFL;
    sigemptyset(&sa.sa_mask);
    sa.sa_flags = 0;
    if (sigaction(SIGHUP, &sa, NULL) < 0)
        err_quit("%s: can't restore SIGHUP default");
```