We see that if you call a deprecated function or try to access deprecated data then the code will not compile and it will issue an error message. We conclude this section with a concocted example of a class with a mixture of deprecated and non-deprecated members:

```
struct [[deprecated("old skule class")]] C
{
    C() : data(1) {}

    [[deprecated]] int data;

    [[deprecated]] void print() { std::cout << "Deprecated\n"; }
    void NewPrint() const { std::cout << "Not deprecated\n"; }
};
```

An example shows which code compiles and which does not:

```
C C;
// C.data = 10;
//C.print();
C.NewPrint();
```

There are a number of other attributes defined for C++17 but a discussion is outside the scope of this book. We are not yet convinced of the usefulness of this feature.

# 2.6.8  Digit Separators

This functionality is a useful way to represent numbers in a more readable form. An example is:

```
int x = 1'000'000; // This is a digit separator
```

There is not much more that we can say about this feature. It can be seen as *syntactic sugaring*.

# 2.6.9  Unrestricted Unions

*A union* is a variable that may hold objects of different types and of different sizes at different times. The compiler keeps track of size and alignment requirements. Thus, unions provide a way to manipulate different kinds of data in a single area of storage (Kernighan and Ritchie, 1988).

C++03 placed restrictions on the types of objects that can be members of a union. For example, they may not contain objects that have a non-trivial constructor or destructor. C++11 does not have these restrictions. We take an example:

```
struct Point
{
    double x, y;
};
```