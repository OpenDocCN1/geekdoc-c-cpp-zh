```
struct stack {};
```

```
template <typename T = double, typename Orientation = col_major,
       typename Where = heap>
class vector;
```

The arguments of a vector can be fully declared:

```
vector<float, row_major, heap> v;
```

The last argument is equal to the default value and can be omitted:

```
vector<float, row_major> v;
```

As for functions, only the final arguments can be omitted. For instance, if the second argument
is the default and the last one is not, we must write them all:

```
vector<float, col_major, stack> w;
```

When all template parameters are set to default values, we can of course omit them all.
However, for grammar reasons not discussed here, the angle brackets still need to be written:

```
vector x; // Error: it is considered a non-template class
```

```
vector<> y; // looks a bit strange but is correct
```

Other than the defaults of function arguments, the template defaults can refer to preceding
parameters:

```
template <typename T, typename U = T>
class pair;
```

This is a class for two values that might have different types. If not we can declare the type
just once:

```
pair<int, float> p1; // object with an int and float value
pair<int> p2; // object with two int values
```

The default can even be expressions of preceding parameters as we will see in Chapter 5.

# 3.3.2 Designing Uniform Class and Function Interfaces

```
=> c++03/accumulate_example.cpp
```

When we write generic classes and functions, we can ask ourselves the chicken-and-egg
question: what comes first? We have the choice to write function templates first and adapt
our classes to them by realizing the corresponding methods. Alternatively, we can develop
the interface of our classes first and implement generic functions against this interface.

The situation changes a little bit when our generic functions should be able to handle
intrinsic types or classes from the standard library. These classes cannot be changed, and we
should adapt our functions to their interface. There are other options that we will introduce
later: specialization and meta-programming, which allow for type-dependent behavior.

As a case study, we use the function accumulate from the Standard Template Library,
Section 4.1. It was developed at a time when programmers used pointers and ordinary arrays
even more frequently than today. Thus, the STL creators Alex Stepanov and David Musser
established an extremely versatile interface that works for pointers and arrays as well as on
all containers of their library.