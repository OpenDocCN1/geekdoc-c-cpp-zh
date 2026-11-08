Output of the preceding program is as follows:

```
```
Enter Name and Price   ALTO 300000
Enter Name and Price   INNOVA 900000
Enter Name and Price   MERCEDES 250000

Information Entered is

Name [ALTO] and Price [300000]
Name [INNOVA] and Price [900000]
Name [MERCEDES] and Price [2500000]
```
```

Although an array can help in storing a number of information, it is not scalable enough. In our case, we might need to store more information that is related to a car, but the array may become cumbersome if we deal with huge sets of data through it. To overcome this problem, C provides a data type called structure, which allows us to group dissimilar data types. A structure can contain different types of elements, which differ in their data types. Each individual structure element is referred to as structure member.

Let’s first learn how to declare a structure.

# # Declaring a Structure

Declaring a structure is more complicated than declaring an array because structure contains a number of individual elements. A generic form of declaring a structure is as follows:

```
```c
struct objectName {
    member 1;
    member 2;
    member 3;
    .................
    member n;
};
```
```

In the preceding declaration, struct is the keyword and objectName is a name that is given to the structure. Individual members are denoted by member1, member2, ..., and member n. These members could be variables, pointers, arrays, or any other structure. The member names inside a structure should be different in nature. In other words, no two members of the same structure are allowed to have the same name. After the structure is declared, we can declare the individual variables of structure type as follows:

```
```c
struct objectName variable 1, variable 2,..............,variable n;
```
```

Consider an example of structure declaration as follows:

```
```c
struct Car {
    char name[20];
    float price;
    char model[20];
    int year;
};
```
```

For the preceding declaration, structure variables can be declared as follows:

```
```c
struct Car car1,car2,car3;
```
```