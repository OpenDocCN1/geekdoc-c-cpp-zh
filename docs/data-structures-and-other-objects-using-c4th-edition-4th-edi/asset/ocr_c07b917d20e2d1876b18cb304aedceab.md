The biggest value, 30, appears at location [2], so with this array as the argument,
our function returns 2. Here is the template function's complete specification:

```
template <class Item>
size_t index_of_maximal(const Item data[], size_t n);
// Precondition: data is an array with at least n items, and n > 0.
// Postcondition: The return value is the index of a maximal item from
// data[0] . . data[n - 1]. Note: Item may be any of the C++ built-in types
// (int, char, etc.), or any class with the > operator defined.
```

Actually, this specification is not exactly what we want. To explain the problem,
we need to know a bit more about how the compiler uses template functions.

When a template function is instantiated, the compiler tries to select the
underlying data type so that the type of each argument results in an exact match
with the type of the corresponding formal parameter. For example, suppose that
d is a double variable. You cannot write maximal(d, 1), since there is no way
for the compiler to have Item be an exact match with the type of the first
argument (double) and also be an exact match with the type of the second argu-
ment (int). The compiler does not convert arguments for a template function.
The arguments must have an exact match, with no type conversion.

The requirement of an exact match applies to all parameters of a template
function. For example, consider the index_of_maximal prototype:

```
template <class Item>
size_t index_of_maximal(const Item data[], size_t n);
```

When we call the function, the second argument must be a size_t value. Many
compilers won't accept any deviation: not an int, not a const size_t, only a
size_t value. On such a strict compiler, the following will fail:

```
const size_t SIZE = 5;
double data[SIZE];
...
cout << index_of_maximal(data, SIZE);
cout << index_of_maximal(data, 5);
```

The first function call, with SIZE as the second argument, fails on many compi-
lers because SIZE is declared as const size_t rather than a mere size_t. The
second function call, with 5 as the second argument, fails because the compiler
takes 5 to be an int rather than a size_t value.

# A Template Function to Find the Biggest Item in an Array

For the index_of_maximal function, we can deal with the problem by slightly
changing the specification. The new specification uses two template parameters,
one for the data type of the array's components, and a second for the data type
of the size of the array, as shown here: