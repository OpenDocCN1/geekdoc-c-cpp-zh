# 13.5 Throwing and Catching Exceptions

This section presents exceptions from a language-technical point of view.

# 13.5.1 Throwing Exceptions

We can **throw** an exception of any type that can be copied or moved. For example:

```
class No_copy {
No_copy(const No_copy&) = delete; // prohibit copying (§17.6.4) };
class My_error {
// ...
};
void f(int n)
{
switch (n) {
case 0: throw My_error{}; case 1: throw No_copy{}; case 2: throw My_error; }
}
// OK
// error : can’t copy a No_copy
// error :My_error is a type,rather than an object
```

The exception object caught (§13.5.2) is in principle a copy of the one thrown (though an optimizer is allowed to minimize copying); that is, a **throw x;** initializes a temporary variable of **x**’s type with **x**. This temporary may be further copied several times before it is caught: the exception is passed (back) from called function to calling function until a suitable handler is found. The type of the exception is used to select a handler in the **catch**-clause of some **try**-block. The data in the exception object – if any – is typically used to produce error messages or to help recovery. The process of passing the exception “up the stack” from the point of throw to a handler is called *stack unwinding*. In each scope exited, the destructors are invoked so that every fully constructed object is properly destroyed. For example:

```
void f()
{
string name {"Byron"}; try {
string s = "in"; g();
}
catch (My_error) { // ...
}
}
```

```
void g() {
string s = "excess"; {
string s = "or"; h();
}
}
```