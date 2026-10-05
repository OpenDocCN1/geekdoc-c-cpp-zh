and then this object is passed by value to a function. When the function exits, the copy’s destructor will be automatically called and the memory allocated by the original object will be freed. This will leave the original object damaged state.

# Returning Objects

A function may return an object to the caller:

```
// Returning objects from a function.
#include <iostream>
class Foo
{
    int i;
    public:
    void set(int n) { i=n; }
    int get() { return i; }
};

// forward declaration; func returns an object of type Foo
Foo func();
int main()
{
    Foo obj = func();
    std::cout << obj.get() << "\n";
}

// define func()
Foo func()
{
    Foo foo;
    foo.set(99);
    return foo;
}

// output
99
```

When an object is returned by a function, a temporary object is automatically created on the stack. It is this object that is actually returned by the function. In our example, the returned object is assigned to the local object obj (by a bitwise copy) and then the