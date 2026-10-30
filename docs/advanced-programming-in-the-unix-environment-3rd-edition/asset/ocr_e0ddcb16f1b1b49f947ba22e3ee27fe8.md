```
int pthread_cond_broadcast(pthread_cond_t *cond);
<pthread.h>
Returns: 0 if OK, error number on failure
p. 415
```

```
int pthread_cond_destroy(pthread_cond_t *cond);
<pthread.h>
Returns: 0 if OK, error number on failure
p. 414
```

```
int pthread_cond_init(pthread_cond_t *restrict cond,
    const pthread_condattr_t *restrict attr);
<pthread.h>
Returns: 0 if OK, error number on failure
p. 414
```

```
int pthread_cond_signal(pthread_cond_t *cond);
<pthread.h>
Returns: 0 if OK, error number on failure
p. 415
```

```
int pthread_cond_timedwait(pthread_cond_t *restrict cond,
    pthread_mutex_t *restrict mutex,
    const struct timespec *restrict timeout);
<pthread.h>
Returns: 0 if OK, error number on failure
p. 414
```

```
int pthread_cond_wait(pthread_cond_t *restrict cond,
    pthread_mutex_t *restrict mutex);
<pthread.h>
Returns: 0 if OK, error number on failure
p. 414
```

```
int pthread_create(pthread_t *restrict tidp,
    const pthread_attr_t *restrict attr,
    void *(*start_routine)(void *),
    void *restrict arg);
<pthread.h>
Returns: 0 if OK, error number on failure
p. 385
```

```
int pthread_detach(pthread_t tid);
<pthread.h>
Returns: 0 if OK, error number on failure
p. 397
```

```
int pthread_equal(pthread_t tid1, pthread_t tid2);
<pthread.h>
Returns: nonzero if equal, 0 otherwise
p. 385
```

```
void pthread_exit(void *real_ptr);
<pthread.h>
p. 389
```