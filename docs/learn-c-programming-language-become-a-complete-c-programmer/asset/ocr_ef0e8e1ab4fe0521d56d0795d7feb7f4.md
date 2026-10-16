```
```cpp
struct S2 {
  int a,b;
  S2(int a = 0, int b = 0): a(aa), b(bb) {}
};
// constructor
S1 x11(1,2); // error: no constructor S1 x12 {1,2}; // OK: memberwise initialization
S1 x13(1); // error: no constructor S1 x14 {1}; // OK: x14.b becomes 0
S2 x21(1,2); // OK: use constructor S2 x22 {1,2}; // OK: use constructor
S2 x23(1); // OK: use constructor and one default argument
S2 x24 {1}; // OK: use constructor and one default argument
```
```

The uniform use of {} initialization only became possible in C++11, so older C++ code uses () and = initialization. Consequently, the () and = may be more familiar to you. However, I don’t know any logical reason to prefer the () notation except in the rare case where you need to distinguish between initialization with a list of elements and a list of constructor arguments. For example:

```
```cpp
vector<int> v1 {77}; // one element with the value 77
vector<int> v2(77); // 77 elements with the default value 0
```
```

This problem – and the need to choose – can occur when a type with an initializer-list constructor (§17.3.4), typically a container, also has an “ordinary constructor” accepting arguments of the element type. In particular, we occasionally must use () initialization for vectors of integers and floating-point numbers but never need to for vectors of strings of pointers:

```
```cpp
vector<string> v1 {77}; // 77 elements with the default value ""
// (vector<string>(std::initializer_list<string>) doesn't accept {77})
vector<string> v2(77); // 77 elements with the default value ""

vector<string> v3 {"Booh!"}; vector<string> v4("Booh!");
// one element with the value “Booh!”
// error: no constructor takes a string argument
vector<int*> v5 {100,0}; // 100 int*s initialized to nullptr (100 is not an int*)

vector<int **> v6 {0,0}; // 2 int*s initialized to nullptr
vector<int**> v7(0,0); // empty vector (v7.size() == 0)
vector<int**> v8; // empty vector (v7.size() == 0)
```
```

The v6 and v7 examples are only of interest to language lawyers and testers.

# 17.3.3 Default Constructors

A constructor that can be invoked without an argument is called a default constructor. Default constructors are very common. For example:

```
```cpp
class Vector {
public:
  Vector(); // default constructor: no elements
  // ...
};
```
```