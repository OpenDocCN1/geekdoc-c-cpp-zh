```
```cpp
std::thread t3{[]{std::cout << "Hello from a lambda." << '\\n';}};

t1.join();
t2.join();
t3.join();

std::cout << '\\n';

};
```
```

All three threads (t1, t2, and t3) write their messages to the console. The work package of thread t2 is a function object (lines 10 - 15), the work package of thread t3 is a lambda function (line 26). In lines 28 - 30, the main thread is waiting until its children are done.

Let’s have a look at the output. This is more interesting.

![](bbox=[0.267, 0.41, 0.73, 0.73])

Creation of threads with various callables

The three threads are executed in an arbitrary order. Even the three output operations can interleave.

In our case, the child’s creator is the main thread, is responsible for the child’s lifetime.

# 3.1.2 Thread Lifetime

The parent has to take care of its children. This simple principle has big consequences for the lifetime of a thread. This small program starts a thread that displays its id.