# Sec. 1.2 Abstract Data Types and Data Structures

ple, Section 12.2 describes the data structure used to implement a sparse matrix, a large two-dimensional array that stores only a relatively few non-zero values. This implementation is quite different from the physical representation of an array as contiguous memory locations.

An abstract data type (ADT) is the realization of a data type as a software component. The interface of the ADT is defined in terms of a type and a set of operations that operate on. The behavior of each operation is determined by its inputs and outputs. An ADT does not specify how the data type is implemented. This implementation details are hidden from the users of the ADT and protected from access, a concept referred to as encapsulation.

A data structure is the implementation for an ADT. In an object-oriented language as C++, an ADT and its implementation together make up a class. Each operation associated with the ADT is implemented by a member function or method. The variables that define the space required by a data item are referred to as data members. An object is an instance of a class, that is, something that creates and takes up space during the execution of a computer program.

The term "data structure" often refers to data stored in a computer's main memory. The related file structure often refers to the organization of data on peripheral storage, such as a disk drive or CD.

Example 1.3 The mathematical concept of an integer, along with operations that manipulate integers, a data type. The C++ int variable is a physical representation of the abstract integer. The int variable type, along with the operations that act on an int variable, form an ADT. Unfortunately, the implementation is not completely true to the abstract integer, as there are limitations on the range of values an int variable can store. If these limitations prove unacceptable, then some other representation for the ADT "integer" must be devised, and a new implementation must be used for the associated operations.

Example 1.4 An ADT for a list of lists might specify the following operations:

+   * Insert a new integer true at a particular position in the list.
* Return true if the list is empty.
* Reinitialize the list.
* Return the number of integers currently in the list.
* Delete the integer at a particular position in the list.

From this description, the input and output of each operation should be clear, but the implementation for lists has not been specified.