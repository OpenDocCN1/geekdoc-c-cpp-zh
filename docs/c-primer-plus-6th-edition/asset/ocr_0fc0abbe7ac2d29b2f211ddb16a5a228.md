methods treat the elements as if they were const. Similarly, crbeg() and crend() are
const versions of rbegin() and rend().

More significantly, STL containers now have move constructors and move assignment
operators in addition to the traditional copy constructors and regular assignment opera-
tors. This describes move semantics later.

# valarray Upgrade

The valarray template was developed independently of the STL, and its original design
precluding using range-based STL algorithms with valarray objects. C++11 adds two
functions, begin() and end(), that each take a valarray argument. They return iterators
to the first and one past the last element of a valarray object, allowing one to use range-ased STL algorithms (see Chapter 16).

# export Departs

C++98 introduced the export keyword in the hereof of creating a way to separate tem-
plate definitions into interface files containing the prototypes and template declarations
and implementation files containing the template function and methods definitions. This
proved to be impractical, and C++11 ends that for export. However, the Standard
retains export as a keyword for possible future use.

# Angle Brackets

To avoid confusion with the >> operator, C++ required a space between the brackets in
nested template declarations:

```
std::vector<std::list<int>> vl; // not ok
```

C++11 removes that requirement:

```
std::vector<std::list<int>> vl; // ok in C++11
```

# The Rvalue Reference

The traditional C++ reference, now called an lvalue reference, binds an identifier to an
lvalue. An lvalue is an expression, such as a variable name or a dereferenced pointer, that
represents data for which the program can obtain an address. Originally, an lvalue was
could appear on the left side of an assignment statement, but the advent of the const
modifier allowed constructs that cannot be assigned to but which are still addressable:

```
* pt = new int;
const int b = 101; // can't assign to b, but &b is valid
int & n = n; // n identifies datum at address &
int & rt = *pt; // pt identifies datum at address pt
const int & rb = b; // b identifies datum at address &
```

C++11 adds the rvalue reference (discussed in Chapter 8), indicated by &&, that
can bind to values—that is, values that can appear on the right-hand side of an