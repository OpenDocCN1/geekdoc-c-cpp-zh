```
~~~
56    t3.join();
57    t4.join();
58 }
~~~
```

The program version 5 output is:

![](bbox=[0.18, 0.232, 0.83, 0.532])

This output looks great. Now we have reached the limits of our testing methodology. There is still a tiny chance for misbehavior. The two operations “is a resource available” and “mark resource as in use” in the lock() function are atomic, but they are still two operations. Between these two operations, the scheduler can place a thread switch. And this thread switch at this most inconvenient time can produce very hard-to-find bugs in the program.

# ### 6.2.6 Correct Busy Waiting with Resource Hierarchy

Thankfully all current computers have an atomic operation "test the resource and if the test is positive mark resource as in use". In the programming language C++, the atomic_flag type makes this special "test and set" operation available for us. File dp_6.cpp has the first correct solution for the dining philosophers problem: