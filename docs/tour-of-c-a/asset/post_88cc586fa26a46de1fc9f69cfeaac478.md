
```cpp
Vector(int);
Vector(initializer_list<T>); // The initializer-list constructor
```

Vector v1 {1, 2, 3}; // The v1's element type from the initializer element type: int
Vector v2 = v1; // The v2's element type from v1's element type: int

```cpp
auto p = new Vector(1, 2, 3); // p is a Vector<int>*
```

```cpp
Vector<int> v3(1); // We need to be explicit about the element type (no element type is mentioned)
```

Clearly, this notation avoids and eliminates annoyances by omitting redundant template arguments. However, it is not a panacea. Like other powerful mechanisms, deduction can cause issues. Consider:

Click here to view code image

```cpp
Vector<string> vs = {"Hello", "World"}; // The OK: Vector<string>
Vector v1 {"Hello", "World"}; // It deduces to Vector<const char*> (Surprise?)
Vector v2 {"Hello", "World"}; // It deduces to Vector<string>
Vector v3 {"Hello", "World"}; // The error: the initializer list is not homogeneous
Vector v4 {"Hello", "World"}; // The OK: the element type is explicit
```

The type of a C-style string literal is const char (§1.7.1). If that is not what is intended for vs, we must be explicit about the element type or use the s to make it string (§10.2).

If elements of an initializer list have different types, we cannot deduce a unique element type, so we get an ambiguity error.

Sometimes, we need to resolve an ambiguity. For example, the standard-library vector has a constructor that takes pairs of iterators delimiting a sequence and also an initializer constructor that can take a pair of values.

Click here to view code image

```cpp
template<typename T>
class Vector {
public:
    Vector(initializer_list<T> iter); // The initializer-list constructor

    template<typename Iter>
    Vector(Iter b, Iter e); // b, e: iterator constructor

    struct iterator { using value_type = T; /* ... */ };
    iterator begin();

};
```

```cpp
Vector v1 {1, 2, 3, 5}; // The element type is int
Vector v2(v1.begin(),v1.begin()+2); // A pair of iterators or a pair of values (of type iterator)
Vector v3(9, 17); // The error: ambiguous
```

We could resolve this using concepts (§8.2), but the standard library and many other important bodies of code were written before our language had support for concepts. For these, we need a way of saying “a pair of values of the same type should be considered iterators.” Adding a deduction guide after the declaration of Vector does exactly that:

Click here to view code image
```cpp
template<typename Iter>
Vector(Iter, Iter) -> Vector<Iter>::value_type;
```

Now we have:
Click here to view code image

```cpp
Vector v1 (1, 2, 3, 4);             // The element type is int
Vector v2(v1.begin(),v1.begin()+2);  // pair-of-iterators: element type is int
Vector v3 (v1.begin(),v1.begin()+2);  // The element type is Vector::iterator
```

The {} syntax prefers the initializer_list constructor (if present), so v3 is a vector of iterators: Vector<int>::iterator.
The initialization syntax (§12.5) is conventional for when we don't want an initializer_list.
The effects of deduction guides are often subtle, so it is best to design class templates so that deduction guides are not needed.
People like acronyms refer to "class template argument deduction" as CTAD.

## 7.3 Parameterized Operations

Templates have many more than simply parameterizing a container with an element type. In particular, they are used for parameterization of both types and algorithms in the standard library (§12.8, §13.5).

- There are three ways of expressing an operation parameterized by types or values:
- A function template
- A function object: an object that can carry data and can be called like a function
- A lambda expression: a shorthand notation for a function object

## 7.3.1 Function Templates

We can write a function that calculates the sum of element values of any sequence that a range-for can traverse (e.g., a container) like this:

Click here to view code image
```cpp
template<typename Sequence, typename Value>
Value sum(const Sequence& s, Value v)
{
    for (auto x : s)
        v += x;
    return v;
}
```

The Value template argument and the function argument v are there to allow the caller to specify the type and initial value of the accumulator (the variable in which to accumulate):

Click here to view code image

```cpp
void user(Vector<int> vi, list<double>& ld, vector<double>& vc)
{
    int x = sum(vi,0.0);
    double d = sum(vi,0.0);
    double dd = sum(ld,0.0);
    auto z = sum(vc,0.0)
}
```

The point of adding ints in double will be sum much larger than the int. Note how the types for sum<Sequence,Value> are deduced from the function arguments. Frankly, we do not need to explicitly specify those types. This sum is a simplified version of the standard-library accumulate() (§17.3). A function template can be a member function, but not virtual member. The compiler will not know all instances of such a template in a program, or could generate virtual (§5.4).

## 7.3.2 Function Objects

A particularly useful template is the function object (sometimes called a functor), which is used to define objects that can be called like functions. For example:

Click here to view code image

```cpp
template<typename T>
class Less {
    T val; // Value to compare against
public:
    Less(const T& v) : val(v) {}
    bool operator()(const T& x) const { return x < val; } // Call operator
};
```

The function operator() implements the application, also called "function call" or just "call." We can define named types of Less for any argument type:

Click here to view code image

| Code | Description |
| :--- | :--- |
| Less(42); | Less(i) compares i to 42 |
| Less("Backus"); | Less(s) compares s to "Backus" |
| Less<string>("Nau"); | "Nau" is a C-style string, so we need <string> to get the right type |

We can call such an object just as a function call:

Click here to view code image

```cpp
void fct(int n, const string& s)
{
    bool b1 = Less(n); // true if n < 42
    bool b2 = Less(s); // true if s < "Backus"
    // ...
}
```

Function objects are widely used as arguments to algorithms. For example, we can count the values for which a predicate returns true:

Click here to view code image

```cpp
template<typename C, typename P>
int count(const C& c, P pred) // assume that C is a container and P is a predicate on its elements
{
  int cnt = 0;
  for (const auto& x : c) {
    if (pred(x))
      cnt++;
  }
  return cnt;
}
```

This is a simplified version of the standard-library count_if algorithm (§13.5). Given objects (§8.2), we can formalize count()'s assumptions about its argument and check them at compile time.

A predicate is something we can invoke to return true or false. For example:

Click here to view code image

```cpp
void fcount(vector<int>& vec, const list<string>& lst, int x, const string& s) {
  cout << "number of values less than " << x << ": " << count(vec,x) << "\n";
  cout << "number of values less than " << s << ": " << count(lst,Less(s)) << "\n";
}
```

Here, Less(x) constructs an object of type Less<int>, which the call operator compares the value of the int called x; Less(s) constructs an object that compares to the value of the string called s.

The beauty of function objects is that they carry the value to be compared with (and type), and we don't have to introduce noisy global variables to hold values. Also, for a simple function object like Less, inlining is simple, a call of Less is far more efficient than an indirect call. The ability to carry data plus their efficiency makes function objects particularly useful as arguments to algorithms.

Function objects used to specify the meaning of key of a general algorithm (such as Less for count()) are sometimes referred to as policy objects.

## 7.3.3 Lambda Expressions

In §7.3.2, we defined Less_than separately from its use. That can be inconvenient. Consequently, there is a notation for implicitly generating function objects:

Click here to view code image

```cpp
void fcount(vector<int>& vec, const list<string>& lst, int x, const string& s) {
  cout << "number of values less than " << x << ": " << count(vec,[](int a){return a < x;}) << "\n";
  cout << "number of values less than " << s << ": " << count(lst,[](const string& a){return a < s;}) << "\n";
}
```
