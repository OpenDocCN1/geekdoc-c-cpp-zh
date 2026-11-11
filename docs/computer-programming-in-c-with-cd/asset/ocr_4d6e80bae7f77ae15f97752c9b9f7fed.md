```
```cpp
d1.book_Detail.author = "Dheeraj Gupta";
d1.book_Detail.price = 365;
cout<<"Name of the book is: "<<d1.book_Detail.name<<"\n";
cout<<"Author of the book is: "<<d1.book_Detail.author<<"\n";
cout<<"Price of the book is: "<<d1.book_Detail.price;
return 0;
}
```
```

# Output:

```
```text
The publisher of the book is: Dreamtech Press
This book is meant for students of: 12
Name of the book is: Exploring C++
Author of the book is: Dheeraj Gupta
Price of the book is: 365
```
```

In Listing 14, you see that a structure, My_Books is created. The instance of this structure is created inside the Detail union. Next, the main() function begins and an instance of the Detail union is created in it. Finally, the instance of the Detail union, declared inside the main() function, is used to access the variables of the Detail union and the My_Books structure.

Now, let's learn to create an instance of a union inside a structure.

# ■  Creating a Union Instance as a Structure Member

You learned that unions are user-defined data types that can have elements of different types as well as an instance of a structure. Similar to the union, a structure can also have an instance of the union itself as its member.

Listing 15 shows the process to define a union instance as an element of the structure (you can find the UnionElement.cpp file on the CD in the code\\chapter5 folder):

# ▶ Listing 15: Create a Structure with the Union Instance as a Member

```
```cpp
#include <iostream.h>

union Detail
{
        char *publication;
        int standard;
};

struct My_Books
{
        char *name;
        char *author;
        int price;
        union Detail book_Detail;
};
```
```