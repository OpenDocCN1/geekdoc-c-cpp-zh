
```c
printf("%d\n", (*p)++);
printf("%d\n", *p++);
printf("%d\n", p--);
printf("%d\n", p++);
printf("%d\n", *p++);
```

Justify your answer.

- 13. Write a program to perform a string copy operation using pointers.
- 14. What do you mean by an array of pointers? Explain with example.
- 15. Determine the output of following code assuming the addresses of variables a and b as 1000 and 2000 respectively (Output can be shown in decimal format). Also specify compilation or runtime errors (if any).

```c
int a=50, b=75;
int *p, *q;
p=&a;
q=&b;
printf("%d\n", *p+10);
printf("%d\n", p+b);
printf("%d\n", (*p) +a);
printf("%d\n", *p + *p);
printf("%d\n", a+p+b);
printf("%d\n", q+p+b);
```

- 16. Write a program to find the smallest and largest number in an array using pointers.

## Chapter 9

## Structures and Unions

## 9.1 Overview

Structure is a template used to create a user-defined data type. This means that, as we create the variables of built-in data types, such as `int`, `float`, and `double`, we can now, also create the variables of user-defined data types, provided that the template for this data type are defined by creating a structure in the program. Structure is a way to combine the logically related data elements into a single unit. Each of the data elements defined inside the structure, are called the members of a structure. The members defined inside the structure can be of a same or different data types. Hence, a structure can be defined as a template which is created for storing heterogeneous values in physically adjacent memory locations.

> **What is a “user-defined” data type?**
>
> C/C++ has a built-in set of primitive data types like `int`, `float`, `char`, `double` etc. which can be directly used in the program. We can create variables of built-in types and perform operations with the values stored in these variables. Along with using built-in data types, we can also create customized data types in a program. “User-defined data type” is a “customized” data type that the programmer can create as per the requirements to store data in computer memory.
>
> **Structures are used to create user-defined data types.**

![](img/57c0d966bb33c67a5a188e6bf39e4e02_460_0.png)

> **What is the need to create user-defined data types in the program?**
>
> Let us assume that you need to store data about the vehicles assembled in an automobile industry. The relevant information that you wish to maintain for each vehicle is “colour”, “no of seats”, “type of fuel” and “mileage” of the vehicle. As and when a new car is assembled you will need to create 4 different variables to store its information in computer memory. Instead, it would be easy if the programmer has an ability to create a variable of type `Car` using the statement,
>
> ```c
> Car c1;
> ```
>
> where c1 stores all the required information about the car in a real world. The variable c1 can internally store the 4 attributes “colour”, “no of seats”, “type of fuel” and “mileage” of the vehicle.
>
> The requirement here is that, we need to create a variable of type Car just like we create variables of primitive types like `int`, `float`, etc. As the data type Car is not a built-in type of C/C++, we must create a

![](img/57c0d966bb33c67a5a188e6bf39e4e02_460_1.png)

![](img/57c0d966bb33c67a5a188e6bf39e4e02_462_0.png)

**Figure 9.1:** Syntax of a structure

int, float, and char. The variables which are of type defined by the structure are called as **objects** of the structure. The following is the syntax to create objects of a structure:

```
struct <StructureName> <ObjectName>;
```

We can create as many objects of the structure as required in the program. Note that, a structure is just a template for creating a ‘user-defined data type’, which means that, the memory for the member variables will not be allocated when a structure is defined, rather its actually allocated when the object of a structure is created. Every object of the structure will contain all the members defined by the structure in the memory that is allocated for that object. Further, each object of a structure will have different copy of the member variables in its memory. This means that, if we create two objects of a structure as o1 and o2 and if the structure contains n members as shown in the Figure 9.2, then each of

![](img/57c0d966bb33c67a5a188e6bf39e4e02_462_1.png)

**Figure 9.2:** Object memory for o1 and o2

the objects will have its own copy of the members in the object memory as shown in the Figure 9.2. Therefore, the total memory required by any object will be the addition of the amount of memory required by each of its members. Hence, the memory required for any structure object must be calculated as shown below:

```
sizeof(Object) = sizeof(member1) + sizeof(member2) ... +
              sizeof(memberN)
```

Every object can obviously store different values in its members. Hence, two different objects of a same structure will have exactly same number of member variables in their object memory but the values of each of the member variables may be different for each of them. The set of ‘values’ of the member variables of a particular object is called as a **state** of that object.

As an example to understand structures, let us assume that we need to store information about three **books** in the computer memory. Also, let us assume that we need to store id, title, author, and price for each of the books present in the library. Since this is a common requirement that, we need to store the members id, title, author, and price for each of the books, we can define a template for every book using a structure as shown below:

```
struct Book
{
int id;
char *title;
char *author;
float price;
};
```

> **What is the advantage that of creating Book as a structure?**
>
> This means that, we have created a “user-defined data type” named as Book. Hence, we will be able to store the variables of type Book just like we create the variables of built-in data types like `int`, `float`, `char`, etc. Following statement can now be used to create a variable b1 of type Book:
>
> ```cpp
> struct Book b1;
> ```
>
> The variable b1 contains members `id`, `title`, `author` and `price` in its memory; thereby making it possible to store complete information about a particular book in b1. We can similarly, create multiple variables of type Book and each variable will contain all the members of the structure. This makes it possible to organize data about different books in the computer memory.

By defining a structure, we are not actually storing the data about any **book** in the real world, but we have just defined a template that compiler will use while allocating memory for every variable which is of type Book. Let us now create a variable b1 of type Book, this can be done by using the following statement:

```
struct Book b1;
```

The variable b1 is now called as an ‘object’ of a structure Book. The object memory of b1 will contain members id, title, author and price as shown in the Figure 9.3. Note that, these members are present in the object memory of b1 because we have defined them inside the structure Book.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_464_0.png)

**Figure 9.3:** Object memory of b1

> **NOTES**
>
> Specifying keyword struct while creating an object of a structure is mandatory in C but optional in C++. In C++, you can also create an object b1 by omitting keyword struct as shown in the statement below:
>
> `Book b1;`
>
> Since structures are supported by both C and C++, we will add keyword struct in all the programs written in this chapter. We will ensure that the program works on C as well as C++ compilers. If you are a C++ programmer adding a keyword struct makes your programs backward compatible with C and hence it's a good practice to add it, anyways. If you are a C programmer you have no choice; you have to add keyword struct while creating objects of structure.

The total memory required for object b1 should be calculated as addition of the memory required by integer member id (which is 2 bytes), character pointer title (which is 2 bytes), character pointer author (which is 2 bytes) and float member price (which is 4 bytes). Therefore, the total memory required by each object of the structure will be 10 bytes as shown in the Figure 9.4. We assume title and author as near pointers and hence consider them of 2 byte each.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_464_1.png)

Total memory required for object b1 = **10 bytes**

**Figure 9.4:** Memory required for object b1
