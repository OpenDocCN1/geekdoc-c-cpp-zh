nothing more than the address of the `end1` function. And the address is of type `omanip`. Here's the `operator<<` function in its entirety:

```
```cpp
ostream& operator<<(ostream &out, omanip func) {
    return (*func)(out);
}
```
```

The `func` parameter contains the address of `end1`. The code shown ends up calling `end1` and supplying it with `out`. You could use this approach for any function that matches the `omanip` type. Using this approach relies on function pointer syntax. As long as you know what is involved, you normally don't need to delve too far into the details. However, if you'd like more details, check out the article at https://www.cprogramming.com/tutorial/function-pointers.html.

This isn't the only way to accomplish coding a manipulator, as explained in the following section, "Writing your own manipulator." That section uses a slightly different approach that works equally well. But the technique described in this section is quite common, and you need to know how it works.

# # Writing your own manipulator

You can write your own manipulators in several ways. The goal is to allow for this type of code:

```
```cpp
cout << mymanipulator;
```
```

and this line causes a function such as the following to get called:

```
```cpp
ostream &operator << (ostream &out, somespecialtype a);
```
```

Several `operator<<` functions are natively available; ultimately, they differ in the second parameter type, `somespecialtype`. Whatever `mymanipulator` is, it must be the `somespecialtype` type as well. This type must be unique or the compiler will complain.

The "What's a manipulator?" section (earlier in this chapter) gives you the details on how the `end1` manipulator works, but that amount of detail is a bit too complicated. The example in this section creates a unique type, and the manipulator is an object of that type. As with other manipulators, function pointers work well. But for the function pointer to be unique, its parameter types must be unique. The example uses that as the parameter for the function, like this:

```
```cpp
struct FullOverManip {};
void FullOverInfo(FullOverManip x) {}
```
```