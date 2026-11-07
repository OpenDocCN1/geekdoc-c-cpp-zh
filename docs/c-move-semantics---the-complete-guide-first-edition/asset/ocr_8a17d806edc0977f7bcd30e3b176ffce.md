# 8.3 Impact of Value Categories When Binding References

Value categories play an important role when we bind references to objects. For example, in C++98/C++03, they define that you can assign or pass an rvalue (a temporary object without a name or an object marked with `std::move()`) to a const value reference but not to a non-const value reference:

```
```cpp
std::string createString();        // forward declaration
```
```

```
```cpp
const std::string& r1{createString()};    // OK
```
```

```
```cpp
std::string& r2{createString()};           // ERROR
```
```

The typical error message printed by the compiler here is “cannot bind a non-const lvalue reference to an rvalue.”

You also get this error message with the call of `foo2()` here:

```
```cpp
void foo1(const std::string&);       // forward declaration
void foo2(std::string&);              // forward declaration
```
```

```
```cpp
foo1(std::string{"hello"});          // OK
foo2(std::string{"hello"});          // ERROR
```
```

# 8.3.1 Overload Resolution with Rvalue References

Let us see the exact rules when passing an object to a reference.

Assume we have a non-const variable `v` and a const variable `c` of a class X:

```
```cpp
class X {
    ...
};

X v{...};
const X c{...};
```
```

Table Rules for binding references lists the formal rules for binding references to passed arguments if we provide all the reference overloads of a function `f()`:

```
```cpp
void f(const X&);    // read-only access
void f(X&);          // OUT parameter (usually long-living object)
void f(X&&);         // can steal value (object usually about to die)
void f(const X&&);   // no clear semantic meaning
```
```

The numbers list the priority for overload resolution so that you can see which function is called when multiple overloads are provided. The smaller the number, the higher the priority (priority 1 means that this is tried first).

Note that you can only pass rvalues (prvalues, such as temporary objects without a name) or xvalues (objects marked with `std::move()`) to rvalue references. That is where their name comes from.

You can usually ignore the last column of the table because const rvalue references do not make much sense semantically, meaning that we get the following rules: