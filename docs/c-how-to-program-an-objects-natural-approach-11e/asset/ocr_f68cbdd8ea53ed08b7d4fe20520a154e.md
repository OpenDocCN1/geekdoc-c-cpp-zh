```
```cpp
// insert 9.5 in doubles
p = doubles.insert(9.5); // value already in set
std::cout << std::format("\n{} {} inserted\n", *p.first,
    (p.second ? "was" : "was not"));
std::cout << "doubles contains: ";
std::ranges::copy(doubles, output);
std::cout << "\n";
}
```

```
```text
9.5 was not inserted
doubles contains: 2.1 3.7 4.2 9.5 13.8
```
```

# 13.11.3 multimap Associative Container

The **multimap associative container** is used for fast storage and retrieval of keys and associated values (often called key–value pairs). Many of the functions used with **multisets** and **sets** are also used with **multimaps** and **maps**. The elements of multimaps and maps are pairs of keys and values. When inserting into a multimap or map, you use a pair object containing the key and the value. The ordering of the keys is determined by a **comparator function** object. For example, in a multimap that uses integers as the key type, keys can be sorted in ascending order by ordering them with comparator function object less<int>.

In a multimap, multiple values can be associated with a single key. This is called a one-to-many relationship. For example, in a credit-card transaction-processing system, one credit-card account can have many associated transactions; in a university, one student can take many courses, and one professor can teach many students; in the military, one rank (like “private”) has many people. A **multimap** supports bidirectional iterators.

# Creating a multimap Containing Key–Value Pairs

Figure 13.8 demonstrates the **multimap associative container** (header <map>). If the order of the keys is not important, you can use **unordered_multimap** (header <unordered_map>) instead. A multimap is implemented to efficiently locate all values paired with a given key. Line 8 creates a multimap in which the key type is int, the type of a key’s associated value is double, and the elements are ordered in ascending order by default. This is equivalent to

```
```cpp
std::multimap<int, double, std::less<int>> pairs{};
```
```

```
```cpp
// fig13_08.cpp
// Standard library multimap class template.
#include <format>
#include <iostream>
#include <map> // multimap class-template definition

int main() {
    std::multimap<int, double> pairs{}; // create multimap
```
```

**Fig. 13.8** | Standard library multimap class template.