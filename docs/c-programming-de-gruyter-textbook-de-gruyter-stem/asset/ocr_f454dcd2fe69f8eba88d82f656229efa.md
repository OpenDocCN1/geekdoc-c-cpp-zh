# 352 — 9 Collections and Their Organization

In this chapter, we only introduce the two basic searching algorithms: sequential searching and binary searching.
in this chapter, the concept of templates will be introduced, and this concept will be used to describe linear collections and the organization of collections in later chapters.

# 9.1 Function Templates and Class Templates

Code reuse is the most important feature in C++. Code has to be written in the most generic form in order to be reusable. A generic code can adapt to various data types automatically. This type of programming is called parameterized programming. C++ provides templates as a tool to support parameterized programming. By **declaring the object types as parameters, a code segment can be used for various object types.**

# 9.1.1 Function Template

Function overloading was introduced in Chapter 3. Function overloading can be to perform similar actions on different data types. In many cases, the algorithm is the same as the operations are performed on different data types. Even with the help of function overloading, identical codes are often repeated many times. The following program is an example of such cases.

```
int abs(int x)
{
    return x<0 ? -x:x;
}
double abs(double x)
{
    return x<0 ? -x:x;
}
```

These functions are identical except that the parameter types differ. In this case, a generic code can efficiently deal with both types of parameters. In C++, programmers only need to write a function template once, and then the compiler will generate corresponding functions for executing the algorithm on specific data types when the function is called.

The definition of a function template is:

```
template <class T> Or template <typename T>
DataType FunctionName(ParameterList)
{Definition of Function Body}
```