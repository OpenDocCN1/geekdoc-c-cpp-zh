# The Set ADT with B-Trees

The rest of this section discusses the algorithms for implementing a set class using B-trees. The class is a template class that depends on the underlying type of the items in the set. There are public member functions for adding and removing items, and also for checking whether a given item is in the set. As you can see in our complete header file (Figure 11.5), there are also several private member functions that will simplify the implementations of the other member functions. We’ll discuss these “helper” functions at the point where they are used, but first let’s examine the private member variables and member constants that we have in mind.

The set class has two private member constants, shown here with a selection of 200 for MINIMUM:

two private member constants of the set

```
```cpp
static const size_t MINIMUM = 200;
static const size_t MAXIMUM = 2 * MINIMUM;
```
```

These constants are private because a programmer who uses the set class does not need to know about their existence. Access to these private values is needed only by the programmer who implements the set class.

After the declaration of the private member constants, the set class has four private member variables. The purpose of these four member variables is to store all the information about the root node of the B-tree that contains the set’s entries. Here are the first three member variables from the set class in Figure 11.5 on page 552:

member variables store information about the root of the B-Tree

```
```cpp
size_t data_count;
Item data[MAXIMUM+1];
size_t child_count;
```
```

Keep in mind that the member variables store information about the root node. For example, data_count stores the number of entries in the B-tree’s root (not in the entire B-tree). The root’s entries are stored in the partially filled array called data, ranging from data[0] through data[data_count-1]. The complete size of the data array is MAXIMUM + 1, which allows space for one extra entry beyond the usual maximum number. You’ll see the benefit of this extra space when we discuss the implementations of the member functions. The number of children of the root node is stored in the member variable child_count. The children of the root have an important property that will allow us to use recursive thinking in our implementations. Here is the property that you should hold onto:

> Every child of the root is also the root of a smaller B-tree.