
## 10.2 Structure Definitions

The keyword struct introduces a structure definition. The identifier card is the structure tag, which names the structure definition and is used with struct to declare variables of the structure type—e.g., struct card. Variables declared within the braces of the structure definition are the structure’s members. Members of the same structure type must have unique names, but two different structure types may contain members of the same name without conflict (we’ll soon see why). Each structure definition must end with a semicolon.

> **Common Programming Error 10.1**
>
> Forgetting the semicolon that terminates a structure definition is a syntax error.

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
>
> A structure cannot contain an instance of itself.

### 10.2.2 Defining Variables of Structure Types

Structure definitions do not reserve any space in memory; rather, each definition creates a new data type that’s used to define variables—like a blueprint of how to build instances of that struct. Structure variables are defined like variables of other types. The definition

```c
struct card aCard, deck[52], *cardPtr;
```

declares aCard to be a variable of type struct card, declares deck to be an array with 52 elements of type struct card and declares cardPtr to be a pointer to struct card. After the preceding statement, we’ve reserved memory for one struct card object named aCard, 52 struct card objects in the deck array and an uninitialized pointer of type struct card. Variables of a given structure type may also be declared by placing a comma-separated list of the variable names between the closing brace of the structure definition and the semicolon that ends the structure definition. For example, the preceding definition could have been incorporated into the struct card definition as follows:

```c
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

- assigning struct variables to struct variables of the *same* type (see Section 10.7)—for a pointer member, this copies only the address stored in the pointer.
- taking the address (&) of a struct variable (see Section 10.4).
- accessing the members of a struct variable (see Section 10.4).
- using the sizeof operator to determine the size of a struct variable.

> **Common Programming Error 10.3**
>
> *Assigning a structure of one type to a structure of a different type is a compilation error.*

Structures may not be compared using operators == and !=, because structure members are not necessarily stored in consecutive bytes of memory. Sometimes there are “holes” in a structure, because computers may store specific data types only on certain memory boundaries such as half-word, word or double-word boundaries. A word is a memory unit used to store data in a computer—usually 4 bytes or 8 bytes. Consider the following structure definition, in which sample1 and sample2 of type struct example are declared:

```c
struct example {
    char c;
    int i;
} sample1, sample2;
```

A computer with 4-byte words might require that each member of struct example be aligned on a word boundary, i.e., at the beginning of a word—this is machine dependent. Figure 10.1 shows a sample storage alignment for a variable of type struct example that has been assigned the character 'a' and the integer 97 (the bit representations of the values are shown). If the members are stored beginning at word boundaries, there’s a three-byte hole (bytes 1–3 in the figure) in the storage for variables of type struct example. The value in the three-byte hole is undefined. Even if the member values of sample1 and sample2 are in fact equal, the structures are not necessarily equal, because the undefined three-byte holes are not likely to contain identical values.

![](img/d0d3b7423c2d9e5650be79209ea1885d_440_0.png)

> **Portability Tip 10.1**
>
> Because the size of data items of a particular type is machine dependent and because storage alignment considerations are machine dependent, so too is the representation of a structure.

## 10.3 Initializing Structures

Structures can be initialized using initializer lists, as with arrays. To initialize a structure, follow the variable name in the definition with an equals sign and a brace-enclosed, comma-separated list of initializers. For example, the declaration

```c
struct card aCard = { "Three", "Hearts" };
```

creates variable aCard to be of type struct card (as defined in Section 10.2) and initializes member face to "Three" and member suit to "Hearts". If there are fewer initializers in the list than members in the structure, the remaining members are automatically initialized to 0 (or NULL if the member is a pointer). Structure variables defined outside a function definition (i.e., externally) are initialized to 0 or NULL if they’re not explicitly initialized in the external definition. Structure variables may also be initialized in assignment statements by assigning a structure variable of the *same* type, or by assigning values to the *individual* members of the structure.

## 10.4 Accessing Structure Members with . and ->

Two operators are used to access members of structures: the structure member operator (.)—also called the dot operator—and the structure pointer operator (->)—also called the arrow operator. The structure member operator accesses a structure member via the structure variable name. For example, to print member suit of structure variable aCard defined in Section 10.3, use the statement

```c
printf("%s", aCard.suit);  // displays Hearts
```

The structure pointer operator—consisting of a minus (-) sign and a greater than (>) sign with no intervening spaces—accesses a structure member via a pointer to the structure. Assume that the pointer cardPtr has been declared to point to struct card and that the address of structure aCard has been assigned to cardPtr. To print member suit of structure aCard with pointer cardPtr, use the statement

```c
printf("%s", cardPtr->suit);  // displays Hearts
```

The expression cardPtr->suit is equivalent to (*cardPtr).suit, which dereferences the pointer and accesses the member suit using the structure member operator. The parentheses are needed here because the structure member operator (.) has a higher precedence than the pointer dereferencing operator (*). The structure pointer operator and structure member operator, along with parentheses (for calling functions) and brackets ([]) used for array indexing, have the highest operator precedence and associate from left to right.

> **Good Programming Practice 10.2**
>
> *Do not put spaces around the -> and . operators. Omitting spaces helps emphasize that the expressions the operators are contained in are essentially single variable names.*

> **Common Programming Error 10.4**
>
> *Inserting space between the - and > components of the structure pointer operator or between the components of any other multiple-keystroke operator except ?: is a syntax error.*

> **Common Programming Error 10.5**
>
> *Attempting to refer to a structure member by using only the member’s name is a syntax error.*

> **Common Programming Error 10.6**
>
> *Not using parentheses when referring to a structure member that uses a pointer and the structure member operator (e.g., `*cardPtr.suit`) is a syntax error. To prevent this problem use the arrow (->) operator instead.*

The program of Fig. 10.2 demonstrates the use of the structure member and structure pointer operators. Using the structure member operator, the members of structure aCard are assigned the values "Ace" and "Spades", respectively (lines 17 and 18). Pointer cardPtr is assigned the address of structure aCard (line 20). Function printf prints the members of structure variable aCard using the structure member operator with variable name aCard, the structure pointer operator with pointer cardPtr and the structure member operator with dereferenced pointer cardPtr (lines 22–24).

```c
1  // Fig. 10.2: fig10_02.c
2  // Structure member operator and
3  // Structure pointer operator
```

**Fig. 10.2** | Structure member operator and structure pointer operator. (Part 1 of 2.)
