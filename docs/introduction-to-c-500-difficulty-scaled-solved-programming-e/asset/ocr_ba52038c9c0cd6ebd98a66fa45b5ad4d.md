# 25 • Namespaces, Type Cast Operators, and Smart Pointers 833

```
int main()
{
    auto sp = make_shared<int>(10);
    weak_ptr<int> wp(sp); /* The reference counter for the allocated
    memory is not increased. */

    shared_ptr<int> ptr = wp.lock(); /* Alternatively, we could write:
    auto ptr = wp.lock(); and ptr and sp point to the same memory. */
    if(ptr)
        cout << *ptr << '\\n';
    else
        cout << "Not valid memory\n";n
    return 0;
}
```

When it is declared it is initialized with sp. As we said, the reference counter for this memory does not increase, it retains 1. The direct access through wp is not allowed. We first use the lock(), which returns a shared_ptr object. If the memory pointed by the weak_ptr has not been released, the object (e.g. ptr) has a valid value and we can safely use it to access the memory. Otherwise, lock() returns an empty shared_ptr object. That is, with weak_ptr and lock() we first check if the memory can be managed and then access it. Thus, the program displays 10. In general, weak_ptr is used in advanced cases.

# THE volatile QUALIFIER

The volatile qualifier is rarely used. Typically, it is used in code that communicates with the hardware of the system. It is used to inform the compiler that the value of a variable may change, even if it does not appear to change within the program. In fact, it prevents the compiler from performing optimizations which may be undesirable. Let's look at an example:

```
int out = 0;
while(out !== 200)
{
    ... // The value of out does not change inside the program.
}
```

The condition checks if the value of out is not than 200. Because the value of out seems to remain the same, an optimizing compiler might replace this loop with an infinite loop, such as while(1). However, if out can be modified by a "hidden" entity, such as the system hardware, this optimization would affect the behaviour of the program. To prevent the compiler from optimizing the code we use the volatile qualifier in its declaration, that is, volatile int out;