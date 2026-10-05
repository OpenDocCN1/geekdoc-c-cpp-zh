# Containers

The STL template class pair<T1, T2> has objects that are pairs of values such that the first element is of type T1 and the second is of type T2. If aPair is an object of type pair<T1, T2>, then aPair.first is the first element, which is of type T1, and aPair.second is the second element, which is of type T2. The member first and second are public members, so no accessor or mutator functions are needed.

The header file for the pair template is <utility>. So, to use the pair template class (or something like it) in your file:

```
#include <utility>
using std::pair;
```

The map template class uses pair template class to store the association between the key and a data item. For example, given the definition

```
map<string, int> numberMap;
```

if we add to the map

```
numberMap["*"] = 10;
```

then when we access this pair using, iterator->first will refer to the key "*" while iterator->second will refer to the data value 10.

A simple example shows how to use the member functions of the template class map is given in Display 19.14.

We mention four other associative containers, although we will not give any details about them. The template classes multiset and multimap are essentially the same as map, respectively, multiset allows repetition of elements and multimap allows multiple values to be associated with each key value. Some implementations of STL also include the hash_set and hash_map classes. These template classes are essentially the same as set and map, except they are implemented using a hash table. Hash tables are described in Chapter 17. Instead of hash, most implementations of the set and map use balanced binary trees. In a balanced binary tree, the number of nodes to the left of the root is approximately equal to the number of nodes to the right. Binary search trees are also described in Chapter 17, although we do not discuss details of balancing

# Efficiency

The STL implementations strive to be optimally efficient. For example, the set and map elements are stored in sorted order so that algorithms search for the elements can be more efficient.

Each of the member functions for each of the template classes has a guaranteed maximum time. These maximum running times are expressed using big-O notation, which we discuss in Section 19.3. (Section 19.3 also gives guaranteed running times for some of the container members we have already discussed. These are given in the subsection entitled "Container Access Running Times." You will be told the guaranteed maximum running times for certain functions described in the rest of this chapter.