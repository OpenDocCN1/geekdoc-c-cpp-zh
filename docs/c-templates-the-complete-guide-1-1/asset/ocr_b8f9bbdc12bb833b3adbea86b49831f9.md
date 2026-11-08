Click here to view code image

```
```cpp
template<typename T>
void foo(T arg1, T arg2)
{
  ...
}
foo("hi", "guys"); //compiles, but...
```
```

Then, that doesn't mean that all problems are gone. Even worse, compile-time problems may have become run-time problems. Consider the following code, where we compare the passed argument using `ptr==nullptr`:

Click here to view code image

```
```cpp
template<typename T>
void foo(T arg1, T arg2)
{
  if (arg1 == nullptr) { //compare addresses of passed arrays
    ...
  }
}
foo("hi", "guys"); //compiles, but...
```
```

As written, you have to know that you should interpret the passed character pointers as strings. But that's possibly the case anyway, because the template also is dealt with arguments coming from string literals that have been decayed already (e.g., by calling from another function or by value or by using `std::array/std::span`, both of which are a typical way to pass a sequence of chars).

Nevertheless, in many cases dealing with `foo()` carefully, especially for checking whether a pointer is passed or a sequence of pointers or even a pointer to an array, and the other expecting the argument to have converted to the same type. One typical way is to prefer forwarding, if you want to use a forwarding function to deal with multiple types. Another approach is to use type traits. In those cases, you might explicitly decide the arguments using the type traits `std::is_pointer<>` (which is also true for pointers, see Section 7.5 on page 278).

Note that other type traits such as `std::is_array<>` simply don't apply, such as for `std::is_pointer<>` (see Section 7.5 on page 279) and Section D.6 on page 716).

# 7.4.1 SPECIAL IMPLEMENTATIONS FOR STRING LITERALS AND RAW ARRAYS

You might have to distinguish your implementation according to whether a pointer or an array was passed. That, of course, requires that a passed array wasn't decayed yet.

To distinguish those cases, you have to detect whether arrays are passed. Basically, there are two options:

+   - You can declare template parameters so that they are only valid for arrays:

Click here to view code image

```
```cpp
template<typename T, int sz>
void foo(T (&arg1)[sz]) 
{
  ...
}
foo("hi", "guys"); // OK (deduce T as const char, sz as 3)
```
```

+   - You can use type traits to detect whether an array (or a pointer) was passed:

Click here to view code image

```
```cpp
template<typename T>
void foo(T arg1, T arg2)
{
  if (std::is_array<T>::value) { //compiles for arrays of different type
    ...
  }
}
```
```

Due to these special handling, often the best way to deal with arrays in templates is to use `std::array` or `std::span`. Another benefit of `std::array` is that it does not support the misuse of the call. However, all this is not a general guarantee. In fact, arrays, like any string literal are raw arrays, so we always have to take them into account.

# 7.5 DEALING WITH RETURN VALUES

For return values, you can also decide between returning by value or by reference. However, returning a reference has the potential of a nasty side effect. The caller might be able to modify an object of your function. There are a few cases where returning references is common programming practice:

+   - Returning elements of containers or strings (e.g., by `operator[]` or `front()`)
+   - Granting write access to class members
+   - Returning objects for chained calls (e.g., `operator<<` and `operator>>` for streams and `operator=` for class objects in general)