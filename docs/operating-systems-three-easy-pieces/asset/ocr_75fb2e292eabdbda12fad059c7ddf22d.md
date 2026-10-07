# CONDITION VARIABLES

```
1 int done = 0;
2 pthread_mutex_t m = PTHREAD_MUTEX_INITIALIZER;
3 pthread_cond_t c = PTHREAD_COND_INITIALIZER;
```

```
5 void thr_exit() {
6 pthread_mutex_lock(&m);
7 done = 1;
8 pthread_cond_signal(&c);
9 pthread_mutex_unlock(&m);
```

```
12 void *child(void *arg) {
13 printf("child\n");
14 thr_exit();
15 return NULL;
```

```
18 void thr_join() {
19 pthread_mutex_lock(&m);
20 while (done == 0)
21 pthread_cond_wait(&c, &m);
22 pthread_mutex_unlock(&m);
```

```
25 int main(int argc, char *argv[]) {
26 printf("parent: begin\n");
27 pthread_t p;
28 pthread_create(&p, NULL, child, NULL);
29 thr_join(p);
30 printf("parent: end\n");
31 return 0;
```

Figure 3.0: Waiting For Child: Use A Condition Variable
is executed when a thread has changed something in the program and wants to wake a sleeping thread waiting on this condition. Specifically, the POSIX calls look like this:

```
pthread_cond_wait(pthread_cond_t *c, pthread_mutex_t *m);
pthread_cond_signal(pthread_cond_t *c);
```

We often refer to these as wait() and signal() for simplicity. One thing you might notice about the wait() is that it also takes a mutex as a parameter; it assumes this mutex is locked when wait() is called. The responsibility of wait() is to release the lock and put the calling thread to sleep (atomically); when the thread wakes up (after some other thread has signaled it), it must re-acquire the lock before returning to the caller. This complexity stems from the desire to prevent certain