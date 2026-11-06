
If the order of the keys is not important, you can use `unordered_multimap` (header `<unordered_map>`) instead.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1955_0.png)

### Performance Tip 15.11

A `multimap` is implemented to efficiently locate all values paired with a given key.

```cpp
// Fig. 15.17: fig15_17.cpp
// Standard Library multimap class template.
#include <iostream>
#include <map> // multimap class-template definition
using namespace std;

int main() {
   multimap<int, double, less<int>> pairs; // create multimap

   cout << "There are currently " << pairs.count(15)
      << " pairs with key 15 in the multimap\n";

   // insert two value-type objects in pairs
   pairs.insert(make_pair(15, 99.3));
   pairs.insert(make_pair(15, 2.7));

   cout << "After inserts, there are " << pairs.count(15)
      << " pairs with key 15\n\n";

   // insert five value-type objects in pairs
   pairs.insert(make_pair(30, 111.11));
   pairs.insert(make_pair(10, 22.22));
   pairs.insert(make_pair(25, 33.333));
   pairs.insert(make_pair(20, 9.345));
   pairs.insert(make_pair(5, 77.54));

   cout << "Multimap pairs contains:\nKey\tValue\n";

   // walk through elements of pairs
   for (auto mapItem : pairs)
      cout << mapItem.first << '\t' << mapItem.second << '\n';
}
```

There are currently 0 pairs with key 15 in the multimap  
After inserts, there are 2 pairs with key 15

Multimap pairs contains:

| Key | Value |
| --- | ---: |
| 5 | 77.54 |
| 10 | 22.22 |
| 15 | 99.3 |
| 15 | 2.7 |
| 20 | 9.345 |
| 25 | 33.333 |
| 30 | 111.11 |

Fig. 15.17 Standard Library `multimap` class template.

Line 8 creates a `multimap` in which the key type is `int`, the type of a key’s associated value is `double` and the elements are ordered in *ascending order*—the template argument `less<int>` is the default ordering; it’s not required in the `multimap` declaration. Line 10 uses function `count` to determine the number of key–value pairs with a key of `15` (none yet, since the container is currently empty).

Line 14 uses function `insert` to add a new key–value pair to the `multimap`. The Standard Library function `make_pair` creates a key–value `pair` object—in this case `first` represents a key (`15`) of type `int` and `second` represents a value (`99.3`) of type `double`. Function `make_pair` automatically uses the types that you specified for the keys and values in the `multimap`’s declaration (line 8). Line 15 inserts another `pair` object with the key `15` and the value `2.7`. Then lines 17–18 output the number of pairs with key `15`. As of C++11, you can use list initialization for `pair` objects, so line 15 can be simplified as

```cpp
pairs.insert({15, 2.7});
```

Similarly, you can use C++11 list initialization to initialize an object being returned from a function. For example, the following returns a pair containing an `int` and a `double`

```cpp
return {15, 2.7};
```

Lines 21–25 insert five additional `pairs` into the `multimap`. The range-based `for` statement in lines 30–32 outputs the contents of the `multimap`, including both keys and values. We infer the type of the loop’s control variable (a `pair` containing an `int` key and a `double` value) with keyword `auto`. Line 31 accesses the members of the current `pair` in each element of the `multimap`. Notice in the output that the keys appear in *ascending order*.

### C++11: List Initializing a Key–Value Pair Container

In this example, we used separate calls to member function insert to place key–value pairs in a `multimap`. If you know the key–value pairs in advance, you can use list initialization when you create the `multimap`. For example, the following statement initializes a `multimap` with three key–value pairs that are represented by the sublists in the main initializer list:

```cpp
multimap<int, double, less<int>> pairs{
    {10, 22.2}, {20, 9.345}, {5, 77.54}};
```

## 15.6.4 `map` Associative Container

The *map associative container* (from header `<map>`) performs fast storage and retrieval of *unique keys and associated values*. Duplicate keys are *not* allowed—a single value can be associated with each key. This is called a **one-to-one mapping**. For example, a company that uses unique employee numbers, such as 100, 200 and 300, might have a `map` that associates employee numbers with their telephone extensions—4321, 4115 and 5217, respectively. With a `map` you specify the key and get back the associated data quickly. Providing the key in a `map`'s subscript operator `[]` locates the value associated with that key in the `map`. Insertions and deletions can be made *anywhere* in a `map`. If the order of the keys is not important, you can use `unordered_map` (header `<unordered_map>`) instead.

