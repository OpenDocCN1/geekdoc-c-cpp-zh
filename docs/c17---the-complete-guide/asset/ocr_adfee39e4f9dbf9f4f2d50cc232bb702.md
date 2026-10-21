```
std::cout << *ip << '\n';
}
else {
    std::cout << "alternative with index 1 not set\n";
}
```

Here, if with initialization is used, which separates the initialization from the condition check.
You can also use the initialization as a condition directly:

```
if (auto ip = std::get_if<1>(&var)) {
    std::cout << *ip << '\n';
}
else {
    std::cout << "alternative with index 1 not set\n";
}
```

Another way to access the values of the different alternatives is using variant visitors.

# Changing the Value

Assignment and emplace() operations exist corresponding to the initializations:

```
std::variant<int, int, std::string> var; // sets first int to 0, index()==0
var = "hello";                         // sets string, index()==2
var.emplace<1>(42);                    // sets second int, index()==1
```

Note that operator= will directly assign the new value if the variant currently holds the matching alternative. emplace() always destroys the old value and assigns the new value.

You can also use get<>() or get_if<>() to assign a new value to the current alternative:

```
std::variant<int, int, std::string> var; // sets first int to 0, index()==0
std::get<0>(var) = 77;                  // OK, because first int already set
std::get<1>(var) = 99;                  // throws exception (other int currently set)
```

```
if (auto p = std::get_if<1>(&var); p) { // if second int set
    *p = 42;                            // modify it
}
```

Another way to modify the values of the different alternatives is using variant visitors.

# Comparisons

For two variants of the same type (i.e., they have the same alternatives in the same order), you can use the usual comparison operators. The operators act according to the following rules:

+   - A variant with a value of an earlier alternative is less than a variant with a value with a later alternative.