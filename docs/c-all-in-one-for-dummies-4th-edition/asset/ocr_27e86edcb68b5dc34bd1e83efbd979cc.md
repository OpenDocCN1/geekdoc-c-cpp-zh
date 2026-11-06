is expected. To get past this problem, you can use `noexcept()` to disregard the exception, like this:

```
```cpp
cout << noexcept(ChangeNum(5,5)) << endl;
```
```

Instead of an exception, the code outputs the captured value of `Total`, which is 0. This is the operator form of `noexcept()`. You also have access to a specifier version of `noexcept()` that isn’t guaranteed to work with older versions of C++. It looks like this:

```
```cpp
auto ChangeNum = [Total](auto Type, int Value) mutable
    noexcept { ... }
```
```

In this case, the inability to throw an exception affects the lambda expression as a whole, along with any functions that it calls. Of course, now you don’t know when exceptional conditions really do happen — the code simply outputs whatever answer it can, which is likely incorrect, when an unforeseen condition occurs.