
```cpp
bool tooBig(int n){ return n > 100; }
list<int> scores;
```

scores.remove_if(tooBig);
Incidentally, this example shows where a class functor might be useful. Suppose you want to remove every value greater than 200 from a second list. It would be nice if you could pass the cut-off value to tooBig() as a second argument so you could use the function with different values, a predicate can have one argument. If, however, you design a TooBig class, you can use class members instead of function arguments to convey additional information:

```cpp
template<class T>
class TooBig {
private:
  T cutoff;
public:
  TooBig(const T & t) : cutoff(t) {}
  bool operator()(const T & v) { return v > cutoff; }
};
```

Here one value (v) is passed as a function argument, and the second argument (cutoff) is set by the class constructor. Given this definition, you can initialize different TooBig objects to different cut-off values to be used in calls to remove_if(). 16.15 illustrates the technique.

## Listing 16.15 functor.cpp

```cpp
// functor.cpp -- using a functor
#include <iostream>
#include <list>
#include <iterator>
#include <algorithm>
```

```cpp
template<class T> // functor class defines operator()
class TooBig {
private:
  T cutoff;
public:
  TooBig(const T & t) : cutoff(t) {}
  bool operator()(const T & v) { return v > cutoff; }
};
```

```cpp
void outint(int n) {std::cout << n << " ";}
```

```cpp
int main() {
  using std::list;
  using std::cout;
  using std::endl;

  TooBig<int> f100(100); // limit = 100
  int vals[10] = {50, 100, 90, 180, 60, 210, 415, 88, 188, 201};
  list<int> yadayada(vals, vals + 10); // range constructor
  list<int> etcetera(vals, vals + 10);
  // C++11 can use the following instead
  list<int> yadayada = {50, 100, 90, 180, 60, 210, 415, 88, 188, 201};
  list<int> etcetera = {50, 100, 90, 180, 60, 210, 415, 88, 188, 201};
  cout << "Original lists:\n";
  for_each(yadayada.begin(), yadayada.end(), cout);
  cout << endl;
  for_each(etcetera.begin(), etcetera.end(), cout);
  cout << endl;
  yadayada.remove_if(f100); // use a named function object
  etcetera.remove_if(TooBig<int>(200)); // construct a function object
  cout << "Trimmed lists:\n";
  for_each(yadayada.begin(), yadayada.end(), cout);
  cout << endl;
  for_each(etcetera.begin(), etcetera.end(), cout);
  cout << endl;
  return 0;
}
```

One functor (f100) is a declared object, and the second (TooBig<int>(200)) is an anonymous object created by a constructor call. Here's the output of the program in Listing 16.15:

Original lists:
50 100 90 180 60 210 415 88 188 201
50 100 90 180 60 210 415 88 188 201
Trimmed lists:
50 100 90 60 88
50 100 90 180 60 88

Suppose that you already have a template function with two arguments:

```cpp
template<class T>
bool tooBig(const T& val, const T& lim) {
  return val > lim;
}
```

## Chapter 16 The String Class and the Standard Template Library

You can use a class to convert it to a one-argument object:

```cpp
template<class T>
class TooBig {
private:
  T cutoff;
public:
  TooBig(const T & t) : cutoff(t) {}
  bool operator()(const T & v) { return v > cutoff; }
};
```

That is, you can use the following:

```cpp
TooBig<int> t100(100);
int x;
cin >> x;
if (t100(x)) // same as tooBig(x,100)
```

So the call t100(x) is the same as tooBig(x,100), but the two-argument function is converted to a one-argument object, with the second argument being used to construct the function object. In short, the class Too2 is a function adapter that adapts a function to a different interface.

As noted in the list, C++11's initializer-list feature simplifies initialization. You can replace

```cpp
list<int> vals[10] = {50, 100, 90, 180, 60, 210, 415, 88, 188, 201};
list<int> yadayada(vals, vals + 10); // range constructor
list<int> etcetera(vals, vals + 10);
```

with this:

```cpp
list<int> yadayada = {50, 100, 90, 180, 60, 210, 415, 88, 188, 201};
list<int> etcetera = {50, 100, 90, 180, 60, 210, 415, 88, 188, 201};
```

## Predefined Functors

The STL defines several elementary functors. They perform actions as adding two values and comparing two values for equality. They are provided to help STL functions that take functions as arguments. For example, the transform() function. The first version takes four arguments. The first two arguments are iterators that specify a range in a container (By now you must be familiar with this approach.). The third is an iterator that specifies where to copy the result. The final is a functor that is applied to each element in the range to produce each new element in the result. For example, consider the following:

```cpp
const int LIM = 5;
double arr1[LIM] = {36, 39, 42, 45, 48};
```

```cpp
vector<double> gr8(arr1, arr1 + LIM);
ostream_iterator<double, char> out(cout, " ");
transform(gr8.begin(), gr8.end(), sqrt);
```

This code calculates the square root of each element and sends the results to the output stream. The destination iterator can be in the original range. For example, replacing it with gr8.begin() would copy the new values over the old values. Clearly, the functor used must be one with a single argument.

The second version uses a functor that takes two arguments, applying the function to one element from each of two ranges. It takes an additional argument, which comes third in order, identifying the start of the range. For example, if m8 were a second vector<double> object and if mean(double, double) returned the mean of two values:

```cpp
transform(gr8.begin(), gr8.end(), m8.begin(), out, mean);
```

Now you want to add the two arrays. You can't use + as an argument because, for type double, + is not a function. You could define a function to add numbers and use it:

```cpp
double add(double x, double y) { return x + y; }
```

```cpp
transform(gr8.begin(), gr8.end(), m8.begin(), out, add);
```

But then you have to define a function for each type. It would be better to define a template, except that you do not have to because the STL already has. The functional (formerly function.h) header defines several template class function objects, including one plus<>().

Using the plus<>() class for ordinary addition is possible, if awkward:

```cpp
#include <functional>

plus<double> add; // create a plus<double> object
double y = add(2.2, 3.4); // using plus<double>::operator()
```

But it is easy to provide a function object as an argument:

```cpp
transform(gr8.begin(), gr8.end(), m8.begin(), out, plus<double>());
```

Here, rather than create a named object, the code uses the plus<double> constructor to construct a functor to do adding. (The parentheses indicate the default construct; which passed to transform() is the constructed function.)

The STL provides functor equivalents for the built-in arithmetic, relational, and logical operators. Table 16.12 shows the names for these functor equivalents. They can be used with C++ built-in types or any user-defined type that overloads the corresponding operator.

### Table 16.12 Operators and Functor Equivalents

| Operator | Functor Equivalent |
| :--- | :--- |
| + | plus |
| - | minus |
| * | multiplies |
| / | divides |
| % | modulus |
| - | negate |
| == | equal_to |
| != | not_equal_to |
| > | greater |
| < | less |
| >= | greater_equal |
| <= | less_equal |
| && | logical_and |
| || | logical_or |
| ! | logical_not |

> Caution
> Older C++ implementations use the function name times instead of multiplies.

## Adaptable Functions and Functor Adapters

The predefined functions in Table 16.12 are all adaptable. Actually, the STL has five related concepts: adaptable generators, adaptable unary functions, adaptable binary functions, adaptable predicates, and adaptable binary predicates.

What makes a functor adaptable is that it carries typedef members identifying its argument type and return type. The members are all result_type, first_argument_type, and second_argument_type, and they represent what they sound like.
