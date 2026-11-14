
In a using declaration, the new name is positioned on the left while a typedef puts it on the right side. For declaring an array, the new type name is not the right-most part of a typedef and the type is split into two parts:

```cpp
typedef double da1[10];
```

In contrast to it, within the using declaration, the type remains in one piece:

```cpp
using da2 = double[10];
```

The difference becomes even more pronounced for function (pointer) types—which you will hopefully never need in type definitions. std::function in §4.4.2 is a more flexible alternative. For instance, declaring a function with a float and an int argument that returns a float reads

```cpp
typedef float float_fun1(float, int);
```

versus

```cpp
using float_fun2 = float (float, int);
```

In all these examples, the using declaration clearly separates the new type name from the definition.

In addition, the using declaration allows us to define Template Aliases. These are definitions with type parameters: Assume we have a template class for tensors of arbitrary order and parameterizable value type:

```cpp
template <unsigned Order, typename Value>
class tensor { ... };
```

Now we like to introduce the type names vector and matrix for tensors of first and second order, respectively. This cannot be achieved with typedef but easily by template aliases via using:

```cpp
template <typename Value>
using vector = tensor<1, Value>;
```

```cpp
template <typename Value>
using matrix = tensor<2, Value>;
```

When we throw the output of the following lines:

```cpp
std::cout << "type of vector<float> is "
<< typeid(vector<float>).name() << '\n';
std::cout << "type of matrix<float> is "
<< typeid(matrix<float>).name() << '\n';
```

into a name demangler, we will see

```
type of vector<float> is tensor<1u, float>
type of matrix<float> is tensor<2u, float>
```

Resuming, if you have experience with typedef, you will appreciate the new opportunities in C++11, and if you are new in the type definition business, you should start with using right away.

## 3.5 A Bit of Theory on Templates: Concepts

> "Gray, dear friend, is all theory and green the life's golden tree."<sup>8</sup>
> —Johann Wolfgang von Goethe

In the previous sections, you might have gotten the impression that template parameters can be substituted by any type. This is in fact not entirely true. The programmer of template classes and functions makes assumptions about the operations that can be performed on the template arguments.

Thus, it is very important to know which argument types are acceptable. We have seen, for instance, that `accumulable` can be instantiated with `int` or `double`. Types without addition like a solver class (on page 74) cannot be used for `accumulable`. What should be accumulated from a set of solvers? All the requirements for the template parameter `T` of function `accumulate` can be summarized as follows:

- `T` is copy-constructible: `T a(b);` is compilable when the type of `b` is `T`.
- `T` is plus-assignable: `a += b;` compiles when the type of `a` and `b` is `T`.
- `T` can be constructed from `int`: `T a(0);` compiles.

Such a set of type requirements is called a _Concept_. A concept `C` that contains all requirements of concept `C` and possibly additional requirements is called a _Refinement_ of `C`. A type `T` that holds all requirements of concept `C` is called a _Model_ of `C`. Plus-assignable types are, for instance, `int`, `float`, `double`, and even `string`.

A complete definition of a template function or class should contain the list of required concepts as is done for functions from the Standard Template Library; see `http://www.sgi.com/tech/stl/`.

Today such requirements are only documentation. Future C++ standards will most likely support concepts as a central language feature. A technical specification mainly by Andrew Sutton, "C++ Extensions for Concepts," [46] is in progress and may be part of C++17.

## 3.6 Template Specialization

On one hand, it is a great advantage that we can use the same implementation for many arguments types. For some argument types we may, however, know a more efficient implementation, and this can be realized in C++ with _Template Specialization_. In principle, we could even implement an entirely different behavior for certain types at the price of utter confusion. Thus, the specialization will be more efficient but behave the same. C++ provides enormous flexibility, and we as programmers are in charge of using this flexibility responsibly and of being consistent with ourselves.

### 3.6.1 Specializing a Class for One Type

=> c++11/vector_template.cpp

In the following, we want to specialize our vector example from Listing 3.3.1 for bool. Our goal is to save memory by packing 8 bool values into one byte. Let us start with the class definition:

```cpp
template <>
class vector<bool>
{
    // ...
};
```

Although our specialized class is not type-parametric anymore, we still need the template keyword and the empty triangle brackets. The name vector was declared to be a class template before, and we need this seemingly surplus template notation to show that the following definition is a specialization of the Primary Template. Thus, defining or declaring a template specialization before the primary template is an error. In a specialization, we must provide within the angle brackets a type for each template parameter. These values may be parameters themselves (or expressions thereof). For instance, if we specialize for one out of three parameters, the two others are still declared as template parameters:

```cpp
template <typename T1, typename T3>
class some_container<T1, int, T3>
{
    // ...
};
```

Back to our boolean vector class: our primary template defines a constructor for an empty vector and one containing n elements. For the sake of consistency, we should define the same. With the non-empty vector, we have to round up the data size when the number of bits is not divisible by 8:

```cpp
template <>
class vector<bool>
{
public:
    explicit vector(int size)
        : my_size(size), data(new unsigned char[(my_size + 7) / 8])
    {
    }
    vector() : my_size(0) {}
private:
    int my_size;
    std::unique_ptr<unsigned char[]> data;
};
```

You may have noticed that the default constructor is identical to that of the primary template. Unfortunately, the method is not "inherited" to the specialization. Whenever we write a specialization, we have to define everything from scratch or use a common base class.9

We are free to omit member functions or variables from the primary template, but for the sake of consistency we should do this only for good reasons, for very good reasons. For instance, we might omit the operator+ because we have no addition for bool. The constant access operator is implemented with shifting and bit masking:

```cpp
template <> class vector<bool>
{
    bool operator[](int i) const
    { return (data[i / 8] >> i % 8) & 1; }
};
```

The mutable access is trickier because we cannot refer to a single bit. The trick is to return a Proxy which provides read and write operations for a single bit:

```cpp
template <> class vector<bool>
{
    vector_bool_proxy operator[](int i)
    { return {data[i / 8], i % 8}; }
    vector_bool_proxy operator[](int i) const
    { return {data[i / 8], i % 8}; }
};
```

The return statement uses a braced list to call the two-argument constructor. Let us now implement our proxy to manage a specific bit within vector<bool>. Obviously, the class needs a reference to the containing byte and the position within this byte. To simplify further operations, we create a mask that has one bit on the position in question and zero bits on all other positions:

```cpp
class vector_bool_proxy
{
public:
    vector_bool_proxy(unsigned char& byte, int p)
        : byte(byte), mask(1 << p) {}

private:
    unsigned char& byte;
    unsigned char mask;
};
```

The reading access is realized with a conversion to bool where we simply mask the referred byte:

```cpp
class vector_bool_proxy
{
    operator bool() const { return byte & mask; }
};
```

Only when the considered bit is 1 in byte, the bitwise AND yields a non-zero value that is evaluated to true in the conversion from unsigned char to bool.
Setting a bit is realized by an assignment operator for bool:

```cpp
class vector_bool_proxy
{
```
