We’ve seen an initial example of the use of this principle in section 9.7.4. Of course, the principle cannot be applied to the copy constructor itself, as you need a copy constructor to make a copy. The copy- and move constructors must always be implemented independently from each other.

# 9.8  Copy Elision and Return Value Optimization

When the compiler selects a member function (or constructor) it applies a simple set of rules, matching arguments with parameter types.

Below two tables are shown. The first table should be used in cases where a function argument has a name, the second table should be used in cases where the argument is anonymous. In each table select the const or non-const column and then use the topmost overloaded function that is available having the specified parameter type.

The tables do not handle functions defining value parameters. If a function has overloads expecting, respectively, a value parameter and some form of reference parameter the compiler reports an ambiguity when such a function is called. In the following selection procedure we may assume, without loss of generality, that this ambiguity does not occur and that all parameter types are reference parameters.

Parameter types matching a function’s argument of type T if the argument is:

+   - a *named* argument (an lvalue or a named rvalue)

|  | the argument is: |
|---|---|
|  | non-const | const |
| Use the topmost available function | (T &) | (T const &) |

Example: for an `int x` argument a function `fun(int &)` is selected rather than a function `fun(int const &)`. If no `fun(int &)` is available the `fun(int const &)` function is used. If neither is available the compiler reports an error.

+   - an *anonymous* argument (an anonymous temporary or a literal value)

|  | the argument is: |
|---|---|
|  | non-const | const |
| Use the topmost available function | (T &&) | (T const &&) |
| available function | (T const &) | (T const &) |

Example: when the return value of an `int arg()` function is passed to a function `fun` for which various overloaded versions are available `fun(int &&)` is selected. If this function is unavailable but `fun(int const &)` is, then the latter function is used. If none of these two functions is available the compiler reports an error.

The tables show that eventually *all* arguments can be used with a function specifying a `T const &` parameter. For *anonymous* arguments a similar *catch all* is available having a higher priority: `T const &&` matches all anonymous arguments. Functions having this signature are normally not defined as their implementations (should be) identical to the implementations of the functions expecting a `T const &` parameter. Since the temporary can apparently not be modified by a function defining a `T const &&` parameter has no alternative but to copy the temporary’s resources. As this task is already performed by functions expecting a `T const &`, there is no need for implementing functions expecting `T const &&` parameters.

As we’ve seen the move constructor grabs the information from a temporary for its own use. That is OK as the temporary is going to be destroyed after that anyway. It also means that the temporary’s data members are modified.