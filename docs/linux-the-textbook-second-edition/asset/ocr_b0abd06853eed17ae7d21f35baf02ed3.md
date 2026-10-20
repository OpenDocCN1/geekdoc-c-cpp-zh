```
pid_t pid;

pid = getpid();
tid = pthread_self();
printf ("pid %u tid %u\n", (unsigned int) pid, (unsigned int) tid);
}
$ gcc -w process_thread.c -o proc_t -lpthread
$ proc_t
pid 17741 tid 71923456
$
```

The thread_ids.c program in the following session creates a thread that displays its ID as well as the ID of the process that creates it. The main thread (i.e., the process) displays its PID and its TID.

```
$ cat thread_ids.c
#include <pthread.h>
#include <stdio.h>

void thread_fn(void *);
void displayids (const char *);

int main (void)
{
    pthread_t tid;
    int rval;

    rval = pthread_create(&tid, NULL, thread_fn, NULL);
    if (rval != 0) {
        printf("Thread creation failed.\n");
        exit(1);
    }
    displayids("Parent/Main thread:      ");
    sleep(1);
    exit(0);
}

void thread_fn (void *arg)
{
    displayids("Child thread:      ");
    return NULL;
}

void displayids (const char *s)
{
    pthread_t tid;
    pid_t pid;

    tid = pthread_self();
    pid = getpid();
    printf ("%s pid %u tid %u\n", s, (unsigned int) pid, (unsigned int) tid);
}
$ gcc -w thread_ids.c -o tids -lpthread
$ tids
Parent/Main thread:      pid 10249 tid 309786368
Child thread:            pid 10249 tid 301491968
$
```

# Exercise 16.17

Replicate the preceding sessions on your system. Do they work as expected on your Linux system?