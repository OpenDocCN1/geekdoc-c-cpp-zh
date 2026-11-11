header files. This saves programmers efforts to create the full code for these collections in every program that needs storing data dynamically.

STL essentially defines variety of template class and exposes the collection class in its API. The list of classes defined as a part of STL is as follows.

# Built-in collections in C++

You can create object of these classes directly to use them in the program. We will explain class list in detail to help you understand the approach in which these collections can be used. The API is quite vast to actually explain each class at the same level of detail; however, going through each of the collections in the same level of detail is not required. When you understand list, you will have a clear idea of how we can use collections in general.

# 16.4.1 Linked list

The linked list API is defined in a header file `list.h`, and hence this header file must be included in the program before using the built-in list. This means that the template class `list` is defined in `list.h`.

As `list` is a template class, you can instantiate it using a generic tagged syntax as we did for other template classes. For example,

```
list<int> l1;
```

creates an object `l1` of class `list` forcing the generic type to take the form of `int`. This means that `l1` is essentially a linked list that can store integers. Similarly, the statement

```
list<float> l2;
```

creates linked list `l2` which can store `float` values. Needless to say, you can also create a linked list to store objects of your class. For example, if `Employee` is a class you defined and you want to store a list of employees, you can create a linked list named as say `l3`, which can store `Employee` objects using the statement below:

```
list<Employee> l3;
```

> **NOTES**
> 
> The linked list we have implemented in Chapter 10 is a singly linked list in which every node has a pointer to the next node. In a linked list, you can just traverse in one direction as shown in the Figure 16.3.
> 
> The built-in class `list` we are talking about is a **doubly linked list**. In this type of list, every node has a pointer to the next node as well as to the node previous to it. So each node has two pointers: one that points to the node before and the other that points to node after. Hence, this list can be traversed in both the directions **forward** (from first node to the last node) as well as **reverse** (from last node to the first node) as shown in Figure 16.4.