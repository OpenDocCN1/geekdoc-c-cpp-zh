block scope; therefore, instance is initialized only once. This initialization happens when the static member function getInstance (lines 10 - 14) is executed the first time.

# The volatile Variable dummy

When I compiled the program with maximum optimization, the compiler removed the call MySingleton::getInstance() in line 30 because the call has no effect; therefore, I got very fast execution but wrong performance numbers. Using the volatile variable dummy (line 12), the compiler is not allowed to optimize away the MySingleton::getInstance() call in line 30.

Here are the reference numbers for the single-threaded use-case.

![](bbox=[0.2, 0.43, 0.8, 0.53])

Meyers Singleton on Linux (single threaded)

![](bbox=[0.26, 0.58, 0.74, 0.68])

Meyers Singleton on Windows (single threaded)

The beauty of the Meyers Singleton is that it becomes thread-safe with C++11.

# 6.3.3 Thread-Safe Meyers Singleton

The C++11 standard guarantees that static variables with block scope are initialized in a thread-safe way. The Meyers Singleton uses a static variable with block scope, so we are done. The only work that is left to do is to rewrite the previously used classical Meyers Singleton for the multithreading use-case.