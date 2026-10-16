
could be appropriate for representing a simple phone book. For example:

```
list<Entry> phone_book = {
{"David Hume",123456},
{"Karl Popper",234567},
{"Bertrand Arthur William Russell",345678}
};
```

When we use a linked list, we tend not to access elements using subscripting the way we commonly do for vectors. Instead, we might search the list looking for an element with a given value. To do this, we take advantage of the fact that a list is a sequence as described in §4.5:

```
int get_number(const string& s)
{
for (const auto& x : phone_book)
if (x.name==s)
return x.number;
return 0; // use 0 to represent “number not found”
}
```

The search for s starts at the beginning of the list and proceeds until s is found or the end of phone_book is reached.

Sometimes, we need to identify an element in a list. For example, we may want to delete it or insert a new entry before it. To do that we use an iterator: a list iterator identifies an element of a list and can be used to iterate through a list (hence its name). Every standard-library container provides the functions begin() and end(), which return an iterator to the first and to one-past-the-last element, respectively (§4.5, §33.1.1). Using iterators explicitly, we can – less elegantly – write the get_number() function like this:

```
int get_number(const string& s)
{
for (auto p = phone_book.begin(); p!=phone_book.end(); ++p)
if (p->name==s)
return p->number;
return 0; // use 0 to represent “number not found”
}
```

In fact, this is roughly the way the terser and less error-prone range for loop is implemented by the compiler. Given an iterator p, *p is the element to which it refers, ++p advances p to refer to the next element, and when p refers to a class with a member m, then p->m is equivalent to (*p).m.

Adding elements to a list and removing elements from a list is easy:

```
void f(const Entry& ee, list<Entry>::iterator p, list<Entry>::iterator q)
{
phone_book.insert(p,ee); // add ee before the element referred to by p
phone_book.erase(q); // remove the element referred to by q
}
```

For a more complete description of insert() and erase(), see §31.3.7.

These list examples could be written identically using vector and (surprisingly, unless you understand machine architecture) perform better with a small vector than with a small list. When all we want is a sequence of elements, we have a choice between using a vector and a list. Unless you have a reason not to, use a vector. A vector performs better for traversal (e.g., find() and count()) and for sorting and searching (e.g., sort() and binary_search()).

## 4.4.3 map

Writing code to look up a name in a list of (name,number) pairs is quite tedious. In addition, a linear search is inefficient for all but the shortest lists. The standard library offers a search tree (a redblack tree) called map:

map: links
4 links
key:
value: links links

In other contexts, a map is known as an associative array or a dictionary. It is implemented as a balanced binary tree.

The standard-library map (§31.4.3) is a container of pairs of values optimized for lookup. We can use the same initializer as for vector and list (§4.4.1, §4.4.2):

```
map<string,int> phone_book {
{"David Hume",123456},
{"Karl Popper",234567},
{"Bertrand Arthur William Russell",345678}
};
```

When indexed by a value of its first type (called the key), a map returns the corresponding value of the second type (called the value or the mapped type). For example:

```
int get_number(const string& s)
{
return phone_book[s];
}
```

In other words, subscripting a map is essentially the lookup we called get_number(). If a key isn’t found, it is entered into the map with a default value for its value. The default value for an integer type is 0; the value I just happened to choose represents an invalid telephone number.

If we wanted to avoid entering invalid numbers into our phone book, we could use find() and insert() instead of [] (§31.4.3.1).

## 4.4.4 unordered_map

The cost of a **map** lookup is **O(log(n))** where **n** is the number of elements in the **map**. That’s pretty good. For example, for a **map** with 1,000,000 elements, we perform only about 20 comparisons and indirections to find an element. However, in many cases, we can do better by using a hashed lookup rather than comparison using an ordering function, such as <. The standard-library hashed containers are referred to as “unordered” because they don’t require an ordering function: **unordered_map**: rep
hash table:

For example, we can use an **unordered_map** from **<unordered_map>** for our phone book:

```
unordered_map<string,int> phone_book {
{"David Hume",123456},
{"Karl Popper",234567},
{"Bertrand Arthur William Russell",345678}
};
```

As for a **map**, we can subscript an **unordered_map**:

```
int get_number(const string& s)
{
return phone_book[s];
}
```

The standard-library **unordered_map** provides a default hash function for **string**s. If necessary, you can provide your own (§31.4.3.4).

## 4.4.5 Container Overview

The standard library provides some of the most general and useful container types to allow the programmer to select a container that best serves the needs of an application:

### Standard Container Summary

- vector<T>
- list<T>
- forward_list<T>
- deque<T>
- set<T>
- multiset<T>
- map<K,V>
- multimap<K,V>
- unordered_map<K,V> unordered_multimap<K,V> unordered_set<T>
- unordered_multiset<T>

A variable-size vector (§31.4)
A doubly-linked list (§31.4.2)

A singly-linked list (§31.4.2)
A double-ended queue (§31.2)
A set (§31.4.3)
A set in which a value can occur many times (§31.4.3) An associative array (§31.4.3)
A map in which a key can occur many times (§31.4.3) A map using a hashed lookup (§31.4.3.2)
A multimap using a hashed lookup (§31.4.3.2) A set using a hashed lookup (§31.4.3.2)
A multiset using a hashed lookup (§31.4.3.2)

The unordered containers are optimized for lookup with a key (often a string); in other words, they are implemented using hash tables.

The standard containers are described in §31.4. The containers are defined in namespace std and presented in headers <vector>, <list>, <map>, etc. (§4.1.2, §30.2). In addition, the standard library provides container adaptors queue<T> (§31.5.2), stack<T> (§31.5.1), deque<T> (§31.4), and priority_queue<T> (§31.5.3). The standard library also provides more specialized container-like types, such as a fixed-size array array<T,N> (§34.2.1) and bitset<N> (§34.2.2).

The standard containers and their basic operations are designed to be similar from a notational point of view. Furthermore, the meanings of the operations are equivalent for the various containers. Basic operations apply to every kind of container for which they make sense and can be efficiently implemented. For example:

- begin() and end() give iterators to the first and one-beyond-the-last elements, respectively.
- push_back() can be used (efficiently) to add elements to the end of a vector, forward_list, list, and other containers.
- size() returns the number of elements.

This notational and semantic uniformity enables programmers to provide new container types that can be used in a very similar manner to the standard ones. The range-checked vector, Vector (§2.3.2, §2.4.3.1), is an example of that. The uniformity of container interfaces also allows us to specify algorithms independently of individual container types. However, each has strengths and weaknesses. For example, subscripting and traversing a vector is cheap and easy. On the other hand, vector elements are moved when we insert or remove elements; list has exactly the opposite properties. Please note that a vector is usually more efficient than a list for short sequences of small elements (even for insert() and erase()). I recommend the standard-library vector as the default type for sequences of elements: you need a reason to choose another.

## 4.5 Algorithms

A data structure, such as a list or a vector, is not very useful on its own. To use one, we need operations for basic access such as adding and removing elements (as is provided for list and vector). Furthermore, we rarely just store objects in a container. We sort them, print them, extract subsets, remove elements, search for objects, etc. Consequently, the standard library provides the most common algorithms for containers in addition to providing the most common container types. For example, the following sorts a vector
