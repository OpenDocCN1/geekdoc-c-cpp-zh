# 7.10  Arbitrary Number of Arguments

The add function discussed previously can take up to five arguments, and it would certainly not be difficult for you to extend this to 20 or even 100 default arguments. I don't want to leave the example as is without giving you a glimpse that you can handle an *arbitrary* number of arguments. If you want an add function that takes an arbitrary number of int values, take a detour via `std::initializer_list`:

```
```cpp
int add(std::initializer_list<int> ns) {
    return std::accumulate(begin(ns), end(ns), 0); // or a for loop
}
```
```

Now, when calling, you just need to add a few curly brackets around the arguments, but they can be any number. For example:

```
```cpp
add({1,2,3,4,5,6,7,8,9})
```
```

# 7.11  Alternative Notation for Function Declaration

There is another way to write the function header with auto and ->, which is at least equivalent, if not better:

```
```cpp
auto FunctionName(ParameterType ParameterName,...) -> ReturnType
```
```

For Listing 7.2, it would look like this:

```
```cpp
auto func() -> int;
auto func() -> std::string;
auto func() -> void;
auto func() -> std::pair<int,std::string>;
auto func() -> vector<int>;
auto func() -> const vector<int>&;
```
```

**Listing 7.11** Alternative syntax for function declarations with trailing return type.

The advantage is that you can recognize the function name better when the return type becomes more complex. This can happen with templates that have multiple type arguments. For programmers who are used to C, this notation looks very strange, but there is really no reason not to use it—except that it will probably take a long time to catch on, if at all.

From C++14 onward, you can omit the return type in function definitions and let the compiler deduce it instead. The compiler then deduces the type based on the first `return` statement.