# 392 DATA STRUCTURES IN C++

a dictionary the objects in the container have both a key and a data component. For map the keys must be unique while multimap allows repeated keys. The set containers are simplified versions of map containers where objects have a single member that serves as both the key and data component.

There are certain operations that are provided by all the standard class in the STL. In this section we will discuss several of the "global" methods. Later sections will illustrate their use for specific container types as well as other methods that are container-specific.

To use a particular container, ADName, from the STL one needs the include directive
#include <ADName>

All the containers are equipped with a default constructor, a constructor that takes arguments for the specific ADT, a copy constructor, an assignment operator and a destructor. Thus, for example, the default constructor for ADName would be invoked with a command as

```
ADName<T> ADObject;
```

Of course, a specific value (i.e., a data type) must be supplied for T to define an ADName object. That choice is the user's decision. This serves the same purpose as our developments in Section 9.5: namely, it makes the ADT container in the sense that it can hold objects from an arbitrary class.

The methods empty and size can be used with any of the STL containers. If ADObject is

```
ADObject.empty();
```

will return true if ADObject contains no elements and false, otherwise. Similarly,

```
ADObject.size();
```

returns the number of elements in ADObject.

```
ADObject1 = ADObject2
```

will evaluate if the two objects contain the same elements arranged in the order. The <, <=, >= operators will also work in the sense of lexicographical comparison between two containers. For example, the operator compares two containers element-by-element

+   - two elements are not equal; the result of applying < to the two containers is then to be the result of applying < to these elements,
- one of the containers has fewer elements than the other; the one with fewer is viewed as "smaller",
- the two containers are found to be equal in which < returns false.