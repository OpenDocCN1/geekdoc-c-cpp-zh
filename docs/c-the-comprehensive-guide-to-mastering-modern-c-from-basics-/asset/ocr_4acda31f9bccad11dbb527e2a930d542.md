You start a thread by creating a std::thread object. As a constructor argument, you then pass something callable, here an instance of the BackgroundTask functor.

Note that the callable object is always copied for the new thread. Therefore, the callable object must be sensibly copyable. If you use backgroundTask for multiple jthread instances, they do not share the same instance.
[ 82 ]

It is quite common to create the callable object directly in the constructor call of jthread:

```
std::jthread myThread{BackgroundTask()}; // temp-value as constructor
argument
```

Be careful not to write BackgroundTask() here, as that does not create a temp-value but declares a function. You can completely avoid this problem by writing simple tasks as lambda expressions when you initialize the jthread:

```
// https://godbolt.org/z/nPGY4r4K
std::jthread myThread{ {
    task1();
    task2();
    task3();
}
```

This means that myThread starts a new thread that runs in parallel. In that thread, the task1, task2, and task3 functions are then executed sequentially.

# 29.1.2 Terminating a Thread Prematurely the case often