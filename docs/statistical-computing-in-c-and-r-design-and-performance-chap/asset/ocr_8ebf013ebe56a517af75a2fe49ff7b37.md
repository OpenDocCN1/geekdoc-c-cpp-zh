# ADT DICTIONARY 349

in dictionaries in general and in hash tables in particular makes pair convenient data containers. As a result, pair objects will have a recurring role in this and the next chapter. An extension of pair that can hold multiple objects of multiple types is discussed in Appendix C.

First, the pair class is made available via the include directive

```
#include <utility>
```

```
The basic structure of the pair class can then be described as in the next listing:

template<class dataType1, class dataType2>
struct pair {
    dataType1 first;
    dataType2 second;
    pair();
    pair(const dataType1& t1, const dataType2& t2);
};
```

As the name suggests, a pair object is composed of two member objects; the first member is an object of dataType1 and the second member is an object of dataType2. The pair struct has a default constructor that initializes first and second members as the defaults for their respective classes. A second constructor initializes first and second members using specified values for the two types. In keeping with our previous examples, both the key and data components for our hash table will be of type int. Thus, we will be storing pair<int, int> objects in the table although this particular struct is not entirely suited for our purpose. The problem surfaces when one attempts to apply a look-up method to pair objects. A key step in Algorithm 9.10 is to see that an array slot is empty in the sense of containing something that can be uniquely distinguished as a NULL entry. Being able to locate such empty slots is what makes the insertion operation so efficient. If the hash table is implemented using an array as will be done here, the object has no obvious way of making it "empty", here the slots in the array will typically be filled with the default class constructor. This produces an "empty" pair<int, int> which has no way of making its "empty" status known to a NULL object.

To provide a null pair we will extend the pair class via inheritance to obtain the new pair class described in the listing below.

Listing 9.3 newPair.h

```
struct newPair : pair<int, int>
{
    bool isNull;
    newPair() : pair<int, int>() {
        isNull = true;
    }
    newPair(const int& key, const int& data) :
        pair<int, int>(key, data) {
        isNull = false;
    }
    newPair(const newPair& pairObj) :
        pair<int, int>(pairObj.first, pairObj.second) {
        this->isNull = pairObj.isNull;
    }
};
```

* There are additional constructors that allow for implicit type conversion. See Chapter 21 of Vandervoorte and Josuttis (2003).