# MULTIPROCESSOR SCHEDULING (ADVANCED)

```
1  typedef struct __Node_t {
2      int        value;
3      struct __Node_t *next;
4  } Node_t;
5
6  int List_Pop() {
7      Node_t *tmp = head;      // remember old head
8      int value = head->value;  // ... and its value
9      head = head->next;      // advance head to next pointer
10     free(tmp);               // free old head
11     return value;          // return value at head
12 }
```

Figure 10.3: Simple List Delete Code

Thread 1 executes the first line, it will have the current value of head stored in its tmp variable; if Thread 2 executes the first line as well, it will also have the same value of head stored in its own private variable (tmp is allocated on the stack, and thus each thread will have its own storage for it). Then, instead of each removing an element from the list, each thread will try to remove the same head element, leading to all sorts of problems (such as an attempted double free of the head at Line 10, as well as potentially returning the same data twice).

The solution, of course, is to make routines correct via locking. In this case, allocating a simple mutex (e.g., thread_mutex.tm) and adding a lock(&m) at the beginning of the routine and an unlock(&m) at the end will solve the problem, ensuring that the code will work as desired. Unfortunately, as we will see, this approach is not without problems, in particular with regards to performance. Specifically, as the number of CPUs grows, access to a synchronized shared data structure becomes quite slow.

# 10.3 One Final Issue: Cache Affinity

One issue arises in building a multiprocessor cache scheduler, known as cache affinity [TC95]. This notion is simple: a process, when run on a particular CPU, builds a fair bit of state in the caches (and TLBs) of the CPU. The next time the process runs, it is advantageous to run it on the same CPU, as it will run faster if some of its state is already present in the caches on that CPU. If, instead, one runs a process on a different CPU each time, the performance of the process will be worse, as it will have to reload its state each time it runs (note it will run correctly on the cache coherence protocols of the hardware). Thus, a multiprocessor scheduler should consider cache affinity when making its scheduling decisions, perhaps preferring to keep a process on the same CPU if at all possible.