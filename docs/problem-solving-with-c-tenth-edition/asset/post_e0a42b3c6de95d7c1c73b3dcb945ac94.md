
## DISPLAY 18.12 Program Using the set Template Class

```cpp
//Program to demonstrate use of the set template class.
#include <iostream>
#include <set>
using std::cout;
using std::endl;
using std::set;

int main()
{
    set<char> s;

    s.insert('A');
    s.insert('D');
    s.insert('D');
    s.insert('C');
    s.insert('C');
    s.insert('B');

    cout << "The set contains:\n";
    set<char>::const_iterator p;
    for (p = s.begin(); p != s.end(); p++)
        cout << *p << " ";
    cout << endl;

    cout << "Removing C.\n";
    s.erase('C');
    for (p = s.begin(); p != s.end(); p++)
        cout << *p << " ";
    cout << endl;

    return 0;
}
```

> No matter how many times you add an element to a set, the set contains only one copy of that element.

### Sample Dialogue

```text
The set contains:
A B C D
Removing C.
A B D
```

The easiest way to add and retrieve data from a map is to use the `[ ]` operator. Given a map object `m`, the expression `m[key]` will return a reference to the data element associated with `key`. If no entry exists in the map for `key`, then a new entry will be created with the default value for the data element. For numeric data types, the default value is 0. For objects of type `string`, the default value is an empty string.

The `[ ]` operator can be used to add a new item to the map or to replace an existing entry. For example, the statement `m[key] = newData;` will create a new association between `key` and `newData`. Note that care must be taken to ensure that map entries are not created by mistake. For example, if you execute the statement `val = m[key];` with the intention of retrieving the value associated with `key` but mistakenly enter a value for `key` that is not already in the map, then a new entry will be made for `key` with the default value and assigned into `val`.

Some basic details about the `map` template class are given in Display 18.13. In order to understand these details, you first need to know something about the `pair` template class.

The STL template class `pair<T1, T2>` has objects that are pairs of values such that the first element is of type `T1` and the second is of type `T2`. If `aPair` is an object of type `pair<T1, T2>`, then `aPair.first` is the first element, which is of type `T1`, and `aPair.second` is the second element, which is of type `T2`. The member variables `first` and `second` are public member variables, so no accessor or mutator functions are needed.

The header file for the `pair` template is `<utility>`. So, to use the `pair` template class, you need the following, or something like it, in your file:

```cpp
#include <utility>
using std::pair;
```

The `map` template class uses the `pair` template class to store the association between the key and a data item. For example, given the definition

```cpp
map<string, int> numberMap;
```

we can add a mapping from `"c++"` to the number 10 by using a pair object:

```cpp
pair<string, int> toInsert("c++", 10);
numberMap.insert(toInsert);
```

or by using the `[ ]` operator:

```cpp
numberMap["c++"] = 10;
```

In either case, when we access this pair using an iterator, `iterator->first` will refer to the key `"c++"` while `iterator->second` will refer to the data value 10. A simple example that shows how to use some of the member functions of the template class `map` is given in Display 18.14.

We will mention two other associative containers, although we will not give any details about them. The template classes `multiset` and `multimap` are essentially the same as `set` and `map`, respectively, except that a `multiset` allows repetition of elements and a `multimap` allows multiple values to be associated with each key value.

## DISPLAY 18.13 map Template Class

### map Template Class Details

Type name `map<KeyType, T>` or `map<KeyType, T, Ordering>` for a map that associates (“maps”) elements of type `KeyType` to elements of type `T`.

The `Ordering` is used to sort elements by key value for efficient storage. If no `Ordering` is given, the ordering used is the binary operator `<`.

Library header: `<map>` places the definition in the `std` namespace.

Defined types include: `key_type` for the type of the key values, `mapped_type` for the type of the values mapped to, and `size_type`. (So, the defined type `key_type` is simply what we called `KeyType` earlier.)

Iterators: `iterator`, `const_iterator`, `reverse_iterator`, and `const_reverse_iterator`. All iterators are bidirectional. Those iterators not including `const_` are neither constant nor mutable, but something in between. For example, if `p` is of type `iterator`, then you can change the value of type `T` but not the key value. Perhaps it is best, at least at first, to treat all iterators as if they were constant.

