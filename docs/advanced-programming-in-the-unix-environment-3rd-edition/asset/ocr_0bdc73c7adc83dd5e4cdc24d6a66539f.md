```
352 /*
353  * Accept a print job from a client.
354  * LOCKING: none.
355  */
357 void *
358 client_thread(void *arg)
359 {
360     int             n, fd, sockfd, nr, nw, first;
361     int32_t         jobid;
362     pthread_t       tid;
363     struct printreq req;
364     struct printr esp res;
365     char            name[FILENMSZ];
366     char            buf[IOBUFSZ];
367     tid = pthread_self();
368     pthread_cleanup_push(client_cleanup, (void *)((long)tid));
369     sockfd = (long)arg;
370     add_worker(tid, sockfd);
371     /*
372      * Read the request header.
373      */
374     if ((n = treadn(sockfd, &req, sizeof(struct printreq), 10)) !=
375         sizeof(struct printreq)) {
376         res.jobid = 0;
377         if (n < 0)
378             res.retcode = htonl(errno);
379         else
380             res.retcode = htonl(EIO);
381         strncpy(res.msg, strerror(res.retcode), MSGLEN_MAX);
382         writen(sockfd, &res, sizeof(struct printr esp));
383         pthread_exit((void *)1);
384     }
```

[352–370] The client_thread is spawned from the main thread when a connect request is accepted. Its job is to receive the file to be printed from the client print command. We create a separate thread for each client print request. The first thing we do is install a thread cleanup handler (see Section 11.5 for a discussion of thread cleanup handlers). The cleanup handler is client_cleanup, which we will see later. It takes a single argument: our thread ID. Then we call add_worker to create a worker_thread structure and add it to the list of active client threads.

[371–384] At this point, we are done with the thread’s initialization tasks, so we read the request header from the client. If the client sends less data than we expect or we encounter an error, we respond with a message indicating the reason for the error and call pthread_exit to terminate the thread.