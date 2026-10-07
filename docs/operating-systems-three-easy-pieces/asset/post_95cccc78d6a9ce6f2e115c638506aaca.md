
In this code, after initialization of the relevant lock and condition¹, a thread checks to see if the variable ready has been yet set to something other than zero. If not, the thread simply calls the wait routine in order to sleep until some other thread wakes it.

The code to wake a thread, which would run in some other thread, looks like this:

```
pthread_mutex_lock(&lock);
ready = 1;
pthread_cond_signal(&cond);
pthread_mutex_unlock(&lock);
```

A few things to note about this code sequence. First, when signaling by modifying the global variable ready), we always make to have the lock held. This ensures that we don't accidentally introduce a race condition into our

Second, you might notice that the wait call acquires a lock as its parameter, whereas the signal call only takes a condition. The reason for this difference is that the wait, in addition to calling the condition did did not: go to sleep, releases the lock when putting caller to sleep. Imagine if it did: how could the other thread acquire the lock and signal to wake up? However, before returning after being woken, the pthread_cond.wait() re-acquires the lock, thus ensuring that any time the waiting thread is running between the lock acquire at the beginning of the wait sequence, and the lock release at the end, it holds the lock.

One last: the waiting thread checks the condition in a while loop, instead of a simple statement. When we study condition variables in a future chapter, but in general, using a while loop is the simple and safe thing to do. Although it rechecks the condition (perhaps adding a little overhead), there are pthread implementations that could spuriously wake a waiting thread; in such case, without rechecking, the waiting thread will continue thinking that the condition has changed even though it is not. It is safer to view waking up as a hint that might have changed, rather than an absolute fact.

Note that sometimes it is tempting to use a simple flag to signal between two threads, instead of a condition variable and associated lock. For example, we could rewrite the code above to look more like this in the code:

```
while (ready == 0)
    // spin
```

The associated signaling code would look like this:
ready = 1;

¹One can use pthread_cond_init() (and pthread_cond_destroy()) instead of the static initializer PTHREAD_COND_INITIALIZER. Sound like more work? It is.

# INTERLUDE: THREAD API

Don't ever do this, for the following reasons. First, it performs poorly in many cases (spinning for a long time just wastes CPU cycles). Second, it is error prone. As recent research shows [X+10], it is surprising to make mistakes when using flags (as above) to synchronize between threads; in that study, roughly half the uses of ad hoc synchronizations were buggy! Don't be lazy; use condition variables even when you can get away without doing so.

If condition variables are confusing, don't worry too much (yet) – we'll be covering them in great detail in a subsequent chapter. Until then, it should suffice to know that they exist and to have some idea how why they are used.

# 27.5 Compiling and Running

All of the code examples in this chapter are relatively easy to get up and running. To compile them, you must include the header pthread.h in your code. On the link line, you must also explicitly link with the threads library, adding the -pthread flag.

For example, to compile a simple multi-threaded program, you have now such to do the following:

```
gcc -o main.c -Wall -pthread
```

As long as main.c includes the threads header, you have now successfully compiled a concurrent program. Whether it works or not, as usual, is a matter entirely different.

# 27.6 Summary

We have introduced the basics of the pthread library, including thread creation, building mutual exclusion via locks, and signaling via condition variables. You don't need much else to write robust and efficient multi-threaded code, except patience and a great deal of care!

We now end the chapter with a set of tips that might be useful to you when you write multi-threaded code (see the aside on the following page for details). There are other aspects of the API that are interesting; if you want more information, man pthread on a Linux system to see over one hundred APIs make up the entire interface. However, the basics discussed herein should enable you to build sophisticated (and hopefully, correct and performant) multi-threaded programs. The hard part with threads is not the APIs, but rather the tricky logic of how you build concurrent programs. Read on to learn more.

# INTERLUDE: THREAD API

# ASIDE: THREAD API GUIDELINES

There are a number of small but important things to remember when you use the POSIX thread library (or really, any thread library) to build a multi-threaded program. They are:

- Keep it simple. Above all else, any code to lock or signal between threads should be as simple as possible. Tricky thread interactions lead to bugs.

- Minimize thread interactions. Try to keep the number of ways in which threads interact to a minimum. Each interaction should be carefully thought out and constructed with tried and true approaches (many of which we will learn about in the coming chapters).

- Check your return codes. Of course, in any C and UNIX programming, you should be checking each return code, and it’s true here as well. Failure to do so will result in bizarre and hard to understand behavior, making you likely to (a) scream, (b) pull some of your hair out, or (c) both.

- Be careful with how you pass arguments to, and return values from threads. In particular, any time you are passing a reference to a variable allocated on the stack, you are probably doing something wrong.

- Each thread has its own stack. As related to the point above, please remember that each thread has its own stack. Thus, if you have a locally-allocated variable inside of some function a thread is executing, it is private to that thread; no other thread can (easily) access it. To share data between threads, the values must be in the heap or otherwise some locale that is globally accessible.

- Always use condition variables to signal between threads. While it is tempting to use a simple flag, don’t do it.

- Use the manual pages. On Linux, in particular, the pthread pages are highly informative and discuss much of the nuances presented here, often in even more detail. Read them carefully!

# INTERLUDE: THREAD API

# References

- [B89] “An Introduction to Programming with Threads” by Andrew D. Birrell. DEC Technical Report, January 1989. Available: https://birrell.org/andrew/papers/035-Threads.pdf A classic but older introduction to threaded programming. Still a worthwhile read, and freely available.

- [B97] “Programming with POSIX Threads” by David R. Butenhof. Addison-Wesley, May 1997. Another one of the best on threads.

- [K96] “Programming with Threads” by a POSIX Standard for Better Multiprocessing. ” Dick Butlar, Jacqueline Farrell, Barnard Nichols. O’Reilly, September 1996 A reasonable book from the excellent, practical publishing house O’Reilly. Our bookshelves certainly contain a great deal of books from this genre, including some excellent offers on Perl, Python, and Javascript (particularly Crockford’s “Javascript: The Good Part”).

- [K+96] “Programming With Threads” by Steve Kleinman, Devang Shah, Bart Smaanders. Prentice Hall, January 1996. Probably one of the best books in this space. Get it at your local library. Or steal it from your mother. More seriously, just ask your mother for it – she’ll let you borrow it, don’t worry.

- [X+10] “Ad Hoc Synchronization Considered Harmful” by Weiwei Xiong, Soyeon Park, Jiaqi Zhang, Yuanyuan Zhou, Zhiqi Ma. OSDI 2010, Vancouver, Canada. This paper shows how seemingly simple synchronization code can lead to a surprising number of bugs. Use condition variables and do the signaling correctly!
