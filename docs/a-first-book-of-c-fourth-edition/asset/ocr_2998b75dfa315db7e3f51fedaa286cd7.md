important. A structure's form consists of the symbolic names, data types, and arrangement of data fields in the structure. The structure's contents refer to the actual data stored in the symbolic names. The following list shows acceptable contents for the structure form shown previously:

+   Part Number: 23421
+   Description: Stapler
+   Quantity in Stock: 3
+   Price: $5.98

This chapter describes the C++ statements required to create, fill, and manipulate structures.

# 16.1 Single Structures

Creating and using a structure involves the same two steps for creating and using any variable. First, the structure must be declared. Second, specific values can be assigned to the structure elements. Declaring a structure requires listing the data types, data names, and arrangement of data items. For example, the definition

```
struct
{
    int month;
    int day;
    int year;
} birth;
```

gives the form of a structure called birth and reserves storage for the data items listed in the structure. The birth structure consists of three data items or fields, which are called structure members.

Assigning actual data values to structure members is referred to as populating the structure, which is a straightforward procedure. Each structure member is accessed by giving the structure name and data item name, separated by a period. For example, birth.month refers to the first member of the birth structure, birth.day refers to the second member of the structure, and birth.year refers to the third member. The period in these names is called the member access operator or dot operator. (Both terms are used.) Program 16.1 shows assigning values to members of the birth structure.