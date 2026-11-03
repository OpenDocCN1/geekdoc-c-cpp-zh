# Chapter 12

# Structures and Unions

# 12.1 INTRODUCTION

We seen that arrays can be used to represent a group of data items that belong to the same type, such as int or float. However, if we want to represent a collection of data items of different types using a single name, then we cannot use an array. Fortunately, C supports a constructed data type known as structure, which is a method for packing data of different types. A structure is a convenient tool for handling a group of logically related data items. For example, it can be used to represent a set of attributes, such as student_name, roll_number and marks. The concept of a structure is analogous to that of a 'record' in many other languages.

Structures help to organize complex data in a more meaningful way. It is a powerful concept that we may often need to use in our program design. The chapter is devoted to the study of structures and their applications in program development. Another related concept known as unions is also discussed.

# 12.2 STRUCTURE DEFINITION—DECLARING STRUCTURES

A structure definition creates a format that may be used to declare structure variables. Let us use an example to illustrate the process of structure definition and the creation of structure variables. Consider a book database consisting of book name, author, number of pages, and price. We can define a structure to hold this information as follows:

```
struct book_bank
{
    char title[20];
    char author[15];
    int pages;
    float price;
};
```

The keyword struct declares a structure to hold the details of four fields, namely title, author, pages, and price. These fields are called structure elements or members. Each member may belong to a differ-