
```
curr->Data = element;
curr->link = NULL;
if(top == NULL)
    top = curr;
else
{
    curr->next = top;
    top->curr;
    // change top as new node
    top=curr;
}
} //end of push
int pop()
{
    node *curr; int element;
    if(isEmpty())
        cout << "\n Stack is empty";
    else
    {
    curr = top;
    element = top->Data;
    top = top->next;
    delete(curr);
    return(element);
    }
} // end of pop
} // end of class stack
```

We can define objects of the stack class in the same way as the previous stack class in Program Code 15.6.

```
PROGRAM CODE 15.6
void main()
{
    stack s, s1, s2; // defining 3 objects of stack
    s, s1, s2
    // calling functions same as previous class
    s.push(5); // 5 is pushed in stack s
    s.push(8); // 8 is pushed in stack s
    s1.push(10); // 10 is pushed in stack s1
}
```

In both implementations (using array and linked list), we can see that the implementation may be different and can be hidden. We also see that independent of the implementation, Program Codes 15.4 and 15.6 are the same.

## Classes to Produce Abstract Data Types

A class is a type that we define, unlike types such as int and char that are already defined for us. A value for a class type is a set of values of the member variables. Consider the following class:

```
class student_account
{
private:
    int BankAccountNo;
    :
    :
public:
    void update();
    double getbalance();
    :
};
```

The programmer who uses this class need not be concerned about how the member functions are implemented.

## Creating an Abstract Data Type

In order to define a class so that it is an ADT, we need to separate the specification of how the type is used by a programmer from the details of how the type is implemented. The separation should be so complete that if we change the implementation of the class, any program that uses the class ADT should not need any additional changes. Hence, the following steps must be adhered to:

- 1. Make all the member variables as private members of the class.
- 2. Make each of the basic operations for ADT either a public member, or a friend function, or an ordinary function, or an overloaded operator. Group the class definition and the function and operator prototypes together. This group along with comments is called the *interface* for ADT.
- 3. Fully specify how to use each of these functions or operators in comments given with the class or with the function or operator prototypes.
- 4. Make the implementation of basic operations unavailable to programmers who use ADT. The implementation consists of the function definitions and overloaded operator definitions; put them in different files.
- 5. Put all these definitions mentioned in a separate file called as the *implementation file*. This file must contain an *include directive* that names the interface file, say #include "student.h". The interface file and implementation file traditionally have the same name but end with different suffixes. The interface file ends with .h and implementation file ends in the same suffix that we use for files that contain C++ code.

- 6. Compile implementation file separately.
- 7. If we want to use the ADT in a program, we place the main part of the program, any additional function definitions, and constant declarations in another file called an application file. This file, also contains an include directive naming the interface file, as in, #include "student.h".
- 8. We must first link the object code produced by compiling the application file and the object code produced by compiling the implementation file. In some systems, linking may be done automatically or semi-automatically.

## 15.3 STANDARD TEMPLATE LIBRARY

C++ classes provide information for creating a library of data structures. The C++ STL is a collection of containers, adaptors, iterators, functions, and algorithms. The STL is a part of the standard C++ class library and can be used as a standard approach for storing and processing data. The task of writing complex application codes can be made easy with the use of STL. The C++ class allows for the implementation of ADTs with appropriate hiding of implementation details.

Standard template library was developed by Alexander Stepanov and Meng Lee of Hewlett Packard. In past, compiler vendors and many third party developers have offered libraries of container classes to handle the storage and processing of data. However, now, standard C++ includes its own built-in container class library, STL. C++ classes provide an excellent mechanism for creating a library of data structures. STL contains many kinds of entities. The three most important kinds are the following:

- 1. Containers
- 2. Algorithms
- 3. Iterators

The STL allows a programmer to use these classes and functions directly in programs to increase productivity.

### 15.3.1 Containers

Container is a way to store data whether the data consists of built-in types such as int and float, or of class objects, that is, container classes whose purpose is to contain other objects.

