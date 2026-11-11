will take the values of id, title, author, and price of object b1 as input from the user. This is because, every member in the statement is accessed by applying a membership operator '.' over object b1.

> **CAUTION**
> Be careful when you specify & symbol in scanf() statement. The & symbol should be specified only for variables id and price and not for arrays title and author. This is because the array name in itself is a pointer storing starting address of an array. This is exactly in line with what we have discussed in Chapter 8, Section 8.7.1.

Similarly, the following statements

```
```c
scanf("%d%s%s%f", &b2.id, b2.title, b2.author, &b2.price);
scanf("%d%s%s%f", &b3.id, b3.title, b3.author, &b3.price);
```
```

will accept the members of object b2 and b3 as input from the user, respectively. Let us assume that, the user inputs the id, title, author, and price for each of the Book objects as shown in the following table:

| Object of structure book | Data entered by the user (id, title, author, and price) |
|---|---|
| b1 | (1, "C++", "Kunal", 800) |
| b2 | (2, "Java", "Jack", 900) |
| b3 | (3, "Fortran", "Jill", 400) |

This means that the state of objects b1, b2, and b3 in the memory, will be as shown in the Figure 9.10.

The following printf() statements, print the member values of each of the Book objects on the screen, as seen in the output of the program:

```
```c
printf("The Book details are\n");
printf("%d\t%s\t%s\t%f\n", b1.id, b1.title, b1.author, b1.price);
printf("%d\t%s\t%s\t%f\n", b2.id, b2.title, b2.author, b2.price);
printf("%d\t%s\t%s\t%f\n", b3.id, b3.title, b3.author, b3.price);
```
```

> **SHORTHAND NOTATION TO CREATE OBJECTS**
> It is possible to create objects of a structure by specifying a comma separated list of object names along with the structure definition. Figure 9.11 shows the syntax of creating multiple objects(obj1,obj2,..., objn) of a structure using a shorthand notation.
> 
> For example, in the given program instead of creating the objects b1, b2, and b3 using a statement struct Book b1,b2,b3; in main(); you can also create them as while defining the structure Book as shown below.
> 
> ```c
> struct Book
> {
> int id;
> ```