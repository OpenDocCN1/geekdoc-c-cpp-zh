
Because elements in an associative container are sorted automatically, when a new element is inserted into the container, it is inserted at the proper place. A convenient and fast way to implement the operation is to use a binary search tree. This is, in fact, how associative containers are implemented. Thus, every element in the container has a parent node (except the root node) and at most two children. For each element, the key in the parent node is larger than the key in the left child and smaller than the key in the right child.

The predefined associative containers in the STL are:

- Sets
- Multisets
- Maps
- Multimaps

This book discusses only the associative containers set and multiset.

## Associative Containers: set and multiset

As described earlier, both the containers set and multiset automatically sort their elements according to some sort criteria. The default sorting criterion is the relational operator < (less than); that is, the elements are arranged in ascending order. The user can also specify other sorting criteria. For user-defined data types, such as classes, the relational operators must be overloaded properly.

The only difference between the containers set and multiset is that the container multiset allows duplicates; the container set does not.

The name of the class defining the container set is set; the name of the class defining the container multiset is multiset. The name of the header file containing the definitions of the classes set and multiset, and the definitions of the functions to implement the various operations on these containers, is set. Thus, to use any of these containers, the program must include the following statement:

```cpp
#include <set>
```

### Declaring set or multiset Associative Containers

The classes set and multiset contain several constructors to declare and initialize containers of these types. This section discusses the various ways that these types of associative containers are declared and initialized. Table 21-17 describes how a set/multiset container of a specific type can be declared and initialized.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1478_0.png)

**TABLE 21-17 Various Ways to Declare a Set/Multiset Container**

| Statement | Effect |
| --- | --- |
| `ctType<elmType> ct;` | Creates an empty set/multiset container, ct. The sort criterion is `<`. |
| `ctType<elmType, sortOp> ct;` | Creates an empty set/multiset container, ct. The sort criterion is specified by `sortOp`. |
| `ctType<elmType> ct(otherCt);` | Creates a set/multiset container, ct. The elements of `otherCt` are copied into ct. The sort criterion is `<`. Both ct and otherCt are of the same type. |
| `ctType<elmType, sortOp> ct(otherCt);` | Creates a set/multiset container, ct. The elements of otherCt are copied into ct. The sort criterion is specified by sortOp. Both ct and otherCt are of the same type. Note that the sort criteria of ct and otherCt must be the same. |
| `ctType<elmType> ct(beg, end);` | Creates a set/multiset container, ct. The elements starting at the position beg until the position end-1 are copied into ct. Both beg and end are iterators. |
| `ctType<elmType, sortOp> ct(beg, end);` | Creates a set/multiset container, ct. The elements starting at the position beg until the position end-1 are copied into ct. Both beg and end are iterators. The sort criterion is specified by sortOp. |

If you want to use sort criteria other than the default, you must specify this option when the container is declared. For example, consider the following statements:

```cpp
set<int> intSet; // Line 1
set<int, greater<int> > otherIntSet; // Line 2
multiset<string> multiSet; // Line 3
multiset<string, greater<string> > otherStringMultiSet; // Line 4
```

The statement in Line 1 declares intSet to be an empty set container, the element type is int, and the sort criterion is the default sort criterion. The statement in Line 2 declares otherIntSet to be an empty set container, the element type is int, and the sort criterion is greater-than. That is, the elements in the container otherIntSet will be arranged in descending order. The statements in Lines 3 and 4 have similar conventions.

The statements in Lines 2 and 4 illustrate how to specify the descending sort criterion.

> In the statements in Lines 2 and 4, note the space between the two > symbols—that is, the space between greater<int> and >. If you are using an old compiler, then this space is important because >> is also a shift operator in C++. However, this restriction is removed in C++0X and the compiler that we used to write programs in this book has implemented it. Therefore, in C++0X, the statements in Lines 2 and 4 can be written as:
>
> ```cpp
> set<int, greater<int>> otherIntSet; // Line 2
> multiset<string, greater<string>> otherStringMultiSet; // Line 4
> ```

### Item Insertion and Deletion from set/multiset

Suppose that ct is either of type set or multiset. Table 21-18 describes the operations that can be used to insert or delete elements from a set. It also illustrates how to use these operations. The name of the function is shown in bold.

**TABLE 21-18** Operations to Insert or Delete Elements from a Set

| Expression | Effect |
| --- | --- |
| `ct.insert(elem)` | Inserts a copy of elem into ct. In the case of sets, it also returns whether the insert operation succeeded. |
| `ct.insert(position, elem)` | Inserts a copy of elem into ct. The position where elem is inserted is returned. The first parameter, position, hints where to begin the search for insert. The parameter position is an iterator. |
| `ct.insert(beg, end);` | Inserts a copy of all the elements into ct starting at the position beg until end-1. Both beg and end are iterators. |