**Figure 15.18** demonstrates a `map` (created at line 8) and uses the same features as **Fig. 15.17** to demonstrate the subscript operator. Lines 27–28 use the subscript operator of class `map`. When the subscript is a key that's already in the `map` (line 27), the operator returns a reference to the associated value. When the subscript is a key that's *not* in the `map` (line 28), the operator inserts the key in the `map` and returns a reference that can be used to associate a value with that key. Line 27 replaces the value for the key `25` (previously `33.333` as specified in line 15) with a new value, `9999.99`. Line 28 inserts a new key–value pair in the `map` (called **creating an association**). Note this example’s `map` could have been initialized with an initializer list of `pair`s, as we showed for a `multimap` in **Section 15.6.3**.

```cpp
// Fig. 15.18: fig15_18.cpp
// Standard Library class map class template.
#include <iostream>
#include <map> // map class-template definition
using namespace std;

int main() {
   map<int, double, less<int>> pairs;

   // insert eight value_type objects in pairs
   pairs.insert(make_pair(15, 2.7));
   pairs.insert(make_pair(30, 111.11));
   pairs.insert(make_pair(5, 1010.1));
   pairs.insert(make_pair(10, 22.22));
   pairs.insert(make_pair(25, 33.333));
   pairs.insert(make_pair(5, 77.54)); // dup ignored
   pairs.insert(make_pair(20, 9.345));
   pairs.insert(make_pair(15, 99.33)); // dup ignored

   cout << "pairs contains:\nKey\tValue\n";

   // walk through elements of pairs
   for (auto mapItem : pairs) {
      cout << mapItem.first << '\t' << mapItem.second << '\n';
   }

   pairs[25] = 9999.99; // use subscripting to change value for key 25
   pairs[40] = 8765.43; // use subscripting to insert value for key 40

   cout << "\nAfter subscript operations, pairs contains:\nKey\tValue\n";

   // use const_iterator to walk through elements of pairs
   for (auto mapItem : pairs) {
      cout << mapItem.first << '\t' << mapItem.second << '\n';
   }

   cout << endl;
}
```

pairs contains:

| Key | Value |
| --- | ---: |
| 5 | 1010.1 |
| 10 | 22.22 |
| 15 | 2.7 |
| 20 | 9.345 |
| 25 | 33.333 |
| 30 | 111.11 |

After subscript operations, pairs contains:

| Key | Value |
| --- | ---: |
| 5 | 1010.1 |
| 10 | 22.22 |
| 15 | 2.7 |
| 20 | 9.345 |
| 25 | 9999.99 |
| 30 | 111.11 |
| 40 | 8765.43 |

Fig. 15.18 Standard Library `map` class template.

## 15.7 Container Adapters

The three **container adapters** are `stack`, `queue` and `priority_queue`. Container adapters are *not first-class containers*, because they do *not* provide the actual data-structure implementation in which elements can be stored and because *adapters do not support iterators*. The benefit of an *adapter class* is that you can choose an appropriate underlying data structure. All three *adapter classes* provide member functions `push` and `pop` that properly insert an element into each adapter data structure and properly remove an element from each adapter data structure, respectively. The next several subsections provide examples of the adapter classes.

### 15.7.1 `stack` Adapter

Class `stack` (from header `<stack>`) enables insertions into and deletions from the underlying container at one end called the *top*, so a stack is commonly referred to as a *last-in, first-out* data structure. We introduced stacks in our discussion of the function-call stack in **Section 6.11**. A `stack` can be implemented with a `vector`, `list` or `deque`. This example creates three integer stacks, using `vector`, `list` and `deque` as the underlying data structure to represent the `stack`. By default, a `stack` is implemented with a `deque`. The `stack` operations are `push` to insert an element at the *top* of the `stack` (implemented by calling function `push_back` of the underlying container), `pop` to remove the *top* element of the `stack` (implemented by calling function `pop_back` of the underlying container), `top` to get a reference to the top element of the `stack` (implemented by calling function `back` of the underlying container), `empty` to determine whether the `stack` is empty (implemented by calling function `empty` of the underlying container) and `size` to get the number of elements in the `stack` (implemented by calling function `size` of the underlying container). In **Chapter 19**, we’ll show you how to develop your own custom stack class template.

**Figure 15.19** demonstrates the `stack` adapter class. Lines 17, 20 and 23 instantiate three integer stacks. Line 17 specifies a `stack` of
