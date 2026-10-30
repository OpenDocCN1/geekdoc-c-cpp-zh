```
```c
449    nw = write(fd, &req, sizeof(struct printreq));
450    if (nw != sizeof(struct printreq)) {
451        res.jobid = 0;
452        if (nw < 0)
453            res.retcode = htonl(errno);
454        else
455            res.retcode = htonl(EIO);
456        log_msg("client_thread: can’t write %s: %s", name,
457                strerror(res.retcode));
458        close(fd);
459        strncopy(res.msg, strerror(res.retcode), MSGLEN_MAX);
460        writen(sockfd, &res, sizeof(struct printresp));
461        unlink(name);
462        snprintf(name, "%s/%s/%d", SPOOLDIR, DATADIR, jobid);
463        unlink(name);
464        pthread_exit((void *)1);
465    }
466    close(fd);
467
468    /*
469     * Send response to client.
470     */
471    res.retcode = 0;
472    res.jobid = htonl(jobid);
473    snprintf(res.msg, "request ID %d", jobid);
474    writen(sockfd, &res, sizeof(struct printresp));
475
476    /*
477     * Notify the printer thread, clean up, and exit.
478     */
479    log_msg("adding job %d to queue", jobid);
480    add_job(&job);
481    pthread_cleanup_pop(1);
482    return((void *)0);
483 }
```
```

**[449–465]** We write the printreq structure to the control file. On error, we log a message, close the descriptor for the control file, send a failure response back to the client, remove the data and control files, and terminate the thread.

**[466–473]** We close the file descriptor for the control file and send a message containing the job ID and a successful status (record set to 0) back to the client.

**[474–481]** We call `add_job` to add the received job to the list of pending print jobs and call `pthread_cleanup_pop` to complete the cleanup processing. The thread terminates when we return.

Note that before the thread exits, we must close any file descriptors we no longer need. Unlike with process termination, file descriptors are not closed automatically when a thread ends if other threads exist in the process. If we didn’t close unneeded file descriptors, we’d eventually run out of resources.