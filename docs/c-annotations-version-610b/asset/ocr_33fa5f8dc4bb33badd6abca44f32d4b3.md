default type to use for the template’s `DataType` parameter). The actual values or types of template parameters are *never* deduced from arguments as is done with function template parameters. So to define a `Matrix` of complex-valued elements, the following syntax is used:

```
Matrix<3, 5, std::complex> complexMatrix;
```

Since the class template `Matrix` uses a default data type a matrix of double-valued elements can be defined like this:

```
Matrix<3, 5> doubleMatrix;
```

A class template object may be declared using the keyword `extern`. For example, to declare the matrix `complexMatrix` use:

```
extern Matrix<3, 5, std::complex> complexMatrix;
```

A class template declaration suffices to compile return values or parameters that are of class template types. Example: the following source file may be compiled, although the compiler hasn’t seen the definition of the `Matrix` class template. Generic classes and (partial) specializations may all be declared. A function expecting or returning a class template object, reference, or parameter automatically becomes a function template itself. This is necessary to allow the compiler to tailor the function to the types of various actual arguments that may be passed to the function:

```
#include <cstddef>

template <size_t Rows, size_t Columns, typename DataType = double>
class Matrix;

template <size_t Columns, typename DataType>
class Matrix<1, Columns, DataType>;

Matrix<1, 12> *function(Matrix<2, 18, size_t> &mat);
```

When class templates are used the compiler must first have seen their implementations. So, template member functions must be known to the compiler when the template is instantiated. This does not mean that *all* members of a template class are instantiated or must have been seen when a class template object is defined. The compiler only instantiates those members that are actually used. This is illustrated by the following class `Demo` that has two constructors and two members. When we use one constructor and call one member in `main` note the sizes of the resulting object file and executable program. Next the class definition is modified in that the unused constructor and member are commented out. Again we compile and link the program. Now observe that these latter sizes are identical to the former sizes. There are other ways to illustrate that only used members are instantiated. The `nm` program could be used. It shows the symbolic contents of object files. Using `nm` we’ll reach the same conclusion: *only template member functions that are actually used are instantiated*. Here is the class template `Demo` that was used for our little experiment. In `main` only the first constructor and the first member function are called and thus only these members were instantiated:

```
#include <iostream>

template <typename Type>
class Demo
{
    Type d_data;
public:
    Demo();
    Demo(Type const &value);
```