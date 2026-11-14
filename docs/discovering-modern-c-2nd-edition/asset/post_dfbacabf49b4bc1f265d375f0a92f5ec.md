
It is more readable and more powerful. For simple definitions, it is just a question of order:

```
typedef double value_type;
```

versus:

```
using value_type = double;
```

In a `using` declaration, the new name is positioned on the left while a `typedef` puts it on the right side. For declaring an array, the new type name is not the rightmost part of a `typedef` and the type is split into two parts:

```
typedef double da1[10];
```

In contrast to it, within the `using` declaration, the type remains in one piece:

```
using da2 = double[10];
```

The difference becomes even more pronounced for function pointers—which you will hopefully never need in type definitions. `std::function` in §4.4.7 is a more flexible alternative. For instance, declaring a function with a `float` and an `int` argument that returns a `float` reads:

```
typedef float (*float_fn1)(float, int);
```

versus:

```
using float_fun2 = float(*)(float, int);
```

In all examples, the `using` declaration clearly separates the new type name from the definition.

In addition, the `using` declaration allows us to define *Template Aliases*. These are definitions with type parameters. Assume we have a template class for tensors of arbitrary rank and parameterizable value type:

Click here to view code image

```
template <unsigned Order, typename Value>
class tensor { ... };
```

Now we'd like to introduce the types `vector` and `matrix` for tensors of first and second rank, respectively. This cannot be achieved with `typedef` but can easily be achieved by template aliases via `using`:

Click here to view code image

```
template <typename Value>
using vector = tensor<1, Value>;

template <typename Value>
using matrix = tensor<2, Value>;
```

When we print the output of the following lines:

Click here to view code image

```
std::cout << "The type of vector<float> is "
          << typeid(vector<float>).name() << ".\n";
std::cout << "The type of matrix<float> is "
          << typeid(matrix<float>).name() << ".\n";
```

In a name demangler, we will see:

Click here to view code image

```
The type of vector<float> is tensor<1u, float>.
The type of matrix<float> is tensor<2u, float>.
```

Resuming, if you have experience with typedef, you will appreciate the new opportunities in C++11, and if you are new to type definitions, you should start with using right away.

## 3.5 Template Specialization

On the one hand, it is a great advantage that we can use the same implementation for many argument types. For some argument types we may, however, know a more efficient implementation, and this can be realized in C++ with Template Specialization. In principle, we could even implement an entirely different behavior for certain types at the price of utter confusion. Thus, the specialization shall be more efficient but behave the same. C++ provides enormous flexibility, and we as programmers are in charge of using this flexibility responsibly and of being consistent with ourselves.

### 3.5.1 Specializing a Class for One Type

=> c++11/vector_template.cpp

In the following, we want to specialize our vector example from Listing 3–1 for bool. Our goal is to save memory by packing 8 bool values into one byte. Let us start with the class definition:

```
template <>
class vector<bool>
{
    // ...
};
```

Although our specialized class is not type-parametric anymore, we still need the template keyword and the empty triangle brackets. The name vector was declared to be a class template before, and we need this seemingly surplus template notation to show that the following definition is a specialization of the Primary Template. Thus, defining or declaring a template specialization before the primary template is an error. In a specialization, we must provide within the angle brackets a type for each template parameter. These values may be parameters themselves (or expressions thereof). For instance, if we specialize for one out of three parameters, the two others are still declared as template parameters:

Click here to view code image

```
template <typename T1, typename T3>
class some_container<T1, int, T3>
{
    // ...
};
```

Back to our boolean vector class: our primary template defines a constructor for an empty vector and one containing n elements. For the sake of consistency, we should define the same.

With the non-empty vector, we have to round up the data size when the number of bits is not divisible by 8:

Click here to view code image

```
template <>
class vector<bool>
{
public:
    explicit vector(int size)
        : my_size(size), data{new unsigned char[(my_size + 7) / 8]}
    {
    }

    vector() : my_size(0) {}
private:
    int my_size;
    std::unique_ptr<unsigned char[]> data;
};
```

