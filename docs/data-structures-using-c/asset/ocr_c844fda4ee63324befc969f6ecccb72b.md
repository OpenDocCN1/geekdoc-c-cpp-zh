structuring of data (along with inter-relationship among data structures) and the operations to process the data (algorithms). In fact, the way we process our data depends on the way we organize it.

# 1.8 IMPLEMENTATION OF DATA STRUCTURES

A data structure is an aggregation of atomic and composite data types into a set with the relationship among them defined. As defined in Section 1.3.4, a data structure D is a triplet, that is, D = (D, F, A), where D is a set of data object, F is a set of functions, and A is a set of rules to implement the functions.

Let us consider an example of integer data type (int) in C++.

```
D = (0, ±1, ±2, ±3, ...)
F = (+, -, *, /, %)
A = (a set of binary arithmetic rules to perform addition, subtraction, division, multiplication, and module operations)
```

The set of axioms A defines semantics of operations on D for F. An implementation of a data structure D is a mapping from D to a set of other data structures E. This mapping specifies how every data object of d is to be represented by objects of E. Moreover, it requires that every function of D must be written using the functions of the implementing data structures E. Thus, we may say that the integers are represented by bit strings, the Boolean is represented by 0 and 1, and an array is represented by a set of sequential locations in memory. We have also defined the term abstract data type, which is a data structure in which rules (A—the set of axioms) do not imply a form of representation.

Hence, another way of viewing implementation of a data structure is that it is a process of refining an ADT until all the operations are expressed effectively so that they are defined in terms of directly executable functions.

Hence, implementation of data structures can be viewed in terms of two phases: specification and implementation. Such a division of tasks is useful as it helps to control the complexity of the entire process.

**Phase I: Specification** At the first stage, a data structure should be designed so that we know what it does and not necessarily how it will do it.

**Phase II: Implementation** At this stage, we define all functions with respect to the description of how to manipulate data. This can be done with algorithms so that the details of the operation can be understood easily, and the reader can implement them easily and effectively with the help of any programming language. Either of the design tools, that is, an algorithm or a flowchart, can be used at this phase. We have already learnt about algorithms as design tools; let us now learn about flowcharts.