
have a vector addition (see §2.7.3). Its result will be a temporary object that is not constant. Thus we can assign values to it or its entries:

```
(v + w) = x;    // nonsense
(v + w)[i] = 7.3; // more nonsense
```

Admittedly, these are quite artificial examples, but it illustrates that there is room for improvement. Assignments should only accept mutable lvalues on the left-hand side. This applies uncompromisingly to intrinsic types. For user types we must enforce this with a reference qualifier:

```
vector& operator=(const vector& src) & { ... }
```

Now, only mutable lvalues are allowed on the left-hand side of an assignment.

Similarly, we can address the behavior of the element access. Our vector's bracket operator has two overloads: for mutable and constant objects. v+w is not constant so the overload for mutable vectors is preferred. Thus, we access a mutable reference to a mutable object's member which is legitimate. The problem is that (v + w)[i] is an lvalue while v+w is not. What we are missing here is the requirement that the bracket operator can only be applied on lvalues:

```
class vector
{
    public:
        double& operator[](int i) & { ... }    // #1
        const double& operator[](int i) const& { ... } // #2
};
```

When we qualify one overload of a method with a reference, we have to qualify the other overloads as references, too. With this implementation, overload #1 cannot be used for temporary vectors, and overload #2 returns a constant reference to which no value can be assigned. As a consequence, we will see a compiler error for the nonsensical assignment above:

```
vector_features.cpp:167:15: error : read-only variable is not
assignable
(v + w)[i] = 3;
~~~~~~~~~~^
```

The reference qualification protected us against a write access but not against reading since constant lvalue references accept rvalues as well. To avoid this implicit conversion, we can implement an rvalue overload as well:

```
class vector
{
public:
    double      operator[](int i) &&     { ... }    // #3
};
```

Note that an rvalue usually represents a temporary that is going to be destroyed, and we, therefore, return a value here and not a reference. We could also decide to forbid the element access for temporaries entirely and delete the operator for rvalues:

```
class vector
{
    double operator[](int i) && = delete;
};
```

Multi-dimensional data structures like matrices can be accessed in different ways. First, we can use the function call operator (§3.7) which allows us to pass multiple indices as arguments. The bracket operator unfortunately accepts only one argument, and we discuss some ways to deal with this in Appendix A.4.3 whereby none of them is satisfying. An advanced approach to call the application operator from concatenated bracket operators will be presented later in Section 6.6.1.2.

## 2.7 Operator Overloading Design

With few exceptions (listed in §1.3.10), most operators can be overloaded in C++. However, some operators make sense to overload only for specific purposes; e.g., the dereferenced member selection p->m is only useful for implementing new smart pointers. In a scientific or engineering context, it is much less obvious how to use this operator intuitively. Along the same lines, a customized meaning of the address operator &o needs a very good reason.

### 2.7.1 Be Consistent!

As mentioned before, the language gives us a high degree of freedom in the design and implementation of operators for our classes. We can freely choose the semantics of every operator. However, the closer our customized behavior is to that of the standard types, the easier it is for others (co-developers, open-source users, ...) to understand what we do and to trust our software.

The overloading can of course be used to represent operations in a certain application domain concisely, i.e., to establish a Domain-Specific Embedded Language (DSEL). In this case, it can be productive to deviate from the typical meanings of the operators. Nonetheless, the DSEL should be consistent in itself. For instance, if the operators =, +, and += are user-defined, then the expressions a = a + b and a += b should have the same effect.

> **Consistent Overloads**
> 
> Define your operators consistently with each other and whenever appropriate provide semantics similar to those of standard types.

We are also free to choose the return type of each operator arbitrarily; e.g., x == y could return a string or a file handle. Again, the closer we stay to the typical return types in C++, the easier it is for everybody (including ourselves) to work with our customized operators.

The only predefined aspects of operators are their Arity: the number of arguments and the relative priority of the operators. In most cases this is inherent in the represented operation: a multiplication always takes two arguments. For some operators, one could imagine a variable arity. For instance, it would be nice if the subscript operator accepted two arguments in addition to the subscribed object so that we could access a matrix element like this: A[i, j]. The only operator allowing for an arbitrary arity (including variadic implementations, §3.11) is the application operator: `operator()`.

Another freedom that the language provides us is the choice of the arguments’ types. We can, for instance, implement a subscription operator for an `unsigned` (returning a single element), for a range (returning a sub-vector), and for a set (returning a set of vector elements). This is indeed realized in MTL4. Compared to MATLAB, C++ offers fewer operators, but we have the unlimited opportunity of overloading them infinitely to create every amount of functionality we like.

### 2.7.2 Respect the Priority

When we implement operators ourselves, we need to make sure that the priorities in C++ match those of the application domain. For instance, we might have the idea of using the LaTeX notation for exponentiation of matrices:

```
A = B^2;
```

A is B squared. So far so good. That the original meaning of ^ is a bitwise exclusive OR does not worry us as we never planned to implement bitwise operations on matrices. Now we add C to B^2:

```
A = B^2 + C;
```

Looks nice. But it does not work (or does something weird). Why? Because + has a higher priority than ^ in C++. Thus, the compiler understands our expression as:

```
A = B ^ (2 + C);
```

Oops. Although the operator notation gives a concise and intuitive interface, some expressions don’t meet our expectations. Therefore:

> **Respect Priorities**
> Pay attention that the semantic/intended priority of your overloaded operators matches the priorities of C++ operators.

### 2.7.3 Member or Free Function

Most operators can be defined as members or as free functions. The following operators—the simple assignment, `operator[]`, `operator->`, and `operator()`—must be methods because they are very tightly bound to the object. We have shown examples of `operator[]` and `operator()` in Section 2.6. In contrast, binary operators whose first argument is a fundamental type or one from another software package can only be implemented as free functions.

The impact of different implementation choices can be demonstrated with the addition operator for our `complex` class:

```
class complex
{
public:
    explicit complex(double rn = 0.0, double in = 0.0)
    : r(rn), i(in) {}
    complex operator+(const complex& c2) const
    {
        return complex(r + c2.r, i + c2.i);
    }
    ...
private:
    double r, i;
};

int main()
{
    complex cc(7.0, 8.0), c4(cc);
    std::cout << "cc + c4 is " << cc + c4 << std::endl;
}
```

Can we also add a `complex` and a `double`?

```
std::cout << "cc + 4.2 is " << cc + 4.2 << std::endl;
```

Not with the implementation above. We can add an overload for the operator accepting a `double` as a second argument:

```
class complex
{
    ...
}
```
