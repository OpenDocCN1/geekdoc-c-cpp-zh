noexcept = 0;

};

If you look at the source code in Command.h, you will also see a virtual deallocate() function. This function is exclusively used for plugins, and its addition to the interface will be discussed in Chapter 7.

# MODERN C++ DESIGN NOTE: THE OVERRIDE KEYWORD

the override keyword was introduced in C++11. Functionally, it prevents a common error that is often surprising to new C++ programmers. Consider the following code snippet:

```
class Base
{
public:

virtual void foo(int);
};
```

class Derived : public Base