# C++ Templates: Generic Functions

Templates are an advanced feature of C++. Templates permit us to create generic functions and classes. In a generic function or class, the type of data upon which the function or class operates is specified as a generic parameter. Thus, we can use one function or class with several different types of data without having to explicitly re-code specific versions of the function or class for each data type.

# Generic Functions

A generic function defines a set of operations or an algorithm that will be applied to data of various types. A generic function permits a single general algorithm to be applied to many data types.

Many algorithms are logically the same, no matter what type of data is being operated upon. For example, the bubble sort algorithm is the same whether it is applied to an array of integers or an array of doubles. Only the type of data being sorted is different. By creating a generic function, we can define the algorithm, independent of the type of data. Once this is done, the compiler can automatically generate the correct function code for the type of data that will be actually used.

In essence, when we create a generic function we are creating a function that automatically overload itself at compile-time.

A generic function is created using the template keyword. The general form of a function template declaration is:

```
template <class Ttype> return-type function_name(parameter list)
{
```