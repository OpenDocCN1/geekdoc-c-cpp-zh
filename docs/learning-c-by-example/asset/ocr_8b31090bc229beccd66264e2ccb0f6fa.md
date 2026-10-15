# 8.5 Thread Mutex

You have resources such as data variable, file, database which can be accessed only by a thread. It’s called mutex. For illustration, you have data which is stored on variable n. You also have 5 threads to access this data. The first rule is data variable can be accessed by one thread. It means data variable will be locked so another thread cannot access it.

Mutex is one of thread synchronization mechanism to control accessing resource.

You can implement thread mutex using the following functions.

```
#include <pthread.h>

int pthread_mutex_init(pthread_mutex_t *restrict mutex,
    const pthread_mutexattr_t *restrict attr);
int pthread_mutex_destroy(pthread_mutex_t *mutex);
int pthread_mutex_lock(pthread_mutex_t *mutex);
int pthread_mutex_unlock(pthread_mutex_t *mutex);
```

Note:

+   - pthread_mutex_init() initialize mutex object
+   - pthread_mutex_destroy() destroy mutex object
+   - pthread_mutex_lock() locak mutex object
+   - pthread_mutex_lock() unlock/release mutex object

For implementation, we create a file, called mutex.c. Firstly we define headers and global variables. Write this code.

```
#include <stdio.h>
#include <pthread.h>
#include <string.h>
#include <errno.h>
#include <unistd.h>

pthread_t thread[5];
int total_finished_jobs;
pthread_mutex_t lock;
```

Variable total_finished_jobs can be accessed by only one thread.

On main() point entry, we instantiate mutex object and create 5 threads.

```
int main(int argc, char* argv[])
{
    int i, ret;
    errno = 0;
```