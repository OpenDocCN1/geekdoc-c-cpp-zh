# Containers 883

Ordering should be a well-behaved ordering that takes two arguments of T and returns a bool value. T is the < elements stored. If no ordering is specified, then the ordering is assumed to be the < operator. Some basic details about the set template class are given in Display 19.11. A simple example shows how to use some of the member functions of the template class is given in Display 19.12.

A map is essentially a function with a set of ordered pairs. For each value first that appears in the map, there is at most one value such that the pair (first, second) is in map. The template class map implements map objects in the STL. For example, if you want to assign a unique number to each string name, you could declare a map as follows:

```
map<string, int> numberMap;
```

For string values as keys, the numberMap object can associate a unique int value. An alternate to think of a map is an associative array. A traditional array maps from a numerical index to a value. For example, a[10]=5 would store the value at index 5. An associative array allows you to define your indices using the data type of your choice. For example, numberMap["c+"]=5 would store the integer 5 with string "c+". For convenience, the [] bracket operator allows you to use an array-like notation to access a map, which can also use the insert or find methods if you want.

Like a set, a map stores its elements sorted by its key values. You can specify the ordering of keys as a third argument in the constructor. If you do not specify an ordering, a default ordering is used. The restrictions on orderings you can are the same as those for the set template class. Note that the ordering is on key value. The second type can be any type and not have anything to do with any ordering. With the set object, the sorting of the stored entries in a map is done for reasons of efficiency.

The easiest way to add and retrieve data from a map is to use the [] operator. Given a map object m, the expression m[key] will return a reference to the data element associated with key. If no entry exists for the key then a new entry will be created with the default value for the data element. This can be used to add a new item to the map or to replace an existing entry. For example, the statement m[key]=newData; Note care be taken to ensure that map entries are not created by mistake. For example, if you execute the statement val=m[key]; with the intention of retrieving the value associated with key that is not already in the map, then a new entry will be made for key with the default value and assigned into val.

Most ordering used to implement the < operator is strict ordering. For who wants the details, a strict ordering must be one of the following: (reflexive) (irreflexive) Ordering(x,y) is always false; (antisymmetric) Ordering(x,y) implies !Ordering(y,x); (transitive) Ordering(x,y) and Ordering(y,z) implies Ordering(x,z); and transitivity of equivalence if x is equivalent to y and y is equivalent to z, then x is equivalent to z. Two elements x and y are equivalent if Ordering(x,y) and Ordering(y,x) are both