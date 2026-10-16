
increased performance. For example, it can also be used to spawn a task for getting information from a user, leaving the “main program” active with something else (§24.6).

## 5.4 Small Utility Components

Not all standard-library components come as part of obviously labeled facilities, such as “containers” or “I/O.” This section gives a few examples of small, widely useful components:

- **clock** and **duration** for measuring time.
- Type functions, such as **iterator_traits** and **is_arithmetic**, for gaining information about types.
- **pair** and **tuple** for representing small potentially heterogeneous sets of values. The point here is that a function or a type need not be complicated or closely tied to a mass of other functions and types to be useful. Such library components mostly act as building blocks for more powerful library facilities, including other components of the standard library.

### 5.4.1 Time

The standard library provides facilities for dealing with time. For example, here is the basic way of timing something:

```
using namespace std::chrono; // see §35.2

auto t0 = high_resolution_clock::now();
do_work();
auto t1 = high_resolution_clock::now();
cout << duration_cast<milliseconds>(t1-t0).count() << "msec\n";
```

The clock returns a **time_point** (a point in time). Subtracting two **time_points** gives a **duration** (a period of time). Various clocks give their results in various units of time (the clock I used measures **nanoseconds**), so it is usually a good idea to convert a **duration** into a known unit. That’s what **duration_cast** does.

The standard-library facilities for dealing with time are found in the subnamespace **std::chrono** in

**<chrono>** (§35.2).
Don’t make statements about “efficiency” of code without first doing time measurements. Guesses about performance are most unreliable.

### 5.4.2 Type Functions

A *type function* is a function that is evaluated at compile-time given a type as its argument or returning a type. The standard library provides a variety of type functions to help library implementers and programmers in general to write code that take advantage of aspects of the language, the standard library, and code in general.

For numerical types, **numeric_limits** from **<limits>** presents a variety of useful

information (§5.6.5). For example:

```
constexpr float min = numeric_limits<float>::min(); // smallest positive float (§40.2)
```

Similarly, object sizes can be found by the built-in sizeof operator (§2.2.2). For example:

```
constexpr int szi = sizeof(int); // the number of bytes in an int
```

Such type functions are part of C++’s mechanisms for compile-time computation that allow tighter type checking and better performance than would otherwise have been possible. Use of such features is often called metaprogramming or (when templates are involved) template metaprogramming (Chapter 28). Here, I just present two facilities provided by the standard library: iterator_traits (§5.4.2.1) and type predicates (§5.4.2.2).

#### 5.4.2.1 iterator_traits

The standard-library sort() takes a pair of iterators supposed to define a sequence (§4.5). Furthermore, those iterators must offer random access to that sequence, that is, they must be randomaccess iterators. Some containers, such as forward_list, do not offer that. In particular, a forward_list is a singly-linked list so subscripting would be expensive and there is no reasonable way to refer back to a previous element. However, like most containers, forward_list offers forward iterators that can be used to traverse the sequence by algorithms and for-statements (§33.1.1).

The standard library provides a mechanism, iterator_traits that allows us to check which kind of iterator is supported. Given that, we can improve the range sort() from §4.5.6 to accept either a vector or a forward_list. For example:

```
void test(vector<string>& v, forward_list<int>& lst)
{
sort(v); // sort the vector
sort(lst); // sort the singly-linked list
}
```

The techniques needed to make that work are generally useful.

First, I write two helper functions that take an extra argument indicating whether they are to be used for random-access iterators or forward iterators. The version taking random-access iterator arguments is trivial:

```
template<typename Ran>
void sort_helper(Ran beg, Ran end, random_access_iterator_tag) {
sort(beg,end); // just sort it
}
// for random-access iterators // we can subscript into [beg:end)
```

The version for forward iterators is almost as simple; just copy the list into a vector, sort, and copy back again:

```
template<typename For> // for forward iterators void sort_helper(For beg, For end, forward_iterator_tag) // we can traverse [beg:end) {
```

```
```cpp
vector<decltype (*beg)> v {beg,end}; // initialize a vector from [beg:end)
sort(v.begin(),v.end());
copy(v.begin(),v.end(),beg); // copy the elements back
}
```
```

The **decltype()** is a built-in type function that returns the declared type of its argument (§6.3.6.3). Thus, **v** is a **vector<X>** where X is the element type of the input sequence.

The real “type magic” is in the selection of helper functions:

