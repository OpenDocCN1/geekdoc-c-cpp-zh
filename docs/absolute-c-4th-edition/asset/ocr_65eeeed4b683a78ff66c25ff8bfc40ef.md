you want to assign a unique number to each string name, you could declare a map object as follows:

```
map<string, int> numberMap;
```

For string values known as keys, the numberMap object can associate a unique int value.

Like a set object, a map object stores its elements in sorted order by its key values. You can specify the ordering on keys as a third entry in the angular brackets, < >. If you do not specify an ordering, a default ordering is used. The restrictions on orderings you can use are the same as those on the orderings allowed for the set template class. Note that the ordering is on key values only. The second type can be any type and need not have anything to do with any ordering. As with the set object, the sorting of the stored entries in a map object is done for reasons of efficiency.

Some basic details about the map template class are given in Display 19.13. In order to understand these details, you need to first know something about the pair template class.

The STL template class pair<T1, T2> has objects that are pairs of values such that the first element is of type T1 and the second is of type T2. If aPair is an object of type pair<T1, T2>, then aPair.first is the first element, which is of type T1, and aPair.second is the second element, which is of type T2. The member variables first and second are public member variables, so no accessor or mutator functions are needed.

The header file for the pair template is <utility>. So, to use the pair template class, you need the following, or something like it, in your file:

```
#include<utility>
using std::pair;
```

We will mention two other associative containers, although we will not give any details about them. The template classes multiset and multimap are essentially the same as set and map, respectively, except that multiset allows repetition of elements and multimap allows multiple values to be associated with each key value.

# EFFICIENCY

The STL was designed with efficiency as an important consideration. In fact, the STL implementations strive to be optimally efficient. For example, the set and map elements are stored in sorted order so that algorithms that search for the elements can be more efficient.

Each of the member functions for each of the template classes has a guaranteed maximum running time. These maximum running times are expressed using what is called big-O notation, which we discuss in Section 19.3. (Section 19.3 also gives some guaranteed running times for some of the container member functions we have already discussed. These are given in the subsection entitled "Container Access Running Times.") When using more advanced references or even later in this chapter, you will be told the guaranteed maximum running times for certain functions.