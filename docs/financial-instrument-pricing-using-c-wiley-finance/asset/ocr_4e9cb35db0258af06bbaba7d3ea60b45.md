This is useful code because it can be generalised to more complex applications. The main advantage is that we use atomics as a notification mechanism.

# 28.6 SMART POINTERS AND THE THREAD-SAFE POINTER INTERFACE

Shared pointers are not thread safe in general. Reading a pointer’s use-count by one thread while another thread modifies the data does not cause a race condition; however, the value may not be up to date. Data races occur if multiple threads access a non-constant member function of `std::shared_ptr<T>`. This is an undesirable feature and for this reason we use overloads of the corresponding access functions for load, store and exchange, called the *high-level interface*. We take an example to show how these functions work. We examine the following class and define aliases for readability reasons:

```
struct X
{
    double val;

    X() : val(0.0) {}
    void operator ()()
    {
        std::cout << "An X " << val << std::endl;
    }
};

template <typename T>
    using GenericPointerType = std::shared_ptr<T>;

using PointerType = GenericPointerType<X>;
```

The next step is to create smarter points of instance of struct X:

```
// Two shared ptrs s and s2
PointerType s(new X);
s->val = 3.14;
std::cout << "Use count s:" << s.use_count() << '\n';

// False
std::cout << "Atomic interface is lock free " << std::boolalpha
          << std::atomic_is_lock_free(&s) << std::endl;

PointerType s2 = nullptr;
std::atomic_store(&s2, s);
std::cout << "Use count s2,s: " << s2.use_count() << ","
          << s.use_count() << '\n';
std::cout << "Value in stored pointer s2: "
          << s2->val << std::endl; // 3.14
```