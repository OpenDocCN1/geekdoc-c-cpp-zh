# INTERLUDE: THREAD API

Don't ever do this, for the following reasons. First, it performs poorly in many cases (spinning for a long time just wastes CPU cycles). Second, it is error prone. As recent research shows [X+10], it is surprising to make mistakes when using flags (as above) to synchronize between threads; in that study, roughly half the uses of ad hoc synchronizations were buggy! Don't be lazy; use condition variables even when you can get away without doing so.

If condition variables are confusing, don't worry too much (yet) – we'll be covering them in great detail in a subsequent chapter. Until then, it should suffice to know that they exist and to have some idea how why they are used.

# 27.5 Compiling and Running

All of the code examples in this chapter are relatively easy to get up and running. To compile them, you must include the header pthread.h in your code. On the link line, you must also explicitly link with the threads library, adding the -pthread flag.

For example, to compile a simple multi-threaded program, you have now such to do the following:

```
prompt gcc -o main.c -Wall -pthread
```

As long as main.c includes the threads header, you have now successfully compiled a concurrent program. Whether it works or not, as usual, is a matter entirely different.

# 27.6 Summary

We have introduced the basics of the pthread library, including thread creation, building mutual exclusion via locks, and signaling via condition variables. You don't need much else to write robust and efficient multi-threaded code, except patience and a great deal of care!

We now end the chapter with a set of tips that might be useful to you when you write multi-threaded code (see the aside on the following page for details). There are other aspects of the API that are interesting; if you want more information, man pthread on a Linux system to see over one hundred APIs make up the entire interface. However, the basics discussed herein should enable you to build sophisticated (and hopefully, correct and performant) multi-threaded programs. The hard part with threads is not the APIs, but rather the tricky logic of how you build concurrent programs. Read on learn more.