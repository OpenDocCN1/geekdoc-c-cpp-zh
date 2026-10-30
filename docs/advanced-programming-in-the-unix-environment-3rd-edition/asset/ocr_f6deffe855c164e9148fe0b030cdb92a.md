obtain the absolute time for the timeout value, we can use the following function (assuming the maximum time blocked is expressed in minutes):

```
#include <sys/time.h>
#include <stdlib.h>

void
maketimeout(struct timespec *tsp, long minutes)
{
    struct timeval now;
    /* get the current time */
    gettimeofday(&now, NULL);
    tsp->tv_sec = now.tv_sec;
    tsp->tv_nsec = now.tv_usec * 1000; /* usec to nsec */
    /* add the offset to get value */
    tsp->tv_sec += minutes * 60;
}
```

If the timeout expires without the condition occurring, pthread_cond_timedwait will reacquire the mutex and return the error ETIMEDOUT. When it returns from a successful call to pthread_cond_wait or pthread_cond_timedwait, a thread needs to reevaluate the condition, since another thread might have run and already changed the condition.

There are two functions to notify threads that a condition has been satisfied. The pthread_cond_signal function will wake up at least one thread waiting on a condition, whereas the pthread_cond_broadcast function will wake up all threads waiting on a condition.

> The POSIX specification allows for implementations of pthread_cond_signal to wake up more than one thread, to make the implementation simpler.

```
#include <pthread.h>

int pthread_cond_signal(pthread_cond_t *cond);
int pthread_cond_broadcast(pthread_cond_t *cond);

Both return: 0 if OK, error number on failure
```

When we call pthread_cond_signal or pthread_cond_broadcast, we are said to be signaling the thread or condition. We have to be careful to signal the threads only after changing the state of the condition.

# Example

Figure 11.15 shows an example of how to use a condition variable and a mutex together to synchronize threads.