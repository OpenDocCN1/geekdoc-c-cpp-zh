
# Homework (Code)

In this homework, you'll gain some experience with writing concurrent code and measuring its performance. Learning to build code that performs well is a critical skill and thus gaining a little experience here it is quite worthwhile.

# Questions

- 1. We'll start by redoing the measurements within this chapter. Use the call `gettimeofday()` to measure time within your program. How accurate is this timer? What is the smallest interval it can measure? Gain confidence in its workings, as we will need it in all questions. You can also look into other timers, such as the cycle counter available on x86 using `rdtsc` instruction.

- 2. Build a simple concurrent counter and measure how long it takes to increase the counter many times as the number of threads increases. How many CPUs are available on the system you are using? Does this number impact your measurements at all? 

- 3. Next, build a version of the sloppy counter. Once again, measure its performance as the number of threads varies, as well as the. Do the numbers match what you see in the chapter?

- 4. Build a version of a linked list that uses hand-over-hand locking [MS04], as cited in the chapter. You should read the first paper to understand how it works, and then implement it. Measure its performance. When does a hand-over-hand list work better than a standard list as shown in the chapter?

- 5. Pick your favorite interesting data structure, such as a B-tree or other slightly more interested structure. Implement it, and start with a simple locking strategy such as a single lock. Measure its performance as the number of concurrent threads increases.

- 6. Finally, think of a more interesting locking strategy for this favorite data structure of yours. Implement it, and measure its performance. How does it compare to the straightforward locking approach?

# Condition Variables

Thus far we have developed the notion of a lock and seen how one can be properly built with the right combination of hardware and OS support. Unfortunately, locks are not the only primitives that are needed to build concurrent programs.

In particular, there are many cases where a thread wishes to check whether a condition is true before continuing its execution. For example, a parent thread might wait for a child thread that has completed before continuing (this is often called a join()); how should such a wait be implemented? Let's look at Figure 30.1.

```
void *child(void *arg) {
    printf("child\n");
    // XXX to indicate we are done?
    return NULL;
}

int main(int argc, char *argv[]) {
    printf("parent: begin\n");
    pthread_t c;
    pthread_create(&c, NULL, child, NULL); // create child
    // XXX to wait for child?
    printf("parent: end\n");
    return 0;
}
```

> Figure 30.1: A Parent Waiting For Its Child

What we would like to see here is the following output:
parent: begin
child
parent: end

We could try using a shared variable, as you see in Figure 30.2. This solution will generally work, but it is hugely inefficient as the parent spins

# CONDITION VARIABLES

```
volatile int done = 0;
void *child(void *arg) {
    printf("child\n");
    done = 1;
    return NULL;
}

int main(int argc, char *argv[]) {
    printf("parent: begin\n");
    pthread_t c;
    pthread_create(&c, NULL, NULL, NULL); // create child
    // spin
    printf("parent: end\n");
    return 0;
}
```

Figure 30.2: Parent Waiting For Child: Spin-based Approach and wastes CPU time. What we would like instead is some way to put the parent sleep until the condition we are waiting for (e.g., the child doing execution) comes.

> THE CRUX: HOW TO WAIT FOR A CONDITION
In multi-threaded programs, it is often useful for a thread to wait for some condition to become true before proceeding. The simple approach, of just spinning until the condition becomes true, is grossly inefficient and wastes CPU cycles, and in some cases, can be incorrect. Thus, how should a thread wait for a condition?

# 30.1 Definition and Routines

To wait for a condition to become true, a thread can make use of what is known as a condition variable. A condition variable enables that threads can put themselves on some state of execution (i.e., some condition) is not as desired (by waiting on the condition); some other thread, when it changes said, can wake one (or more) of those waiting threads and allow them to continue (signaling on the condition). The idea goes back Dijkstra's use of "private semaphores" [D68]; a similar idea was later named a "condition variable" by Hoare in his monitors [H74].

To declare such condition variable, one writes something like this: pthread_cond_t c, which declares c as a condition variable (note: proper initialization is also required). A condition variable has two operations associated with it: wait() and signal(). The wait() call is executed when a thread wants to put itself to sleep; the signal() call

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
10 return;
}
```

```
12 void *child(void *arg) {
13 printf("child\n");
14 return NULL;
15 }
```

```
18 void thr_join() {
19 pthread_mutex_lock(&m);
20 while (done == 0) {
21 pthread_cond_wait(&c, &m);
22 }
23 pthread_mutex_unlock(&m);
24 }
```

```
25 int main(int argc, char *argv[]) {
26 printf("parent: begin\n");
27 pthread_t c;
28 pthread_create(&c, NULL, child, NULL);
29 thr_join();
30 printf("parent: end\n");
31 return 0;
}
```

> Figure 30.3: Waiting For Child: Use Condition Variable

We often refer to these as wait() and signal(). One thing you might notice about wait() is that it also takes a mutex as a parameter; it assumes the lock is held when wait() is called. This complexity stems from the desire to prevent race conditions from occurring when a thread is trying to sleep.

Specifically, the POSIX calls look like this:

```
pthread_cond_wait(&c, &m);
pthread_cond_signal(&c);
```

This wakes the parent thread; this code sets the state variable `done`, and signals the parent waiting. Finally, the parent will run (returning from wait() with the lock), unlock the lock, and print the final message-end.

There are two cases to consider. In the first, the parent creates the thread but continues running itself calls `thr_join()` to wait for the child. In this case, it will acquire the lock, check if the child is done (it is not), and put itself to sleep by calling `wait()` (hence the lock). The child will eventually run, print the message "child", and call `thr_exit()` to wake the parent.

In the second case, the child immediately upon creation, sets `done` to 1, calls a waking thread (but there is none, so it just returns), and the parent calls `thr_join()`, sees `done` is 1, and thus does not wait and returns.

One last note: you might observe that the parent uses a `while` loop to check if an statement is done when deciding to wait on the condition. While this does not seem strictly necessary per logic of the program, it is always a good idea, as we will see.

To make sure you understand the importance of each piece of `thr_join()` code, let's try a few implementation. First, you might be wondering if we need the state variable `done`. What if the code looked like the example below? (Figure 30.4)

Unfortunately this approach is broken. The child runs immediately and calls `thr_exit()` immediately; in this case, the child will signal, but there is no thread asleep on the condition. When the parent runs, it will simply call wait and be stuck; no thread will ever wake. From this example, you should appreciate the importance of the state variable `done`; it records the value of threads that are interested in knowing. Sleeping, waking, and locking all are built around it.

```
void thr_exit() {
    pthread_mutex_lock(&m);
    pthread_cond_signal(&c);
    pthread_mutex_unlock(&m);
}

void thr_join() {
    pthread_mutex_lock(&m);
    pthread_cond_wait(&c, &m);
    pthread_mutex_unlock(&m);
}
```

Figure 30.4: Parent Waiting: No State Variable

OPERATING SYSTEMS [Version 1.01]
WWW.OSTEP.ORG
