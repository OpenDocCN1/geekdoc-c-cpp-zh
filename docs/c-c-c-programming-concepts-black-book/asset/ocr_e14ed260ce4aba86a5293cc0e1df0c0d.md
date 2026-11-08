![](bbox=[0.211, 0.163, 0.813, 0.367])

# Figure 13.13: Showing the Salient Features of OOP

The advantages of OOP may be enumerated as follows:

+   - [ ] Provides better understanding of the system, which is achieved by **modularity**
+   - [ ] Combines data and behavior into one package, which is known as an **object**. The advantage of this combination is as follows:
+     - Separate development teams can work independently
+     - An object class can be developed, reused, or purchased
+     - Update operation may affect a limited number of object classes
+   - [ ] Avoids duplication of common behavior with the use of **hierarchy** or **inheritance**. The reasons of such avoidance are as follows:
+     - Behavior depends on the individual object
+     - New kinds of objects can be added later without any harm
+   - [ ] Changes the implementation of an object without affecting its behavior
+   - [ ] Reduces the risk of building complex software systems

An object is defined as something that can perform a set of related activities. The set of activities performed by an object defines the behavior of the object. For example, the Employee object can give a name or address. Object has state and exhibits some well-defined behavior. The state of an object includes all the properties of the object, which are static. The values of these properties are dynamic in nature. Identity of an object distinguishes it from all the other objects. In C++, an object is a region of storage with associated semantics and can be declared as follows:

```
```cpp
int a;
```
```

The preceding declaration specifies that a is an object of type int.

Within the context of the object model of C++, the word object refers to an instance of the class. A class defines the actual behavior of several objects. Objects are often referred through references, which are aliases to an object. Bjarne Stroustrup in his book, *The C++ Programming Language (Second Edition, Addison-Wesley, 1992)*, said that *the obvious implementation of a reference is as a (constant) pointer that is de-referenced each time it is used.*

Class is a group of objects that share a common structure and behavior. Figure 13.14 describes operations, requests, and methods in the context of classes: