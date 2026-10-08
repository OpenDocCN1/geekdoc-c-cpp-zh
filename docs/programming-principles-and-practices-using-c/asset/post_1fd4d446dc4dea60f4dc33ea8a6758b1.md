
To get the best of both worlds, we can build an **array** container that provides the benefits of arrays without the weaknesses. The **array** is now part of the standard defined in `<array>`, but let’s see how we might define it. The idea is simple and useful:

```cpp
template <typename T, int N>
// requires Element<T>()
struct array {
    // not quite the standard array
    using value_type = T;
    using iterator = T*;
    using const_iterator = const T*;
    using size_type = unsigned int;
    // the type of a subscript
    T elems[N];
    // no explicit construct/copy/destroy needed
    iterator begin() { return elems; }
    const_iterator begin() const { return elems; }
    iterator end() { return elems+N; }
    const_iterator end() const { return elems+N; }
    size_type size() const;
    T& operator[](int n) { return elems[n]; }
    const T& operator[](int n) const { return elems[n]; }
    const T& at(int n) const;
    // range-checked access
    T& at(int n);
    // range-checked access
    T * data() { return elems; }
    const T * data() const { return elems; }
};
```

This definition isn’t complete or completely standards-conforming, but it will give you the idea. It will also give you something to use if your implementation doesn’t yet provide the standard **array**. If available, it is in `<array>`. Note that because **array<T,N>** “knows” that its size is N, we can (and do) provide assignment, `==`, `!=`, etc., just as for **vector**.
As an example, let’s use an array with the STL version of **high()** from §20.4.2:

```cpp
void f()
{
    array<double,6> a = { 0.0, 1.1, 2.2, 3.3, 4.4, 5.5 };
    array<double,6>::iterator p = high(a.begin(), a.end());
    cout << "the highest value was " << *p << '\n';
}
```

Note that we did not think of **array** when we wrote **high()**. Being able to use **high()** for an **array** is a simple consequence of following standard conventions for both.

## 20.10 Container overview

The STL provides quite a few containers:

| Standard containers | Description |
|---|---|
| **vector** | a contiguously allocated sequence of elements; use it as the default container |
| **list** | a doubly-linked list; use it when you need to insert and delete elements without moving existing elements |
| **deque** | a cross between a **list** and a **vector**; don’t use it until you have expert-level knowledge of algorithms and machine architecture |
| **map** | a balanced ordered tree; use it when you need to access elements by value (see §21.6.1–3) |
| **multimap** | a balanced ordered tree where there can be multiple copies of a key; use it when you need to access elements by value (see §21.6.1–3) |
| **unordered_map** | a hash table; an optimized version of **map**; use for large maps when you need high performance and can devise a good hash function (see §21.6.4) |
| **unordered_multimap** | a hash table where there can be multiple copies of a key; an optimized version of **multimap**; use it for large maps when you need high performance and can devise a good hash function (see §21.6.4) |
| **set** | a balanced ordered tree; use it when you need to keep track of individual values (see §21.6.5) |
| **multiset** | a balanced ordered tree where there can be multiple copies of a key; use it when you need to keep track of individual values (see §21.6.5) |
| **unordered_set** | like **unordered_map**, but just with values, not (key,value) pairs |
| **unordered_multiset** | like **unordered_multimap**, but just with values, not (key,value) pairs |
| **array** | a fixed-size array that doesn’t suffer most of the problems related to the built-in arrays (see §20.9) |

You can look up incredible amounts of additional information on these containers and their use in books and online documentation. Here are a few quality information sources:

*   Josuttis, Nicolai M. *The C++ Standard Library: A Tutorial and Reference*. Addison-Wesley, 2012. ISBN 978-0321623218. Use only the 2nd edition.
*   Lippman, Stanley B., Jose Lajoie, and Barbara E. Moo. *The C++ Primer*. Addison-Wesley, 2005. ISBN 0201721481. Use only the 5th edition.
*   Stroustrup, Bjarne. *The C++ Programming Language*. Addison-Wesley, 2012. ISBN 978-0321714114. Use only the 4th edition.
*   The documentation for the SGI implementation of the STL and the iostream library: www.sgi.com/tech/stl. Note that they also provide complete code.

Do you feel cheated? Do you think we should explain all about containers and their use to you? That’s just not possible. There are too many standard facilities, too many useful techniques, and too many useful libraries for you to absorb them all at once. Programming is too rich a field for anyone to know all facilities and techniques – it can also be a noble art. As a programmer, you must acquire the habit of seeking out new information about language facilities, libraries, and techniques. Programming is a dynamic and rapidly developing field, so just being content with what you know and are comfortable with is a recipe for being left behind. “Look it up” is a perfectly reasonable answer to many problems, and as your skills grow and mature, it will more and more often be the answer.

On the other hand, you will find that once you understand **vector, list**, and **map** and the standard algorithms presented in Chapter 21, you’ll find other STL and STL-style containers easy to use. You’ll also find that you have the basic knowledge to understand non-STL containers and code using them.

What is a container? You can find the definition of an STL container in all of the sources above. Here we will just give an informal definition. An STL container:

*   Is a sequence of elements `[begin():end()]`.
*   Provides copy operations that copy elements. Copying can be done with *assignment* or a copy constructor.
*   Names its element type **value_type**.
*   Has iterator types called **iterator** and **const_iterator**. Iterators provide `*`, `++` (both prefix and postfix), `==`, and `!=` with the appropriate semantics. The iterators for **list** also provide `--` for moving backward in the sequence; that’s called a *bidirectional iterator*. The iterators for **vector** also provide `--`, `[]`, `+`, and `—` and are called **random-access iterators**. (See §20.10.1.)
*   Provides `insert()`, `erase()`, `front()` and `back()`, `push_back()` and `pop_back()`, `size()`, etc.; `vector` and `map` also provide subscripting (e.g., operator []).
*   Provides comparison operators (`==`, `!=`, `<`, `<=`, `>`, and `>=`) that compare the elements. Containers use lexicographical ordering for `<`, `<=`, `>`, and `>=`; that is, they compare the elements in order starting with the first.

The aim of this list is to give you an overview. For more detail see Appendix B. For a more precise specification and complete list, see *The C++ Programming Language* or the standard.

Some data types provide much of what is required from a standard container, but not all. We sometimes refer to those as “almost containers.” The most interesting of those are:

| “Almost containers” | Description |
|---|---|
| `T[n]` built-in array | no `size()` or other member functions; prefer a container, such as `vector`, `string`, or `array`, over a built-in array when you have a choice |
| `string` | holds only characters but provides operations useful for text manipulation, such as concatenation (`+` and `+=`); prefer the standard string to other strings |
| `valarray` | a numerical vector with vector operations, but with many restrictions to encourage high-performance implementations; use only if you do a lot of vector arithmetic |

In addition, many people and many organizations have produced containers that meet the standard container requirements, or almost do so.
If in doubt, use `vector`. Unless you have a solid reason not to, use `vector`.

## 20.10.1 Iterator categories

We have talked about iterators as if all iterators are interchangeable. They are interchangeable if you do only the simplest operations, such as traversing a sequence once reading each value once. If you want to do more, such as iterating backward or subscripting, you need one of the more advanced iterators.
