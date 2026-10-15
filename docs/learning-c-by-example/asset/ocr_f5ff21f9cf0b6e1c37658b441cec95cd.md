# 8.6 Condition Variables

We have learned thread synchronization using thread mutex. Now we explore another thread synchronization using condition variables in controlling accessing resource.

There are two methods to implement condition variables on thread synchronization:

+   - Signaling
+   - Broadcasting

Each method will be explained on next section.

# 8.6.1 Signaling

The idea of signaling is after you access a resource you must notify to another thread to start accessing resource. To implement it, we can use the following functions.

```
#include <pthread.h>

int pthread_cond_init(pthread_cond_t *restrict cond,
    const pthread_condattr_t *restrict attr);

int pthread_cond_wait(pthread_cond_t *restrict cond,
    pthread_mutex_t *restrict mutex);

int pthread_cond_destroy(pthread_cond_t *cond);
```

To notify another thread, you can use pthread_cond_signal() which is defined as below.

```
#include <pthread.h>

int pthread_cond_signal(pthread_cond_t *cond);
```

For illustration, we create two threads that act as producer and consumer. Producer can write data and consumer can only read data. The data can be accessed by one thread, either producer or consumer.

Let’s start to create a file, called condvariable.c. Firstly we define headers and global variables.

```
#include <stdio.h>
#include <pthread.h>
#include <string.h>
#include <errno.h>
#include <unistd.h>
```