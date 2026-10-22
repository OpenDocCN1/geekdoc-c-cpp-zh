
```
std::string returnString();
std::string s = "hi";
printV(s); //copy constructor
printV(std::string("hi")); //copying usually optimized away (if not, move constructor)
printV(returnString()); // copying usually optimized away (if not, move constructor)
printV(std::move(s)); // move constructor
```

In the first call we pass an lvalue, which means that the copy constructor is used. However, in the second and third calls, when directly calling the function template for prvalues (temporary objects created on the fly or returned by another function; see Appendix B), compilers usually optimize passing the argument so that no copying constructor is called at all. Note that since C++17, this optimization is required. Before C++17, a compiler that doesn’t optimize the copying away, must at least have to try to use move semantics, which usually makes copying cheap. In the last call, when passing an xvalue (an existing nonconstant object with std::move()), we force to call the move constructor by signaling that we no longer need the value of s.

Thus, calling an implementation of printV() that declares the parameter to be passed by value usually is only expensive if we pass an lvalue (an object we created before and typically still use afterwards, as we didn’t use std::move() to pass it). Unfortunately, this is a pretty common case. One reason is that it is pretty common to create objects early to pass them later (after some modifications) to other functions.

## Passing by Value Decays

There is another property of passing by value we have to mention: When passing arguments to a parameter by value, the type decays. This means that raw arrays get converted to pointers and that qualifiers such as const and volatile are removed (just like using the value as initializer for an object declared with auto):⁴

```
template<typename T>
void printV (T arg) {
...
}
```

```
std::string const c = "hi";
printV(c); // c decays so that arg has type std::string
```

```
printV("hi"); //decays to pointer so that arg has type char const*
int arr[4];
printV(arr); // decays to pointer so that arg has type char const*
```

Thus, when passing the string literal "hi", its type char const[3] decays to char const* so that this is the deduced type of T. Thus, the template is instantiated as follows:

```
void printV (char const* arg)
{
...
}
```

This behavior is derived from C and has its benefits and drawbacks. Often it simplifies the handling of passed string literals, but the drawback is that inside printV() we can’t distinguish between passing a pointer to a single element and passing a raw array. For this reason, we will discuss how to deal with string literals and other raw arrays in Section 7.4 on page 115.

## 7.2 Passing by Reference

Now let’s discuss the different flavors of passing by reference. In all cases, no copy gets created (because the parameter just refers to the passed argument). Also, passing the argument never decays. However, sometimes passing is not possible, and if passing is possible, there are cases in which the resulting type of the parameter may cause problems.

### 7.2.1 Passing by Constant Reference

To avoid any (unnecessary) copying, when passing nontemporary objects, we can use constant references. For example:

```
template<typename T>
void printR (T const& arg) {
...
}
```

With this declaration, passing an object never creates a copy (whether it’s cheap or not):

```
std::string returnString();
std::string s = "hi";
printR(s); // no copy
printR(std::string("hi")); // no copy
printR(returnString()); // no copy
printR(std::move(s)); // no copy
```

Even an int is passed by reference, which is a bit counterproductive but shouldn’t matter that much. Thus:

```
int i = 42;
printR(i); // passes reference instead of just copying i
```

results in printR() being instantiated as:

```
void printR(int const& arg) {
...
}
```

Under the hood, passing an argument by reference is implemented by passing the address of the argument. Addresses are encoded compactly, and therefore transferring an address from the caller to the callee is efficient in itself. However, passing an address can create uncertainties for the compiler when it compiles the caller’s code: What is the callee doing with that address? In theory, the callee can change all the values that are “reachable” through that address. That means, that the compiler has to assume that all the values it may have cached (usually, in machine registers) are invalid after the call. Reloading all those values can be quite expensive. You may be thinking that we are passing by constant reference: Cannot the compiler deduce from that that no change can happen? Unfortunately, that is not the case because the caller may modify the referenced object through its own, non-const reference.⁵

This bad news is moderated by inlining: If the compiler can expand the call inline, it can reason about the caller and the callee together and in many cases “see” that the address is not used for anything but passing the underlying value. Function templates are often very short and therefore likely candidates for inline expansion. However, if a template encapsulates a more complex algorithm, inlining is less likely to happen.

## Passing by Reference Does Not Decay

When passing arguments to parameters by reference, they do not decay. This means that raw arrays are not converted to pointers and that qualifiers such as const and volatile are not removed. However, because the call parameter is declared as T const&, the template parameter T itself is not deduced as const. For example:

```
template<typename T>
void printR (T const& arg) {
...
}

std::string const c = "hi";
printR(c); // T deduced as std::string, arg is std::string const&

printR("hi"); // T deduced as char[3], arg is char const(&)[3]
int arr[4];
printR(arr); // T deduced as int[4], arg is int const(&)[4]
```

Thus, local objects declared with type T in `printR()` are not constant.

### 7.2.2 Passing by Nonconstant Reference

When you want to return values through passed arguments (i.e., when you want to use *out* or *inout* parameters), you have to use nonconstant references (unless you prefer to pass them via pointers). Again, this means that when passing the arguments, no copy gets created. The parameters of the called function template just get direct access to the passed argument.

Consider the following:

```
template<typename T>
void outR (T& arg) {
...
}
```

Note that calling `outR()` for a temporary (prvalue) or an existing object passed with `std::move()` (xvalue) usually is not allowed:

```
std::string returnString();
std::string s = "hi";
outR(s); // OK: T deduced as std::string, arg is std::string&
outR(std::string("hi")); // ERROR: not allowed to pass a temporary (prvalue)
outR(returnString()); // ERROR: not allowed to pass a temporary (prvalue)
outR(std::move(s)); // ERROR: not allowed to pass an xvalue
```

You can pass raw arrays of nonconstant types, which again don’t decay:

```
int arr[4];
outR(arr); // OK: T deduced as int[4], arg is int(&)[4]
```

Thus, you can modify elements and, for example, deal with the size of the array.
For example:

```
template<typename T>
void outR (T& arg) {
if (std::is_array<T>::value) {
std::cout << "got array of " << std::extent<T>::value << " elems\n";
}
...
}
```

However, templates are a bit tricky here. If you pass a const argument, the deduction might result in arg becoming a declaration of a constant reference, which means that passing an rvalue is suddenly allowed, where an lvalue is expected:

```
std::string const c = "hi";
outR(c); // OK: T deduced as std::string const
outR(returnConstString()); // OK: same if returnConstString() returns
const string
outR(std::move(c)); // OK: T deduced as std::string const
outR("hi"); // OK: T deduced as char const[3]
```

Of course, any attempt to modify the passed argument inside the function template is an error in such cases. Passing a const object is possible in the call expression itself, but when the function is fully instantiated (which may happen later in the compilation process) any attempt to modify the value will trigger an error (which, however, might happen deep inside the called template; see Section 9.4 on page 143).

- If you want to disable passing constant objects to nonconstant references, you can do the following:
- Use a static assertion to trigger a compile-time error:

```
template<typename T>
void outR (T& arg) {
static_assert(!std::is_const<T>::value,
"out parameter of foo<T>(T&) is const");
...
}
```

- Disable the template for this case either by using std::enable_if<> (see Section 6.3 on page 98):

```
template<typename T,
typename = std::enable_if_t<!std::is_const<T>::value>
void outR (T& arg) {
...
}
```
