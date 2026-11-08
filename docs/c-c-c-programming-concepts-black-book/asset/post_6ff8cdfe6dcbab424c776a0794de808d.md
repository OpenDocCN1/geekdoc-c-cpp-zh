
![](img/43c5f409f9b17790a628c4b4df854b61_170_0.png)

## 5 Advanced Concepts on C

| If you need an information on: | See page: |
|---|---|
| Structures | 130 |
| Declaring a Structure | 131 |
| Unions | 148 |
| File Management in C | 150 |
| Binary Files | 160 |
| File Management Functions | 166 |
| Bitwise Operators | 169 |
| Type Qualifiers | 176 |
| Memory Segmentation in C | 178 |

## Chapter 5

Working with functions and arrays might not fulfill all the real life tasks that a programmer needs to perform using the C language. A major portion of such activities requires advanced and complex concepts. Some of these concepts are structures, unions, and files.

Structures are one of the most used constructs in C. They enable a programmer to group together dissimilar set of information. Similar to structures, unions also comprise dissimilar set of information. However, unlike structures, all the members of a union share the same memory location. Files are another crucial type of information management. C provides two types of files: text files and binary files. A text file consists of consecutive characters; whereas, a binary file is a collection of bytes. C also provides several file management functions, such as fclose(), feof(), ferror(), fgetpos(), freopen(), and ftell(), to perform file related tasks.

In this chapter, we learn about some of the advanced concepts in C programming. The chapter discusses structures and unions along with their implementations in depth. We also learn about the concept of file management in C. Moreover, we learn about bitwise operations in C along with their implementations. Towards the end, we learn about type qualifiers and memory segmentation in C.

Let’s start the chapter by discussing structures, in detail.

### Structures

C provides some basic data types, such as int, float, and char, to store small information. However, in real world, information does not appear as small as the basic data types; instead, it appears as a collection of several things, where each thing has its own attributes. Let’s consider a real life entity, car. It can contain information, such as model name and price, which are dissimilar in nature. That is, model name is a string; whereas, price is an integer. Now, to perform similar operations on this information, we can use several arrays to hold the elements of same type. Listing 5.1 shows the arrays to store information about a car:

Listing 5.1: Storing the Information in the Arrays

```c
#include<stdio.h>

int main()
{
    char name[3][10];
    int price[3];
    int i;

    for(i=0;i<=2;i++)
    {
        printf("\n Enter Name and Price ");
        scanf("%s %d",&name[i],&price[i]);
    }

    printf("\n Information Entered is \n");
    for(i=0;i<=2;i++)
    {
        printf("\n Name [%s] and Price [%d] ",name[i],price[i]);
    }

    getch();
    return 0;
}
```

Output of the preceding program is as follows:

```
Enter Name and Price   ALTO 300000
Enter Name and Price   INNOVA 900000
Enter Name and Price   MERCEDES 2500000

Information Entered is

Name [ALTO] and Price [300000]
Name [INNOVA] and Price [900000]
Name [MERCEDES] and Price [2500000]
```

Although an array can help in storing a number of information, it is not scalable enough. In our case, we might need to store more information that is related to a car, but the array may become cumbersome if we deal with huge sets of data through it. To overcome this problem, C provides a data type called structure, which allows us to group dissimilar data types. A structure can contain different types of elements, which differ in their data types. Each individual structure element is referred to as structure member.

Let’s first learn how to declare a structure.

### Declaring a Structure

Declaring a structure is more complicated than declaring an array because structure contains a number of individual elements. A generic form of declaring a structure is as follows:

```c
struct objectName {
    member 1;
    member 2;
    member 3;
    .................
    member n;
};
```

In the preceding declaration, struct is the keyword and objectName is a name that is given to the structure. Individual members are denoted by member1, member2, ..., and member n. These members could be variables, pointers, arrays, or any other structure. The member names inside a structure should be different in nature. In other words, no two members of the same structure are allowed to have the same name. After the structure is declared, we can declare the individual variables of structure type as follows:

```c
struct objectName variable 1, variable 2,..............,variable n;
```

Consider an example of structure declaration as follows:

```c
struct Car {
    char name[20];
    float price;
    char model[20];
    int year;
};
```

