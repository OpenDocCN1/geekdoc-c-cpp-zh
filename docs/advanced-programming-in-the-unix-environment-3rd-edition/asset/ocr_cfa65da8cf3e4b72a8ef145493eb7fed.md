```
```c
520  /*
521   * Cancellation routine for the worker thread.
522   *
523   * LOCKING: acquires and releases workerlock.
524   */
525  void
526  client_cleanup(void *arg)
527  {
528      struct worker_thread     *wtp;
529      pthread_t                tid;
530
531      tid = (pthread_t)((long)arg);
532      pthread_mutex_lock(&workerlock);
533      for (wtp = workers; wtp != NULL; wtp = wtp->next) {
534          if (wtp->tid == tid) {
535              if (wtp->next != NULL)
536                  wtp->next->prev = wtp->prev;
537              if (wtp->prev != NULL)
538                  wtp->prev->next = wtp->next;
539              else
540                  workers = wtp->next;
541              break;
542          }
543      }
544      pthread_mutex_unlock(&workerlock);
545      if (wtp != NULL) {
546          close(wtp->sockfd);
547          free(wtp);
548      }
549  }
```
```

[520–542] The `client_cleanup` function is the thread cleanup handler for the worker threads that communicate with client commands. This function is called when the thread calls `pthread_exit`, calls `pthread_cleanup_pop` with a nonzero argument, or responds to a cancellation request. The argument is the thread ID of the thread terminating.

We lock the workerlock mutex and search the list of worker threads until we find a matching thread ID. When we find a match, we remove the worker thread structure from the list and stop the search.

[543–548] We unlock the workerlock mutex, close the socket file descriptor used by the thread to communicate with the client, and free the memory backing the `worker_thread` structure.

Since we try to acquire the workerlock mutex, if a thread reaches a cancellation point while the `kill_workers` function is still walking the list, we will have to wait until `kill_workers` releases the mutex before we can proceed.