```
```cpp
template<typename C>
void sort(C& c)
{
    using Iter = Iterator_type<C>;
    sort_helper(c.begin(),c.end(),Iterator_category<Iter>{});
}
```
```

Here, I use two type functions: **Iterator_type<C>** returns the iterator type of **C** (that is, **C::iterator**) and then **Iterator_category<Iter>{}** constructs a “tag” value indicating the kind of iterator provided:

- **std::random_access_iterator_tag** if C’s iterator supports random access.
- **std::forward_iterator_tag** if C’s iterator supports forward iteration.

Given that, we can select between the two sorting algorithms at compile time. This technique, called *tag dispatch* is one of several used in the standard library and elsewhere to improve flexibility and performance.

The standard-library support for techniques for using iterators, such as tag dispatch, comes in the form of a simple class template **iterator_traits** from **<iterator>** (§33.1.3). This allows simple definitions of the type functions used in **sort()**:

```
```cpp
template<typename C>
using Iterator_type = typename C::iterator; // C’s iterator type
template<typename Iter>
using Iterator_category = typename std::iterator_traits<Iter>::iterator_category; //
Iter’s category
```
```

If you don’t want to know what kind of “compile-time type magic” is used to provide the standard-library features, you are free to ignore facilities such as **iterator_traits**. But then you can’t use the techniques they support to improve your own code.

#### 5.4.2.2 Type Predicates

A standard-library type predicate is a simple type function that answers a fundamental question about types. For example:

```
```cpp
bool b1 = Is_arithmetic<int>(); bool b2 = Is_arithmetic<string>();
// yes,int is an arithmetic type
// no,std::string is not an arithmetic type
```
```

These predicates are found in **<type_traits>** and described in §35.4.1. Other examples are **is_class**, **is_pod**, **is_literal_type**, **has_virtual_destructor**, and **is_base_of**. They are most useful when we write templates. For example:

naming is not particularly creative and may look a bit odd at first, but such consistent naming is a boon when we want to write generic code.

The standard-library pair (from <utility>) is quite frequently used in the standard library and elsewhere. A pair provides operators, such as =, ==, and <, if its elements do. The make_pair() function makes it easy to create a pair without explicitly mentioning its type (§34.2.4.1). For example:

```
void f(vector<string>& v)
{
auto pp = make_pair(v.begin(),2); // pp is a pair<vector<string>::iterator,int>
// ...
}
```

If you need more than two elements (or less), you can use tuple (from <utility>; §34.2.4.2). A tuple is a heterogeneous sequence of elements; for example:

```
tuple<string,int,double> t2("Sild",123, 3.14); // the type is explicitly specified
auto t = make_tuple(string("Herring"),10, 1.23); // the type is deduced
// tisatuple<string,int,double>
```

```
string s = get<0>(t); // get first element of tuple int x = get<1>(t);
double d = get<2>(t);
```

The elements of a tuple are numbered (starting with zero), rather than named the way elements of pairs are (first and second). To get compile-time selection of elements, I must unfortunately use the ugly get<1>(t), rather than get(t,1) or t[1] (§28.5.2).

Like pairs, tuples can be assigned and compared if their elements can be.

A pair is common in interfaces because often we want to return more than one value, such as a result and an indicator of the quality of that result. It is less common to need three or more parts to a result, so tuples are more often found in the implementations of generic algorithms.

## 5.5 Regular Expressions

Regular expressions are a powerful tool for text processing. They provide a way to simply and tersely describe patterns in text (e.g., a U.S. ZIP code such as TX 77845, or an ISO-style date, such as 2009-06-07) and to efficiently find such patterns in text. In <regex>, the standard library provides support for regular expressions in the form of the std::regex class and its supporting functions. To give a taste of the style of the regex library, let us define and print a pattern:

```
regex pat (R"(\w{2}\s*\d{5}(-\d{4})?)"); // ZIP code pattern: XXdddd-dddd and variants
cout << "pattern: " << pat << '\n';
```

People who have used regular expressions in just about any language will find \w{2}\s*\d{5}(-\d{4})? familiar. It specifies a pattern starting with two letters \w{2} optionally followed by some space \s* followed by five digits \d{5} and optionally followed by a dash and four digits-\d{4}. If you are not familiar with regular expressions, this may be a good time to learn about them ([Stroustrup,2009], [Maddock,2009], [Friedl,1997]).
