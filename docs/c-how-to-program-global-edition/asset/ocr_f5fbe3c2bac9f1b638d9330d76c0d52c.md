Keyword struct introduces a structure definition. The identifier card is the structure tag, which names the structure definition and is used with struct to declare variables of the structure type—e.g., struct card. Variables declared within the braces of the structure definition are the structure’s members. Members of the same structure type must have unique names, but two different structure types may contain members of the same name without conflict (we’ll soon see why). Each structure definition must end with a semicolon.

> **Common Programming Error 10.1**
> *Forgetting the semicolon that terminates a structure definition is a syntax error.*

The definition of struct card contains members face and suit, each of type char *. Structure members can be variables of the primitive data types (e.g., int, float, etc.), or aggregates, such as arrays and other structures. As we saw in Chapter 6, each element of an array must be of the same type. Structure members, however, can be of different types. For example, the following struct contains character array members for an employee’s first and last names, an unsigned int member for the employee’s age, a char member that would contain ‘M’ or ‘F’ for the employee’s gender and a double member for the employee’s hourly salary:

```
```c
struct employee {
    char firstName[20];
    char lastName[20];
    unsigned int age;
    char gender;
    double hourlySalary;
};
```
```

# 10.2.1 Self-Referential Structures

A variable of a struct type cannot be declared in the definition of that same struct type. A pointer to that struct type, however, may be included. For example, in struct employee2:

```
```c
struct employee2 {
    char firstName[20];
    char lastName[20];
    unsigned int age;
    char gender;
    double hourlySalary;
    struct employee2 teamLeader; // ERROR
    struct employee2 *teamLeaderPtr; // pointer
};
```
```

the instance of itself (teamLeader) is an error. Because teamLeaderPtr is a pointer (to type struct employee2), it’s permitted in the definition. A structure containing a member that’s a pointer to the same structure type is referred to as a self-referential structure. Self-referential structures are used in Chapter 12, to build linked data structures.

> **Common Programming Error 10.2**
> *A structure cannot contain an instance of itself.*