Many times, a programmer uses many objects of a particular class. For example, arrays. Array can be considered as one of the most basic and elementary containers. Arrays are one of the most powerful data structures. Many other data structures use array as a building block. If STL makes such a data structure available, a programmer will be able to use it as a ready-to-use data structure.

The STL makes seven basic kinds of containers available and three more that are desired from the basic kinds. In addition, we can create our own containers based on these basic kinds of containers.

Use of containers is for achieving efficiency. We have learnt and used array as a data structure and its pros and cons. An array could be slow in many situations; and it might be time consuming to switch to other data structure, implement the same, and then use it. Use of STL is less time consuming. STL provides many kinds of containers. The programmer can choose one or a few of them as per the need of the application without knowing the implementation details. Table 15.1 lists some examples of container classes.

Table 15.1 List of container classes

| Container class | Description |
| :--- | :--- |
| Vector | Array |
| List | Doubly linked list |
| Slist | Singly linked list |
| Queue | Queue structure, that is, FIFO structure |
| Stack | Stack structure, that is, LIFO structure |
| Deque | Combination of stack and queue, having facility for insertion and removal from both ends |
| Set | Set of unique elements |
| Map | Store key and data pair |

Containers are categorized into two types:

- 1. Sequence containers
- 2. Associative containers

### Sequence Containers

A sequence container stores a set of elements which can be visualized as a line, similar to houses on a street. Each element is related to the other by its position along the line. Each element, except at ends, is preceded by one specific element and followed by a specific element. These containers refer to sequential organization of elements, such as in arrays.

The sequence containers are as follows:

- 1. Vectors
- 2. Lists
- 3. Deques

The containers that are derived from sequence containers are stacks, queues, and priority queues. To instantiate an STL container object, we must include an appropriate header file. We then use the template format with the kind of objects to be stored as the parameters.

For example,

```
deque <int> intDeque; and
list<student> SComp;
```

Here, student is a defined data type. The containers take care of all memory allocations that a user need not specify.

### Vectors

The array data structure has certain limitations. Owing to its static implementation, it results into poor utilization and runtime difficulties of not exceeding the size. In addition, array size is to be specified at the compile time; that is, in the source code. All these difficulties can be overcome through the vector container provided by STL. The template class describes an object that controls a varying-length sequence of elements of type T.

A vector is a sequence container that supports random access iterators. It is optimized for insertions and deletions at the ends of the collection. Insertions and deletions anywhere else in the collection, such as at the beginning or middle, take linear time. Storage management is handled automatically. It supports for any data type and for automatic resizing when adding elements.

Vector reallocation occurs when a member function must grow the controlled sequence beyond its current storage capacity.

Table 15.2 List of vector constructors, functions, and operators

| Function/constructor/operator | Description |
|---|---|
| vector<T> v; | Creates an empty vector of data type T |
| vector<T> v(n); | Creates a vector of n default values |
| vector<T> v(n, e); | Creates a vector of n copies of e |
| v.~vector<T>(); | Destroys all elements and frees memory |
| i = v.size(); | Gets the number of elements |
| l = v.capacity(); | Maximum number of elements before reallocation |
| l = v.max_size(); | Implementation of maximum number of elements |
| B = v.empty(); | True, if empty. Same as v.size() == 0 |
| v.reserve(n); | Sets the capacity to n before reallocation |
| v = v1; | Assigns v1 to v |
| v[i] = e; | Assigns the i^th element as e |
| v.at(i) = e; | At the i^th position set element e |
| v.front() = e; | Same as v[0] = e |
| v.back() = e; | Same as v[v.size() - 1] = e |
| v.push_back(e); | Adds e to the end of v. Expands v if necessary |
| v.pop_back(); | Removes the last element of v |
| v.clear(); | Removes all elements |
| iter = v.assign(n, e); | Replaces the existing elements with n copies of e |
