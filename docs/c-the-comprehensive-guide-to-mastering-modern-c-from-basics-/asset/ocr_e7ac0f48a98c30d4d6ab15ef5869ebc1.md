exception passes through multiple constructors on the stack (the list of current function calls) upward without being caught by a matching catch, then all previous constructions are undone. Only exactly then, when a constructor has been completely executed, the object considered valid and fully created.

A small, lean example class that is only supposed to encapsulate a character buffer could look like the following listing.

```
// https://godgodbolt.org/z/9eeG575Wz
struct Buffer {
    const char *data;
    explicit Buffer(unsigned sz) : data(new char[sz]) {}
    ~Buffer() { delete data; }
    Buffer(const Buffer&) = delete;
    Buffer& operator=(const Buffer&) = delete;
};
```

# **Listing 17.5** An RAII character buffer class.

It should be mentioned that—true to the idea that there are “sixteen ways to stack a cat”—the same task could be better accomplished using unique_ptr<char[]>; this is just a simple example.

In C, this would usually involve a malloc, and (careful or paranoid{43 }) programmers would need to check the return value to see if the memory was allocated correctly. If not, the process must be aborted somehow. In C++, new always returns a valid pointer or throws a bad_alloc exception. So there are two possible outcomes from the constructor;[ 44 ]