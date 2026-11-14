
Abstract classes can be considered as interfaces: we can declare references and pointers thereof but no objects. Note that C++ allows us to mix pure and regular virtual functions. Objects of sub-classes can only be built when all pure virtual functions are overridden.

Side note to Java programmers: In Java, all member functions are by nature virtual (i.e., methods cannot be non-virtual). Java provides the language feature interface where methods are only declared but not defined (unless they have the attribute default where allows for an implementation). This corresponds to a C++ class where all methods are pure virtual.

Large projects often establish multiple levels of abstraction:

- Interface: no implementations;
- Abstract class: default implementations;
- Specific classes.

This helps to keep a clear mental picture for an elaborate class system.

## 6.1.4 Functors via Inheritance

In Section 3.8, we discussed functors and mentioned that they can be implemented in terms of inheritance as well. Now, we keep our promise. First we need a common base class for all functors to be realized:

```cpp
struct functor_base
{
    virtual double operator()(double x) const = 0;
};
```

This base class can be abstract since it only serves us as an interface, for instance, to pass a functor to finite_difference evaluation:

```cpp
double finite_difference(functor_base const& f,
                             double x, double h)
{
    return (f(x+h) - f(x)) / h;
}
```

Evidently, all functors to be differentiated must be derived from functor_base, for instance:

```cpp
class para_sin_plus_cos
: public functor_base
{
public:
    para_sin_plus_cos(double p) : alpha(p) {}

    virtual double operator()(double x) const override
    {
        return sin(alpha * x) + cos(x);
    }

private:
    double alpha;
};
```

We reimplemented para_sin_plus_cos so that we can approximate the derivative of sin(αx) + cos x with finite differences:

```cpp
para_sin_plus_cos sin1(1.0);
cout << finite_difference(sin1, 1., 0.001) << endl;
double df1 = finite_difference(para_sin_plus_cos(2.), 1., 0.001),
df0a = finite_difference(para_sin_plus_cos(2.), 0., 0.001);
```

The object-oriented approach allows us as well to realize functions with states. If we like, we could also implement the finite differences as OOP functors and combine them similarly as the generic functors.

The disadvantages of the OOP approach are:

- Performance: operator() is always called as a virtual function.
- Applicability: Only classes that are derived from functor_base are allowed as arguments. A template parameter allows for traditional functions and any kind of functors including those from Section 3.8.

Thus, functors should be implemented whenever possible with the generic approach from Section 3.8. Only when functions are selected at run time does the use of inheritance provide a benefit.

2. We refrain from the term Instantiation to avoid confusion. The term is used in Java for saying that an object is built from a class (whereas some authors even call objects specific classes). In C++, instantiation almost always names the process of creating a specific class/function from a class/function template. We have occasionally seen the term "class instantiation" for the creation of an object from a class but this is not common terminology, and we avoid using it.

3. However, declaring them final enables the compiler to remove the overhead of late binding.

## 6.2 Removing Redundancy

By using inheritance and implicit up-casting, we can avoid the implementation of redundant member and free functions. The fact that classes are implicitly casted to super-classes allows us to implement common functionality once and reuse it in all derived classes. Say we have several matrix classes (dense, compressed, banded, triangle, ...) that share member functions like num_rows and num_cols⁴. These can be easily outsourced into a common super-class—including the corresponding data members:

```cpp
class base_matrix
{
public:
    base_matrix(size_t nr, size_t nc) : nr(nr), nc(nc) { }

    size_t num_rows() const { return nr; }
    size_t num_cols() const { return nc; }
private:
    size_t nr, nc;
};
class dense_matrix
    : public base_matrix
{ ... };
class compressed_matrix
    : public base_matrix
{ ... };
class banded_matrix
    : public base_matrix
{ ... };
...
```

All matrix types now provide the member functions from base_matrix by inheritance. Having the common implementations in one place not only saves typing but also ensures that modifications apply in all relevant classes at once. This is not an issue in this toy example (especially as there is not much to change anyway), but keeping all redundant code snippets consistent becomes pretty laborious in large projects.

Free functions can be reused in the same manner, for instance:

```cpp
inline size_t num_rows(const base_matrix& A)
{ return A.num_rows(); }
inline size_t num_cols(const base_matrix& A)
{ return A.num_cols(); }
inline size_t size(const base_matrix& A)
{ return A.num_rows() * A.num_cols(); }
```

These free functions can be called for all matrices derived from base_matrix thanks to implicit up-casting. This form of common base class functionality does not cost run time.

We can also consider the implicit up-cast of free functions' arguments as a special case of a more general concept: the is-a relation; for instance, compressed_matrix is-a base_matrix and we can pass a compressed_matrix value to every function that expects a base_matrix.

## 6.3 Multiple Inheritance

C++ provides multiple inheritance which we will illustrate now with some examples.

### 6.3.1 Multiple Parents

A class can be derived from multiple super-classes. For more figurative descriptions and for a less clumsy discussion of base classes' base classes we occasionally use the terms parents and grandparents which are intuitively understood. With two parents, the class hierarchy looks like a V (and with many like a bouquet). The members of the sub-class are the union of all super-class members. This bears the danger of ambiguities:

```cpp
class student
{
    virtual void all_info() const {
        cout << "[student] My name is " << name << endl;
        cout << " I passed the following grades: " << passed << endl;
    }
    ...
};

class mathematician
{
    virtual void all_info() const {
        cout << "[mathman] My name is " << name << endl;
        cout << " I proved: " << proved << endl;
    }
    ...
};

class math_student
: public student, public mathematician
{
};
// all_info not defined -> ambiguously inherited

int main ()
{
    math_student bob("Robert Robson", "Algebra", "Fermat's Last Theorem");
    bob.all_info();
}
```

math_student inherits all_info from student and from mathematician and there is no priority for one or another. The only way to disambiguate all_info for math_student is to define the method in the class math_student appropriately.

This ambiguity allows us to illustrate a subtlety of C++ that we should be aware of. public, protected, and private modify accessibility, not visibility. This becomes painfully clear when we try to disambiguate member functions by inheriting one or more super-classes as private or protected:

```cpp
class student { ... };
class mathematician { ... };
class math_student
    : public student, private mathematician
    { ... };
```

Now the methods of student are public and those of mathematician private. Calling math_student::all_info we hope to see now the output of student::all_info. Instead we get two error messages: first that math_student::all_info is ambiguous and in addition that mathematician::all_info is inaccessible.

### 6.3.2 Common Grandparents

It is not rare that multiple base classes share their base classes as well. In the previous section, mathematician and student had no super-classes. From the sections before, it would be more natural to derive them both from person. Depicting this inheritance configuration builds a diamond shape as in Figure 6-2. We will implement this in two slightly different ways.

### 6.3.2.1 Redundancy and Ambiguity

=> c++11/oop_multi.cpp

First, we implement the classes in a straightforward way:

```cpp
class person { ... } // as before
class student { ... } // as before
```

```cpp
class mathematician
    : public person
```

![](img/ba4defb7bf504868bf19451f3cd4b9bb_326_0.png)

Figure 6-2: Diamond-shaped class hierarchy
