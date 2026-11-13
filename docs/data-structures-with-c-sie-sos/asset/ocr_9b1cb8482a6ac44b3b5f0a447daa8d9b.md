# 1.5 ABSTRACT DATA TYPES (ADT)

An abstract data type (ADT) refers to a set of data values and associated operations that are specified accurately, independent of any particular implementation. With an ADT, we know what a specific data type can do, but how it actually does it is hidden. In broader terms, the ADT consists of a set of definitions that allow us to use the functions while hiding the implementation.

The properties of an abstract data type are emphasized through the following examples.

# Example 1.7 List Representation

Consider a list L consisting of data items—1, 2, 3, 4, 5, 6, 7, 8, 9 as shown in Fig. 1.11(a). We can use any of four data structures to support L—a linear list, a matrix, a tree, or a graph, as given in Fig. 1.11(b), (c) and (d) respectively.

![](bbox=[0.088, 0.37, 0.922, 0.75])

Fig. 1.11 Data structures which support a list

Assume that we place the list on an ADT. The users should not be aware of the structure that we use, i.e., whether it is a tree, or graph or something else. As long as they are able to insert and retrieve data, it does not make a difference as to how we store the data.