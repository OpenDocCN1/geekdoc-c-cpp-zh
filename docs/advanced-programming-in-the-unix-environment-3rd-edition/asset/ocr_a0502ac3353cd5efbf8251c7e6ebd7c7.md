If we know that we don’t need the thread’s termination status at the time we create the thread, we can arrange for the thread to start out in the detached state by modifying the detachstate thread attribute in the pthread_attr_t structure. We can use the pthread_attr_setdetachstate function to set the detachstate thread attribute to one of two legal values: PTHREAD_CREATE_DETACHED to start the thread in the detached state or PTHREAD_CREATE_JOINABLE to start the thread normally, so its termination status can be retrieved by the application.

```
#include <pthread.h>
int pthread_attr_getdetachstate(const pthread_attr_t *restrict attr,
                                int *detachstate);
int pthread_attr_setdetachstate(pthread_attr_t *attr, int detachstate);
Both return: 0 if OK, error number on failure
```

We can call pthread_attr_getdetachstate to obtain the current detachstate attribute. The integer pointed to by the second argument is set to either PTHREAD_CREATE_DETACHED or PTHREAD_CREATE_JOINABLE, depending on the value of the attribute in the given pthread_attr_t structure.

# Example

Figure 12.4 shows a function that can be used to create a thread in the detached state.

```
#include "apue.h"
#include <pthread.h>
int
makethread(void *(*fn)(void *), void *arg)
{
    int         err;
    pthread_t   tid;
    pthread_attr_t  attr;
    err = pthread_attr_init(&attr);
    if (err != 0)
        return(err);
    err = pthread_attr_setdetachstate(&attr, PTHREAD_CREATE_DETACHED);
    if (err == 0)
        err = pthread_create(&tid, &attr, fn, arg);
    pthread_attr_destroy(&attr);
    return(err);
}
```

Figure 12.4  Creating a thread in the detached state

Note that we ignore the return value from the call to pthread_attr_destroy. In this case, we initialized the thread attributes properly, so pthread_attr_destroy shouldn’t fail. Nonetheless, if it does fail, cleaning up would be difficult: we would have to destroy the thread we just created, which might already be running, asynchronous to the execution of this function. When we choose to ignore the error