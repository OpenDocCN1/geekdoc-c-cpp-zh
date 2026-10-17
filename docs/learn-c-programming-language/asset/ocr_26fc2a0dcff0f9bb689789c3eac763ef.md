```
```cpp
vals[4] = 50
```
```

When returning a reference, be careful that the object being referred to does not go out of scope. So it is not legal to return a reference to local var. But you can always return a reference on a static variable.

```
```cpp
int& func() {
    int q;

    //! return q; // Compile time error

    static int x;

    return x;    // Safe, x lives outside this scope
}
```
```