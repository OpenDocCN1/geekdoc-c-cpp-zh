
## C Structures, Unions, Bit Manipulation and Enumerations

### Objectives

In this chapter, you'll:

- Create and use structs, unions and enums.
- Understand self-referential structs.
- Learn about the operations that can be performed on struct instances.
- Initialize struct members.
- Access struct members.
- Pass struct instances to functions by value and by reference.
- Use typedefs to create aliases for existing type names.
- Learn about the operations that can be performed on unions.
- Initialize unions.
- Manipulate integer data with the bitwise operators.
- Create bit fields for storing data compactly.
- Use enum constants.
- Consider the security issues of working with structs, bit manipulation and enums.

Keyword struct introduces a structure definition. The identifier card is the structure tag, which names the structure definition and is used with struct to declare variables of the structure type—e.g., struct card. Variables declared within the braces of the structure definition are the structure’s members. Members of the same structure type must have unique names, but two different structure types may contain members of the same name without conflict (we’ll soon see why). Each structure definition must end with a semicolon.

> **Common Programming Error 10.1**
> *Forgetting the semicolon that terminates a structure definition is a syntax error.*

The definition of struct card contains members face and suit, each of type char *. Structure members can be variables of the primitive data types (e.g., int, float, etc.), or aggregates, such as arrays and other structures. As we saw in Chapter 6, each element of an array must be of the same type. Structure members, however, can be of different types. For example, the following struct contains character array members for an employee’s first and last names, an unsigned int member for the employee’s age, a char member that would contain ‘M’ or ‘F’ for the employee’s gender and a double member for the employee’s hourly salary:

```c
struct employee {
    char firstName[20];
    char lastName[20];
    unsigned int age;
    char gender;
    double hourlySalary;
};
```

### 10.2.1 Self-Referential Structures

A variable of a struct type cannot be declared in the definition of that same struct type. A pointer to that struct type, however, may be included. For example, in struct employee2:

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

the instance of itself (teamLeader) is an error. Because teamLeaderPtr is a pointer (to type struct employee2), it’s permitted in the definition. A structure containing a member that’s a pointer to the same structure type is referred to as a self-referential structure. Self-referential structures are used in Chapter 12, to build linked data structures.

> **Common Programming Error 10.2**
> *A structure cannot contain an instance of itself.*

### 10.2.2 Defining Variables of Structure Types

Structure definitions do not reserve any space in memory; rather, each definition creates a new data type that's used to define variables—like a blueprint of how to build instances of that struct. Structure variables are defined like variables of other types. The definition

```
struct card aCard, deck[52], *cardPtr;
```

declares aCard to be a variable of type struct card, declares deck to be an array with 52 elements of type struct card and declares cardPtr to be a pointer to struct card. After the preceding statement, we've reserved memory for one struct card object named aCard, 52 struct card objects in the deck array and an uninitialized pointer of type struct card. Variables of a given structure type may also be declared by placing a comma-separated list of the variable names between the closing brace of the structure definition and the semicolon that ends the structure definition. For example, the preceding definition could have been incorporated into the struct card definition as follows:

```
struct card {
    char *face;
    char *suit;
} aCard, deck[52], *cardPtr;
```

### 10.2.3 Structure Tag Names

The structure tag name is optional. If a structure definition does not contain a structure tag name, variables of the structure type may be declared only in the structure definition—not in a separate declaration.

> **Good Programming Practice 10.1**
> 
> *Always provide a structure tag name when creating a structure type. The structure tag name is required for declaring new variables of the structure type later in the program.*

### 10.2.4 Operations That Can Be Performed on Structures

The only valid operations that may be performed on structures are:

- assigning struct variables to struct variables of the same type (see Section 10.7)—for a pointer member, this copies only the address stored in the pointer.
- taking the address (&) of a struct variable (see Section 10.4).
- accessing the members of a struct variable (see Section 10.4).
- using the sizeof operator to determine the size of a struct variable.

> **Common Programming Error 10.3**
> 
> *Assigning a structure of one type to a structure of a different type is a compilation error.*

Structures may not be compared using operators == and !=, because structure members are not necessarily stored in consecutive bytes of memory. Sometimes there are "holes" in a structure, because computers may store specific data types only on certain memory boundaries such as half-word, word or double-word boundaries. A word is a memory unit used to store data in a computer—usually 4 bytes or 8 bytes. Consider the following structure definition, in which sample1 and sample2 of type struct example are declared:

```
struct example {
    char c;
    int i;
} sample1, sample2;
```

A computer with 4-byte words might require that each member of struct example be aligned on a word boundary, i.e., at the beginning of a word—this is machine dependent. Figure 10.1 shows a sample storage alignment for a variable of type struct example that has been assigned the character 'a' and the integer 97 (the bit representations of the values are shown). If the members are stored beginning at word boundaries, there's a three-byte hole (bytes 1–3 in the figure) in the storage for variables of type struct example. The value in the three-byte hole is undefined. Even if the member values of sample1 and sample2 are in fact equal, the structures are not necessarily equal, because the undefined three-byte holes are not likely to contain identical values.

![](img/bf54db922e6fa8319cba11069e785521_434_0.png)

Fig. 10.1 | Possible storage alignment for a variable of type struct example showing an undefined area in memory

> Portability Tip 10.1
> Because the size of data items of a particular type is machine dependent and because storage alignment considerations are machine dependent, so too is the representation of a structure.

### 10.3 Initializing Structures

Structures can be initialized using initializer lists as with arrays. To initialize a structure, follow the variable name in the definition with an equals sign and a brace-enclosed, comma-separated list of initializers. For example, the declaration

```
struct card aCard = { "Three", "Hearts" };
```

creates variable aCard to be of type struct card (as defined in Section 10.2) and initializes member face to "Three" and member suit to "Hearts". If there are fewer initializers in the list than members in the structure, the remaining members are automatically initialized to 0 (or NULL if the member is a pointer). Structure variables defined outside a function definition (i.e., externally) are initialized to 0 or NULL if they're not explicitly initialized in the external definition. Structure variables may also be initialized in assignment statements by assigning a structure variable of the same type, or by assigning values to the individual members of the structure.

### 10.4 Accessing Structure Members with . and ->

Two operators are used to access members of structures: the structure member operator (.)—also called the dot operator—and the structure pointer operator (->)—also called the arrow operator. The structure member operator accesses a structure member via the
