
```cpp
while (true)
{
    if ((right = format.find('%', right)) == string::npos)       // 1
        throw std::runtime_error("printcpp: too many arguments");

    if (format.find("%%", right) != right)                     // 2
        break;

    ++right;
    cout << format.substr(left, right - left);
    left = ++right;
}
cout << format.substr(left, right - left) << value;
printcpp(format.substr(right + 1), args...);
```

- At 1 the format string is searched for a parameter specification %. If none is found then the function is called with too many arguments and it throws an exception;
- At 2 it verifies that it has not encountered %%. If only a single % has been seen the while-loop ends, the format string is inserted into cout up to the % followed by value, and the recursive call receives the remaining part of the format string as well as the remaining parameter pack;
- If %% was seen the format string is inserted up to the second %, which is ignored, and processing of the format string continues beyond the %%.

Make sure that the overloaded function is at least declared before the compiler processes the function template’s definition or it won’t call the overloaded function `printcpp` when compiling the function template.

Different from C’s `printf` function `printcpp` only recognizes `%` and `%%` as format specifiers. The above implementation does not recognize, e.g., field widths. Type specifiers like `%c` and `%x` are of course not needed as `ostream`’s insertion operator is aware of the types of the arguments that are inserted into the `ostream`. Extending the format specifiers so that field widths etc. are recognized by this `printcpp` implementation is left as an exercise to the reader. Here is an example showing how `printcpp` can be called:

```cpp
printcpp("Hello % with %%main%% called with % args"
         " and a string showing %\n",
         "world", argc, string("A String"));
```

### 21.5.2 Perfect forwarding (C++11)

Consider `string`’s member insert. `string::insert` has several overloaded implementations. It can be used to insert text (completely or partially) provided by a string or by a `char const *` argument; to insert single characters a specified number of times; iterators can be used to specify the range of characters to be inserted; etc., etc. All in all, string offers as many as five overloaded insert members.

Assume the existence of a class `Inserter` that is used to insert information into all kinds of objects. Such a class could have a `string` data member into which information can be inserted. Inserter’s interface only partially has to copy string’s interface to realize this: only `string::insert`’s interfaces must be duplicated. The members duplicating interfaces often contain one statement (calling the appropriate member function of the object’s data member) and are for this reason often implemented in-line. Such *wrapper functions* merely *forward* their parameters to the matching member functions of the object’s data member.

Another example is found in *factory functions* that also frequently forward their parameters to the constructors of objects that they return.

Before the C++11 standard the interfaces of overloaded functions needed to be duplicated by the forwarding entity: `Inserter` needed to duplicate the interfaces of all five `string::insert` members; a factory function needed to duplicate the interfaces of the constructors of the class of the objects it returned.

The C++11 standard simplifies and generalizes forwarding of parameters by offering *perfect forwarding*, implemented through rvalue references and variadic templates. With perfect forwarding the arguments passed to functions are 'perfectly forwarded' to nested functions. Forwarding is called *perfect* as the arguments are forwarded in a type-safe way. To use perfect forwarding nested functions must define parameter lists matching the forwarding parameters both in types and number.

Perfect forwarding is easily implemented:

- The forwarding function is defined as a template (usually a *variadic* template, but single argument forwarding is also possible. To define and forward a single argument omit the ellipsis from the following code);
- The forwarding function's parameter list is an *rvalue reference parameter pack* (e.g., `Params &&...params`);
- `std::forward` is used to forward the forwarding function's arguments to the nested function, keeping track of their types and number. Before `forward` can be used the `<utility>` header file must have been included.
- The nested function is called using this statement to specify its arguments:
  `std::forward<Params>(params)....`

In the next example perfect forwarding is used to implement *one* member `Inserter::insert` that can be used to call any of the five overloaded `string::insert` members. The insert function that's actually called now simply depends on the types and number of arguments that are passed to `Inserter::insert`:

```cpp
class Inserter
{
    std::string d_str;   // somehow initialized
    public:
                        // constructors not implemented,
                        // but see below
    Inserter();
    Inserter(std::string const &str);
    Inserter(Inserter const &other);
    Inserter(Inserter &&other);

    template<typename ...Params>
    void insert(Params &&...params)
    {
        d_str.insert(std::forward<Params>(params)...);
    }
};
```

A factory function returning an `Inserter` can also easily be implemented using perfect forwarding. Rather than defining four overloaded factory functions a single one now suffices. By providing the factory function with an additional template type parameter specifying the class of the object to construct the factory function is turned into a completely general factory function:

```cpp
template <typename Class, typename ...Params>
Class factory(Params &&...params)
{
    return Class(std::forward<Params>(params)...);
}
```

Here are some examples showing its use:

```cpp
Inserter inserter(factory<Inserter>("hello"));
string delimiter(factory<string>(10, '='));
Inserter copy(factory<Inserter>(inserter));
```

The function `std::forward` is provided by the standard library. It performs no magic, but merely returns params as a nameless object. That way it acts like `std::move` that also removes the name from an object, returning it as a nameless object. The unpack operator has nothing to do with the use of `forward` but merely tells the compiler to apply `forward` to each of the arguments in turn. Thus it behaves similarly to C’s ellipsis operator used by variadic functions.

Perfect forwarding was introduced in section 20.4.5: a template function defining a `Type && param`, with `Type` being a template type parameter converts `Type &&` to `Tp &&` if the function is called with an argument of type `Tp &&`. Otherwise it binds `Type` to `Tp`, with `param` being defined as `Tp && param`. As a result a lvalue argument binds to an lvalue-type (`Tp &`) while an rvalue argument binds to an rvalue-type (`Tp &&`).

The function `std::forward` merely passes the argument (and its type) on to the called function or object. Here is its simplified implementation:

```cpp
template <typename T>
T &&forward(T &&a)
{
    return a;
}
```

Since `T &&` turns into an lvalue reference when `forward` is called with an lvalue (or lvalue reference) and remains an rvalue reference if `forward` is called with an rvalue reference, and since `forward` (like `std::move`) anonymizes the variable passed as argument to `forward`, the argument value is forwarded while passing its type from the function’s parameter to the called function’s argument.

This is called *perfect forwarding* as the nested function can only be called if the types of the arguments that were used when calling the ‘outer’ function (e.g., `factory`) exactly match the types of the parameters of the nested function (e.g., `Class`’s constructor). Perfect forwarding therefore is a tool to realize type safety.

A cosmetic improvement to `forward` requires users of `forward` to specify the type to use rather than to have the compiler deduce the type as a result of the function template parameter type deduction’s process. This is realized by a small support struct template:

```cpp
template <typename T>
struct identity
{
    typedef T type;
};
```

This struct merely defines `identity::type` as `T`, but as it is a struct it must be specified explicitly. It cannot be determined from the function’s argument itself. The subtle modification to the above implementation of `forward` thus becomes (cf. section 21.2.1 for an explanation of the use of typename):

```cpp
template <typename T>
T &&forward(typename identity<T>::type &&arg)
{
    return arg;
}
```

Now `forward` must explicitly state `arg`’s type, as in:

```cpp
std::forward<Params>(params)
```