```cpp
intSetA.insert(30);                         //Line 14
intSetA.insert(39);                         //Line 15
intSetA.insert(59);                         //Line 16
intSetA.insert(238);                        //Line 17
intSetA.insert(156);                        //Line 18

cout << "Line 19: intSetA: ";              //Line 19
copy(intSetA.begin(), intSetA.end(), screen); //Line 20
cout << endl;                               //Line 21

intSetA.erase(59);                          //Line 22

cout << "Line 23: After removing 59, intSetA: "; //Line 23
copy(intSetA.begin(), intSetA.end(), screen);     //Line 24
cout << endl;                                      //Line 25

intGtIt = intSetA.begin();                   //Line 26
++intGtIt;                                    //Line 27
++intGtIt;                                    //Line 28
++intGtIt;                                    //Line 29

intSetA.erase(intGtIt);                       //Line 30

cout << "Line 31: After removing the fourth "
     << "element, " << endl
     << "        intSetA: ";                 //Line 31
copy(intSetA.begin(), intSetA.end(), screen); //Line 32
cout << endl;                                //Line 33

set<int, greater<int> > intSetB(intSetA);   //Line 34

cout << "Line 35: intSetB: ";                //Line 35
copy(intSetB.begin(), intSetB.end(), screen); //Line 36
cout << endl;                                //Line 37

intSetB.clear();                             //Line 38

cout << "Line 39: After removing all elements, " //Line 39
     << "intSetB: ";                         //Line 39
copy(intSetB.begin(), intSetB.end(), screen); //Line 40
cout << endl;                                //Line 41

multiset<string, greater<string> > namesMultiSet; //Line 42
multiset<string, greater<string> >::iterator iter; //Line 43

ostream_iterator<string> pScreen(cout, " "); //Line 44

namesMultiSet.insert("Donny");              //Line 45
namesMultiSet.insert("Zippy");              //Line 46
namesMultiSet.insert("Goofy");              //Line 47
namesMultiSet.insert("Hungry");             //Line 48
namesMultiSet.insert("Goofy");                         //Line 49
namesMultiSet.insert("Donny");                         //Line 50

cout << "Line 51: namesMultiSet: ";
copy(namesMultiSet.begin(), namesMultiSet.end(),
     pScreen);                                           //Line 52
cout << endl;                                            //Line 53

return 0;
}
```

### Sample Run:

```text
Line 9: intSet: 3 8 16 20
Line 19: intSetA: 238 156 84 59 39 36 30
Line 23: After removing 59, intSetA: 238 156 84 39 36 30
Line 31: After removing the fourth element,
          intSetA: 238 156 84 36 30
Line 35: intSetB: 238 156 84 36 30
Line 39: After removing all elements, intSetB:
Line 51: namesMultiSet: Zippy Hungry Goofy Goofy Donny Donny
```

The statement in Line 1 declares intSet to be a set container. The statement in Line 2 declares intSetA to be a set container whose elements are to be arranged in descending order. The statement in Line 3 declares intGtIt to be a set iterator. The iterator intGtIt can process the elements of any set container whose elements are of type int and are arranged in descending order. The statement in Line 4 declares screen to be an ostream iterator that outputs the elements of any container whose elements are of type int.

The statements in Lines 5 through 8 insert 16, 8, 20, and 3 into intSet, and the statement in Line 10 outputs the elements in intSet. In the output, see the line marked Line 9; it contains the output of the statements in Lines 9 through 11.

The statements in Lines 12 through 18 insert 36, 84, 30, 39, 59, 238, and 156 into intSetA, and the statement in Line 20 outputs the elements of intSetA. In the output, see the line marked Line 19. It contains the output of the statements in Lines 19 through 21. Notice that the elements of intSetA appear in descending order.

The statement in Line 22 removes 59 from intSetA. After the statement in Line 26 executes, intGtIt points to the first element of intSetA. The statement in Line 27 advances intGtIt to the next element of intSetA. After the statement in Line 29 executes, intGtIt points to the fourth element of intSetA. The statement in Line 30 removes the element of intSetA pointed to by intGtIt. The meanings of the statements in Lines 34 through 41 are similar.

The statement in Line 42 declares namesMultiSet to be a container of type multiset. The elements in namesMultiSet are of type string and are arranged in descending order. The statement in Line 43 declares iter to be a multiset iterator.
