# # 13

# # Structure and Union

We have seen so far how to store numbers, characters, strings, and even large sets of these primitives using arrays, but what if we want to store collections of different kinds of data that are somehow related. For example, a file about an employee will probably have his/her name, age, the hours of work, salary, etc. Physically, all of that is usually stored in someone’s filing cabinet. In programming, if you have lots of related information, you group it together in an organized fashion. Let us say you have a group of employees, and you want to make a database! It just would not do to have tons of loose variables hanging all over the place. Then we need to have a single data entity where we will be able to store all the related information together. But this cannot be achieved by using the arrays alone, as in the case of arrays, we can group multiple data elements that are of the same data type, and is stored in consecutive memory locations, and is individually accessed by a subscript. That is where the user defined data type *Structures* come in.

*Structure* is commonly referred to as a user-defined data type. C’s *structures* allow you to store multiple variables of any type in one place (the structure). A structure can contain any of C’s data types, including arrays and other structures. Each variable within a structure is named a *member* of the structure. They can hold any number of variables, and you can make arrays of structures. This flexibility makes structures ideally useful for creating databases in C. Similar to the structure there is another user defined data type called *Union* which allows the programmer to store

a single storage in more than one way, i.e. a variable declared as union can store within its storage space, the data of different types, at different times. In this unit, we will be discussing the user-defined data type structures and unions.

# ## DEFINITION OF STRUCTURE

A structure is a collection of variables under a single name. These variables can be of different types, and each has a name which one can select it from the structure. A structure is a suitable way of grouping several pieces of related information together.

A structure can be defined as a new named type, thus extending the number of available types. It can use other structures, arrays or pointers as some of its members, though this can get complicated unless you are careful. That means we can say that structures is the collection of different data types and having a common name. A struct (short for STRUCTURE), is a collection of variables of different types. Structures are sometimes referred to as abstract data types or ADTs for short. We already know how to store a group of variables of the same type using arrays. Variables in a struct are called members or fields, and are accessed by their name. Variables in an array are called elements, and are accessed using square brackets and an index.

# ## DECLARATION OF STRUCTURES

To declare a structure you must start with the keyword struct followed by the structure name or structure tag and within the braces