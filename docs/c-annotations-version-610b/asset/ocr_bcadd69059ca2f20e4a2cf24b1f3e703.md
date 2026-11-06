```
```cpp
{
    int x;

    increase(x);          // passed as reference
}
```
```

It is arguable whether code such as the above should be preferred over C’s method, though. The statement `increase(x)` suggests that not x itself but a *copy* is passed. Yet the value of x changes because of the way `increase()` is defined. However, references can also be used to pass objects that are only inspected (without the need for a copy or a const *) or to pass objects whose modification is an accepted side-effect of their use. In those cases using references are strongly preferred over existing alternatives like copy by value or passing pointers.

Behind the scenes references are implemented using pointers. So, as far as the compiler is concerned references in C++ are just const pointers. With references, however, the programmer does not need to know or to bother about levels of indirection. An important distinction between plain pointers and references is of course that with references no indirection takes place. For example:

```
```cpp
extern int *ip;
extern int &ir;

ip = 0;      // reassigns ip, now a 0-pointer
ir = 0;      // ir unchanged, the int variable it refers to
             // is now 0.
```
```

In order to prevent confusion, we suggest to adhere to the following:

+   - In those situations where a function does not alter its parameters of a built-in or pointer type, value parameters can be used:

```
```cpp
void some_func(int val)
{
    cout << val << '\n';
}

int main()
{
    int x;

    some_func(x);        // a copy is passed
}
```
```

+   - When a function explicitly must change the values of its arguments, a pointer parameter is preferred. These pointer parameters should preferably be the function’s initial parameters. This is called *return by argument*.

```
```cpp
void by_pointer(int *valp)
{
    *valp += 5;
}
```
```

+   - When a function doesn’t change the value of its class- or struct-type arguments, or if the modification of the argument is a trivial side-effect (e.g., the argument is a stream) references can be used. Const-references should be used if the function does not modify the argument:

```
```cpp
void by_reference(string const &str)
{
    cout << str;    // no modification of str
}
```
```