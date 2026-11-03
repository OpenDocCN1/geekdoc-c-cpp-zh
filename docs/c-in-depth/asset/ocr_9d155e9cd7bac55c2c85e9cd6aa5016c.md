# Chapter 10

# Structure And Union

Array is a collection of same type of elements but in many real life applications we may need to gr different types of logically related data. For example if we want to create a record of a person t contains name, age and height of that person, then we can't use array because all the three data eleme are of different types.

![](bbox=[0.35, 0.4, 0.85, 0.55])

To store these related fields of different data types we can use a structure, which is capable of stor heterogeneous data. Data of different types can be grouped together under a single name using structu The data elements of a structure are referred to as members.

# 10.1 Defining a Structure

Definition of a structure creates a template or format that describes the characteristics of its memb All the variables that would be declared of this structure type, will take the form of this template. general syntax of a structure definition is-

```
struct tagname{
    datatype member1;
    datatype member2;
    .............
    datatype memberN;
};
```

Here struct is a keyword, which tells the compiler that a structure is being defined. member1, memb ............ memberN are known as members of the structure and are declared inside curly bra There should be a semicolon at the end of the curly braces. These members can be of any data t like int, char, float, array, pointers or another structure type. tagname is the name of the structure it is used further in the program to declare variables of this structure type.

Definition of a structure provides one more data type in addition to the built in data types. We can dec variables of this new data type that will have the format of the defined structure. It is importan