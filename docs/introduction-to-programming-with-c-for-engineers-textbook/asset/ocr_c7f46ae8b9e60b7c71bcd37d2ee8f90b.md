On line [15], a new object x is created with the help of auto. As we already know, it will be of char type, since 'c' is const char but auto will leave only char. However, on line [18], we wish to define a vector that stores objects of the same type as x. Let’s assume that we do not know explicitly what type it is: how do we write it? For this purpose, we can use `decltype(x)`, which will return the type of object x in this case. This works fine, so vec will be created, containing 10 elements, each initialized with a copy of x (Table 3.4). We can easily access each element of a vector in the for loop, as on line [21]. Here auto again simplifies writing the code, although an explicit type can also be used, as follows:

```
```cpp
// The same with explicit type
for( char k : vec )
    cout << k;
```
```

But auto is more flexible compared to providing an explicit type. As we have already mentioned, if auto is used, then a relevant but pure type will be chosen. However, we can easily define a constant type, as in the following code lines:

```
```cpp
// Now k will be const char type
for( const auto k : vec )
    cout << k;
```
```

Or we can define a constant reference type:

```
```cpp
// Now k will be const char reference type
for( const auto& k : vec )
    cout << k;
```
```

This allows for indirect access to the elements of vec, to avoid making copies of them. Here we signal a possibility; a full discussion of references is postponed until Section 3.11. But the results of all the previous for loops are to print this:

```
```text
cccccccccc
```
```

Using `auto` can be tricky in some cases. For example, what type do we expect in the following example?

```
```cpp
auto text { "The quick brown fox" };

// What type is text? Do we need to know?
cout << text << endl;
```
```

The type of text is not `std::string`, neither `char*` - it is `const char*`. However, if we used the following initialization

```
```cpp
auto text = { "The quick brown fox" };
```
```