You may have noticed that the default constructor is identical to that of the primary template. Unfortunately, the method is not “inherited” to the specialization. Whenever we write a specialization, we have to define everything from scratch or use a common base class.9

9. The author tried to overcome this verbosity [20].

We are free to omit member functions or variables from the primary template, but for the sake of consistency we should do this only for good reasons, for very good reasons. For instance, we might omit the operator+ because we have no addition for bool. The constant access operator is implemented with shifting and bit masking:

Click here to view code image

```
template <> class vector<bool>
{
bool operator[](int i) const
{ return (data[i / 8] >> i % 8) & 1; }
};
```

The mutable access is trickier because we cannot refer to a single bit. The trick is to return a Proxy—a placeholder design pattern that provides an interface to something else. Our vector_bool_proxy shall provide a bool interface for a single bit in our vector:

Click here to view code image

```
template <> class vector<bool>
{
vector_bool_proxy operator[](int i)
{ return {data[i / 8], i % 8}; }
};
```

The return statement uses a braced list to call the two-argument constructor. Let us now implement our proxy to manage a specific bit within `vector<bool>`. Obviously, the class needs a reference to the containing byte and the position within this byte. To simplify further operations, we create a mask that has a 1-bit on the position in question and 0-bits on all others:

Click here to view code image

```
class vector_bool_proxy
{
public:
    vector_bool_proxy(unsigned char& byte, int p)
        : byte(byte), mask(static_cast<unsigned char>(1 << p))
    {}

private:
    unsigned char& byte;
    unsigned char mask;
};
```

Note that the result of `1 << p` is `int` and storing this to `mask` would be a narrowing conversion without the cast. The reading access is realized with a conversion to `bool` by simply masking the referred byte:

Click here to view code image

```
class vector_bool_proxy
{
    operator bool() const { return byte & mask; }
};
```

Only when the considered bit in `byte` is 1, the bitwise AND yields a non-zero value that is evaluated to `true` in the implicit conversion from `unsigned char` to `bool`. Setting a bit is realized by an assignment operator for `bool`:

Click here to view code image

```
class vector_bool_proxy
{
    vector_bool_proxy& operator=(bool b)
    {
        if (b)
            byte |= mask;
        else
            byte &= ~mask;
        return *this;
    }
};
```

The assignment is simpler to implement when we distinguish between the assigned values. When the argument is `true`, we apply an OR with the mask so that the bit in the considered position is switched on. All other positions remain unchanged since OR with 0 has no effect (0 is the identity element of bitwise OR). Conversely, with `false` as an argument, we first invert the mask and apply it with AND to the byte reference. Then the inverted mask's 0-bit on the active position turns the bit off and on all other positions, the AND with 1-bits preserves those bit values.

With this specialization of `vector` for `bool`, we use only about an eighth of the memory. Nonetheless, our specialization is (mostly) consistent with the primary template: we can create vectors and read and write them in the same fashion. To be precise, the compressed vector is not perfectly identical to the primary template, e.g., when we take references of elements or when type deduction is involved. However, we made the specialization as similar as possible to the generic version and in most situations we will not realize the differences and it will work in the same way.

### 3.5.2 Specializing and Overloading Functions

In this section, we discuss and assess the advantages and disadvantages of template specialization for functions.

#### 3.5.2.1 Specializing a Function to a Specific Type

Functions can be specialized in the same manner as classes. Unfortunately, they do not participate in overload resolution, and a less specific overload is prioritized over the more specific template specialization; see [64]. For that reason Sutter and Alexandrescu give in [66, Item 66] the following:

> Advice
> Do not use function template specialization!

To provide a special implementation for one specific type or type tuple as above, we can simply use overloading. This works better and is even simpler, e.g.:

![](img/5682e787fc967e93d7e33e8bac5f58a0_267_0.png)
