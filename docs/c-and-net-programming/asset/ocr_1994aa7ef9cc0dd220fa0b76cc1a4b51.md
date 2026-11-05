# 5.3 Assigning the values to structure members

```
bk.title = "C#";
bk.author = "Ravi";
bk.subject = "Programming";
bk.book_id=3
```

# 5.4 Copying values from one structure to another structure

When object of any structure is created, the data member of that structure automatically comes in memory. For copying values from one structure to another structure, assignment operator is used.

# Example

```
Book bk1;
Book bk2;
bk2 = bk1; (structure bk1 is copied to bk2 structure)
```

# 5.5 Using structure in a program

# Example

```
//illustration of structure
using System;
-namespace StructureDemo
struct Book
{
public string title;
public string author;
public string subject;
public int book_id;
public float price;
};
public class StructureBook
{
public static void Main(string[] args)
{
Books Bk1; /* Declare Book1 of type Book */
Books Bk2; /* Declare Book2 of type Book */
/* book 1 */
Bk1.title = "C";
Bk1.author = "VPK";
Bk1.subject = "Programming";
Bk1.book_id = 1212;
Bk1.price =670;
```