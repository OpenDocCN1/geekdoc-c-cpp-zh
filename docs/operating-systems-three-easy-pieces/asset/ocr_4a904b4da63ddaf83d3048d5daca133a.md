# INTERLUDE: THREAD API

The routines should be easy to understand and use. When you have a region of code that is a critical section, and thus needs to be protected to ensure correct operation, locks are quite useful. You can probably imagine what the lock looks like:

```
pthread_mutex_t lock;
pthread_mutex_lock(&lock);
x = x + 1; // or whatever your critical section is
pthread_mutex_unlock(&lock);
```

The intent of code is as follows: if no other thread holds the lock when pthread_mutex_lock is called, the thread will acquire the lock and enter the critical section. If another thread does indeed hold lock, the trying to grab the lock will not return from the call until it has acquired the lock or that thread holding the lock has released it via the unlock call). Of course, many threads may be waiting inside the lock acquisition function at a given time; only the thread with the lock acquired, would call unlock.

Unfortunately, code is broken, in two ways. The first problem is a lock of proper initialization. All locks must be properly initialized in order to guarantee that they have the correct values to work with and work as desired when lock and unlock are called.

With POSIX threads, there are two ways to initialize locks. One way is to use PTHREAD_MUTEX_INITIALIZER, as follows:

```
pthread_mutex_t lock = PTHREAD_MUTEX_INITIALIZER;
```

Doing sets lock to the default values and makes the lock usable. The dynamic way to do it (i.e., at run time) is to make a call to pthread_mutex_init(), as follows:

```
int rc = pthread_mutex_init(&lock, NULL);
asert(rc == 0); // always check success!
```

The first argument to this routine is the address of the lock itself, whereas the second is an optional set of attributes. Read more about passing NULL uses the defaults. Other way works, but we usually use the dynamic (lock) method. That corresponding call to pthread_mutex_destroy() should also be made, when you are done with the lock; see the main page for all details.

The second problem with the code above is that it fails to check error when calling lock and unlock. Unlike virtually any library routine you call in a UNIX system, these routines can also fail! If your code doesn't properly check error code, it will happen silently, in this case could allow multiple threads into a critical section. Minimally, use wrappers, which assert that the routine succeeded, as shown in Figure 27.4 (page 325); more sophisticated (non-toy) programs, which can't simply exit when something goes wrong, check for failure and do something appropriate when a call does not succeed.

OPERATING SYSTEMS [Version 1.01]

WWW.OSTEP.ORG