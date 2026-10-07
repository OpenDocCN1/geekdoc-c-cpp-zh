
in dictionaries in general and in hash tables in particular makes pair convenient data containers. As a result, pair objects will have a recurring role in this and the next chapter. An extension of pair that can hold multiple objects of multiple types is discussed in Appendix C.

First, the pair class is made available via the include directive

```
#include <utility>
```

The basic structure of the pair class can then be described as in the next listing:

```cpp
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

```cpp
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

- There are additional constructors that allow for implicit type conversion. See Chapter 21 of Vandervoorte and Josuttis (2003).

Since pair is a struct, public inheritance allows newPair objects to have the same access to the members first and second as a pair object. Notice how the newPair constructors invoke the base class (i.e., pair) constructors via the mandatory initializer lists. This leaves them with the task of defining the Boolean isNull that represents the main point of departure from the base class. This new class provides the "fix" for our problem by evaluating to true when the default constructor is used. An approach that would work well here would be to use composition (i.e., embed a pair object in the newPair class) rather than inheritance. This idea is explored in Exercise 9.20.

The declaration for a class hashTable will hold newPair objects is now given by

Listing 9.4 hashTable.h

```cpp
class hashTable {
    int Size, hashTable;
    int Shift;
    newPair* pTable;

    bool empty(int i) const {
        cout << std::boolalpha << " isNull is "
             << pTable[i].isNull << endl;
        return pTable[i].isNull;
    }

public:
    hashTable() {};
    hashTable(int tablesize, int shift = 1);
    hashTable(const hashTable& hT);
    ~hashTable()();

    hashTable& operator=(const hashTable& hT);
    bool operator+=(const hashTable& hT) const;
    int insert(newPair* a);
    int lookUp(int a) const;
    int hash(int a) const;
    int getData(int a) const;
};
```

The class has four data members: the number of slots in the table hashTable, the current number of objects in the table size, the shift parameter for linear probing Shift and a pointer to newPair that points to the beginning location where newPair objects will be stored in memory. The utility function checks whether a designated slot is empty for one use and accordingly, has been made private. Note the use of the isNull number of the newPair class in the definition of the method. The boolalpha format flag from Exercise 3.1 is used to convert the 0 and 1 values for the Boolean variable to true/false.

The public methods for class hashTable include the constructors, destructor, hash function and functions for filling in and looking up values in the table. A default "do nothing" constructor is given inline in Listing 9.4. The other constructor definition is

```cpp
hashTable::hashTable(int tablesize, int shift) :
tableSize(tablesize), Shift(shift), Size(0) {
    pTable = new newPair[tableSize];
}
```

The input values for the shift and table size are used in an initializer list to set the values of the class members Shift and tableSize. The Size member is set to 0 and a pointer to newPair is initialized to hold hashTable newPair objects.

As dynamic memory allocation is involved, an explicit destructor is needed as such

```cpp
hashTable::~hashTable() {
    if (pTable != 0)
        delete[] pTable;
}
```

For the same reason a copy constructor and an overloaded assignment operator are needed. The task of creating these functions as well as the overloaded comparison == is relegated to Exercise 9.18.

The hash function that will be the one from Example 9.2. The code that implements

```cpp
int hashTable::hash(int a) const {
    cout << " hashes to " << a % tableSize << endl;
    return a % tableSize;
}
```

This C++ class operator requires that we must include the cmake header file.
The look-up operation is carried out with

```cpp
int hashTable::lookUp(int a) const {
    int ind = hash(a);
    while (empty(ind) && !(pTable[ind].first == a)) {
        cout << " Collision to " << ind << endl;
        cout << " Next try " << ind << " Shift";
        ind = (ind + Shift) % tableSize;
        cout << " hashes to " << ind << endl;
    }
    return ind;
}
```

First, the supplied key is hashed. Then, linear probing according to the value of the Shift class member is used to find either a nonempty slot corresponding to the hashed key or one empty index. Additional output statements have been included here for the purpose of a later example. With the lookUp method in place the actual retrieval of a data value is straightforward accomplishing using

```cpp
int hashTable::getData(int a) const {
    return pTable[lookUp(a)].second;
}
```

A hashTable object is filled using the insert method below.

```cpp
int hashTable::insert(newPair a) {
    int ind = lookUp(a.first);
    if (pTable[ind].first == a.first) {
        cout << " Already inserted this value " << endl;
        return -1;
    }
    cout << " Inserting at " << ind << " " << ind << endl;
    pTable[ind] = a; Size++;
    return ind;
}
