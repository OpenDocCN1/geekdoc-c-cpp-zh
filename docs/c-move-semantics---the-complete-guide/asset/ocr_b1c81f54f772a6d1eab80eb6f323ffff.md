# Chapter 11

# Perfect Passing with auto&&

After discussing the usual case of move semantics in generic code, perfect forwarding a parameter, we now have to talk about dealing with return values perfectly. In this chapter, we discuss how to forward return values perfectly to somewhere else. For this purpose, we introduce `auto&&` as another way to declare a *universal reference* (again also called *forwarding reference*). However, we also discuss applications of `auto&&` that have nothing to do with forwarding values.

The next chapter then discusses how to perfectly return values.

# 11.1  Default Perfect Passing

We often have to pass a return value to another function:

```
```cpp
// pass return value of compute() to process():
process(compute(t));  // OK, uses perfect forwarding of returned value
```
```

In non-generic code, you know the types involved. However, in generic code, you want to make sure that the return value of `compute()` is perfectly passed to `process()`.

The good news is: if you pass a return value to another function directly, the value is passed perfectly, keeping its type and value category. You do not have to worry about move semantics; it will automatically be used if supported.

# 11.1.1  Default Perfect Passing in Detail

Here is a complete example:

```
```cpp
#include <iostream>
#include <string>

void process(const std::string& t) {
    std::cout << "process(const std::string&)\n";
}
```
```