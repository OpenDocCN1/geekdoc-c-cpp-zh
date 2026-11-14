
A function computing a scalar product expects two vectors as arguments:

```
double dot(const vector& v, const vector& w) { ... }
```

This function can be called with integer arguments:

```
double d = dot(8, 8);
```

What happens? Two temporary vectors of size 8 are created with the implicit constructor and passed to the function dot. This nonsense can be easily avoided by declaring the constructor explicit.

Which constructor will be explicit is in the end the class designer's decision. It is pretty obvious in the vector example: no right-minded programmer wants the compiler converting integers automatically into vectors.

Whether the constructor of the complex class should be explicit depends on the expected usage. Since a complex number with a zero imaginary part is mathematically identical to a real number, the implicit conversion does not create semantic inconsistencies. An implicit constructor is more convenient because a double value or literal can be used wherever a complex value is expected. Functions that are not performance-critical can be implemented only once for complex and used for double.

In C++03, the explicit attribute only mattered for single-argument constructors. From C++11 on, explicit is also relevant for constructors with multiple arguments due to uniform initialization, Section 2.3.4.

### C++11 2.3.1.4 Delegation

In the examples before, we had classes with multiple constructors. Usually such constructors are not entirely different and have some code in common; i.e., there is often some redundancy. In C++03, it was typically ignored when it only concerned the setup of primitive variables; otherwise the suitable common code fragments were outsourced into a method that was then called by multiple constructors.

C++11 offers Delegating Constructors; these are constructors that call other constructors. Our complex class could use this feature instead of default values:

```
class complex
{
public:
    complex(double r, double i) : r{r}, i{i} {}
    complex(double r) : complex{r, 0.0} {}
    complex() : complex{0.0} {}
    ...
};
```

Obviously, the benefit is not impressive for this small example. Delegating constructors becomes more useful for classes where the initialization is more elaborate (more complex than our complex).

### 2.3.1.5 Default Values for Members

Another new feature in C++11 is default values for member variables. Then we only need to set values in the constructor that are different from the defaults:

```
class complex {
    public:
        complex(double r, double i) : r(r), i(i) {}
        complex(double r) : r(r) {}
        complex() {}
        ...
    private:
        double r = 0.0, i = 0.0;
};
```

Again, the benefit is certainly more pronounced for large classes.

### 2.3.2 Assignment

In Section 2.3.1.2, we have seen that we can copy objects of user classes without getters and setters—at least during construction. Now, we want to copy into existing objects by writing:

```
x = y;
u = v = w = x;
```

To this end, the class must provide an assignment operator (or refrain from stopping the compiler to generate one). As usual, we consider first the class complex. Assigning a complex value to a complex variable requires an operator like

```
complex& operator=(const complex& src)
{
    r = src.r; i = src.i;
    return *this;
}
```

Evidently, we copy the members r and i. The operator returns a reference to the object for enabling multiple assignments. this is a pointer to the object itself, and since we need a reference, we dereference this pointer. The operator that assigns values of the object's type is called Copy Assignment and can be synthesized by the compiler. In our example, the generated code would be identical to ours and we could omit our implementation here.

What happens if we assign a double to a complex?

```
c = 7.5;
```

It compiles without the definition of an assignment operator for double. Once again, we have an implicit conversion: the implicit constructor creates a complex on the fly and assigns this one. If this becomes a performance issue, we can add an assignment for double:

```
complex& operator=(double nr)
{
    r = nr; i = 0;
}
```

As before, vector's synthesized operator is not satisfactory because it only copies the address of the data and not the data itself. The implementation is very similar to the copy constructor:

```
1 vector& operator=(const vector& src)
2 {
3   if (this == &src)
4     return *this;
5   assert(my_size == src.my_size);
6   for (int i = 0; i < my_size; ++i)
7     data[i] = src.data[i];
8   return *this;
9 }
```

It is advised [45, p. 94] that copy assignment and constructor be consistent to avoid utterly confused users.

An assignment of an object to itself (source and target have the same address) can be skipped (lines 3 and 4). In line 5, we test whether the assignment is a legal operation by checking the equality of the vector sizes. Alternatively the assignment could resize the target if the sizes are different. This is a technically legitimate option but scientifically rather questionable. Just think of a context in mathematics or physics where a vector space all of a sudden changes its dimension.

### 2.3.3 Initializer Lists

C++11 introduces the Initializer Lists as a new feature—not to be confused with “member initialization list” (§2.3.1). To use it, we must include the header <initializer_list>. Although this feature is orthogonal to the class concept, the constructor and assignment operator of a vector are excellent use cases, making this a suitable location for introducing initializer lists. It allows us to set all entries of a vector at the same time (up to reasonable sizes).

Ordinary C arrays can be initialized entirely within their definition:

```
float v[] = {1.0, 2.0, 3.0};
```

This capability is generalized in C++11 so that any class may be initialized with a list of values (of the same type). With an appropriate constructor, we could write:

```
vector v = {1.0, 2.0, 3.0};
```

or

```
vector v{1.0, 2.0, 3.0};
```

We could also set all vector entries in an assignment:

```
v = {1.0, 2.0, 3.0};
```

Functions that take vector arguments could be called with a vector that is set up on the fly:

```
vector x = lu_solve(A, vector{1.0, 2.0, 3.0});
```

## 2.3 Setting Values: Constructors and Assignments

The previous statement solves a linear system for the vector (1, 2, 3)^T with an LU factorization on A.

To use this feature in our vector class, we need a constructor and an assignment accepting initializer_list<double> as an argument. Lazy people can implement the constructor only and use it in the copy assignment. For demonstration and performance purposes, we will implement both. It also allows us to verify in the assignment that the vector size matches:

```
#include <initializer_list>
#include <algorithm>

class vector
{
  // ...
  vector(std::initializer_list<double> values)
  {
    my_size(values.size()), data(new double[my_size])
    {
      std::copy(std::begin(values), std::end(values),
                std::begin(data));
    }
  }

  self& operator=(std::initializer_list<double> values)
  {
    assert(my_size == values.size());
    std::copy(std::begin(values), std::end(values),
              std::begin(data));
    return *this;
  }
};
```

To copy the values within the list into our data, we use the function std::copy from the standard library. This function takes three iterators as arguments. These three arguments represent the begin and the end of the input and the begin of the output. The free functions begin and end were introduced in C++11. In C++03, we have to use the corresponding member functions, e.g., values.begin().

### 2.3.4 Uniform Initialization

Braces {} are used in C++11 as universal notation for all forms of variable initialization by

- Initializer-list constructors,
- Other constructors, or
- Direct member setting.

The latter is only allowed for arrays and classes if all (non-static) variables are public and the class has no user-defined constructor.4 Such types are called Aggregates and setting their values with braced lists accordingly Aggregate Initialization.
