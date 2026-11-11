As an example, let us enhance the structure Book to store the ‘date of publishing’ for each of the books along with the members id, title, author, and price. The attribute ‘date of publishing’ in itself is a composition of three integer values dd, mm, and yyyy. This means that, we should now create a structure Date with members dd, mm, and yyyy, so that its object can represent a particular date in the computer memory. The following is the definition of the structure Date containing fields dd, mm, and yyyy to represent the day, month, and year, parts of the date, respectively.

```
```cpp
struct Date
{
    int dd;
    int mm;
    int yyyy;
};
```
```

As the publishing date is required to be stored for each of the Book objects, we will define the structure Date inside the structure Book by creating the object of Date (named as dop) as a member of the structure Book. dop represents the ‘date of publishing’ of the book as shown in the Figure 9.23.

![](bbox=[0.24, 0.44, 0.92, 0.705])

Figure 9.23: Nesting of structures

The statement,

```
```cpp
struct Book b1;
```
```

creates an object of structure Book named as b1. As Book is an outer structure, the object memory of b1 will also include the object dop which is the object of inner structure, along with the members id, title, author, and price which are directly defined in Book, as shown in the Figure 9.24.

As discussed before, the members id, title, author, and price for object b1 can be taken as input from the user by using the following scanf() statement. This is because these members are directly defined in the outer structure as seen in the Figure 9.24.