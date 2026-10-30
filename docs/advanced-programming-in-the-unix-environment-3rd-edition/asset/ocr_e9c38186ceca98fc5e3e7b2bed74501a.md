```
```c
if (nr < 0) {
    log_ret("can't read %s", name);
    goto defer;
}

/*
 * Read the response from the printer.
 */
if (printer_status(sockfd, jp)) {
    unlink(name);
    sprintf(name, "%s/%s/%d", SPOOLDIR, REQDIR, jp->jobid);
    unlink(name);
    free(jp);
    jp = NULL;
}
defer:
    close(fd);
    if (sockfd >= 0)
        close(sockfd);
    if (jp != NULL) {
        replace_job(jp);
        nanosleep(&ts, NULL);
    }
}

/*
 * Read data from the printer, possibly increasing the buffer.
 * Returns offset of end of data in buffer or -1 on failure.
 *
 * LOCKING: none.
 */
ssize_t
readmore(int sockfd, char **bpp, int off, int *bszp)
```
```

**[754–757]** When we reach the end of the file, read will return 0. However, if read fails, we log an error message and jump to defer.

**[758–767]** After sending the file to the printer, we call `printer_status` to read the printer’s response to our request. On success, `printer_status` returns a nonzero value and we delete the data and control files. Then we free the job structure, set its pointer to `NULL`, and fall through to the defer label.

**[768–777]** At the defer label, we close the file descriptor for the open data file. If the socket descriptor is valid, we close it. On error, `jp` will point to the job structure for the job we are trying to print, so we place the job back on the head of the pending job list and delay for 1 minute. On success, `jp` is `NULL`, so we simply go back to the top of the loop to get the next job to print.

**[778–785]** The `readmore` function is used to read part of the response message from the printer.