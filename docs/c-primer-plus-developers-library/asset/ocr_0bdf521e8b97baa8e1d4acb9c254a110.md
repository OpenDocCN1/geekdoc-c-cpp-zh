That is, *end* points to a location one past the last value to be used. Consider the following statement:

```
string six(allS+6, allS + 10);    // ctor #6
```

Because the name of an array is a pointer, both `alls + 6` and `alls + 10` are type `char *`, so the template is used with its iter replaced by type `char *`. The first argument points to the first w in the `alls` array, and the second argument points to the space following the first well. Thus, `six` is initialized to the string "well". Figure 16.1 shows how the constructor works.

```
```cpp
char alls[] = "All's well that ends well";
string six(alls + 6, alls + 10);
range = [alls + 6, alls + 10);
```
```

![](bbox=[0.338, 0.354, 0.779, 0.439])

Figure 16.1  A string constructor using a range.

Now suppose you want to use this constructor to initialize an object to part of another string object—say, the object `five`. The following does not work:

```
string seven(five + 6, five + 10);
```

The reason is that the name of an object, unlike the name of an array, is not treated as the address of an object, hence `five` is not a pointer and `five + 6` is meaningless. However, `five[6]` is a `char` value, so `&five[6]` is an address and can be used as an argument to the constructor:

```
string seven(&five[6], &five[10]); // ctor #6 again
```

The seventh constructor copies a portion of one string object to the constructed object:

```
string eight(four, 7, 16);       // ctor #7
```

This statement copies 16 characters from `four` to `eight`, starting at position 7 (the eighth character) in `four`.

# C++11 Constructors

The `string(string && str) noexcept` constructor is similar to the copy constructor in that the new string is a copy of `str`. However, unlike the copy constructor, it doesn’t guarantee that `str` will be treated as `const`. This form of constructor is termed a *move constructor*. The compiler can use it in some situations instead of the copy constructor to