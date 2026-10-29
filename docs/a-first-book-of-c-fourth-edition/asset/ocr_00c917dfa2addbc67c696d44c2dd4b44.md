# Chapter

# 16
Data Structures

+   16.1 Single Structures
+   16.2 Arrays of Structures
+   16.3 Structures as Function Arguments
+   16.4 Dynamic Structure Allocation
+   16.5 Unions
+   16.6 Common Programming Errors
+   16.7 Chapter Summary

![](bbox=[0.62, 0.48, 1.0, 0.78])

A structure is a historical holdover from C. From a programmer's perspective, a structure is equivalent to a class having all public instance variables and no methods. In commercial applications, a structure is referred to, and is the same thing as, a record. In C++, a structure provides a way to store values of different data types, such as an integer part number, a character description, and a double-precision price.

For example, a store maintains a record of items in inventory, with the following data items maintained for each inventory item:
Part Number:
Description:
Quantity in Stock:
Price:

Each data item is a separate entity referred to as a data field. Taken together, the data fields form a single unit referred to as a record, which in C++ is called a structure. Although the store could keep track of hundreds of inventory items, the form of each item's structure is identical. In dealing with structures, distinguishing between a structure's form and its contents is