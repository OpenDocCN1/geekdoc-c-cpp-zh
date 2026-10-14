handle a group of logically related data items known as structures. declare an array of structures, each element of the array representing a

structure variable.

pass structure as an argument to functions and return structure from functions.

refer to (i.e., point to) an incomplete type, including itself.

handle a group of logically related data items in terms of unions.

# 10.2 Basics of Structures

C supports a constructed data type known as structure, which is a method for packing data of different types. A structure is a convenient tool for handling a group of logically related data items. Structures help to organize complex data in a more meaningful way. It is a powerful concept that we may often need to use in our program design.

Structure Definition: A Structure definition creates a format that may be used to declare structure variables. For e.g., Consider a book database consisting of book name, author, number of pages and price.

```
struct book_bank
{
char title[20];
char author[15];
int pages;
```