`begin()`, `end()`, `rbegin()`, and `rend()` have the expected behavior. Adding or deleting elements does not affect iterators, except for an iterator located at the element removed.

### Sample Member Functions

| Member Function (m is a Map Object) | Meaning |
| --- | --- |
| `m.insert(Element)` | Inserts `Element` in the map. `Element` is of type `pair<KeyType, T>`. Returns a value of type `pair<iterator, bool>`. If the insertion is successful, the second part of the returned pair is `true` and the iterator is located at the inserted element. |
| `m.erase(Target_Key)` | Removes the element with the key `Target_Key`. |
| `m.find(Target_Key)` | Returns an iterator located at the element with key value `Target_Key`. Returns `m.end()` if there is no such element. |
| `m[Target_Key]` | Returns a reference to the object associated with the key `Target_Key`. If the map does not already contain such an object, then a default object of type `T` is inserted and returned. |
| `m.size()` | Returns the number of pairs in the map. |
| `m.empty()` | Returns `true` if the map is empty; otherwise returns `false`. |
| `m1 == m2` | Returns `true` if the maps contain the same pairs; otherwise returns `false`. |

The `map` template class also has a default constructor, a copy constructor, as well as other specialized constructors not mentioned here. It also has a destructor that returns all storage for recycling and a well-behaved assignment operator.

## DISPLAY 18.14 Program Using the map Template Class

```cpp
//Program to demonstrate use of the map template class.
#include <iostream>
#include <map>
#include <string>
using std::cout;
using std::endl;
using std::map;
using std::string;

int main()
{
    map<string, string> planets;
    planets["Mercury"] = "Hot planet";
    planets["Venus"] = "Atmosphere of sulfuric acid";
    planets["Earth"] = "Home";
    planets["Mars"] = "The Red Planet";
    planets["Jupiter"] = "Largest planet in our solar system";
    planets["Saturn"] = "Has rings";
    planets["Uranus"] = "Tilts on its side";
    planets["Neptune"] = "1500 mile-per-hour winds";
    planets["Pluto"] = "Dwarf planet";
    cout << "Entry for Mercury - " << planets["Mercury"]
        << endl << endl;
    if (planets.find("Mercury") != planets.end())
        cout << "Mercury is in the map." << endl;
    if (planets.find("Ceres") == planets.end())
        cout << "Ceres is not in the map." << endl << endl;
    cout << "Iterating through all planets: " << endl;
    map<string, string>::const_iterator iter;
    for (iter = planets.begin(); iter != planets.end(); iter++)
    {
        cout << iter->first << " - " << iter->second << endl;
    }
    return 0;
}
```

### Sample Dialogue

```text
Entry for Mercury - Hot planet

Mercury is in the map.
Ceres is not in the map.

Iterating through all planets:
Earth - Home
Jupiter - Largest planet in our solar system
Mars - The Red Planet
Mercury - Hot planet
Neptune - 1500 mile-per-hour winds
Pluto - Dwarf planet
Saturn - Has rings
Uranus - Tilts on its side
Venus - Atmosphere of sulfuric acid
```

The iterator will output the map in order sorted by the key. In this case the output will be listed alphabetically by planet.

## PROGRAMMING TIP Use Initialization, Ranged for, and auto with Containers

Several features introduced in C++11 make it easier to work with collections. In particular, you can initialize your container objects using the uniform initializer list format, which consists of initial data in curly braces. You can also use `auto` and the ranged `for` loop to easily iterate through a container. Consider the following two initialized collection objects:

```cpp
map<int, string> personIDs = {
    {1,"Walt"},
    {2,"Kenrick"}
};
set<string> colors = {"red","green","blue"};
```

We can iterate through each container conveniently using a ranged `for` loop and `auto`:

```cpp
for (auto p : personIDs)
    cout << p.first << " " << p.second << endl;
for (auto p : colors)
    cout << p << " ";
```

The output of this snippet is:

```text
1 Walt
2 Kenrick
blue green red
```

## Efficiency

The STL was designed with efficiency as an important consideration. In fact, the STL implementations strive to be optimally efficient. For example, the `set` and `map` elements are stored in sorted order so that algorithms that search for the elements can be more efficient.

Each of the member functions for each of the template classes has a guaranteed maximum running time. These maximum running times are expressed using what is called big-O notation, which we discuss in Section 18.3.