For the preceding declaration, structure variables can be declared as follows:

```c
struct Car car1,car2,car3;
```

The structure variable declaration sets aside the memory for each variable. In our case, a total of 52 bytes of memory will be allocated to each structure variable. Note that the bytes are always allocated in adjacent memory locations.

The declaration of structure type and structure variables can be combined together as follows:

```c
struct car {
    char name[20];
    float price;
    char model[20];
    int year;
} car1, car2;
```

Similar to variables and arrays, structure variables can be initialized when they are declared. The format to initialize the structure variables is given as follows:

```c
struct car car1 = {"HONDA", 1400000, "CITY", 2009};
```

In the preceding format, the first value will be assigned to the first member variable; the second value will be assigned to the second member variable; the third value will be assigned to the third member variable; and the fourth value will be assigned to the fourth member variable.

Some important points that need to be kept in mind while declaring a structure are as follows:

- The closing brace in the structure declaration must be followed by a semicolon
- A structure type declaration does not tell the compiler anything about the allocation of memory; it just creates the structure
- Usually, a structure declaration precedes any other declaration done in the program

Next, let's learn how to access the elements of a structure.

### Accessing Structure Elements

Individual elements of a structure are accessed with the help of a dot operator (.). A generic format of accessing a structure member is given as follows:

```c
variable.member;
```

In the preceding format, variable refers to the name of a structure type variable and member denotes the name of the member within the structure. The associativity of the dot operator is left to right.

Listing 5.2 shows how to store and access the individual elements of a structure:

Listing 5.2: Storing and Accessing the Individual Structure Elements

```c
#include<stdio.h>

struct Car             /* Declaring the structure */
{
    char name[50];
    char model[50];
    float price;
    int mfdate;
    int mileage;
};

struct Car varA;   /* Declaring structure type variables */

int main()
{
    int i;
    printf("\n Enter Name of the Car -> ");
    gets(varA.name);
    printf("\n Enter Model of the Car -> ");
    gets(varA.model);
    printf("\n Enter Price of the Car -> ");
    scanf("%f",&varA.price);
    printf("\n Enter Manufacturing Date of the Car -> ");
    scanf("%d",&varA.mfdate);
    printf("\n Enter Mileage of the Car -> ");
    scanf("%d",&varA.mileage);

    printf("\n Details Entered are \n");
    printf("\n Name of the Car -> %s",varA.name);
    printf("\n Address of Name of the Car -> %d",&varA.name);
    printf("\n Model of the Car -> %s",varA.model);
    printf("\n Address of Model of the Car -> %d",&varA.model);
    printf("\n Price of the Car -> %f",varA.price);
    printf("\n Address of Price of the Car -> %d",&varA.price);
    printf("\n Manufacturing Date of the Car -> %d",varA.mfdate);
    printf("\n Address of Manufacturing Date of the Car -> %d",&varA.mfdate);
    printf("\n Mileage of the Car -> %d",varA.mileage);
    printf("\n Address of Mileage of the Car -> %d",&varA.mileage);

    getch();
    return 0;
}
```

In Listing 5.2, notice that all the members of the structure are accessed with the help of the dot operator. We have defined a structure called Car. This structure contains certain attributes of a car. All the attributes mentioned in the structure are referred as the member variables of that structure. After defining the structure, we have declared a variable called varA, which is of type Car. Inside the main() function, we have accessed each element of the structure using the same structure variable and a dot operator. Output of the preceding program is as follows:

```
Enter Name of the Car -> MAHINDRA
Enter Model of the Car -> SCORPIO
Enter Price of the Car -> 900000
Enter Manufacturing Date of the Car -> 2008
Enter Mileage of the Car -> 12

Details Entered are

Name of the Car -> MAHINDRA
Address of Name of the Car -> 4210784
Model of the Car -> SCORPIO
Address of Model of the Car -> 4210834
Price of the Car -> 900000.000000
Address of Price of the Car -> 4210884
Manufacturing Date of the Car -> 2008
Address of Manufacturing Date of the Car -> 4210888
Mileage of the Car -> 12
Address of Mileage of the Car -> 4210892
```
