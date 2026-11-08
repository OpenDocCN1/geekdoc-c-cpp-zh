And indeed, with a few small (but important) differences, you can rewrite a method and turn it into a free function by making the implicit this parameter explicit.

```
string greeting(Person * const p) {  // implicit parameter made explicit
    return format("Hello {} from {}", p->name_, p->city_);
}
```

**Listing 12.7** How to separate methods and data from each other.

You must not name the parameter `this` because this is a keyword in C++; here, it is called `p`.

There are cases where you also need to use `this->` for attribute access in a method—namely, when two or more identical identifiers conflict. Then you need to be explicit:

```
// https://godbolt.org/z/hEvqWqqc6
int value = 5;                         // global variable
struct Wrap {
    int value = 3;                     // data field
    void set(int value) {              // parameter
        this->value = value + ::value;
    }
};
```

Here, `this->value` refers to the data field of Wrap, `value` refers to the parameter, and `::value` refers to the global variable.

It is a good idea to bundle data and functions together. Whether you should always and consistently do this is a design question. For example, C++ allows the extension of existing functionality through new overloads of free functions, not just by adding methods to an existing data type. The operator<< for `std::ostream` is a good example of this.

# 12.4 The Better “print”

It pains me every time I present you with something as impractical as `print` as an example of a function. There are several important things to note about `print` as a method or the corresponding free function, simple as it may be. You now know enough about C++ that I can explain the better alternative to you. Take another look at the method:

```
void Person::print() {
    cout << format("{} ({}) from {}", name_, age_, city_);
}
```