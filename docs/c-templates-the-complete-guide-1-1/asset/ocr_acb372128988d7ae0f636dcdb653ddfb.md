In cases when there is no connection between template and call parameters and when template parameters cannot be obtained, you must specify the template argument explicitly with the call. For example, you can introduce a third template argument type to define the return type of a function template:

Click here to view code image

```
```cpp
template<typename T, typename T2, typename RT>
RT max (T a, T2 b);
```
```

However, template argument deduction does not take return types into account, and RT does not appear in the types of the function call parameters. Therefore, RT cannot be deduced.

As a consequence, you have to specify the template argument list explicitly.

Click here to view code image

```
```cpp
template<typename T1, typename T2, typename RT>
RT max (T1 a, T2 b);

::max<int,double,double>(4, 7.2);       // OK; but ambiguous
```
```

So far, we have looked at cases in which either all or none of the function template arguments were mentioned explicitly. Another approach is to specify only the first arguments explicitly and to allow their deduction process to derive the rest. In general, you must specify all the argument types up to the last argument type that cannot be determined implicitly. Thus, if you change the order of the template parameters in our example, the caller needs to specify only the return type:

Click here to view code image

```
```cpp
template<typename RT, typename T1, typename T2>
RT max (T1 a, T2 b)
{
    return b < a ? a : b;
}

::max<double>(4, 7.2)      // OK: return type is double,
T1 and T2 are deduced
```
```

In this example, the call to max<double> explicitly asks RT to be double, but the parameters T1 and T2 are deduced to be int and double from the arguments.

Note that these modified versions of max() don't lead to significant advantages. For one reason, you can already specify the parameter types of the function call. In fact, the result is not dependent on the argument type you pass. Thus, if a max() is used to keep it simple and not use an operator version, you can use the following implementation instead. This way, you can also define the function template parameters in a different order.

See Chapter 6 for details of the deduction process.

# 1.3.2 Deducing the Return Type

If a return type depends on template parameters, the simplest and best approach to deduce the return type is to let the compiler find out. Since C++14, this is possible by simply not declaring any return type (you still have to declare the return type to be auto):

Click here to view code image

basics/auto.cpp

```
```cpp
template<typename T1, typename T2>

auto max (T1 a, T2 b)
{
    return b < a ? a : b;
}
```
```

In fact, the use of auto for the return type without a corresponding trailing-return-type syntax (which would be introduced with ->) means that the actual return type must be deduced from the return statement(s) in the function body. Of course, depending on the return type the function body has to be possible. Therefore, the code must be available and multiple return statements have to match.

Before C++14, it is only possible to let the compiler determine the return type by using the type of the function point of instantiation. In C++11 we can benefit from the fact that the trailing return type syntax allows us to use the call parameters. That is, we can declare that the return type is derived from what operator< yields:

Click here to view code image

basics/decltype.cpp

```
```cpp
template<typename T1, typename T2>
auto max (T1 a, T2 b) -> decltype(b<a?b:a)
{
    return b < a ? a : b;
}
```
```

Here, the resulting type is determined by the rules for operator ?:, which are fairly elaborate but generally produce an intuitively expected result.