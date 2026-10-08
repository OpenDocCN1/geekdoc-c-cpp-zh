# 13.1. Structs: Defining Custom Data Types

# 13.1.3 Pointers to Structures

Pointers can also point to structures and unions, allowing dynamic allocation and manipulation of complex data structures. Declaring pointers to structures is straightforward:

```
struct Person *ptr;
```

To access structure members through a pointer, we can use the arrow operator (--) or by dereferencing:

```
ptr->age = 26;
(*ptr).age = 26;
```

This arrow operator is especially useful when dealing with structures containing pointers, such as linked lists.
Example code:

```
#include <stdio.h>

struct Person {
    char name[18];
    int age;
    float height;
};

int main() {
```

```
// Declare and initialize struct variables
struct Person1 = {"Sarah", 20, 1.65f};
struct Person2 = {"Adam", 25, 1.8f};
```

```
// Declare pointer to struct
struct Person *ptr;
```

```
// Assign address of struct variables to pointers
tr = &person1;
```

```
// Access struct members using arrow notation
printf("Name: %s\n", ptr->name);
printf("Age: %d\n", ptr->age);
printf("Height: %f\n", ptr->height);
```

```
// Change pointer to point to other struct
tr = &person2;
```

```
// Access struct members using dereferencing
printf("Name: %s\n", (*ptr).name);
printf("Age: %d\n", (*ptr).age);
printf("Height: %f\n", (*ptr).height);
```