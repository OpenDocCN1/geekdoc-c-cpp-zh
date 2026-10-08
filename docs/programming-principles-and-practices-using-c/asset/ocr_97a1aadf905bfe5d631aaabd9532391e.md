declaration(s) of my_find(). Instead, we just don’t use the last argument. Since we don’t use it we can leave it unnamed:

```
```cpp
int my_find(vector<string> vs, string s, int)    // 3rd argument unused
{
    for (int i = 0; i<vs.size(); ++i)
        if (vs[i]==s) return i;
    return -1;
}
```
```

You can find the complete grammar for function definitions in the ISO C++ standard.

# 8.5.2 Returning a value

We return a value from a function using a return-statement:

```
```cpp
T f()      // f() returns a T
{
    V v;
    // ...
    return v;
}

T x = f();
```
```

Here, the value returned is exactly the value we would have gotten by initializing a variable of type T with a value of type V:

```
```cpp
V v;
// ...
T t(v);    // initialize t with v
```
```

That is, value return is a form of initialization.

A function declared to return a value must return a value. In particular, it is an error to “fall through the end of the function”:

```
```cpp
double my_abs(int x)    // warning: buggy code
{
    if (x < 0)
        return -x;
    else if (x > 0)
        return x;
}
    // error: no value returned if x is 0
```
```