```
```cpp
void foo(const X&);        // for constant values (read-only access)
void foo(X&);              // for variable values (out parameters)
void foo(X&&);             // for values that are no longer used (move semantics)

template<typename T>
void callFoo(T&& arg) {          // arg is a universal/forwarding reference
    foo(std::forward<T>(arg));   // becomes foo(std::move(arg)) for passed rvalues
}

X v;
const X c;

callFoo(v);              // OK, expands to foo(arg), so it calls foo(X&)
callFoo(c);              // OK, expands to foo(arg), so it calls foo(const X&)
callFoo(X{});            // OK, expands to foo(std::move(arg)), so it calls foo(X&&)
callFoo(std::move(v));   // OK, expands to foo(std::move(arg)), so it calls foo(X&&)
callFoo(std::move(c));   // OK, expands to foo(std::move(arg)), so it calls foo(const X&)
```
```

Whatever we pass to callFoo() becomes an lvalue (because the parameter arg is an object with a name). However, the type of arg depends on what we pass:

+   - If we pass an lvalue, arg is an lvalue reference (X&), when we pass a non-const X, or const X&, when we pass a const X).
+   - If we pass an rvalue (an unnamed temporary object or an object marked with std::move()), arg is an rvalue reference (X&& or const X&&).

By using std::forward<>(), we forward the parameter with std::move() if and only if we have an rvalue reference (i.e., arg binds to an rvalue).

# 9.3  Rvalue References versus Universal References

Unfortunately, universal/forwarding references use the same syntax as ordinary value references (formally, they are special rvalue references). This is a serious source of trouble and confusion. If you see a declaration with two ampersands, you have to double-check whether a real type name or the name of a function template parameter is used.

In other words, there is a significant difference between

```
```cpp
void foo(Coll&& arg)      // arg is an ordinary rvalue reference of type Coll
```
```

and

```
```cpp
template<typename Coll>
void foo(Coll&& arg)       // arg is a universal/forwarding reference of any type
```
```

Let us discuss the differences in detail.