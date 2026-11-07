
## std::move() for Reference or Static Members

If the members are references or static, different rules apply.² A reference or static member of an rvalue is still an lvalue. Again, this rule reflects that the value of such a member is not really part of the object. Saying “I no longer need the value of the object” should not imply “I no longer need the value (of a member) that is not part of the object.”

Therefore, it makes a difference how you use `std::move()` if you have reference or static members:

- Using `std::move()` for the *object* has no effect:

  ```cpp
  struct S {
      static std::string statString;  // static member
      std::string& refString;         // reference member
  };

  S obj;
  ...
  coll.push_back(std::move(obj).statString);  // copies statString
  coll.push_back(std::move(obj).refString);   // copies refString
  ```

- Using `std::move()` for the *members* has the usual effect:

  ```cpp
  struct S {
      static std::string statString;
      std::string& refString;
  };
  S obj;
  ...
  coll.push_back(std::move(obj).statString);  // moves statString
  coll.push_back(std::move(obj).refString);   // moves refString
  ```

Whether such a move is useful is a different question. Stealing the value of a static member or referenced member means that you modify a value outside the object you use. It might make sense, but it could also be surprising and dangerous. Usually, a type S should better protect access to these members.

In generic code, you might not know whether members are static or references. Therefore, using the approach to mark the object with `std::move()` is less dangerous, even though it looks weird:

```cpp
coll.push_back(std::move(obj).mem1);  // move value, copy reference/static
coll.push_back(std::move(obj).mem2);  // move value, copy reference/static
```

In the same way, `std::forward<>()`, which we introduce later, can be used to perfectly forward members of objects. See *basics/members.cpp* for a complete example.

² Thanks to Andrey Upadyshev for pointing this out.

## 8.3 Impact of Value Categories When Binding References

Value categories play an important role when we bind references to objects. For example, in C++98/C++03, they define that you can assign or pass an rvalue (a temporary object without a name or an object marked with `std::move()`) to a const value reference but not to a non-const value reference:

```cpp
std::string createString();        // forward declaration

const std::string& r1{createString()};    // OK

std::string& r2{createString()};           // ERROR
```

The typical error message printed by the compiler here is “cannot bind a non-const lvalue reference to an rvalue.”

You also get this error message with the call of `foo2()` here:

```cpp
void foo1(const std::string&);       // forward declaration
void foo2(std::string&);              // forward declaration

foo1(std::string{"hello"});          // OK
foo2(std::string{"hello"});          // ERROR
```

### 8.3.1 Overload Resolution with Rvalue References

Let us see the exact rules when passing an object to a reference.

Assume we have a non-const variable `v` and a const variable `c` of a class X:

```cpp
class X {
    ...
};

X v{...};
const X c{...};
```

Table Rules for binding references lists the formal rules for binding references to passed arguments if we provide all the reference overloads of a function `f()`:

```cpp
void f(const X&);    // read-only access
void f(X&);          // OUT parameter (usually long-living object)
void f(X&&);         // can steal value (object usually about to die)
void f(const X&&);   // no clear semantic meaning
```

The numbers list the priority for overload resolution so that you can see which function is called when multiple overloads are provided. The smaller the number, the higher the priority (priority 1 means that this is tried first).

Note that you can only pass rvalues (prvalues, such as temporary objects without a name) or xvalues (objects marked with `std::move()`) to rvalue references. That is where their name comes from.

You can usually ignore the last column of the table because const rvalue references do not make much sense semantically, meaning that we get the following rules:

| Call | `f(X&)` | `f(const X&)` | `f(X&&)` | `f(const X&&)` |
|---|---:|---:|---:|---:|
| `f(v)` | 1 | 2 | no | no |
| `f(c)` | no | 1 | no | no |
| `f(X{})` | no | 3 | 1 | 2 |
| `f(move(v))` | no | 3 | 1 | 2 |
| `f(move(c))` | no | 2 | no | 1 |

*Table 8.1. Rules for binding references*

- A non-const lvalue reference takes only non-const values.
- An rvalue reference takes only non-const rvalues.
- A const lvalue reference can take everything and serves as the fallback mechanism in case other overloads are not provided.

The following extract from the middle of the table is the rule for the fallback mechanism of move semantics:

| Call | `f(const X&)` | `f(X&&)` |
|---|---:|---:|
| `f(X{})` | 3 | 1 |
| `f(move(v))` | 3 | 1 |

If we pass an rvalue (temporary object or object marked with `std::move()`) to a function and there is no specific implementation for move semantics (declared by taking an rvalue reference), the usual copy semantics is used, taking the argument by const&.

Please note that we will extend this table later when we introduce universal/forwarding references.

There we will also learn that sometimes, you can pass an lvalue to an rvalue reference (when a template parameter is used). Be aware that not every declaration with && follows the same rules. The rules here apply if we have a *type* (or type alias) declared with &&.

### 8.3.2 Overloading by Reference and Value

We can declare functions by both reference and value parameters. For example:

```cpp
void f(X);         // call-by-value
void f(const X&);  // call-by-reference
void f(X&&);
void f(const X&&);
```

In principle, declaring all these overloads is allowed. However, there is no specific priority between call-by-value and call-by-reference. If you have a function declared to take an argument by value (which can take any argument of any value category), any matching declaration taking the argument by reference creates an ambiguity.

Therefore, you should usually only take an argument either by value or by reference (with as many reference overloads as you think are useful) but never both.

## 8.4 When Lvalues become Rvalues

As we have learned, when a function is declared with an rvalue reference parameter of a concrete type, you can only bind these parameters to rvalues. For example:

```cpp
void rvFunc(std::string&&);      // forward declaration

std::string s{...};
rvFunc(s);                         // ERROR: passing an lvalue to an rvalue reference
rvFunc(std::move(s));             // OK, passing an rvalue
```

However, note that sometimes, passing an lvalue seems to work. For example:

```cpp
void rvFunc(std::string&&);      // forward declaration

rvFunc("hello");                 // OK, although "hello" is an lvalue
```

Remember that string literals are lvalues when used as an expression. Therefore, passing them to an rvalue reference does not compile. However, there is a hidden operation involved, because the type of the argument (array of six content characters) does not match the type of the parameter. We have an implicit type conversion, performed by the string constructor, which creates a temporary object that does not have a name.

Therefore, what we really call is the following:

```cpp
void rvFunc(std::string&&);      // forward declaration

rvFunc(std::string{"hello"});    // OK, "hello" converted to a string is a prvalue
```

## 8.5 When Rvalues become Lvalues

Let us now look at the implementation of a function that declares the parameter as an rvalue reference:

```cpp
void rvFunc(std::string&& str) {
    ...
}
```

As we have learned, we can only pass rvalues:

```cpp
std::string s{...};
rvFunc(s);                         // ERROR: passing an lvalue to an rvalue reference
rvFunc(std::move(s));             // OK, passing an rvalue
rvFunc(std::string{"hello"});     // OK, passing a prvalue
```

However, when we use the parameter `str` inside the function, we are dealing with an object that has a name. This means that we use `str` as an lvalue. We can do only what we are allowed to do with an lvalue.

This means that we cannot directly call our own function recursively:

```cpp
void rvFunc(std::string&& str) {
    rvFunc(str);                  // ERROR: passing an lvalue to an rvalue reference
}
```
