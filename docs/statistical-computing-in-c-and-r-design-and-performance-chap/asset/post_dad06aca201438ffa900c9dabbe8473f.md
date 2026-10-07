
# DATA STRUCTURES IN C++

its Data member will be overwritten by the value data. Otherwise, a new node will be inserted with the Key value key and Data component data.

Removal of elements from a map is accomplished by the erase method. The method takes two forms. One version of erase takes an iterator that points to the position of the node that to be erased. In this instance the node is removed and the function returns nothing. The other option is to use a key value for the erase function. In that instance, erase removes the object with the specified key and returns the integer 1 for a map object, and more generally, the number of erased objects for a multimap allows duplicate keys.

The listing below illustrates the use of a map container.

```cpp
//map.cpp
#include <iostream>
#include <utility>
#include <map>

using std::cout; using std::endl; using std::map; using std::pair;

int main() {
    map<int, int> m;
    m.insert(pair<int, int> (4, 4)); m.insert(pair<int, int> (0, 2));
    cout << m[0] << endl;
    m[0] = 1;
    cout << m[0] << endl;
    m[1] = 2;
    cout << m[1] << endl;
    m[3] = 1; m[2] = 11; m[6] = 5; m[7] = 7; m[4] = 5; m[21] = -3;
    m[-15] = 99; m[-19] = -16; m[-5] = 3; m[-3] = 1; m[-2] = 14;

    map<int, int>::iterator iter;
    for(iter = m.begin(); iter != m.end(); ++iter)
        cout << iter->first << " : " << iter->second;
    cout << endl;

    iter = m.find(-2);
    cout << iter->second << endl;
    m.erase(iter); m.erase(-15); m.erase(-1);

    map<int, int>::reverse_iterator riter;
    for(riter = m.rbegin(); riter != m.rend(); ++iter)
        cout << riter->first << " : " << riter->second;
    cout << endl;
    return 0;
}
```

Here we revisit the binary search tree from Figure 9.9. The tree is constructed using both the insert method and the operator. After inserting a node with key 0 and data member 2, the value of the data member is accessed and changed using the index method. Output is produced to see the effect of these two processes as well as that of insertion. An iterator created and used to explore the container while printing the key values for each node in the process. The find method is then employed to locate the node with a key of -2. The iterator returned from find is used in the erase method to remove that particular node from the tree. Finally, several nodes are removed with erase their key values and the container is explored again using an iterator to assess the changes that have been made. In this latter instance we have carried out the exploration with a reverse iterator. The starting point for a reverse iteration through a container is obtained from rbegin with rend providing the corresponding stopping point. The ++ operator will move the iterator backward from the current node. Of course, there is the question of how forward or backward movement will actually take place. This question is resolved by running the program.

The output from our program is

```
2
1
2
-16 -15 -3 -2 -1 0 1 2 3 4 5 6 7 21
14
21 7 6 5 4 3 2 1 0 -3
```

The insertion and indexing operations have produced the expected output. The “mystery” concerning the behavior induced by ++ the internal map forward iterator class has been implemented so that the movement is from smaller to larger values. Reverse iterators move from larger to the smaller keys. The last line of output produced with the reverse iterator based for loop verifies that both forms of the erase method (i.e., the one with iterator argument and the one that has keys arguments) have worked correctly.

# 10.7 Algorithm basics

As noted in the introduction, the STL consists of three basic components: data structures, iterators and algorithms. In this final section, we describe various aspects of the latter of these three resources. A complete exposition is beyond the scope of the present text. An overview of the entire algorithm package is provided, for example, in Malik (2007) Josritus (1999) also giving a detailed and thorough treatment. Our goal here is to merely demonstrate some the features and power of the algorithm package that can pave the way for a more in depth study.

The STL library is composed of a group of data processing methods that perform basic operations on data structures. These include searching, sorting and transforming as well as few numeric calculations. Rather being tied to specific container classes, the algorithm functions have an independent identity. This is achieved by having them with iterators rather than container objects. This means they can also be utilized with user-created ADTs.

The algorithm library becomes available with the include directive

```cpp
#include <algorithm>
```

This provides access to groups of functions whose purposes can be categorized as (e.g., Josritus 1999) nonmodifying or modifying, removing and mutating. Modifying algorithms do not alter the elements in the container. Searching methods fall into this group. Modifying algorithms change the elements while mutating. A small set of numeric methods are available that include summation, inner products and partial sums. These latter require the inclusion of

```cpp
#include <numeric>
```

In general, the invocation of algorithm can take one of several forms. The simplest is

```cpp
algorithm(begin, end)
```

where begin and end are STL-compliant iterators that provide the beginning and end of the range to be processed. In such a case, two ranges may be involved with the second providing a destination for the results of the algorithm. An end iterator is not necessary as that position is determined by the length of the range from begin to end. A third type of argument for an algorithm is

```cpp
algorithm(begin, end, functionObject)
```

These latter differ from the previous two only in terms of the addition of a function object or functor (e.g., Section 8.2) that provides the tool to be used in processing the elements. Not, as was the case for iterators, functions need to inherit from an STL class. The possibilities in this case are `unary_function` and `binary_function`.

To illustrate some of the basic ideas, we will use the g5Array class of Section 10.3.3. Our goal will be to create three methods for the class that are all implemented using the library algorithm. The methods that we will create are one that will look up for a specified date, the g5 objects in the container by the date and compute a chi-square statistic.

The most straightforward way to implement that for sorting. It follows

```cpp
std::vector<g5> g5Array::sort() {
    std::vector<g5> sort(ndArray);
    std::copy(this->begin(), this->end(), sort.begin());
    g5Less f;
    std::sort(sort.begin(), sort.end(), f);

    return sort;
}
```

This method uses two algorithms: `sort` and `copy`. There are three main sorting methods in the algorithm library: `sort`, `partial_sort` and `stable_sort`. The sort method is akin to quicksort while partial and stable are merges. All of these require random access iterators which means we must first transfer the elements of the g5Array object to, e.g., a vector object. This object will need to have `ndArray` slots. Once it is created, the `begin()` and `end()` iterators of the g5 iterator for the vector object gives the beginning of the range where the data is to be replicated.

The function that will be used for g5 objects is
